# Drand Off-Chain Unbiased Voting

> Implementing an unbiased off-chain voting process using Lilypad and Bacalhau, with Drand Time-lock encryption

## Introduction

This example illustrates how [DeFi Kicks](https://ethglobal.com/showcase/defikicks-b1wo0) leverages Lilypad, Bacalhau, and Drand to implement an unbiased off-chain voting mechanism. The purpose of using these technologies is to ensure that voting happens in an unbiased, decentralized manner, thus promoting true democracy within the DefiKicks ecosystem.

The contracts and docker images have also been added as an example in [Lilypad Github](https://github.com/bacalhau-project/lilypad/tree/main/examples)

For more info on DeFi Kicks and their use of Lilypad, see the [DefiKicks Github](https://github.com/md0x/defikicks)

## Overview

The DeFi Kicks project utilizes a three-step mechanism to ensure an unbiased voting system. Here's a summarized outline of how it operates:

### 1. Off-Chain Voting

The voting process is performed off-chain to maintain efficiency and privacy. Users cast their votes by encrypting them on the front end, signing the message for authenticity, and then sending them to be stored. Time-lock encryption is utilized, making the vote only decryptable after a predetermined amount of time, which ensures fairness and protects against any attempts to tamper with the votes.

### 2. Vote Resolution Request

Once the voting phase for a proposal has ended, anyone can request a vote resolution. This action requires a certain fee and can only be performed if the vote is in the ResolutionToRequest state. This fee covers the usage of Lilypad and Bacalhau for off-chain vote resolution.

### 3. Off-Chain Resolution in Bacalhau through Lilypad

Once a vote resolution request has been submitted and the necessary fee paid, Bacalhau, via Lilypad, takes care of the off-chain resolution. It processes the vote data, decrypting the votes when the predetermined time has elapsed, and generates the final voting results. This off-chain resolution ensures a high level of security and accuracy, providing an unbiased outcome for the voting process.

In summary, this mechanism leverages the strengths of off-chain voting and resolution in a decentralized environment, guaranteeing privacy, fairness, and tamper resistance in the voting process, which are all critical to maintaining the trust and integrity of the DeFi Kicks project.

## Technical Details

### 1. Off-Chain Voting

Vote details are packaged into a message object and signed cryptographically. This message is then encrypted using a time-lock mechanism, which ensures decryption only after a certain time. The encrypted vote, along with the user's account details and signature, are stored as a vote object. Lastly, the new vote is stored and the system is notified.

The following code snippet shows how the off-chain voting mechanism is implemented in the frontend of the DefiKicks application. The original code can be found in the [DefiKicks Github](https://github.com/md0x/defikicks/blob/master/web/pages/vote.tsx#L25)

```typescript
const vote = async (proposal: any, voteString: string) => {
  /// ... other code

  const votePhase = 5 * 60;

  const message = {
    proposalId: proposal.id,
    proposalName: proposal.name,
    proposalDescription: proposal.description,
    proposalAdapter: proposal.ipfsHash,
    vote: voteString,
  };

  const messageString = JSON.stringify(message);

  const signature = await library?.getSigner().signMessage(messageString);

  // Encrypt the message using Drand time-lock encryption
  const cyphertext = await timelockEncryption(messageString, 30);

  const vote = {
    proposalId: proposal.id,
    cyphertext,
    account,
    signature,
  };

  newVotes.push(vote);

  console.log("Your vote", JSON.stringify(vote, null, 2));

  await storeVotes(proposal.id, newVotes);
  await notifyNewVote();
};
```

### 2. On-chain: Resolution request

Once the off-chain voting phase has ended anyone can request it's resolution by calling the `requestVoteResolution` function in the [Governor smart contract](https://github.com/md0x/defikicks/blob/master/contracts/contracts/GovernorContract.sol#L154). This function in turn will trigger a Lilypad job that will fetches all the votes and resolve the voting process.

The Lilypad job is defined as docker image that runs a javascript script that fetches all the votes and resolves the voting process. We will go into the details of the script in a later section.

The Lilypad job spec is dinamically built to send the proposal ID as environment variable together with a node url used to fetch the vote power of each voter. The node url is also used to fetch the proposal details from the chain.

See the [original smart contract](https://github.com/md0x/defikicks/blob/master/contracts/contracts/GovernorContract.sol#L154) for more details.

```js
    function requestVoteResolution(bytes32 proposalId) public payable virtual {
        require(
            state(proposalId) == ProposalState.ResolutionToRequest,
            "Governor: vote not in ResolutionToRequest state"
        );
        uint256 lilypadFee = bridge.getLilypadFee();
        require(msg.value >= lilypadFee, "Governor: insufficient fee");

        string memory spec = getSpecForProposalId(proposalId);

        uint256 id = bridge.runLilypadJob{value: lilypadFee}(
            address(this),
            spec,
            uint8(LilypadResultType.StdOut)
        );
        require(id > 0, "job didn't return a value");
        proposals[proposalId].bridgeId = id;
        jobIdToProposal[id] = proposalId;
        emit VoteResolutionRequested(proposalId, id);
    }
```

### 3.1 Off-chain: Lilypad job execution with Bacalhau

The script run in Bacalhau perform the following steps:

1. Retrieve all the off-chain votes from a decentralised storage (Ceramic stream or IPFS)
2. Decrypt the votes using Drand timelock decryption function
3. Verify the signature of the decrypted vote
4. Compute the vote power of each voter
5. Compute the vote result using the vote power of each voter
6. Compute the inflationary rewards for each voter that voted for the winning option
7. Put the reward information in a Merkle tree and compute the Merkle root together with the proof for each voter
8. Encode all the information in a hex string and console.log it
   as this is the stdout that will be sent back to the Governor smart contract by the Bacalhau operators that run the job.

Here is the vote decryption and verification code, for the full script see the [original script](https://github.com/md0x/defikicks/blob/master/bacalhau-container/index.js)

```js
// other code
const votes = await getVotes(proposal.id);

const decryptedVotes = [];

for (const vote of votes) {
  let message;
  try {
    message = await timelockDecryption(vote.cyphertext);
  } catch (e) {}
  decryptedVotes.push({
    ...vote,
    message,
  });
}

const signedVotes = [];

for (const vote of decryptedVotes) {
  const recoveredAddress = ethers.utils.verifyMessage(
    vote.message,
    vote.signature
  );
  if (recoveredAddress === vote.account) {
    signedVotes.push(vote);
  }
}
// other code

const calldata = ethers.utils.defaultAbiCoder.encode(
  [
    {
      type: "tuple",
      components: [
        { name: "forVotes", type: "uint256" },
        { name: "againstVotes", type: "uint256" },
        { name: "abstainVotes", type: "uint256" },
        { name: "voteMerkleRoot", type: "bytes32" },
        { name: "data", type: "string" },
      ],
    },
  ],
  [
    {
      forVotes,
      againstVotes,
      abstainVotes,
      voteMerkleRoot: tree.root,
      data,
    },
  ]
);

console.log("calldata", calldata);
```

### 3.2 On-chain: Lilypad job resolution

Once the job is picked up by the Bacalhau operators and executed, the resolutions are brought on-chain and the Governor smart contract receives a `lilypadFulfilled` callback from Lilypad.

The `_result` string contains all the vote resolution information encoded in a hex string. The string is decoded and the resolution information is stored in the smart contract.

For more information on how the result is decoded see the [original smart contract](https://github.com/md0x/defikicks/blob/master/contracts/contracts/GovernorContract.sol)

```js
    function lilypadFulfilled(
        address _from,
        uint _jobId,
        LilypadResultType _resultType,
        string calldata _result
    ) external override {
        require(_resultType == LilypadResultType.StdOut);
        require(msg.sender == address(bridge));

        ResolutionResponse memory resolutionResponse = abi.decode(
            hexStrToBytes(_result),
            (ResolutionResponse)
        );
        ProposalCore storage proposal = proposals[jobIdToProposal[_jobId]];
        proposal.voteMerkleRoot = resolutionResponse.voteMerkleRoot;
        proposal.forVotes = resolutionResponse.forVotes;
        proposal.againstVotes = resolutionResponse.againstVotes;
        proposal.abstainVotes = resolutionResponse.abstainVotes;

        emit ProposalUpdated(
            jobIdToProposal[_jobId],
            resolutionResponse.voteMerkleRoot,
            resolutionResponse.forVotes,
            resolutionResponse.againstVotes,
            resolutionResponse.abstainVotes,
            resolutionResponse.data
        );
    }
```

---
description: The Lilypad v0 Smart Contracts
---

# Lilypad Smart Contracts

## Using the Lilypad Contracts

1. Create a contract that implements [`LilypadCallerInterface`](https://github.com/bacalhau-project/lilypad/blob/main/hardhat/contracts/LilypadCallerInterface.sol). As part of this interface you need to implement 2 functions:
   * `lilypadFulfilled` - a callback function that will be called when the job completes successfully
   * `lilypadCancelled` - a callback function that will be called when the job fails
2. To trigger a job from your contract, you need to call the `LilypadEvents` contract which the bridge is listening to. You will connect to Bacalhau network via this bridge. Create an instance of [`LilypadEvents`](https://github.com/bacalhau-project/lilypad/blob/main/hardhat/contracts/LilypadEvents.sol) by passing the public contract address above to the `LilypadEvents` constructor.&#x20;
3. To make a call to Bacalhau, call `runLilypadJob` from your function. You need to pass the following parameters:

## LilypadEvents Contract

This contract is the bridge between the Bacalhau network and smart contracts & does all the heavy lifting. \


To use Lilypad, you only need to take note of one function in this events contract -  the `runLilypadJob(address _from, string memory _spec, uint8 _resultType)` function which takes the following parameters.\


|      Name     |                                                               Type                                                              |                                                                                                                                   Purpose                                                                                                                                   |
| :-----------: | :-----------------------------------------------------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|    `_from`    |                                                            `address`                                                            |                                                               The address of the calling contract, to which success or failure will be passed back. You should probably use address(this) from your contract.                                                               |
|    `_spec`    |                                                             `string`                                                            |                                                                                          A Bacalhau job spec in JSON format. See docs for more information on creating a job spec.                                                                                          |
| `_resultType` | [`LilypadResultType`](https://github.com/bacalhau-project/lilypad/blob/main/hardhat/contracts/LilypadCallerInterface.sol#L4-L9) | The type of result that you want to be returned - specified in the LilypadCaller Interface. If you specify CID, the result tree will come back as a retrievable IPFS CID. If you specify StdOut, StdErr or ExitCode, those raw values output from the job will be returned. |

{% hint style="info" %}
Open LilypadEvents Contract in Remix -> [Click here](https://remix.ethereum.org/bacalhau-project/lilypad/blob/main/hardhat/contracts/LilypadEventsUpgradeable.sol)
{% endhint %}

```solidity
// SPDX-License-Identifier: MIT
pragma solidity >=0.8.4;
import "hardhat/console.sol";
import "@openzeppelin/contracts/utils/Counters.sol";
import "@openzeppelin/contracts-upgradeable/proxy/utils/Initializable.sol";
import "@openzeppelin/contracts-upgradeable/access/AccessControlUpgradeable.sol";
import "@openzeppelin/contracts-upgradeable/proxy/utils/UUPSUpgradeable.sol";
import "./LilypadCallerInterface.sol";

error LilypadEventsUpgradeableError();

/**
    @notice An experimental contract for POC work to call Bacalhau jobs from FVM smart contracts
*/
contract LilypadEventsUpgradeable is Initializable, AccessControlUpgradeable, UUPSUpgradeable {
    bool private initialized;
    bytes32 public constant UPGRADER_ROLE = keccak256("UPGRADER_ROLE");
    
    uint256 public LILYPAD_FEE = 0.03 * 10**18;
    uint256 private escrowAmount = 0;
    uint256 private escrowMinAutoPay  = 5 * 10**18;
    address private escrowAddress = 0x5617493b265E9d3CC65CE55eAB7798796D9108E4; 
    uint256[50] private __gap; //for extra memory slots that may be needed in future upgrades.

    using Counters for Counters.Counter;
    Counters.Counter private _jobIds;

    /// @custom:oz-upgrades-unsafe-allow constructor
    constructor() {
        _disableInitializers();
    }

    function initialize() public initializer {
        require(!initialized, "Contract Instance has already been initialized");
        console.log("Deploying LilypadEvents contract");
        initialized = true;
        __AccessControl_init();
        __UUPSUpgradeable_init();
        _setupRole(DEFAULT_ADMIN_ROLE, msg.sender);
        _grantRole(UPGRADER_ROLE, msg.sender);
    }

    function _authorizeUpgrade(address newImplementation)
        internal
        onlyRole(UPGRADER_ROLE)
        override
    {}

    struct LilypadJob {
        address requestor;
        uint id; //jobID
        string spec; 
        LilypadResultType resultType;
    }
    LilypadJob[] public lilypadJobHistory;

    struct LilypadJobResult {
        address requestor;
        uint id;
        bool success;
        string result;
        LilypadResultType resultType;
    }
    LilypadJobResult[] public lilypadJobResultHistory;
    mapping(address => LilypadJobResult[]) lilypadJobResultByAddress; // jobs by requestor

    /** Events **/
    event NewLilypadJobSubmitted(LilypadJob job);
    event LilypadJobResultsReturned(LilypadJobResult result);
    event LilypadEscrowPaid(address, uint256);

    /** Escrow/ Balance functions **/
    function getEscrowAddress()public view onlyRole(UPGRADER_ROLE) returns(address) {
        return escrowAddress;
    }

    function getEsrowMinAutoPay()public view onlyRole(UPGRADER_ROLE) returns(uint256) {
        return escrowMinAutoPay;
    }

    function setEscrowMinAutoPay(uint256 _minAmount) public onlyRole(UPGRADER_ROLE){
      escrowMinAutoPay = _minAmount;
    }

    function setEscrowWalletAddress(address _escrowAddress) public onlyRole(UPGRADER_ROLE) {
      escrowAddress = _escrowAddress;
    }

    function withdrawBalanceToEscrowAddress() public onlyRole(UPGRADER_ROLE) {
        require(address(this).balance > 0, "No money in contract able to be withdrawn");
        address payable recipient = payable(escrowAddress);
        //ecrowAmount and contract amount Should be the same (if not should be zero'd anyway);
        escrowAmount = 0;
        uint256 amount = address(this).balance;
        recipient.transfer(amount);
        emit LilypadEscrowPaid(recipient, amount);
    }

    function getLilypadFee() public view returns (uint256) {
        return LILYPAD_FEE;
    }

    function getContractBalance() public view onlyRole(UPGRADER_ROLE) returns (uint256) {
      return address(this).balance;
    }

    function setLilypadFee(uint256 _newFee) public onlyRole(UPGRADER_ROLE) {
        LILYPAD_FEE=_newFee;
    }

    /** Lilypad Job via Bacalhau network functions **/
    /** Run your own docker image spec on the network with the _specName = "CustomSpec", You need to pass in the Bacalhau specification for this **/
    function runLilypadJob(address _from, string memory _spec, uint8 _resultType) public payable returns (uint) {
        require(msg.value >= LILYPAD_FEE, "Not enough payment sent to cover job fee");

        uint thisJobId = _jobIds.current();
        LilypadJob memory jobCalled = LilypadJob({
            requestor: _from,
            id: thisJobId,
            spec: _spec,
            resultType: LilypadResultType(_resultType)
        });

        lilypadJobHistory.push(jobCalled);
        emit NewLilypadJobSubmitted(jobCalled);
        _jobIds.increment();

        escrowAmount += msg.value; 
        if(escrowAmount > escrowMinAutoPay){
            uint256 escrowToSend = escrowAmount;
            address payable recipient = payable(escrowAddress);
            //should check contract balance before proceeding
            if(address(this).balance >= escrowToSend) {
              escrowAmount = 0;
              recipient.transfer(escrowToSend);
              emit LilypadEscrowPaid(recipient, escrowToSend);
            }
        }

        return thisJobId;
    }

    // this should really be owner only - our admin contract should be the only one able to call it
    function returnLilypadResults(address _to, uint _jobId, LilypadResultType _resultType, string memory _result) public {
        LilypadJobResult memory jobResult = LilypadJobResult({
            requestor: _to,
            id: _jobId,
            result: _result,
            success: true,
            resultType: _resultType
        });
        lilypadJobResultHistory.push(jobResult);
        lilypadJobResultByAddress[_to].push(jobResult);

        emit LilypadJobResultsReturned(jobResult);
        LilypadCallerInterface(_to).lilypadFulfilled(address(this), _jobId, _resultType, _result);
    }

    function returnLilypadError(address _to, uint _jobId, string memory _errorMsg) public onlyRole(UPGRADER_ROLE) {
        LilypadJobResult memory jobResult = LilypadJobResult({
            requestor: _to,
            id: _jobId,
            success: false,
            result: _errorMsg,
            resultType: LilypadResultType.StdErr
        });
        lilypadJobResultHistory.push(jobResult);
        lilypadJobResultByAddress[_to].push(jobResult);

        emit LilypadJobResultsReturned(jobResult);
        LilypadCallerInterface(_to).lilypadCancelled(address(this), _jobId, _errorMsg);
    }

    function fetchAllJobs() public view returns (LilypadJob[] memory) {
        return lilypadJobHistory;
    }

    function fetchAllResults() public view returns (LilypadJobResult[] memory) {
        return lilypadJobResultHistory;
    }

    function fetchJobsByAddress(address _requestor) public view returns (LilypadJobResult[] memory) {
        return lilypadJobResultByAddress[_requestor];
    }
}
```

##

## LilypadCaller Interface

This interface ensures that the results of a job run on the Bacalhau network via Lilypad can be returned to the originating contract.\
\
This interface needs to be implemented by a smart contract for Lilypad to run.

{% hint style="info" %}
Open the LilypadCaller Interface in Remix -> [Click here](https://remix.ethereum.org/bacalhau-project/lilypad/blob/main/hardhat/contracts/LilypadCallerInterface.sol)
{% endhint %}

```solidity
// SPDX-License-Identifier: MIT
pragma solidity >=0.8.4;

enum LilypadResultType {
  CID,
  StdOut,
  StdErr,
  ExitCode
}

interface LilypadCallerInterface {
  function lilypadFulfilled(address _from, uint _jobId, LilypadResultType _resultType, string calldata _result) external;
  function lilypadCancelled(address _from, uint _jobId, string calldata _errorMsg) external;
}
```


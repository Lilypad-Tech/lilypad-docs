---
description: Sorry! We're working on this page!
hidden: true
---

# Lilypad Smart Contracts

## Using the Lilypad Contracts

We have deployed the [LilypadOnChainJobCreator](https://github.com/Lilypad-Tech/lilypad/blob/main/hardhat/contracts/LilypadOnChainJobCreator.sol) contract which you can use to trigger running jobs on the lilypad network from other smart contracts.

It works in tandem with the `lilypad jobcreator` on-chain which will watch the on-chain contract and manage jobs on behalf of contracts that submit them.

### **Creating a job**

You will need to know the contract address for the on-chain job creator so we can submit transactions to it.

The production controller address is `0x8e136587e3e5266d5244f6aa896E5CAf8E969946` and you can ask it for the address of the on-chain job creator `getJobCreatorAddress()`

Running a job involves 2 phases:

* calling `approve` on the ERC-20 contract to allow the solver to spend your tokens
* trigger the job via the on chain job manager

Now we know the address of the on-chain job controller - we can ask it for 3 things:

* the address of the ERC-20 token contract - `getTokenAddress()`
* how much the required deposit it - `getRequiredDeposit()`
* the address of the solver that will handle running the job for us - `getControllerAddress()`

Knowing these 3 things means we can call the standard ERC-20 `approve` to allow the solver to spend our tokens on our behalf.

Now - we can call the `runJob` method of the on chain controller from another contract. This will cause the job-creator service to kick in and do the following things:

* check that funds have been approved for the solver
* transfer those funds to it's wallet
* run the job on lilypad
* call the `submitResults` method on the on-chain job creator
* the on-chain job creator will call the `submitResults` of the original calling contract

The following is an example on-chain smart contract:

```solidity
// SPDX-License-Identifier: Apache-2.0
pragma solidity ^0.8.6;

import "@openzeppelin/contracts/access/Ownable.sol";
import "@openzeppelin/contracts-upgradeable/proxy/utils/Initializable.sol";
import "./ILilypadJobManager.sol";
import "./ILilypadJobClient.sol";

contract ExampleClient is Ownable, Initializable, ILilypadJobClient {

  address private jobManagerAddress;
  ILilypadJobManager private jobManagerContract;

  mapping(uint256 => string) private jobResults;

  event JobCreated(
    uint256 id,
    string message
  );

  event JobCompleted(
    uint256 id,
    string dealId,
    string dataId
  );

  function initialize(address _jobManagerAddress) public initializer {
    setJobManagerAddress(_jobManagerAddress);
  }

  function setJobManagerAddress(address _jobManagerAddress) public onlyOwner {
    require(_jobManagerAddress != address(0), "Job manager address");
    jobManagerAddress = _jobManagerAddress;
    jobManagerContract = ILilypadJobManager(jobManagerAddress);
  }

  function getJobResult(uint256 _jobID) public view returns (string memory) {
    return jobResults[_jobID];
  }

  function runCowsay(
    string memory message
  ) public {
    string[] memory inputs = new string[](1);
    inputs[0] = string(abi.encodePacked("Message=", message));
    uint256 id = jobManagerContract.runJob(
      "cowsay:v0.0.4",
      inputs,
      msg.sender
    );

    emit JobCreated(
      id,
      message
    );
  }

  function submitResults(
    uint256 id,
    string memory dealId,
    string memory dataId
  ) public override {
    jobResults[id] = dataId;
    emit JobCompleted(
      id,
      dealId,
      dataId
    );
  }
}
```

Here is an example of a script that brings all of this together:

```javascript
import bluebird from 'bluebird'
import {
  connectToken,
  connectJobManager,
  connectExampleClient,
  getWallet,
  getAddress,
} from '../utils/web3'
import { ethers } from 'hardhat'

async function main() {
  // it's annoying to not be able to use argv but hardhat complains about it
  const message = process.env.MESSAGE || 'Hello World!'

  const token = await connectToken()
  const manager = await connectJobManager()
  const client = await connectExampleClient()

  const setRequiredDepositTx = await manager
    .connect(getWallet('solver'))
    .setRequiredDeposit(ethers.parseEther("2"))
  await setRequiredDepositTx.wait()

  const requiredDeposit = await manager.getRequiredDeposit()

  console.log(`requiredDeposit: ${Number(requiredDeposit)}`)

  const paytokensTx = await token
    .connect(getWallet('job_creator'))
    .approve(getAddress('solver'), requiredDeposit)
  await paytokensTx.wait()

  console.log(`tokens approved: ${paytokensTx.hash}`)

  const runjobTx = await client
    .connect(getWallet('job_creator'))
    .runCowsay(message)
  const receipt = await runjobTx.wait()
  if(!receipt) throw new Error(`no receipt`)

  console.log(`submitted job: ${runjobTx.hash}`)

  let jobID = 0

  receipt.logs.forEach(log => {
    const logs = client.interface.parseLog(log as any)
    if(!logs) return
    jobID = Number(logs.args[0])
  })

  console.log(`Job ID: ${jobID}`)
  console.log(`Waiting for job to be completed...`)

  let result = ''

  while(!result) {
    result = await client.getJobResult(jobID)
    if(!result) {
      await bluebird.delay(1000)
    }
  }

  console.log(`Job result: ${result}`)
}

main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});

```

### View results

After the job is completed, a job result ID will be displayed in your terminal. The job result can be accessed through the following URL:

```
https://ipfs.io/ipfs/<JOB RESULT ID>/stdout
```

{% hint style="info" %}
Please note that the IPFS link might take some time to display the result.
{% endhint %}

## Lilypad Hardhat template

The [Lilypad Hardhat template](https://github.com/Lilypad-Tech/lilypad-hardhat-template) demonstrates how to use Lilypad within the Hardhat development environment for onchain interactions. It provides the tools and structure needed to deploy smart contracts that interact with Lilypad nodes onchain.

This template includes an example of running a job using the [`cowsay`](../developer-resources/module-marketplace/build-a-job-module/cowsay.md) module. The `cowsay` module is a simple program that generates an ASCII picture of a cow with a message.

### Getting started

You can run this template directly in [Gitpod](https://gitpod.io/new/#https://github.com/Lilypad-Tech/lilypad-hardhat-template).

The environment will automatically run a preinstall script that checks if Lilypad and Bacalhau are installed. If they are not already present on the user's machine, the script will install them.

1. Open the [Gitpod](https://gitpod.io/new/#https://github.com/Lilypad-Tech/lilypad-hardhat-template) environment
2.  Run Lilypad:

    ```bash
    npm run lilypad:up
    ```

This script builds Docker services, starts necessary components (Bacalhau, geth), funds the accounts used, deploys the contracts, and sequentially launches Lilypad related services in the background.

### Usage

This will execute [cowsay](https://docs.lilypad.tech/lilypad/lilypad-milky-way-examples/hello-cow-world) onchain using Lilypad, with the specified input message.

In a separate terminal, run this command to execute cowsay onchain:

```bash
npm run lilypad:onchain:cowsay
```

To view the results of the job, refer to [this section](lilypad-smart-contracts.md#view-results).

To update the smart contract, you can modify `ExampleClient` in `contracts/ExampleClient.sol`. Once you've made the changes, run `npm run deploy`.

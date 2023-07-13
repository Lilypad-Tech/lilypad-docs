---
description: Running a fraud detection job with Lilypad
---

# Ethereum Address Fraud Detector

## Fraud Detection

{% hint style="info" %}
Open this contract in Remix -> [Click here](https://remix.ethereum.org/bacalhau-project/lilypad/blob/main/examples/contracts/FraudDetector.sol)
{% endhint %}

### Introduction

This example uses the Fraud Detection Docker image found on [Docker Hub HackFS](https://hub.docker.com/layers/hakymulla/hackfs/inference/images/sha256-acce32dc6cc65d86eb335fe1c6c77169aa518c2d5e06bdb35cb875ce0b480179?context=repo).

Run the Image with Bacalhau using the command `bacalhau docker --network=http --domain=api.etherscan.com run hakymulla/hackfs:inference -- python predict.py --address "0x427aE6048C7d2DEd45a07Ea46F2873d0F9ddDb35"`

Run Bacalhau get \[Job ID] to the format of the spec needed to call runLilypadJob.

For more info on the dataset, how to create the Fraud Detection Script and Docker Image see [My HackFS Github](https://github.com/hakymulla/HackFS-2023).

### Code

This example can be found in the Examples folder in the Lilypad-v0 Project Github.

To run this example, you can simply deploy it to any supported network and pass in the contact address to the constructor which corresponds to your network. See deployed-network-details.md.

### Walkthrough

{% hint style="info" %}
Open this example in remix -> [click here](https://remix.ethereum.org/bacalhau-project/lilypad/edit/main/examples/contracts/FraudDetector.sol)
{% endhint %}

To Deploy on Filecoin Calibration Net, use the LilypadEvents Contract Address deployed on the testnet (0xdC7612fa94F098F1d7BB40E0f4F4db8fF0bC8820).

Call the IsFraudDetector function and add an Ethereum Address as input.

IsFraudDetector is a payable function that calls the the bridge runLilypadJob.

### Job Results

In this example the Lilypad FraudDetection Job Results is returned as a StdOut. You can use the allResult function to see the results.

### With Tableland

Let's build on the above example by Creating and Interacting with Tableland table using smart contracts.

{% hint style="info" %}
Open this example in remix -> [click here](https://remix.ethereum.org/bacalhau-project/lilypad/edit/main/examples/contracts/FraudDetectorTableland.sol)
{% endhint %}

During contract deployment, a tableland table is created. The bridge while calling the lilypadFulfilled also saves the results of inference to the table which can be used to monitor the model perfomance.

Storing a reference to the table ID and prefix within your contract is advisable since it enhances ease of reference in different methods, facilitating smoother execution.

```
uint256 public _tableId;
string private constant _TABLE_PREFIX = "fraud_detect";
```

#### Create a table

The TablelandDeployments contract helps set up the TablelandTables interface by returning ITablelandTables instantiated with the correct registry address, inferred by the chain being used. This is added to the constructor. The table columns includes an id, address and the result.

```
 _tableId = TablelandDeployments.get().create(
        address(this),
        SQLHelpers.toCreateFromSchema(
            "id integer primary key,"
            "address text,"
            "result text",
            _TABLE_PREFIX
        )
    );
```

#### Write table data

A insert function is created to write to the above table

```
function insert(
    string memory _address,
    string memory _value
) public payable onlyBridge {
    TablelandDeployments.get().mutate(
        address(this),
        _tableId,
        SQLHelpers.toInsert(
            _TABLE_PREFIX,
            _tableId,
            "id, address, result",
            string.concat(
                Strings.toString(_counter),
                ",",
                SQLHelpers.quote(_address),
                ",",
                SQLHelpers.quote(_value)
            )
        )
    );
    _counter += 1;
}
```

notice the onlyBridge modifier, only the bridge can write to the table and happens during the call back.

```
modifier onlyBridge() {
    require(msg.sender == bridgeAddress, "Not owner");
    _;
}
```

The above insert function is called in the lilypadFulfilled function

```
insert(prompts[_jobId], _result);
```

Query the table on [Click here](https://tablescan.io/playground).

<figure><img src="https://github.com/hakymulla/lilypad-docs/raw/c26568b0ebe74361e37d452048cb8ababc9dcc87/lilypad/.gitbook/assets/tableland.png" alt=""><figcaption></figcaption></figure>

# Transactions

A transaction is a fundamental data structure in a blockchain that represents a transfer of value between participants. It is a signed data message that is broadcast to the network and, if valid, is included in a block.

Transactions in this project follow the UTXO (Unspent Transaction Output) model. This means that a transaction consumes one or more existing UTXOs and creates one or more new UTXOs.

## Transaction Structure

A transaction is composed of the following main components:

- **Inputs:** A list of inputs that reference existing UTXOs to be spent.
- **Outputs:** A list of new UTXOs to be created.
- **Transaction ID (txid):** A unique identifier for the transaction.

```mermaid
graph TD
    subgraph "Previous Transaction"
        PrevTX(txid: ..., outputs: [...])
    end

    subgraph "Current Transaction"
        direction LR
        subgraph "Inputs"
            Input1("prevTxId, prevOutIndex, publicKey, signature")
        end
        subgraph "Outputs"
            Output1("value, publicKey")
            Output2("value, publicKey")
        end
    end

    Input1 -- "references" --> PrevTX
```

### Transaction Inputs

A transaction input specifies which UTXO is being spent. It contains the following fields:

- **`prevTxId`:** The transaction ID of the transaction that created the UTXO being spent.
- **`prevOutIndex`:** The index of the output in the previous transaction that created the UTXO.
- **`publicKey`:** The public key of the owner of the UTXO. This is used to verify the signature.
- **`signature`:** A digital signature created by the owner of the UTXO. This proves that the owner has authorized the spending of the UTXO.

### Transaction Outputs

A transaction output creates a new UTXO that can be spent in a future transaction. It contains the following fields:

- **`value`:** The amount of cryptocurrency to be locked in the new UTXO.
- **`publicKey`:** The public key of the recipient. This is the "address" to which the value is being sent.

### Transaction ID (txid)

The `txid` is the unique identifier of the transaction. It is calculated by hashing the serialized transaction data.

`txid = Hash(serialize(transaction))`

## Digital Signatures

A digital signature is what authorizes the spending of a UTXO. It is created by the owner of the private key corresponding to the public key in the UTXO.

The signature is not created over the entire transaction data, but over a specific part of it called the **transaction preimage**. This is to prevent a circular dependency where the signature would have to be part of the data being signed.

The preimage consists of the serialized transaction data, but with the signature fields in the inputs left empty.

```
preimage = serialize({
  inputs:  [{ prevTxId, prevOutIndex }],
  outputs: [{ value, publicKey }]
})
```

This means that if any part of the transaction is changed (e.g., the output value or recipient), the preimage will change, and the signature will become invalid. In this project, all inputs are signed with a `SIGHASH_ALL`-like flag, meaning the signature covers all inputs and outputs.

## Transaction Fees

Transaction fees are an incentive for miners to include a transaction in a block. The fee is not explicitly defined in the transaction data but is calculated as the difference between the sum of the input values and the sum of the output values.

`fee = sum(input values) - sum(output values)`

For example, if you spend a UTXO worth 8 coins and create two outputs, one for 5 coins to a recipient and one for 2 coins back to yourself as change, the transaction fee would be:

`fee = 8 - (5 + 2) = 1`

The miner who includes this transaction in a block will collect this 1-coin fee.

## The Coinbase Transaction

The coinbase transaction is a special type of transaction that is created by the miner of a block. It is always the first transaction in a block.

The coinbase transaction has the following characteristics:

- **It has no real inputs:** It has a single "dummy" input that does not reference a real UTXO and does not require a signature.
- **It creates new coins:** The output of the coinbase transaction creates new coins out of thin air. The value of this output is the sum of the block subsidy (a fixed reward for mining the block) and the total transaction fees from all other transactions in the block.

`coinbase output value = block subsidy + total fees`

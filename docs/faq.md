# Frequently Asked Questions (FAQ)

This document provides answers to some of the common questions that you may have as you work on this project.

## General Concepts

### What is a blockchain?

A blockchain is a distributed, immutable ledger that is used to record transactions. It is a chain of blocks, where each block is cryptographically linked to the previous one. See [Blockchain Primitives](concepts/blockchain-primitives.md) for more details.

### What is the genesis block?

The genesis block is the very first block in a blockchain. It is the only block that does not have a previous block to reference.

## Transactions

### Where does the transaction fee go?

The transaction fee is not an explicit output in a transaction. It is calculated as the difference between the sum of the input values and the sum of the output values. The miner who includes the transaction in a block collects the fee by adding it to the coinbase transaction. See [Transactions](concepts/transactions.md) for more details.

### Why do inputs need signatures?

Each input in a transaction spends a previously unspent transaction output (UTXO). The UTXO specifies a public key that is authorized to spend it. The signature in the input proves that the creator of the transaction has control of the corresponding private key. See [Signatures and the Preimage](concepts/signatures-preimage.md) for more details.

### What is the transaction preimage?

The transaction preimage is the specific part of the transaction data that is signed to create a digital signature. It includes the input references and the outputs, but not the signature fields themselves. This prevents a circular dependency. See [Signatures and the Preimage](concepts/signatures-preimage.md) for more details.

### What is the difference between a `txid` and a `blockHash`?

A `txid` is the unique identifier for a transaction, calculated by hashing the serialized transaction data. A `blockHash` is the unique identifier for a block, calculated by hashing the serialized block header. See [Serialization and Hashing](concepts/serialization-hashing.md) for more details.

## Mining and Blocks

### Why do we need to topologically sort transactions in a block?

Transactions in a block can have dependencies on each other (a "child" transaction can spend an output from a "parent" transaction). By placing the transactions in topological order (parents before children), we ensure that when the block is validated, the inputs for every transaction are valid. See [Mempool](concepts/mempool.md) for more details.

### What is the block subsidy?

The block subsidy is a fixed amount of new coins that are created in the coinbase transaction of a new block. It is part of the block reward that is given to the miner. See [Mining](concepts/mining.md) for more details.

## Project-Specific Questions

### Why is the block size limited to 2000 bytes?

We have set a fixed block size limit to simplify the block assembly process. This is a pedagogical choice to help you focus on the core logic of selecting transactions based on their fees and dependencies, without the complexity of a dynamic block size mechanism.

### Can I use multiple key pairs?

For the sake of simplicity, this project assumes that each participant uses a single key pair. However, the concepts you will learn can be easily extended to a system where participants can have multiple keys and addresses.

### Why are the diagrams in this documentation rendered with Mermaid?

We use Mermaid to create clear and consistent diagrams that help visualize the concepts explained in the documentation. It is a widely used tool for creating diagrams in Markdown and is well-supported by many platforms.

# Glossary

This glossary provides definitions for the key terms used in this project.

### Block

A data structure that bundles a set of transactions. It is the fundamental building block of the blockchain. Each block is linked to the previous block, forming a chain of blocks. See [Blockchain Primitives](blockchain-primitives.md).

### Block Header

The part of a block that contains metadata, such as the hash of the previous block, the Merkle root of the transactions, and the nonce. See [Blockchain Primitives](blockchain-primitives.md).

### Block Reward

The reward given to a miner for successfully mining a new block. It consists of the block subsidy and the transaction fees from the transactions included in the block. See [Mining](mining.md).

### Coinbase Transaction

The first transaction in a block, created by the miner. It has no real inputs and is used to collect the block reward. See [Transactions](transactions.md).

### DAG (Directed Acyclic Graph)

A data structure used to represent the dependencies between unconfirmed transactions in the mempool. See [Mempool](mempool.md).

### Difficulty

A measure of how hard it is to find a valid hash for a new block in a Proof-of-Work system. See [Mining](mining.md).

### Digital Signature

A cryptographic mechanism used to prove ownership and authorize transactions. See [Signatures and the Preimage](signatures-preimage.md).

### Fee

The difference between the sum of the input values and the sum of the output values in a transaction. It is an incentive for miners to include the transaction in a block. See [Transactions](transactions.md).

### Hash

A fixed-size, unique fingerprint of data, created using a cryptographic hash function. We use SHA-256 in this project. See [Serialization and Hashing](serialization-hashing.md).

### Input

A part of a transaction that references a previous unspent transaction output (UTXO) and provides the authorization to spend it. See [Transactions](transactions.md).

### Mempool

The set of all unconfirmed transactions that are waiting to be included in a block. See [Mempool](mempool.md).

### Merkle Root

A single hash that represents the entire set of transactions in a block. It is the root of the Merkle tree. See [Merkle Trees and Proofs](merkle.md).

### Merkle Tree

A binary tree of hashes used to efficiently summarize and verify the integrity of a large set of data. See [Merkle Trees and Proofs](merkle.md).

### Mining

The process of creating new blocks and adding them to the blockchain in a Proof-of-Work system. See [Mining](mining.md).

### Nonce

A random value that miners change in the block header while searching for a valid hash that meets the difficulty requirement. See [Blockchain Primitives](blockchain-primitives.md).

### Output

A part of a transaction that creates a new unspent transaction output (UTXO). See [Transactions](transactions.md).

### Preimage

The specific serialized data that is signed in a transaction to create a digital signature. See [Signatures and the Preimage](signatures-preimage.md).

### Private Key

A secret key used to create digital signatures. It must be kept private by its owner.

### Proof-of-Work (PoW)

A consensus algorithm that requires a significant amount of computational effort to create a new block. See [Mining](mining.md).

### Public Key

A key that is shared with others and is used to verify digital signatures. In our blockchain, it also serves as the "address" for receiving funds.

### Topological Sort

An ordering of the nodes in a Directed Acyclic Graph (DAG) such that for every directed edge from node A to node B, node A comes before node B in the ordering. See [Mempool](mempool.md).

### UTXO (Unspent Transaction Output)

A discrete amount of cryptocurrency that has been authorized by a sender and can be spent by a receiver. The set of all UTXOs is known as the UTXO set. See [The UTXO Model](utxo.md).

---
[← Back: Serialization and Hashing](serialization-hashing.md) · [Next: Validation Rules →](../spec/validation.md)
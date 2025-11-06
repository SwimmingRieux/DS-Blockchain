# Assignment: Build a UTXO Blockchain Node

This assignment will guide you through the process of implementing a minimal UTXO-based blockchain, complete with a command-line interface (CLI) for interacting with your node and miner. This project is designed for those new to blockchain development and is broken down into manageable milestones.

## 🎯 Learning Objectives

Upon successful completion of this assignment, you will be able to:

- **Understand and implement UTXO accounting:** Grasp the fundamentals of the Unspent Transaction Output (UTXO) model and how to use digital signatures to authorize transactions.
- **Build a mempool with fee-based prioritization:** Implement a mempool (memory pool) as a Directed Acyclic Graph (DAG) to store unconfirmed transactions, prioritizing them based on their fee-per-byte.
- **Construct and mine blocks:** Develop a block template by greedily selecting transactions from the mempool, ensuring the block does not exceed a fixed size limit. You will then mine the block using a Proof-of-Work (PoW) algorithm.
- **Generate and verify Merkle proofs:** Create and validate Merkle proofs to efficiently prove the inclusion of a transaction in a block.

## 🚀 Getting Started

1.  **Familiarize yourself with the concepts:** Before you start coding, make sure you have a solid understanding of the core blockchain primitives. Review the [conceptual documents](index.md#learning-materials) to learn about blocks, transactions, Merkle trees, and more.
2.  **Follow the milestones:** The assignment is broken down into several milestones. Follow the [Milestones & Checklists](milestones.md) to guide your implementation process.
3.  **Start with the data structures:** Begin by implementing the core data structures, such as the `Block`, `Transaction`, and `Mempool`.

## 📋 Assignment Tasks

Your primary task is to build a CLI node that can perform the following actions:

- **`GiveKeyPair`:** Generate a new public/private key pair.
- **`SetDifficulty`:** Set the mining difficulty for the blockchain.
- **`AddTransactionToMempool`:** Add a new transaction to the mempool.
- **`EvictMempool`:** Evict transactions from the mempool.
- **`MineBlock`:** Mine a new block.
- **`GetMerkleProof`:** Get a Merkle proof for a given transaction.
- **`VerifyTxInclusion`:** Verify that a transaction is included in a block.

To support this functionality, you will need to implement the following data structures:

- **Blockchain:** A linked list of blocks.
- **UTXO Map:** A data structure to keep track of the unspent transaction outputs.
- **Mempool DAG:** A Directed Acyclic Graph to store and manage unconfirmed transactions.
- **Balanced Trees:** Two balanced trees for ancestor and descendant scores in the mempool.

## ⛓️ Constraints and Rules

To ensure consistency and fair grading, your implementation must adhere to the following constraints:

- **Block Size Limit:** 2000 bytes (including the header and all transactions).
- **Hash Function:** SHA-256 must be used consistently for all hashing operations.

Your implementation must also pass the following validation rules:

- Inputs must reference existing UTXOs.
- Digital signatures must be valid.
- No double-spending of UTXOs.
- Transaction fees must be non-negative (≥ 0).
- The total block size must not exceed 2000 bytes.
- The block hash must satisfy the PoW difficulty.
- The Merkle root in the block header must be correct.

---
[Back to Index](index.md) · [Next: Milestones & Checklists →](milestones.md)

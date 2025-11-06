# Assignment: Build a UTXO Blockchain Node

This assignment will guide you through the process of implementing a minimal UTXO-based blockchain, complete with a command-line interface (CLI) for interacting with your node and miner. This project is designed for those new to blockchain development and is broken down into manageable milestones.

## 🎯 Learning Objectives

Upon successful completion of this assignment, you will be able to:

- **Understand and implement UTXO accounting:** Grasp the fundamentals of the Unspent Transaction Output (UTXO) model and how to use digital signatures to authorize transactions.
- **Build a mempool with fee-based prioritization:** Implement a mempool (memory pool) as a Directed Acyclic Graph (DAG) to store unconfirmed transactions, prioritizing them based on their fee-per-byte.
- **Construct and mine blocks:** Develop a block template by greedily selecting transactions from the mempool, ensuring the block does not exceed a fixed size limit. You will then mine the block using a Proof-of-Work (PoW) algorithm.
- **Generate and verify Merkle proofs:** Create and validate Merkle proofs to efficiently prove the inclusion of a transaction in a block.

## 🚀 Getting Started

1.  **Familiarize yourself with the concepts:** Before you start coding, make sure you have a solid understanding of the core blockchain primitives. Review the documents in the `concepts` directory to learn about blocks, transactions, Merkle trees, and more.
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
- **Public Keys:** Outputs must store full public keys, not hashes of public keys.
- **Simplifications:** No versioning, timestamps, locktime, or sequence numbers are required. The mining difficulty is fixed and does not need to be retargeted. No networking component is required.

Your implementation must also pass the following validation rules:

- Inputs must reference existing UTXOs.
- Digital signatures must be valid.
- No double-spending of UTXOs.
- Transaction fees must be non-negative (≥ 0).
- The total block size must not exceed 2000 bytes.
- The block hash must satisfy the PoW difficulty.
- The Merkle root in the block header must be correct.

##  deliverables and Evaluation

### Deliverables

- **Source Code:** Your complete source code, along with a `README` file that explains how to compile and run your project.
- **Report:** A short report (which can be a section in your `README`) that maps your code to the requirements in this specification.
- **Sample Data:** Sample input and output data, including a sample transaction in JSON format, a listing of your mempool, and a mined block in JSON format.

### Evaluation Criteria

We will test your implementation based on the following criteria:

- Correct acceptance and rejection of transactions.
- Correct ordering of transactions in the mempool after adding and evicting transactions.
- Proper construction of blocks that adhere to the size limit.
- Valid Proof-of-Work and Merkle root.
- Correct verification of Merkle proofs (returning `true` or `false` as appropriate).

## 🕒 Time Guidance

- **Total Time:** Approximately 10–14 hours, spread across 2–3 weeks, depending on your prior experience.
- **Recommended Pace:** Aim to complete 1–2 milestones per study session.

---
[Back to Index](index.md) · [Next: Milestones & Checklists →](milestones.md)

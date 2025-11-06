# Assignment Milestones

This document breaks down the assignment into a series of manageable milestones. Each milestone has a clear set of tasks and acceptance criteria to help you track your progress and verify that your implementation is correct.

## Milestone 1: The Building Blocks

In this milestone, you will implement the fundamental data structures and cryptographic primitives of your blockchain.

### Tasks

-   **Key Pair Generation:** Implement a function to generate a new public/private key pair. The keys should be represented as hexadecimal strings.
-   **Serialization:** Define and implement a deterministic set of rules for serializing your data structures (blocks, transactions, etc.).
-   **Transaction ID (txid):** Implement a function to calculate the `txid` of a transaction by hashing its serialized data.
-   **UTXO Set:** Implement the UTXO set as a map where the key is `txid:index` and the value is `{ value, publicKey }`.

### Acceptance Criteria

-   The `GiveKeyPair` command correctly prints a new key pair.
-   Serializing the same transaction twice produces the exact same byte sequence.
-   Adding outputs from a new transaction correctly creates new entries in the UTXO set.

## Milestone 2: Creating and Validating Transactions

Now that you have the basic building blocks, you will implement the logic for creating and validating transactions.

### Tasks

-   **Transaction Structure:** Define the structure of a transaction, including inputs (`prevTxId`, `prevOutIndex`, `publicKey`, `signature`) and outputs (`value`, `publicKey`).
-   **Transaction Preimage:** Implement the logic to create the transaction preimage for signing.
-   **Signature Verification:** Implement a function to verify the digital signature of a transaction. This includes checking that the referenced UTXOs exist, the public keys match, and the signature is valid for the preimage.
-   **Fee Calculation:** Implement the logic to calculate the transaction fee as `sum(inputs) - sum(outputs)` and ensure that it is non-negative.

### Acceptance Criteria

-   A valid transaction is accepted by your node.
-   A transaction with a tampered output (e.g., a changed value or recipient) fails signature verification.
-   A transaction with a negative fee is rejected.

## Milestone 3: The Mempool

In this milestone, you will implement the mempool, which is the waiting area for unconfirmed transactions.

### Tasks

-   **DAG Structure:** Implement the mempool as a Directed Acyclic Graph (DAG) to track the dependencies between transactions.
-   **Transaction Scoring:** Implement the ancestor and descendant fee rate scoring mechanisms. Use two balanced binary search trees to maintain the order of transactions.
-   **`AddTransactionToMempool`:** Implement the `AddTransactionToMempool` command, which should print the mempool sorted in descending order by ancestor fee rate.
-   **`EvictMempool`:** Implement the `EvictMempool` command, which should remove the `x` least valuable transactions (by descendant fee rate) and their descendants, and then print the mempool sorted in ascending order by descendant fee rate.

### Acceptance Criteria

-   Transactions with dependencies are correctly ordered in the mempool.
-   Evicting a transaction also removes all of its descendants.

## Milestone 4: Assembling a Block

Now it's time to play the role of a miner and assemble a new block from the transactions in the mempool.

### Tasks

-   **Greedy Selection:** Implement a greedy algorithm to select transactions from the mempool based on their ancestor fee rate, ensuring that the total block size does not exceed the 2000-byte limit.
-   **Dependency Management:** Ensure that if a transaction is included in a block, all of its unconfirmed ancestors are also included.
-   **Topological Sort:** Topologically sort the selected transactions before including them in the block.
-   **Coinbase Transaction:** Create the coinbase transaction to collect the block reward (subsidy + fees).

### Acceptance Criteria

-   The total size of the assembled block (including the header) is within the 2000-byte limit.
-   The transactions in the block are in a valid topological order (parents before children).

## Milestone 5: Mining the Block

In this milestone, you will implement the Proof-of-Work mining process.

### Tasks

-   **Merkle Root:** Calculate the Merkle root of the transactions in the block.
-   **Proof-of-Work:** Implement the mining loop that searches for a `nonce` that results in a block hash with the required number of leading zero bits.
-   **Block Output:** Output the full, valid block in JSON format.

### Acceptance Criteria

-   The hash of the mined block meets the specified difficulty.
-   The fields in the outputted block JSON match the specification.

## Milestone 6: Proving Inclusion

The final milestone is to implement Merkle proofs, which allow for efficient verification of transaction inclusion.

### Tasks

-   **`GetMerkleProof`:** Implement the `GetMerkleProof` command, which should return the list of sibling hashes and their positions required to prove the inclusion of a transaction.
-   **`VerifyTxInclusion`:** Implement the `VerifyTxInclusion` command, which should return `true` if the proof is valid and `false` otherwise.

### Acceptance Criteria

-   A valid Merkle proof correctly verifies against the Merkle root in the block header.

## Conclusion

By completing these milestones, you will have built a fully functional, single-node blockchain from the ground up. Congratulations on this significant achievement!

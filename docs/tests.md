# Testing Your Implementation

This document provides a set of tests that you can use to verify that your implementation is working correctly at each milestone. Running these tests will help you catch bugs early and ensure that you are on the right track.

## Milestone 1: Keys and UTXOs

### Test: Key Pair Generation

-   **Command:** `GiveKeyPair`
-   **Expected Outcome:** The command should print two hexadecimal strings, representing the private key and the public key.

## Milestone 2: Transactions and Signatures

### Test: Valid Transaction Admission

1.  Create a valid transaction in JSON format that references an existing UTXO and is correctly signed.
2.  **Command:** `AddTransactionToMempool <path-to-your-tx.json>`
3.  **Expected Outcome:** The command should print the state of the mempool in JSON format, with the transactions sorted in descending order by ancestor fee rate.

### Test: Tampered Transaction

1.  Take a valid transaction and modify one of the output values.
2.  **Command:** `AddTransactionToMempool <path-to-tampered-tx.json>`
3.  **Expected Outcome:** The transaction should be rejected due to a signature verification failure.

## Milestone 3: The Mempool

### Test: Transaction Eviction

-   **Command:** `EvictMempool 1`
-   **Expected Outcome:** The command should remove the transaction with the lowest descendant fee rate (and all of its descendants) from the mempool. The output should be the state of the mempool, sorted in ascending order by descendant fee rate.

## Milestone 4 & 5: Block Assembly and Mining

### Test: Mining a Block

1.  **Commands:**
    ```bash
    $ ./your-node-program SetDifficulty 12
    $ ./your-node-program MineBlock
    ```
2.  **Expected Outcome:** The command should output a valid block in JSON format. The block hash must meet the specified difficulty, the total size must be less than or equal to 2000 bytes, and the coinbase transaction must correctly collect the block subsidy and transaction fees.

## Milestone 6: Merkle Proofs

### Test: Merkle Proof Verification

1.  **Commands:**
    ```bash
    $ ./your-node-program GetMerkleProof <txid> <block-height>
    $ ./your-node-program VerifyTxInclusion <proof-file> <merkle-root>
    ```
2.  **Expected Outcome:** The `VerifyTxInclusion` command should return `true` for a transaction that is included in the block and `false` for a transaction that is not.

## Example: Transaction JSON

This is an example of a minimal transaction in JSON format, with one input and two outputs.

```json
{
  "inputs": [
    { "prevTxId": "abc...", "prevOutIndex": 0, "publicKey": "02..", "signature": "30.." }
  ],
  "outputs": [
    { "value": 5000, "publicKey": "02.." },
    { "value": 2000, "publicKey": "03.." }
  ]
}
```

## Example: Mempool JSON

This is an example of the output of the `AddTransactionToMempool` command, showing two transactions in the mempool.

```json
{
  "count": 2,
  "txs": [
    { "txid": "a1..", "ancestorFee": 900, "ancestorSize": 450, "ancestorFeeRate": 2.0 },
    { "txid": "b2..", "ancestorFee": 100, "ancestorSize": 200, "ancestorFeeRate": 0.5 }
  ]
}
```

## Example: Block JSON

This is an example of a mined block in JSON format.

```json
{
  "header": {
    "prevBlockHash": "000...",
    "merkleRoot": "def...",
    "difficulty": 12,
    "nonce": 12345
  },
  "transactions": [
    { ... coinbase transaction ... },
    { ... transaction 1 ... },
    { ... transaction 2 ... }
  ]
}
```

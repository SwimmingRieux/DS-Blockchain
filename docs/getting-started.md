# Getting Started (Lab 0)

Goal: set up your environment and learn the core flow by running small, verifiable steps.

## Task A: Generate a keypair
- Run `GiveKeyPair` and save the output.
- Checkpoint: you can paste your `publicKey` into outputs later.

## Task B: Understand UTXOs
- Read `concepts/utxo.md`.
- Draw a small picture of one UTXO you own: `(txid, index, value, publicKey)`.

## Task C: Build a sample transaction
- Start from one UTXO you own (invent one if needed for practice).
- Create a JSON with 1 input and 2 outputs (pay + change).
- Check against `spec/json-formats.md`.
- Checkpoint: compute its txid by serializing then hashing.

## Task D: Sign the preimage
- Recreate the preimage skeleton (inputs as references, outputs with values and recipients).
- Sign with your private key; attach `signature` to the input.
- Checkpoint: tamper with an output value by +1 and observe signature failure.

## Task E: Add to mempool
- `AddTransactionToMempool <tx-json>`
- Observe the printed order (sorted descending by ancestor fee per byte).
- Checkpoint: create a child tx that spends the change; add it and confirm the DAG order.

## Task F: Mine a block
- `SetDifficulty 12` (or similar), then `MineBlock`.
- Checkpoint: verify block JSON—header fields, merkleRoot, nonce; total size ≤ 2000 bytes.

## Task G: Prove inclusion
- `GetMerkleProof <txid> <height>`, then `VerifyTxInclusion`.
- Checkpoint: result is `true` for your tx; `false` for a random txid.

When finished with Lab 0, you can proceed milestone-by-milestone with `milestones.md`. Each milestone has acceptance criteria to help you self-verify your implementation.

---
[Back to Index](index.md) · [← Back: Tests & Example I/O](tests.md) · [Next: Background (Bitcoin vs This Project) →](concepts/background.md)

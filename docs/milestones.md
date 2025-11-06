# Milestones & Checklists

Use these to track progress. Each milestone has acceptance criteria you must satisfy.

## M1: Keys, Serialization, txid, UTXO
- Implement keypair generation (hex output)
- Implement deterministic serialization rules
- Compute `txid = Hash(serialize(tx))`
- UTXO map: key `txid:index`, value `{ value, publicKey }`
- Acceptance:
  - `GiveKeyPair` prints two hex strings
  - Serializing the same tx twice yields identical bytes
  - Adding outputs produces correct UTXO entries

## M2: Transactions & Signatures
- Input carries `prevTxId`, `prevOutIndex`, `publicKey`, `signature`
- Preimage = inputs (references only) + outputs (values, public keys)
- Verify: referenced UTXOs exist and match input public keys; signature valid
- Fees: inputs − outputs ≥ 0
- Acceptance:
  - Valid tx admitted; tampered outputs cause signature failure
  - Negative fee rejected

## M3: Mempool DAG & Scoring
- Track parents/children; prevent cycles
- Maintain ancestor and descendant aggregates; RB-trees for ordering
- `AddTransactionToMempool` prints the mempool sorted in descending order by ancestor fee per byte
- `EvictMempool x` removes x least valuable by descendant fee per byte (and their descendants), then prints the mempool sorted in ascending order by descendant fee per byte
- Acceptance:
  - Dependent txs show correct ordering and removal

## M4: Block Assembly (≤ 2000 bytes)
- Greedy selection by ancestor fee per byte within the size limit
- Include required ancestors; topologically sort the chosen subset
- Create coinbase paying subsidy + fees
- Acceptance:
  - Selected set fits within 2000 bytes (including header)
  - Topological order validated (parents before children)

## M5: Mining
- Compute Merkle root; search nonce until `leadingZeroBits` satisfied
- Output full block JSON in specified format
- Acceptance:
  - Block hash meets difficulty; JSON fields match spec

## M6: Merkle Proofs
- `GetMerkleProof txid height` returns sibling list with positions
- `VerifyTxInclusion` returns true for included tx and false otherwise
- Acceptance:
  - Proof verifies against the block’s header merkleRoot

---
[← Back: Assignment Brief](assignment.md) · [Next: Grading Rubric & Submission →](rubric.md)

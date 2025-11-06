# Assignment Brief: UTXO Blockchain (Single-Node Miner)

This assignment guides you to implement a minimal UTXO-based blockchain with a CLI node/miner. It is structured for first-time learners and broken into milestones with checklists.

## Learning objectives
- Understand UTXO accounting and input-level signatures
- Build a mempool as a DAG with fee/byte prioritization
- Assemble blocks greedily under a byte-size limit and mine with PoW
- Generate and verify Merkle proofs

## What you must build
1. CLI node that accepts commands:
   - GiveKeyPair, SetDifficulty, AddTransactionToMempool, EvictMempool, MineBlock, GetMerkleProof, VerifyTxInclusion
2. Data structures:
   - Blockchain (linked list), UTXO map, Mempool DAG, two balanced trees for ancestor/descendant scores
3. Validation rules (must pass):
   - Inputs reference existing UTXOs, signatures verify, no double-spends, fees ≥ 0, block ≤ 2000 bytes, PoW difficulty satisfied, Merkle root correct

## Constraints (fixed for grading)
- Block size limit = 2000 bytes (header + all transactions)
- Hash = SHA-256 (use consistently)
- Outputs store full public keys (not hashes)
- No version/timestamp/locktime/sequence; no retargeting; no networking

## Deliverables
- Source code with a README (how to run)
- A short report (or README section) mapping your code to this spec
- Demo inputs/outputs: sample tx JSON, mempool listings, and a mined block JSON

## Milestones
- See detailed checklists in [Milestones & Checklists](milestones.md)

## What we will test
- Correct acceptance/rejection of transactions
- Correct mempool ordering after add/evict
- Proper block construction under the size limit
- Valid PoW and Merkle root
- Proof verification returns true/false correctly

## Time guidance
- Total time: ~10–14 hours across 2–3 weeks, depending on experience
- Recommended pace: 1–2 milestones per study session

---
[Back to Index](index.md) · [Next: Milestones & Checklists →](milestones.md)

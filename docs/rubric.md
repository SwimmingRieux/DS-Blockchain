# Grading Rubric & Submission

Total: 100 points

- M1 Keys/Serialization/UTXO: 15
- M2 Transactions/Signatures/Fees: 20
- M3 Mempool DAG & Scoring (add/evict outputs correct): 20
- M4 Block Assembly under 2000 B + Topo Order + Coinbase: 20
- M5 Mining (difficulty, block JSON correctness): 15
- M6 Merkle Proofs & Verification: 10

Deductions:
- -5 incorrect JSON shapes or field names that break consumers
- -5 non-deterministic serialization that changes txid across runs
- -5 for accepting double-spends in mempool or blocks

## Submission
- Push code and docs to your repo
- README must include:
  - How to build/run
  - Commands to reproduce your demo (add txs, mine block, get proof)
  - Which optional pieces (if any) you implemented
- Provide sample input/output transcripts demonstrating each milestone

---
[← Back: Milestones & Checklists](milestones.md) · [Next: Tests & Example I/O →](tests.md)

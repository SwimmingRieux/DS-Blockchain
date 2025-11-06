# Background: Bitcoin vs This Project

This project mirrors the essential ideas of Bitcoin while simplifying many details so they’re easier to learn.

## What we keep (core ideas)
- UTXO model: transactions consume previous outputs and create new ones
- Input-level signatures: each input proves authorization
- Fees are implicit: inputs − outputs; miner collects via coinbase
- Mempool as a dependency structure: parents before children
- Merkle root in block header; Proof-of-Work mining with a nonce

## What we simplify (on purpose)
- One public key per participant (no address formats)
- Outputs store full public keys (not hashes)
- Fixed block size limit (2300 bytes) rather than dynamic/weight rules
- No networking: commands via CLI; no peers or propagation
- No locktime/sequence/version/timestamp; no coinbase maturity
- No difficulty retargeting and no chain reorgs

## Why these choices
- Pedagogy: fewer moving parts → you can focus on core data structures
- Determinism: easier to test and understand
- Small sizes: blocks are small, proofs are short, code is simpler

After you master this project, you’ll be ready to learn the real-world extensions Bitcoin uses.

# Data Structures + Blockchain: Course Project

Welcome! This site is an assignment-first, beginner-friendly guide to building a simplified UTXO-based blockchain.

## Start here (assignment flow)
- [Assignment Brief](assignment.md)
- [Milestones & Checklists](milestones.md)
- [Grading Rubric & Submission](rubric.md)
- [Tests & Example I/O](tests.md)

## Learning materials
- [Getting Started (Lab 0)](getting-started.md)
- [Background: Bitcoin vs This Project](concepts/background.md)
- Concepts
  - [Blockchain Primitives](concepts/blockchain-primitives.md)
  - [Transactions](concepts/transactions.md)
  - [UTXO Set](concepts/utxo.md)
  - [Mempool: DAG and RB-Trees](concepts/mempool.md)
  - [Mining and Difficulty](concepts/mining.md)
  - [Merkle Trees and Proofs](concepts/merkle.md)
  - [Signatures & Preimage](concepts/signatures-preimage.md)
  - [Serialization & Hashing](concepts/serialization-hashing.md)
  - [Glossary](concepts/glossary.md)
- Specs
  - [Validation Rules](spec/validation.md)
  - [CLI Commands](spec/cli.md)
  - [Constant JSON Formats](spec/json-formats.md)
- Support
  - [FAQ](faq.md)

## Architecture (simple view)
<div class="mermaid">
flowchart TD
  CLI["CLI Commands"] --> Parser["Parser"]
  Parser --> MP["Mempool<br/>(DAG + RB-trees)"]
  MP --> Asm["Block Assembler<br/>(greedy fee/byte + topo order)"]
  Asm --> Miner["Miner (PoW)"]
  Miner --> BC["Blockchain<br/>(Linked List)"]
  BC <--> UTXO["UTXO Map"]
</div>


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

## System flow (end-to-end)
{% raw %}
<div class="mermaid">
flowchart TD
  subgraph CLI["CLI"]
    A1["GiveKeyPair"]
    A2["AddTransactionToMempool"]
    A3["EvictMempool"]
    A4["MineBlock"]
    A5["GetMerkleProof / Verify"]
  end

  A2 --> V1["Validate tx<br/>- check UTXO exists<br/>- pubKey match<br/>- signature ok<br/>- fee >= 0"]
  V1 -- ok --> M1["Update Mempool<br/>- add node to DAG<br/>- update ancestor/descendant aggregates<br/>- update both RB-trees"]
  V1 -- fail --> R1["Reject and explain"]
  M1 --> O1["Print mempool<br/>(sorted descending by ancestor fee per byte)"]

  A3 --> E1["Evict x least valuable<br/>(by descendant fee per byte)<br/>and their descendants"]
  E1 --> O2["Print mempool<br/>(sorted ascending by descendant fee per byte)"]

  A4 --> S1["Select txs greedy<br/>by ancestor fee per byte<br/>under 2000 bytes"]
  S1 --> S2["Ensure parents included"]
  S2 --> S3["Topological sort"]
  S3 --> H1["Compute txids and Merkle root"]
  H1 --> P1["Find nonce (PoW)<br/>leadingZeroBits"]
  P1 --> B1["Build block JSON"]
  B1 --> U1["Apply block<br/>- update UTXO map<br/>- remove mined from mempool"]
  B1 --> O3["Output block JSON"]

  A5 --> MP1["Prove/Verify using Merkle root"]
</div>
{% endraw %}


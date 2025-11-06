# Background: This Project vs. Bitcoin

This project is designed to be a simplified, educational version of a UTXO-based blockchain like Bitcoin. By stripping away some of the complexities of a real-world implementation, you can focus on the core concepts and data structures that make a blockchain work.

This document provides a comparison between the features of this project and those of Bitcoin, and explains the pedagogical reasons for the simplifications we have made.

## Feature Comparison

Here is a side-by-side comparison of the key features of this project and Bitcoin:

| Feature                  | This Project                                       | Bitcoin                                                              |
| ------------------------ | -------------------------------------------------- | -------------------------------------------------------------------- |
| **Accounting Model**     | UTXO Model                                         | UTXO Model                                                           |
| **Signatures**           | Input-level signatures                             | Input-level signatures                                               |
| **Fees**                 | Implicit (inputs - outputs)                        | Implicit (inputs - outputs)                                          |
| **Mempool**              | DAG with parent-child dependencies                 | DAG with parent-child dependencies                                   |
| **Mining**               | Proof-of-Work with nonce                           | Proof-of-Work with nonce                                             |
| **Public Keys**          | Full public keys stored in outputs                 | Public key hashes (addresses) stored in outputs                      |
| **Block Size**           | Fixed limit (2000 bytes)                           | Dynamic weight limit                                                 |
| **Networking**           | None (CLI-based)                                   | Peer-to-peer network for transaction and block propagation           |
| **Advanced Features**    | None (no locktime, sequence, version, timestamp)   | Includes locktime, sequence, version, and timestamps                 |
| **Difficulty Adjustment**| Manual (fixed)                                     | Automatic retargeting every 2016 blocks                              |
| **Chain Reorganization** | Not handled                                        | Handled (longest chain rule)                                         |

## Why These Simplifications?

The simplifications in this project were made for specific pedagogical reasons:

- **Focus on Core Concepts:** By removing features like networking and dynamic difficulty adjustment, you can focus your attention on the core data structures and algorithms, such as the UTXO set, the mempool, and the block assembly process.
- **Determinism:** The absence of a network and the use of a fixed difficulty make the system deterministic. This makes it much easier to test your implementation and reason about its behavior.
- **Simplicity:** A simpler codebase is easier to understand, debug, and complete in a reasonable amount of time.

## A Stepping Stone to the Real World

By mastering the concepts in this project, you will build a strong foundation in the fundamentals of blockchain technology. You will be well-prepared to tackle the more advanced and complex features of real-world blockchains like Bitcoin.

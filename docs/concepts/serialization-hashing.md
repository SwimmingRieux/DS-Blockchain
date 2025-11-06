# Serialization and Hashing

Serialization and hashing are two of the most important concepts in blockchain technology. They are the foundation upon which the integrity and consistency of the distributed ledger are built.

- **Serialization** is the process of converting a data structure, such as a block or a transaction, into a format that can be easily stored or transmitted. In a blockchain, it is crucial that all participants in the network serialize data in the exact same way to ensure that they all get the same hash.
- **Hashing** is the process of taking an input of any size and producing a fixed-size output, known as a hash. This process is one-way, meaning it is computationally infeasible to reverse. In a blockchain, hashing is used to create unique identifiers for blocks and transactions, and to ensure the integrity of the data.

## Serialization

To ensure that all nodes in the network can agree on the state of the blockchain, there must be a strict set of rules for how data is serialized. In this project, we will use the following rules:

- **Field Order:** The fields of a data structure must be serialized in the exact order that they are documented.
- **Encoding:** All strings must be encoded using UTF-8, and all numbers must be encoded in big-endian format. Alternatively, a consistent JSON canonicalization scheme can be used.

### Transaction Signing Preimage

When creating a digital signature for a transaction, we do not sign the entire transaction data. Instead, we sign a specific subset of the data called the **transaction preimage**. This is to avoid a circular dependency where the signature would have to be part of the data being signed.

The preimage includes only the input references (`prevTxId` and `prevOutIndex`) and the outputs (`value` and `publicKey`). The signature fields in the inputs are left empty.

## Hashing

Once a data structure has been serialized, it can be hashed to produce a unique, fixed-size identifier.

### Transaction ID (txid)

The `txid` is the unique identifier for a transaction. It is calculated by hashing the full serialized transaction data, including the digital signatures.

`txid = Hash(serialize(full transaction))`

### Block Hash

The `blockHash` is the unique identifier for a block. It is calculated by hashing the serialized block header.

`blockHash = Hash(serialize(header))`

The block header contains the following fields:

- `prevBlockHash`
- `merkleRoot`
- `difficulty`
- `nonce`

For all hashing operations in this project, you should consistently use a single hash function, such as SHA-256.

## Data Size Model

To select transactions for a new block, the miner needs to know the size of each transaction to ensure that the total block size does not exceed the 2000-byte limit. The size of a transaction is the sum of the sizes of its fields.

Here is a table of the field sizes used in this project:

| Field             | Size (bytes) |
| ----------------- | :----------: |
| Hash              |      32      |
| Index (output)    |      4       |
| Value             |      8       |
| PublicKey (comp.) |      33      |
| Signature         |      64      |

### Example Calculation

Let's calculate the size of a typical transaction with one input and two outputs:

- **Input:** `prevTxId` (32) + `prevOutIndex` (4) + `publicKey` (33) + `signature` (64) = 133 bytes
- **Outputs:** 2 * (`value` (8) + `publicKey` (33)) = 82 bytes
- **Total:** 133 + 82 = 215 bytes (plus a few bytes for counters/overhead)

Now, let's consider the size of a block with a header, a coinbase transaction, and nine typical transactions:

- **Header:** `prevBlockHash` (32) + `merkleRoot` (32) + `difficulty` (1) + `nonce` (4) = 69 bytes
- **Coinbase Transaction:** 1 dummy input (36) + 1 output (41) = 77 bytes (plus overhead)
- **9 Transactions:** 9 * 215 = 1935 bytes
- **Total:** 69 + 77 + 1935 = 2081 bytes

This total exceeds the 2000-byte block size limit, which shows that a miner must be careful when selecting transactions to include in a block.

## Why it Matters

The strict rules for serialization and hashing are what make the blockchain secure and immutable. Any tiny change to the data in a block or transaction will result in a completely different hash. This makes it easy to detect any tampering with the data and is a fundamental building block for features like Merkle proofs.

---
[← Back: Digital Signatures and the Transaction Preimage](signatures-preimage.md) · [Next: Glossary →](glossary.md)
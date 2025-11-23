# Serialization and Hashing

Serialization and hashing are two of the most important concepts in blockchain technology. They are the foundation upon which the integrity and consistency of the distributed ledger are built.

- **Serialization** is the process of converting a data structure, such as a block or a transaction, into a format that can be easily stored or transmitted. In a blockchain, it is crucial that all participants in the network serialize data in the exact same way to ensure that they all get the same hash. In this project, we will use JSON as our serialization format.
- **Hashing** is the process of taking an input of any size and producing a fixed-size output, known as a hash. This process is one-way, meaning it is computationally infeasible to reverse. In a blockchain, hashing is used to create unique identifiers for blocks and transactions, and to ensure the integrity of the data.

## Serialization

To ensure that all nodes in the network can agree on the state of the blockchain, there must be a strict set of rules for how data is serialized. In this project, we will serialize our data structures into a JSON string. To ensure that the JSON string is always the same, we will follow these rules:

- **Field Order:** The fields of a data structure must be serialized in the exact order that they are documented.
- **No extra whitespace:** The JSON string should not contain any extra whitespace.

For example, a simple object like `{ "b": 1, "a": 2 }` should be serialized as `{"a":2,"b":1}` if the documented order is `a` then `b`.

### Transaction Signing Preimage

When creating a digital signature for a transaction, we do not sign the entire transaction data. Instead, we sign a specific subset of the data called the **transaction preimage**. This is to avoid a circular dependency where the signature would have to be part of the data being signed.

The preimage includes only the input references (`prevTxId` and `prevOutIndex`) and the outputs (`value` and `publicKey`). The signature fields in the inputs are left empty. The preimage is then serialized into a JSON string before being signed.

## Hashing

Once a data structure has been serialized into a JSON string, it can be hashed to produce a unique, fixed-size identifier.

### Transaction ID (txid)

The `txid` is the unique identifier for a transaction. It is calculated by hashing the full serialized transaction JSON string, including the digital signatures.

`txid = Hash(serialize(full transaction))`

### Block Hash

The `blockHash` is the unique identifier for a block. It is calculated by hashing the serialized block header JSON string.

`blockHash = Hash(serialize(header))`

The block header contains the following fields (for the genesis block, `prevBlockHash` is a string of 64 zeros):

- `prevBlockHash`
- `merkleRoot`
- `difficulty`
- `nonce`

For all hashing operations in this project, you should consistently use a single hash function, such as SHA-256.

## Why it Matters

The strict rules for serialization and hashing are what make the blockchain secure and immutable. Any tiny change to the data in a block or transaction will result in a completely different hash. This makes it easy to detect any tampering with the data and is a fundamental building block for features like Merkle proofs.

---
[← Back: Digital Signatures and the Transaction Preimage](signatures-preimage.md) · [Next: Glossary →](glossary.md)
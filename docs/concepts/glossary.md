# Glossary

- Block: A group of transactions plus a header linking to the previous block
- Coinbase: The first transaction in a block that creates new coins and collects fees
- DAG: Directed Acyclic Graph representing dependencies among unconfirmed transactions
- Difficulty: How hard it is to find a block hash with leading zeros
- Fee: The difference `sum(inputs) − sum(outputs)` of a transaction
- Hash: A fixed-size fingerprint of data (we use SHA-256)
- Input: A reference to a previous unspent output, plus authorization
- Merkle root: Hash that commits to all transaction ids in the block
- Mempool: Set of unconfirmed transactions waiting to be mined
- Output: A coin created by a transaction; identified by `(txid, index)`
- Preimage: The exact serialized content being signed
- Topological sort: An order of DAG nodes where parents come before children
- UTXO: Unspent Transaction Output; the spendable coins set

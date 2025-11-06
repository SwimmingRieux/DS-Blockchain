# Blockchain Primitives

This project uses the minimum fields needed for a functioning, educational blockchain.

## Block
- Header
  - `prevBlockHash` (32 B): hash of previous block header
  - `merkleRoot` (32 B): root over `txid`s
  - `difficulty` (1 B): leading-zero bits requirement
  - `nonce` (4 B): varied to satisfy difficulty
- Body
  - Transactions (first is coinbase)

`blockHash = Hash(header)` and is not stored inside the header.

### Block size (bytes; fixed constant)
- “Block size” means the total serialized bytes of the header + all transactions.
- We set a fixed limit: 2000 bytes.

## Transaction
- `inputs[]`: each references a previous unspent output `(prevTxId, prevOutIndex)` and carries `publicKey` and `signature`
- `outputs[]`: new coins `(value, publicKey)`
- `txid`: hash of the serialized transaction

### ASCII ER snapshot (what references what)
```
TX  --has-->  INPUT
TX  --creates--> OUTPUT
INPUT --spends--> UTXO (which is an OUTPUT identified by (txid, index))
```

### Fees (implicit)
- `fee = sum(inputs) − sum(outputs) ≥ 0`
- Miner collects all fees via the block’s coinbase output

## Chain as a linked list
- Each block header points to the previous via `prevBlockHash`
- The node keeps a pointer to the current tip and validates each added block


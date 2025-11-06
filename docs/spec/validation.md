# Validation Rules

## Transaction validation (non-coinbase)
- For each input
  - Referenced UTXO `(prevTxId, prevOutIndex)` exists and is unspent
  - UTXO.publicKey equals input.publicKey
  - Signature verifies over the preimage
- Sum(inputs) ≥ Sum(outputs)
- Fee = Sum(inputs) − Sum(outputs) ≥ 0
- No input references the same UTXO twice in the same tx

## Coinbase transaction
- Exactly one dummy input
- Outputs value = `subsidy + sum(fees of included txs)`

## Block validation
- First transaction is coinbase; others are not
- No intra-block double-spends
- Merkle root matches transactions’ `txid`s
- Proof of Work meets `difficulty.leadingZeroBits`
- Block size limit: total serialized bytes of header + transactions ≤ 2000 bytes
- Header `prevBlockHash` equals hash of previous block header

## Mempool admission
- All transaction rules apply; parents may be unconfirmed but must be present (or referenced) in the mempool
- Maintain DAG edges to parents; reject if it creates a cycle

## Signing preimage (what you sign and verify)
```
preimage = serialize({
  inputs:  [{ prevTxId, prevOutIndex }],
  outputs: [{ value, publicKey }]
})
```
- All inputs sign the same preimage (SIGHASH_ALL-like)
- Verification uses the input’s `publicKey`

## Beginner’s note: fees and coinbase
- Users set a fee by making `sum(outputs) < sum(inputs)`; the difference is the fee
- Miners collect all fees in the block’s coinbase output


# Transactions

A transaction consumes previously unspent outputs (UTXOs) and creates new outputs.

## Structure
- Inputs
  - `prevTxId`, `prevOutIndex`: identify a UTXO
  - `publicKey`: the spender’s key
  - `signature`: proves authorization over the preimage
- Outputs
  - `value` (integer)
  - `publicKey` (recipient)
- `txid` = `Hash(serialize(tx))`

## What does the signature cover?
Signature is over the transaction preimage:

```
preimage = serialize({
  inputs:  [{ prevTxId, prevOutIndex }],
  outputs: [{ value, publicKey }]
})
```

- Inputs include only references in the preimage (no signatures) to avoid circularity
- All inputs sign the same preimage (SIGHASH_ALL-like)

If any output value or recipient changes, the preimage changes and signatures fail to verify.

## Fees by example
- You spend a 8-coin UTXO
- Outputs: 5 to Bob, 2 back to you → outputs sum to 7
- Fee = `8 − 7 = 1`
- Miner collects the fee by adding it to the block’s coinbase output

## Coinbase transaction
- First tx in a block
- Has a dummy input (no real UTXO, no signature)
- Outputs value = `subsidy + totalFeesOfThisBlock`


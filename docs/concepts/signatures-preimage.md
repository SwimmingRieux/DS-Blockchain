# Signatures and the Preimage (Beginner-Friendly)

Think of a signature like sealing a filled envelope. You list exactly what you’re sending and to whom, then you seal it. If anyone changes the contents, the seal won’t match.

## What is signed?
We sign a clean version of the transaction that includes:
- Inputs: only the references to coins you’re spending (`prevTxId`, `prevOutIndex`)
- Outputs: each `value` and `publicKey`

We do NOT include signatures in what we sign, to avoid circularity.

```
preimage = serialize({
  inputs:  [{ prevTxId, prevOutIndex }],
  outputs: [{ value, publicKey }]
})
```

## Why every input has a signature
- Each input spends one previous output (a UTXO)
- The output stores a `publicKey` of the owner
- The input includes the matching `publicKey` and a `signature` proving control of the private key

## What the node checks
1. Finds the referenced UTXO
2. Compares UTXO.publicKey to the input’s publicKey
3. Rebuilds the preimage and verifies the signature with the publicKey
4. Checks amounts: `sum(inputs) ≥ sum(outputs)`; fee is the difference

## Fees intuition
- You pay a fee by not allocating the full input amount to outputs
- The miner later collects these fees in the coinbase (first transaction of the block)

## Tamper-resistance
- If anyone changes an output value or recipient public key, the preimage changes → signatures no longer verify

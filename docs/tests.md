# Tests & Example I/O

Use these tests to verify each milestone.

## Sanity: Keypair
- Command: `GiveKeyPair`
- Expect: two hex strings separated by a space

## Transaction admission
1) Build a valid tx referencing an existing UTXO; sign correctly
2) `AddTransactionToMempool <tx-json>`
- Expect: mempool JSON listing sorted in descending order by ancestor fee per byte

## Tamper test
- Change an output value by 1 and submit again
- Expect: rejection due to signature verification failure

## Eviction
- `EvictMempool 1`
- Expect: the least-valuable tx (by descendant fee per byte) and its descendants removed; listing sorted in ascending order by descendant fee per byte

## Mining
- `SetDifficulty 12`; `MineBlock`
- Expect: block JSON with header, merkleRoot, nonce; hash meets difficulty; total size ≤ 2000 bytes; coinbase collects subsidy + fees

## Merkle proof
- `GetMerkleProof <txid> <height>` then `VerifyTxInclusion ...`
- Expect: `true` for included tx; `false` for random txid

## Example: minimal tx JSON
```json
{
  "inputs": [
    { "prevTxId": "abc...", "prevOutIndex": 0, "publicKey": "02..", "signature": "30.." }
  ],
  "outputs": [
    { "value": 5000, "publicKey": "02.." },
    { "value": 2000, "publicKey": "03.." }
  ]
}
```

## Example: mempool output (after add)
```json
{
  "count": 2,
  "txs": [
    { "txid": "a1..", "ancestorFee": 900, "ancestorSize": 450, "ancestorFeeRate": 2.0 },
    { "txid": "b2..", "ancestorFee": 100, "ancestorSize": 200, "ancestorFeeRate": 0.5 }
  ]
}
```

---
[← Back: Grading Rubric & Submission](rubric.md) · [Next: Getting Started (Lab 0) →](getting-started.md)

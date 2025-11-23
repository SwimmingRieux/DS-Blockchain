# Constant JSON Formats

## Transaction (input and display)
```json
{
  "inputs": [
    { "prevTxId": "hex", "prevOutIndex": 0, "publicKey": "hex", "signature": "hex" }
  ],
  "outputs": [
    { "value": 5000, "publicKey": "hex" }
  ]
}
```

## Block (output of MineBlock)
```json
{
  "blockHash": "hex",
  "header": {
    "prevBlockHash": "hex", // For the genesis block, this is a string of 64 zeros.
    "merkleRoot": "hex",
    "difficulty": { "leadingZeroBits": 18 },
    "nonce": 123456
  },
  "transactions": [
    {
      "txid": "hex",
      "inputs": [
        { "prevTxId": "hex", "prevOutIndex": 0, "publicKey": "hex", "signature": "hex" }
      ],
      "outputs": [
        { "value": 5000, "publicKey": "hex" }
      ]
    }
  ]
}
```

## Mempool listing after AddTransactionToMempool
- Sorted descending by ancestor fee per byte
```json
{
  "count": 3,
  "txs": [
    { "txid": "hexA", "ancestorFee": 900, "ancestorFeeRate": 2.0 },
    { "txid": "hexB", "ancestorFee": 400, "ancestorFeeRate": 1.6 },
    { "txid": "hexC", "ancestorFee": 80,  "ancestorFeeRate": 0.8 }
  ]
}
```

## Mempool listing after EvictMempool
- Sorted ascending by descendant fee per byte
```json
{
  "count": 2,
  "txs": [
    { "txid": "hexX", "descendantFee": 70, "descendantFeeRate": 0.35 },
    { "txid": "hexY", "descendantFee": 200, "descendantFeeRate": 0.67 }
  ]
}
```

---
[← Back: CLI Commands](cli.md) · [Next: FAQ →](../faq.md)
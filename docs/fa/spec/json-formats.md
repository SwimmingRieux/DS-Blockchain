# فرمت‌های ثابت JSON

## تراکنش (ورودی و نمایش)
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

## بلاک (خروجی MineBlock)
```json
{
  "blockHash": "hex",
  "header": {
    "prevBlockHash": "hex", // برای بلاک جنسیس، این یک رشته متشکل از 64 صفر است.
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

## لیست ممپول پس از AddTransactionToMempool
- مرتب شده نزولی بر اساس کارمزد اجدادی به ازای هر بایت
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

## لیست ممپول پس از EvictMempool
- مرتب شده صعودی بر اساس کارمزد فرزندی به ازای هر بایت
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
[← بازگشت: دستورات CLI](cli.md) · [بعدی: سوالات متداول →](../faq.md)
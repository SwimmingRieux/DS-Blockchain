# UTXO Set

The UTXO set is a map of all currently unspent outputs.

- Key: `txid:outputIndex`
- Value: `{ value, publicKey }`

## Updates on block apply
- For each non-coinbase tx input: remove the referenced UTXO
- For each tx output: add a new UTXO keyed by `txid:index`

Consistency rule: within a block, no UTXO may be spent twice.


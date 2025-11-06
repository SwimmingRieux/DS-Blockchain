# CLI Commands

## GiveKeyPair
- Output: `privateKey publicKey` (hex), space-separated

## SetDifficulty x
- Set required leading-zero bits to `x`

## AddTransactionToMempool txJson
- Parse and validate transaction; admit to mempool
- Output: mempool sorted in descending order by ancestor fee per byte

## EvictMempool x
- Remove `x` least valuable transactions by descendant fee per byte (removing their descendants too)
- Output: mempool sorted in ascending order by descendant fee per byte

## MineBlock
- Select by ancestor fee per byte up to the block size limit, topo-sort, compute Merkle root, do PoW, create coinbase, update UTXO and mempool
- Output: full block JSON

## GetMerkleProof txid height
- Output: `{ siblings: [hex...], positions: ["L"|"R"...] }`

## VerifyTxInclusion txid height proofJson
- Output: `true` or `false`


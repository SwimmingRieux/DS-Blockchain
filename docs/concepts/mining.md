# Mining and Difficulty

After selecting transactions, the miner computes a Merkle root and searches for a nonce so that the block hash has the required number of leading zero bits.

## Steps
1. Select transactions greedily by ancestor fee rate up to the fixed block size limit (2000 bytes total including header and all transactions). Always include parents if a child is chosen.
2. Topologically sort the selected subgraph (parents before children) so validation passes in order.
3. Compute `txid` for each; build the Merkle tree; set `merkleRoot` in the header.
4. Iterate `nonce` until `Hash(header)` has ≥ `difficulty.leadingZeroBits` leading zeros.
5. Create the coinbase paying `subsidy + totalFees` to the miner’s public key.
6. Apply block: update UTXO set (remove spent, add new), clear mined txs from mempool (and update DAG + trees), advance chain tip.

## Why topological order?
- Children spend parents’ outputs. Putting parents first guarantees inputs are valid when each tx is checked.

## Difficulty
- Represented as `leadingZeroBits`
- Higher number → harder PoW

```
Select → Topological sort → Merkle root → Nonce search → Block
```


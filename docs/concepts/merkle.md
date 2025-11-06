# Merkle Trees and Proofs

We compute a binary Merkle tree over the `txid`s of transactions in a block. The root is committed in the block header.

## Why it matters here
- Enables `GetMerkleProof` and `VerifyTxInclusion`
- Lets you prove a transaction is in a block without sending all transactions

## Building (simple rules)
- Leaves: the `txid`s in block order
- If odd number of leaves in a level, duplicate the last hash to make it even
- Parent = Hash(left || right)

## ASCII example
```
Leaves (txids): a, b, c, d

Level 0:   a       b       c       d
           |       |       |       |
Level 1:  h_ab            h_cd        where h_ab = H(a||b), h_cd = H(c||d)
                \        /
Level 2:             h_root = H(h_ab || h_cd)
```

## Proof structure
- For leaf `c`, the proof is: sibling `d`, then sibling `h_ab`, with positions (R then L)
- The verifier starts with `c`, combines with `d` on the right → `h_cd`, then combines with `h_ab` on the left → `h_root`

## Verification steps
1. Start `x = txid`
2. For each step, combine `x` with the sibling on the correct side and hash
3. Compare final `x` to the header’s `merkleRoot`

If equal, the transaction is included in that block.



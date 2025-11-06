# FAQ

## Where does the fee go?
Fees are not an explicit output to the miner. They are `sum(inputs) − sum(outputs)` for each transaction. The miner collects the total of all fees in the coinbase output of the block.

## Why do inputs need signatures?
Each input spends exactly one previous output. That output names a public key. The input must prove control of the matching private key by signing the transaction preimage.

## What is the preimage?
The exact serialized content you sign: input references `(prevTxId, prevOutIndex)` and outputs `(value, publicKey)`. Signatures do not include themselves.

## Why topological order in a block?
Children depend on parents. Placing parents first ensures each child’s inputs are valid when it is validated.

## Why 2300 bytes for block size?
We estimated 1 coinbase + 9 typical transactions ≈ 2101 bytes under our size model and chose 2300 for comfortable headroom.

## Why are diagrams ASCII?
GitHub Pages may not render Mermaid reliably with our theme. ASCII ensures everyone sees the diagrams correctly.

## Can I use multiple keys?
For simplicity, this project uses a single keypair per participant. The concepts extend naturally to multiple keys.

# Mining and Difficulty

After selecting transactions, the miner computes a Merkle root and searches for a nonce so that the block hash has the required number of leading zero bits.

## Mining flow
{% raw %}
<div class="mermaid">
flowchart TD
  S1["Start mining"] --> S2["Select txs greedy<br/>by ancestor fee per byte<br/><= 2000 bytes"]
  S2 --> S3["Include required parents"]
  S3 --> S4["Topological sort"]
  S4 --> S5["Compute txids"]
  S5 --> S6["Build Merkle tree<br/>= merkleRoot"]
  S6 --> S7["Assemble header<br/>(prevHash, merkleRoot, difficulty, nonce)"]
  S7 --> L{"hash(header) meets<br/>leadingZeroBits?"}
  L -- no --> INC["nonce++"]
  INC --> L
  L -- yes --> S8["Create coinbase<br/>(subsidy + fees)"]
  S8 --> S9["Output block JSON"]
  S9 --> S10["Apply block<br/>update UTXO and clear mined"]
</div>
{% endraw %}

## Why topological order?
- Children spend parents’ outputs. Putting parents first guarantees inputs are valid when each tx is checked.

## Difficulty
- Represented as `leadingZeroBits`
- Higher number means harder PoW

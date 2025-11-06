# Mempool: DAG and RB-Trees

Unconfirmed transactions form a directed acyclic graph (DAG):
- Edge parent → child if child spends an output created by parent
- Parents must be confirmed or included before children

We maintain two orderings using balanced trees:
- Ancestor fee rate (for selection):
  - score = (fee(tx) + fees(ancestors)) / (size(tx) + size(ancestors))
  - size(·) is the serialized byte size of the transaction (see Serialization & Hashing)
  - Used to greedily pick transactions for block assembly; listings are printed in descending order by this score
- Descendant fee rate (for eviction):
  - score = (fee(tx) + fees(descendants)) / (size(tx) + size(descendants))
  - Used to remove least valuable transactions (and their descendants); listings are printed in ascending order by this score

## Flow: AddTransactionToMempool
<div class="mermaid">
flowchart TD
  A[tx JSON] --> V[Validate\nUTXO exists? pubKey match?\nsignature ok? fee >= 0?]
  V -->|ok| G[Insert node in DAG\nattach to parents]
  G --> U[Update aggregates\n(ancestor/descendant)]
  U --> T[Update RB-trees\n(ancestor & descendant)]
  T --> O[Print mempool\n(sorted desc by ancestor fee/byte)]
  V -->|fail| R[Reject]
</div>

## Flow: EvictMempool(x)
<div class="mermaid">
flowchart TD
  X[x] --> P[Pick x least valuable\nby descendant fee/byte]
  P --> D[Remove chosen txs\nand all their descendants]
  D --> U[Update aggregates\n& RB-trees]
  U --> O[Print mempool\n(sorted asc by descendant fee/byte)]
</div>

## Block assembly
- Greedy selection by ancestor fee per byte up to the fixed block size limit of 2000 bytes (header + txs)
- Always include all required ancestors for any chosen child
- Build subgraph of chosen txs; topological sort; include in block


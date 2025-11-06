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
{% raw %}
<div class="mermaid">
flowchart TD
  A["tx JSON"] --> V["Validate<br/>UTXO exists? pubKey match?<br/>signature ok? fee >= 0?"]
  V -- ok --> G["Insert node in DAG<br/>attach to parents"]
  G --> U["Update aggregates<br/>(ancestor and descendant)"]
  U --> T["Update RB-trees<br/>(ancestor and descendant)"]
  T --> O["Print mempool<br/>(sorted descending by ancestor fee per byte)"]
  V -- fail --> R["Reject"]
</div>
{% endraw %}

## Flow: EvictMempool(x)
{% raw %}
<div class="mermaid">
flowchart TD
  X["x"] --> P["Pick x least valuable<br/>by descendant fee per byte"]
  P --> D["Remove chosen txs<br/>and all their descendants"]
  D --> U["Update aggregates and RB-trees"]
  U --> O["Print mempool<br/>(sorted ascending by descendant fee per byte)"]
</div>
{% endraw %}

## Block assembly
- Greedy selection by ancestor fee per byte up to the fixed block size limit of 2000 bytes (header + txs)
- Always include all required ancestors for any chosen child
- Build subgraph of chosen txs; topological sort; include in block


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

```
A --> C
B --> C
C --> D
```

## Updates
- AddTransactionToMempool: validate, insert node, update ancestor/descendant aggregates, update both trees
- EvictMempool(x): remove x least valuable by descendant score and their descendants; update structures
- After Add: print mempool sorted in descending order by ancestor fee per byte
- After Evict: print mempool sorted in ascending order by descendant fee per byte

## Block assembly
- Greedy selection by ancestor fee per byte up to the fixed block size limit of 2000 bytes (header + txs)
- Always include all required ancestors for any chosen child
- Build subgraph of chosen txs; topological sort; include in block


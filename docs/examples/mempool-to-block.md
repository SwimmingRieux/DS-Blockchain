# Example: Mempool Scoring and Block Assembly

Assume mempool has txs: A, B, C, D with edges A→C, B→C, C→D.

## Scores (illustrative)
- fee/size:
  - A: 200/400 = 0.5
  - B: 250/250 = 1.0
  - C: 150/200 = 0.75 (ancestors A,B)
  - D: 100/150 = 0.67 (ancestor C)

### Ancestor fee rates
- A: (200)/400 = 0.50
- B: (250)/250 = 1.00
- C: (200+250+150)/(400+250+200) = 600/850 ≈ 0.71
- D: (200+250+150+100)/(400+250+200+150) = 700/1000 = 0.70

Sorted by ancestor rate: B, C, D, A.

## Greedy selection with fixed capacity
- Block capacity is 10 transactions INCLUDING coinbase
- Pick B
- Next consider C (requires A and B): include A+B+C if capacity allows
- Then consider D (requires A+B+C): include if capacity allows

## Topological order of chosen subgraph
- One valid order: A, B, C, D (parents before children)

## Block assembly
- Coinbase first (counts toward capacity)
- Then A, B, C, D in topo order
- Compute Merkle root, mine nonce, output block JSON


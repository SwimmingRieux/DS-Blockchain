# Serialization and Hashing

To compute `txid` and `blockHash`, we serialize data in a consistent way and hash it.

## Serialization rules (project-specific)
- Order fields exactly as documented
- Use UTF-8 for strings, big-endian for numbers (or a simple JSON canonicalization if you prefer; just be consistent)
- For the signing preimage, include only input references and outputs (no signatures)

## Transaction id (txid)
- `txid = Hash(serialize(full transaction))`
- The full transaction includes signatures in its normal serialized form (distinct from the signing preimage)

## Block hash
- `blockHash = Hash(serialize(header))`
- The header contains `prevBlockHash`, `merkleRoot`, `difficulty`, `nonce`

## Hash function
- Use SHA-256 (single or double) across the project consistently

## Size model (used for block size and fee-per-byte)
- Field sizes (bytes):
  - Hash: 32
  - Index (output index): 4
  - Value: 8
  - PublicKey (compressed): 33
  - Signature: 64
- Header size: ~69 (32 prev + 32 merkle + 1 difficulty + 4 nonce)
- Typical transaction (1 input, 2 outputs): ~217
  - 1 input: 32 + 4 + 33 + 64 = 133
  - 2 outputs: 2 × (8 + 33) = 82
  - plus small counters/overhead ≈ 2 → ~217 total
- Coinbase transaction (1 dummy input, 1 output): ~79
  - dummy input: 32 + 4 = 36; output: 8 + 33 = 41; + small overhead ≈ 2

### Ten-transaction example
- Example total: 69 (header) + 79 (coinbase) + 9 × 217 = 2101 bytes
- Project fixed block size limit: 2000 bytes (stricter than the example total)

Notes:
- Real sizes vary by input/output counts; selection is greedy by ancestor fee per byte under this model

## Why it matters
- Any tiny change in content → different hash → protects integrity and enables Merkle proofs

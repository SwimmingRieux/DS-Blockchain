# Getting Started: A Hands-On Introduction

This guide provides a hands-on introduction to the core concepts of the blockchain you will be building. By following these steps, you will learn the fundamental workflow of creating a key pair, building a transaction, and mining a block.

Think of this as "Lab 0" – a practical exercise to complete before you start working on the main assignment milestones.

## Task 1: Generate a Key Pair

Your first step is to create a public/private key pair. This will be your identity on the blockchain.

- **Action:** Run the `GiveKeyPair` command.

  ```bash
  $ ./your-node-program GiveKeyPair
  ```

- **Checkpoint:** The command will output a new key pair. Save this information, as you will need it for the following steps. The `publicKey` is your "address" that you can share with others, while the `privateKey` must be kept secret.

## Task 2: Understand UTXOs

Before you can create a transaction, you need to understand the UTXO model.

- **Action:** Read the [UTXO Model](concepts/utxo.md) documentation.
- **Checkpoint:** Draw a diagram of a UTXO that you own. It should include the `txid` and `index` (which you can make up for now), the `value`, and your `publicKey` from Task 1.

## Task 3: Build a Sample Transaction

Now, let's create a transaction. For this exercise, you can invent a UTXO that you own.

- **Action:** Create a JSON file that represents a transaction with one input and two outputs (one for the payment and one for the change that comes back to you). Refer to the [JSON Formats spec](spec/json-formats.md) for the correct format.
- **Checkpoint:** Manually calculate the `txid` of your transaction by serializing the transaction data and hashing it with SHA-256.

## Task 4: Sign the Transaction

A transaction is not valid until it is signed. The signature proves that you are the owner of the funds being spent.

- **Action:** Create the transaction preimage (the data to be signed) and sign it with your private key. Add the resulting `signature` to the input in your transaction JSON.
- **Checkpoint:** To understand the importance of the signature, try tampering with your transaction. For example, change the `value` of one of the outputs by one coin. You should observe that if you were to re-verify the signature against this modified transaction, the verification would fail.

## Task 5: Add the Transaction to the Mempool

Once a transaction is created and signed, it is broadcast to the network and added to the mempool.

- **Action:** Use the `AddTransactionToMempool` command to add your transaction to the mempool.

  ```bash
  $ ./your-node-program AddTransactionToMempool <path-to-your-tx.json>
  ```

- **Checkpoint:** The command should print the current state of the mempool, sorted by ancestor fee rate. To further your understanding, create a second transaction that spends the change output from your first transaction. Add this "child" transaction to the mempool and observe how the DAG (Directed Acyclic Graph) of dependencies is represented.

## Task 6: Mine a Block

Now it's time to mine a block and include your transaction in it.

- **Action:** First, set the mining difficulty. Then, run the `MineBlock` command.

  ```bash
  $ ./your-node-program SetDifficulty 12
  $ ./your-node-program MineBlock
  ```

- **Checkpoint:** The command will output the newly mined block in JSON format. Inspect the block and verify that the header fields are correct, the `merkleRoot` is valid, and the `nonce` results in a hash that meets the difficulty requirement. Also, check that the total block size is less than or equal to the 2000-byte limit.

## Task 7: Prove Inclusion

The final step is to prove that your transaction is included in the block.

- **Action:** Use the `GetMerkleProof` and `VerifyTxInclusion` commands.

  ```bash
  $ ./your-node-program GetMerkleProof <txid> <block-height>
  $ ./your-node-program VerifyTxInclusion <proof-file> <merkle-root>
  ```

- **Checkpoint:** The `VerifyTxInclusion` command should return `true` for your transaction and `false` for a random, non-existent transaction ID.

---
[← Back: Tests & Example I/O](tests.md) · [Next: Background →](concepts/background.md)

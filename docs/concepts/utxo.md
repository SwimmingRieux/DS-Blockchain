# The UTXO Model

The Unspent Transaction Output (UTXO) model is a fundamental concept in many cryptocurrencies, including Bitcoin and the blockchain you are building in this project. It is an alternative to the account-based model used by other blockchains like Ethereum.

In the UTXO model, there are no accounts or balances at the protocol level. Instead, the blockchain keeps track of a set of unspent transaction outputs (UTXOs). A UTXO is a discrete amount of cryptocurrency that has been authorized by a sender and can be spent by a receiver.

## The UTXO Set

The UTXO set is a data structure that contains all the UTXOs that are currently available to be spent. It is a global state that is updated every time a new block is added to the blockchain.

The UTXO set can be thought of as a collection of digital coins. Each UTXO has two main attributes:

- **Value:** The amount of cryptocurrency that the UTXO represents.
- **Locking Script (`publicKey`):** A script that specifies the conditions that must be met to spend the UTXO. In our case, this is simply a public key, which means that the UTXO can be spent by providing a valid digital signature from the corresponding private key.

Each UTXO is uniquely identified by the hash of the transaction that created it (`txid`) and its index in the list of outputs of that transaction.

- **Key:** `txid:outputIndex`
- **Value:** `{ value, publicKey }`

## How the UTXO Set is Updated

When a new block is added to the blockchain, the UTXO set is updated as follows:

1.  **Remove Spent UTXOs:** For each input in each transaction in the block (except for the coinbase transaction), the UTXO that it references is removed from the UTXO set.
2.  **Add New UTXOs:** For each output in each transaction in the block, a new UTXO is created and added to the UTXO set.

Within a single block, a UTXO cannot be spent twice. This is a critical consensus rule that prevents double-spending.

### Example

Let's consider a simple example:

- The current UTXO set contains one UTXO: `{ txid: 1, index: 0, value: 10, publicKey: Alice }`.
- Alice wants to send 7 coins to Bob.
- Alice creates a transaction with one input (referencing the UTXO she owns) and two outputs:
    - Output 0: `value: 7, publicKey: Bob`
    - Output 1: `value: 3, publicKey: Alice` (this is the change)

When this transaction is included in a block, the UTXO set is updated as follows:

- The UTXO `{ txid: 1, index: 0 }` is removed.
- Two new UTXOs are added:
    - `{ txid: 2, index: 0, value: 7, publicKey: Bob }`
    - `{ txid: 2, index: 1, value: 3, publicKey: Alice }`

```mermaid
graph TD
    subgraph "Transaction 1 (creates initial UTXO)"
        A[txid: 1, index: 0] --> B{value: 10, publicKey: Alice}
    end

    subgraph "Transaction 2 (spends the UTXO)"
        C(Input: txid 1, index 0) --> D{txid: 2}
        D --> E{Output 0: value: 7, publicKey: Bob}
        D --> F{Output 1: value: 3, publicKey: Alice (change)}
    end

    subgraph "Initial UTXO Set"
        direction LR
        U1(txid: 1, index: 0)
    end

    subgraph "Updated UTXO Set"
        direction LR
        U2(txid: 2, index: 0)
        U3(txid: 2, index: 1)
    end

    C -.-> U1
```

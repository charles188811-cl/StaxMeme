

# StaxMeme -  Ultra Advanced Memecoin Token Contract**

## Overview

This smart contract implements an **ultra-advanced memecoin token system** with **manual block height tracking**, **cooldown-based transfers**, **staking mechanics**, and a basic **governance proposal system**. It's written in Clarity for the Stacks blockchain.

---

## 🚀 Features

* **Fungible Token**: A STX-based fungible token (`memecoin`) with configurable supply.
* **Manual Block Height Handling**: Custom block height simulation to decouple logic from actual chain height — useful for testing or alternate timelines.
* **Transfer Cooldowns**: Enforces a 10-block delay between user transfers to prevent spam.
* **Token Staking**: Stake tokens with customizable lock periods (based on manual block height).
* **Governance Proposals**: On-chain governance allowing proposal creation and (potential) voting.
* **Upgradeable**: Owner-controlled logic and clearly defined error codes for extensibility.

---

## 🧱 Data Structures

### 📦 Fungible Token

```clarity
(define-fungible-token memecoin)
```

### ⚙️ Configurable Parameters

* `token-name`: Default `"MemeToken"`
* `token-symbol`: Default `"MEME"`
* `max-supply`: `1,000,000,000 MEME`

### ⛓ Manual Block Height

```clarity
(define-data-var current-block-height uint u0)
```

Call `update-block-height` to increment this manually.

---

## 🧾 Core Functions

### 🕒 `update-block-height`

Manually increments the block height:

```clarity
(define-public (update-block-height) ...)
```

---

### 📦 `transfer`

Transfers tokens with a 10-block cooldown per address:

```clarity
(define-public (transfer (amount uint) (recipient principal)) ...)
```

---

### 💰 `stake-tokens`

Locks tokens in the contract for a specified number of blocks:

```clarity
(define-public (stake-tokens (amount uint) (lock-period uint)) ...)
```

---

### 🔓 `unstake-tokens`

Allows token withdrawal after the lock period:

```clarity
(define-public (unstake-tokens) ...)
```

---

### 🗳 `create-governance-proposal`

Creates a governance proposal with description and voting deadline:

```clarity
(define-public (create-governance-proposal (description (string-utf8 200)) (voting-period uint)) ...)
```

---

## ❌ Error Codes

| Code | Description                 |
| ---- | --------------------------- |
| 100  | Owner-only access           |
| 101  | Insufficient balance        |
| 102  | Transfer cooldown violation |
| 103  | Max supply reached          |
| 104  | Airdrop failure             |
| 105  | Token burn failed           |
| 111  | No staking info found       |
| 112  | Unlock block not reached    |

---

## 📚 State Maps & Vars

* `transfer-last-block`: Tracks last transfer block per user
* `staking-deposits`: Tracks stakes (amount, stake-block, unlock-block)
* `governance-proposals`: Governance proposal records
* `next-proposal-id`: Autoincrement proposal ID

---

## ✅ How to Use

### 1. Deploy Contract

Deploy the contract via Clarity-compatible deployment tools.

### 2. Mint Tokens (via owner logic — not shown)

Ensure tokens are minted and distributed (token mint logic is assumed external or added later).

### 3. Increment Block Height

Call this function to simulate block progress:

```clarity
(update-block-height)
```

### 4. Transfer Tokens

Send tokens respecting the cooldown logic:

```clarity
(transfer u100 'SP...recipient)
```

### 5. Stake Tokens

Lock up tokens for a duration (in blocks):

```clarity
(stake-tokens u500 u50) ;; 50 blocks
```

### 6. Unstake

After lock period:

```clarity
(unstake-tokens)
```

### 7. Governance

Propose:

```clarity
(create-governance-proposal u"Add staking rewards" u20)
```

---

## 🔐 Ownership & Permissions

* The `CONTRACT-OWNER` is statically set to `tx-sender` on contract deploy.
* Ensure appropriate logic is added for ownership functions (e.g., minting or burning).

---

## 🔮 Future Enhancements

* Voting mechanism for proposals
* On-chain execution of passed proposals
* Reward system for staking
* Token minting & burning by owner

---

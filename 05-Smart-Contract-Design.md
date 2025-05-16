# 5. Smart Contract Design

KTON V2 employs a layered smart-contract stack written in **FunC** and **Tact** (for interface contracts).  Below we outline the most important components and their security considerations.

## 5.1 Pool Root Contract

```rust
;; simplified pseudo-code
struct PoolRoot {
  owner: address;           ;; Halter / Sudoer
  controller: address;
  jetton_minter: address;
  exchange_rate: uint128;   ;; TON per KTON (µTON precision)
  tvl: uint128;             ;; cached TVL for UI
  halted: bool;
}
```

### Key Functions

* `deposit(ton_amount)` — Mints `ton_amount / exchange_rate` **KTON** and sends to caller.
* `redeem(kton_amount)` — Burns KTON, returns TON after cooldown or immediately with fee.
* `update_rate()` — Pulls reward balance from controller and adjusts `exchange_rate`.
* `halt(mode)` — Emergency stop toggles (deposit, redeem, both).
* `set_controller(addr)` — Only via **SudoerExecutor**.

## 5.2 Controller Contract

* Maintains validator wallets and dispatches `add_stake` / `recover_stake` messages.
* Uses **nonce-based replay protection** to avoid double stakes.
* Tracks per-validator performance and automatically rotates out underperformers.

## 5.3 Jetton Minter

* Implements **TIP-3.3** with extensions for **permit()** (EIP-2612-style off-chain approvals).
* Emits `Transfer`, `Mint`, `Burn` events compatible with major indexers.
* Owner set to **Pool Root** to ensure 1:1 backing.

## 5.4 Governance Contracts

Governance is split into two layers:

1. **Proposal Hub** — Receives proposals and stores metadata.
2. **Timelock Executor** — Queues successful proposals and calls target contracts after the delay.

Planned upgrade: **Sub-DAO modules** for node-operator whitelisting and risk-parameter committees.

## 5.5 Security Enhancements (V2 vs V1)

| Area | V1 | V2 |
|------|----|----|
| Upgrades | Owner key could upgrade instantly | **SudoerExecutor** enforces 48 h timelock |
| Emergency Halt | All-or-nothing pause | Granular mode (deposit / redeem / both) |
| Treasury | Same owner as pool | **Separate contract & key** |
| Error Codes | Generic failure | Descriptive codes + event logs |
| Gas Limits | Hard-coded | Configurable via governance |

## 5.6 Formal Specification

The protocol invariants are specified in **K / Reach** style property tests:

1. *Total backing*: `total_kton * exchange_rate <= ton_balance(pool_root)`
2. *No mint-out-of-thin-air*: Only `deposit()` can call `jetton_minter::mint`.
3. *Slashing isolation*: `controller` may not transfer TON except `add_stake` and `recover_stake`.

## 5.7 Upgrade Procedure

1. Governance proposes a new contract hash and parameters.
2. Proposal accumulates quorum over **7 days** (configurable).
3. Timelock (48 h) begins; front-end and social channels broadcast the pending upgrade.
4. Anyone may execute the upgrade after the delay by calling `sudoer_executor::execute()`.

Next: **[6. Governance and Tokenomics](06-Governance-and-Tokenomics.md)** 
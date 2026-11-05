# 3. KTON Basics

## 3.1 What Is KTON?

* **Liquid Staking Token (Jetton):** A transferable representation of staked TON plus accrued rewards.
* **1 $KTON ≠ 1 TON:** The exchange rate grows over time as validator rewards accumulate.
* **ERC-20 Equivalent:** Jettons follow the **TIP-3** standard, the token interface for TON smart contracts.

## 3.2 How It Works

1. **Deposit** TON into the pool via <https://app.kton.io/> or the Telegram Mini App.
2. **Mint** — The pool issues **$KTON** to your wallet proportional to your deposit divided by the current exchange rate.
3. **Earn** — Validators generate rewards, increasing the exchange rate *TON per KTON*.
4. **Redeem** — Burn $KTON to reclaim TON at the pool's rate: at the next rotation with no fee, or at once from the pool's idle balance for the instant-withdrawal fee.

## 3.3 Key Metrics

| Metric | Description |
|--------|-------------|
| **Total Value Locked (TVL)** | Total TON controlled by the pool. Visible on DefiLlama. |
| **APY** | Annualised yield after fees. Target **8 %** with MEV. |
| **Exchange Rate** | TON per KTON. Starts at 1.0 and increases with rewards. |
| **Instant Withdrawal Fee** | Fee for being paid out at once from the pool's idle balance instead of at the next rotation. |

## 3.4 Contract Addresses

| Network | Contract | Address |
|---------|----------|---------|
| TON Mainnet | **KTON Jetton Minter** | `EQBuIhXNNkWf9AW9miNGNTSO_uFZ23ejfIWrieXge5f733mw` |
| TON Mainnet | **Pool** | `EQA9HwEZD_tONfVz6lJS0PVKR5viEiEGyj9AuQewGQVnXPg0` |
| TON Mainnet | **Controller** | `Ef9GOR1wqJFPVpbHOxObSATkdbfTizRTmDi6DdjJFYaRKhoK` |
| TON Mainnet | **Validator** | `Uf_lhdKTXcTJUnCVWYWXaoziqxkkLl-8PBP0be601QkE9TyT` |

> Always verify addresses on-chain via [TONScan](https://tonscan.org/) before interacting.

## 3.5 Fees

* **Protocol Fee:** A DAO-governed share of validator rewards goes to the treasury.
* **Instant Withdrawal Fee:** Set by governance (0.2% as of November 2026) and shown in the app before you sign.

## 3.6 Risks

* **Validator Slashing:** Mitigated by diversification and conservative staking thresholds.
* **Smart-Contract Risk:** Minimised through audits and formal verification.
* **DEX Price:** DEX pools set their own price for KTON, and it has been well below the pool's rate (on 2026-11-05 selling on STON.fi paid about 6% less than redeeming). Redeem through the pool instead of selling on a DEX.

Next: **[4. Technical Architecture](04-Technical-Architecture.md)** 
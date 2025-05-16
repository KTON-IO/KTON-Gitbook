# 6. Governance and Tokenomics

## 6.1 Governance Overview

KTON follows a progressive decentralisation model.

### Voting Power

| Token | Purpose | Voting Weight |
|-------|---------|---------------|
| **$KTON** | Liquidity token & governance power | *1x* (per jetton) |

### Core Modules

* **Parameter Committee** — Adjusts APY targets, fees, withdrawal buffer.
* **Operator Committee** — Whitelists / slashes node operators.
* **Treasury Committee** — Allocates budget for audits, liquidity mining and R&D.

All modules operate under the **Timelock Executor** described in Chapter 5.

## 6.2 Token Supply & Distribution

_KTON does not employ a separate governance token at this stage.  Voting rights and economic exposure are both represented by **$KTON** itself.  Therefore, no additional token supply schedule is required._

| Allocation | Notes |
|------------|-------|
| Staking Rewards | Reflected via $KTON exchange-rate growth |
| Treasury Reserve | Managed by DAO using $KTON inflows |

## 6.3 Fee Model

* **Validator Rewards Fee:** A configurable share (set by DAO) goes to treasury.
* **Instant Withdrawal Fee:** Dynamic fee; its distribution between burn and treasury is determined by governance.
* **MEV Rewards:** Split between node operators and nominators based on a DAO-approved formula.

## 6.4 Treasury Management

Treasury assets (TON, KTON, USDT) are held in a **multisig wallet**.  Expenditures require DAO proposal approval and timelock execution.

Typical budget items:

* Security audits & formal verification.
* Liquidity incentives (DEX pools, lending markets).
* Ecosystem grants for wallets, analytics, DeFi integrations.
* Community marketing & hackathons.

## 6.5 Road to Full Decentralisation

| Phase | Milestone | Control Level |
|-------|-----------|---------------|
| Alpha | Mainnet launch, Council multisig | Centralised |
| Beta | Governance token distribution | Hybrid |
| Gamma | On-chain voting live | Decentralised |
| Delta | Sub-DAOs activated | Fully decentralised |

Next: **[7. Security and Audits](07-Security-and-Audits.md)** 
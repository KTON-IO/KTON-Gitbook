# 4. Technical Architecture

KTON is engineered around a **modular, upgradable smart-contract system** dubbed **LST V2**.  The design separates critical functions into isolated contracts, enabling safer upgrades and clearer auditability.

## 4.1 Core Participants

| Role | Description |
|------|-------------|
| **Nominators** | Deposit TON, receive $KTON, earn rewards. |
| **Node Operators** | Run validator nodes on behalf of the pool. |
| **Governance DAO** | Adjusts parameters, elects operators, manages treasury. |

## 4.2 Contract Breakdown

| Contract | Key Responsibilities |
|----------|----------------------|
| **Pool Root** | User entry-point: handles deposits, redemptions, exchange-rate updates. |
| **Controller** | Stakes funds with the TON Elector, coordinates validator rotation & MEV optimisation. |
| **Jetton Minter** | Issues & burns $KTON, tracks total supply. |
| **Governance Root** | Stores DAO parameters, quorum rules and on-chain proposals. |
| **Treasury** | Collects protocol fees, executes budget proposals. |
| **SudoerExecutor** | One-time upgrade agent with 48-hour time lock. |
| **Emergency Halter** | Can pause specific functions if anomalies detected. |

### 4.2.1 Pool Root

* Maintains the **exchange rate** (`ton_per_kton`).
* Emits **Deposit** / **Redeem** events for indexers.
* Calls `controller::stake()` when available balance crosses threshold.

### 4.2.2 Controller

* Generates validator wallet keys deterministically.
* Submits `ton_elector::add_stake` and `recover_stake` messages.
* Implements **MEV strategy** by dynamically adjusting validator weight.
* Supports **multi-controller** configuration for geo-redundancy.

### 4.2.3 Governance Root

* Accepts proposals signed by $KTON holders.
* Uses **quadratic voting** (planned upgrade) to balance whales and retail.
* Enforces **time-lock** of 24-48 h before executing approved upgrades.

## 4.3 Data Flow

KTON uses a structured flow of funds and data between the user wallets and various system components:

1. Users deposit TON coins into the Pool Root contract
2. Pool Root mints KTON tokens via the Jetton Minter
3. TON coins are staked through the Controller contract
4. The Controller interacts with TON Elector for validator operations
5. Rewards flow from TON Elector back to the Controller
6. The Controller updates exchange rates in the Pool Root
7. When redeeming, Pool Root burns KTON tokens via Jetton Minter
8. Finally, TON coins are returned to users

## 4.4 Security Layers

1. **Static Analysis & Formal Verification** — Scripts ensure invariant properties before deployment.
2. **Role-Based Access Control** — Separate keys for halter, sudoer, approver & treasury.
3. **Circuit Breakers** — Halter can freeze deposits, redemptions or full contract.
4. **Time-Delayed Upgrades** — SudoerExecutor enforces a public notice period.
5. **On-chain Monitoring** — Metrics exported to Prometheus & Grafana dashboards.

Continue to **[5. Smart Contract Design](05-Smart-Contract-Design.md)** for contract-level details. 
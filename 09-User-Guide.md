# 9. User Guide: Staking & Using KTON

This chapter provides a step-by-step walkthrough for staking TON, managing $KTON and interacting with DeFi integrations.

> **Quick Access**: Use our Telegram Mini App for the simplest staking experience - <https://t.me/ktonio_bot>

## 9.1 Requirements

* **TON Wallet** (Tonkeeper, MyTonWallet, OpenMask or OWallet)
* At least **1 TON** balance for staking + gas
* Optional: Telegram account for the Mini App

## 9.2 Staking via Web App

1. Visit **<https://app.kton.io/>**.
2. Connect your wallet and grant signature permission.
3. Enter the amount of TON you wish to stake (≥1).
4. Review the quoted **KTON** amount and click **Stake**.
5. Approve the transaction in your wallet.
6. Receive **KTON** within seconds; check your wallet balance or TonViewer.

## 9.3 Staking via Telegram Mini App

1. Open the bot **[@ktonio_bot](https://t.me/ktonio_bot)**.
2. Tap **"Stake"** and select TON from your in-chat Wallet.
3. Confirm amount and authenticate with your passcode/biometrics.
4. Wait a few seconds for **KTON** to appear in the bot's portfolio view.

## 9.4 Redeeming KTON

### Standard Withdrawal (No Fee)

* Burn **KTON** in the web app; receive TON after the current validator cycle ends (currently up to 36 h, planned optimisation to **≤18 h**).

### Instant Withdrawal (Withdraw now)

* In the web app choose **Withdraw now**: the pool pays you at once from its idle balance, for the instant-withdrawal fee (0.2% as of November 2026, shown before you sign).
* The amount is limited to the pool's idle balance at that moment; for more, use the standard withdrawal above.

### Do Not Sell KTON on a DEX

* DEX pools set their own price for KTON, and it has been well below the pool's rate: on 2026-11-05 selling on STON.fi paid about 6% less than redeeming. Wallet swap screens route through the same pools.
* Redeem through the pool instead, using either option above.

## 9.5 Using KTON in DeFi

### Borrowing Against KTON

1. Open **EVAA** lending app (Telegram-based).
2. Deposit **KTON** as collateral.
3. Borrow TON or USDT up to the protocol's maximum LTV.
4. Monitor health factor to avoid liquidation.

## 9.6 Tracking Your Portfolio

* **TonViewer**: <https://tonviewer.com/> (enter wallet address)
* **TONScan**: <https://tonscan.org/jetton/EQBuIhXNNkWf9AW9miNGNTSO_uFZ23ejfIWrieXge5f733mw>

## 9.7 FAQs

**Q:** *Can I stake from a hardware wallet?*  
A: Yes — Tonkeeper Ledger support is live.

**Q:** *Is there a minimum lock-up?*  
A: No. Withdraw any time; validator cycle only affects standard withdrawals.

**Q:** *What happens if a validator is slashed?*  
A: Losses are socialised across the pool; controller diversifies stake to minimise impact. 
# 7. Security and Audits

Security is a first-class priority for KTON.  The smart-contract suite has undergone a comprehensive, independent security review by **TonBit** in April 2025.  This chapter summarises the scope, methodology and findings of that audit.

## 7.1 Audit Overview

| Item | Detail |
|------|--------|
| Auditor | **TonBit** (contact: [@tonbit](https://twitter.com/tonbit) • contact@bitslab.xyz) |
| Timeline | Thu 3 Apr 2025 – Wed 16 Apr 2025 |
| Platform | The Open Network (TON) |
| Languages | FunC |
| Repository | <https://github.com/KTON-IO/liquid-staking-contract> |
| Commits Reviewed | `b0352cd`, `10786c7`, `b0a69b5` |
| Techniques | Architecture review, unit testing, manual code inspection |

## 7.2 Scope of Review

TonBit analysed the **core liquid staking contracts**, controller logic, governance, pool storage, payout NFT modules and supporting libraries.  A total of 25 source files (see Appendix A) were examined, with their SHA-1 hashes recorded to guarantee provenance.

## 7.3 Issue Statistics

| Severity | Count | Status |
|----------|-------|--------|
| Critical | 0 | — |
| Major | 0 | — |
| Medium | 2 | **Fixed** |
| Minor | 0 | — |
| Informational | 1 | **Fixed** |
| **Total** | **3** | **All Fixed** |

No critical or major vulnerabilities were discovered.  All identified issues were remediated by the KTON team before main-net deployment.

## 7.4 Key Findings & Resolutions

### CON-1  Missing Fee Check in Balance Validation (Medium)
* **Location:** `contracts/controller.func` (lines 479-506)
* **Risk:** Potential under-funding of storage balance due to unaccounted gas/forwarding fees.
* **Fix:** Added explicit checks to include gas and forwarding fees in balance validation logic.

### POO-1  Incorrect Rounding Direction (Medium)
* **Location:** `contracts/pool.func` (lines 410-416)
* **Risk:** Slight over-estimation of loanable funds in edge cases.
* **Fix:** Implemented conservative rounding that always favours protocol safety.

### CON-2  Incorrect Comment (Informational)
* **Location:** `contracts/controller.func` (lines 153-157)
* **Issue:** Mismatched comment describing loan principal vs. profit share.
* **Fix:** Updated comment to accurately reflect logic.

## 7.5 Auditor Checklist

TonBit's review covered (but was not limited to) the following vectors:

* Transaction-ordering & timestamp dependencies
* Integer overflow / underflow and rounding errors
* Denial-of-service & logical oversights
* Access control & role separation
* Centralisation risks
* Compliance of business logic with specification
* Gas efficiency
* Protection against arbitrary token minting

## 7.6 Methodology

TonBit employed a blended approach of **manual line-by-line review**, **unit testing** and **static analysis**.  Where necessary, code was deployed to TON test-net to emulate real transaction flows.  All communications and fixes were tracked collaboratively with the KTON engineering team.

## 7.7 Conclusion

The TonBit audit concluded that the KTON V2 contract suite is **sound and production-ready**.  With all medium and informational findings resolved, the protocol meets a high security standard appropriate for an institutional-grade liquid staking service.

## 7.8 Open-Source Transparency

KTON's entire smart-contract stack is **100 % open source** under the MIT licence.  Anyone can inspect, verify, and contribute to the codebase on GitHub, enabling continuous "crowd-audit" from the wider TON developer community.

* Public repository: <https://github.com/KTON-IO/liquid-staking-contract>
* Commit history and audit artefacts are permanently available for reproducibility.

## 7.9 Defence-in-Depth Improvements in V2

| Area | V1 Limitation | V2 Enhancement |
|------|--------------|----------------|
| Super-admin Control | Single superuser could unilaterally upgrade contracts. | **Multi-sig governance** — any upgrade now requires at least two independent approvals (Sudoer + Guardian). |
| System Stability | Any critical bug forced a full protocol halt. | **Modular hot-patching** allows targeted fixes without stopping deposits/withdrawals. |
| Validator Oversight | Manual monitoring by node operators. | **Real-time validator monitoring** dashboard built by TONX for automated alerting and slashing risk mitigation. |

These upgrades were additionally **cross-audited** by two internal security teams ("Team A" & "Team B") to maximise coverage and minimise blind spots.

---

*Last updated: May 2025*

---

### Appendix A – Files in Scope (SHA-1)

For transparency, the table below lists the file identifiers (as referenced by TonBit) and their corresponding SHA-1 hashes at the time of review.

| ID | File | SHA-1 Hash |
|----|------|-----------|
| CCO | `elector/config-code.fc` | 86b5937b60b948d8aae93095bfba876136759c83 |
| ECO | `elector/elector-code.fc` | 2b05a7eedcd1d37452028076d7035a2463aacb6d |
| NCU | `contracts/network_config_utils.func` | 5bbd9279574035906099792bb1a2f6003cfb963a |
| PMH | `contracts/pool_mint_helpers.func` | 5b4e94143afcbc54348506bdf048ab34ce2fcde8 |
| VER | `contracts/versioning.func` | b53c2212dda2dfe490acfad0b1c95e38558a325d |
| ASS | `contracts/asserts.func` | 183d8096a46b11532a49ba388be17ea146c05ddd |
| NCO | `contracts/payout_nft/nft-collection.func` | e90656be3eb26afdba3799d555a3ee4f4f892a37 |
| TYP | `contracts/payout_nft/types.func` | b842d47f8664697a9259645bbb50eb91ee0d3d98 |
| MUT | `contracts/payout_nft/metadata_utils.func` | 63a7a89fd8d860d2fee1b6d277d01555f5ffac78 |
| PAR | `contracts/payout_nft/params.func` | 0f9f4a2a31d1398374b6a8a2cb841dec265ba7ec |
| OCO | `contracts/payout_nft/op-codes.func` | 764c3348a51196578cf99c172e39005d47b09d14 |
| MES | `contracts/payout_nft/messages.func` | a0c095360e5c2ad16b6e5fd2184f9595b68d4ab1 |
| ERR | `contracts/payout_nft/errors.func` | 3a2a8b71e2b134ca355b393be7e585316cce82fa |
| NIT | `contracts/payout_nft/nft-item.func` | c9b8fc9c714c8bafca6f5d8adf355c03fa5cff49 |
| TYP1 | `contracts/types.func` | dd0249b9dcaaab159abea843497d1e6dd9407885 |
| MUT1 | `contracts/metadata_utils.func` | 9fb25672739d7e2cf6da2cbd578d364a6606da42 |
| PST | `contracts/pool_storage.func` | 880c2ac81679de5863b9f2bd3c25acff288b03c9 |
| OCO1 | `contracts/op-codes.func` | f4632bead38e628905c4e82cf9155071bed2ae7d |
| LIB | `contracts/librarian.func` | 04017e4d2000102de80ad00a866ce6580b40bf34 |
| DPA | `contracts/dao_params.func` | a38462fc812128e50bf3c786cbd24b6636eb0bd6 |
| MES1 | `contracts/messages.func` | afc63199ac393dd01be37c9f8c499a3e4ab72de2 |
| ACA | `contracts/address_calculations.func` | acac2cc54b0f3288d60ad8a794930b17fa9ff1e1 |
| RHE | `contracts/roles_helper.func` | 6279b3fd604b02a654438e62f68ee2b531032471 |
| ERR1 | `contracts/errors.func` | 226cdad500ae1abf38f9681160d78a4ebecba294 |
| SRE | `contracts/sudoer_requests.func` | 3930b608d675da7a7fa087e8c5f1617d82891a55 |
| POO | `contracts/pool.func` | 9d62e7e11ec3b9fbd8f593190b0bc23d72553b0c |
| CON | `contracts/controller.func` | 0d332172d816a549ffc2cac800e17f143121acef |

*Note: This appendix reproduces TonBit's identifiers for reference; readers need not reproduce the full table in downstream integrations.*

Next: **[8. DeFi Integrations](08-DeFi-Integrations.md)** 
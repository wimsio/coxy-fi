# Coxy Fi White Paper

**Company:** Coxygen Global (Pty) Ltd

**Author:** Bernard Sibanda

**Version:** 0.1 (Intranet Pilot – WIMS Cardano/Coxygen/Zonke Communities)

**Date:** 20 February 2026

**Aim:** Financial Inclusion

## Disclaimer and Risk Notice (Read First)

Coxy Fi is an experimental RealFi (real-world finance) micro-lending protocol intended to promote financial inclusion and community-based entrepreneurship. Coxy Fi involves significant risk, including (but not limited to) smart contract vulnerabilities, stablecoin de-pegging, counterparty default risk, market and liquidity risks, and operational risks relating to off-chain repayment methods.

Nothing in this document constitutes financial advice, investment advice, legal advice, or an offer to sell or a solicitation to buy any security or financial product. Participation is voluntary. By using Coxy Fi, participants acknowledge that they are acting knowingly, willingly, and freely, accept all risks, and agree to comply with the applicable Terms & Conditions and Privacy Policy of Coxygen Global (Pty) Ltd, as updated from time to time.

To the maximum extent permitted by law, **no directors, staff, contractors, community moderators, or affiliates of Coxygen Global (Pty) Ltd shall be held liable** for any direct or indirect loss, including loss of funds, loss of access, or loss of opportunity arising from participation in Coxy Fi.

Coxy Fi may begin as an intranet pilot within the Coxygen/Zonke community environment. As adoption grows, additional compliance, licensing, and operational controls may be introduced. Participants are responsible for ensuring their own compliance with laws and regulations in their jurisdiction.

## Table of Contents

1. Introduction
2. Vision and Aim: Financial Inclusion
3. Problem Statement
4. Core Principles
5. Scope: Intranet RealFi Pilot and Community Domains
6. Supported Assets and Rationale (Stablecoins and ADA)
7. Participants and Roles
8. Identity, Privacy, and the Coxy DID / CFDID
9. Credit Profile and Eligibility Rules
10. Lending and Borrowing Flow (P2P Marketplace)
11. Repayment Methods
12. Default, “Three Chances,” and Decentralized Punishment
13. Fees and Economics
14. Governance and Upgrades
15. Security and Technical Architecture
16. Risks and Mitigations
17. Roadmap
18. Glossary of Terms

## 1. Introduction

Coxy Fi is a peer-to-peer (P2P) micro-loan marketplace designed to connect crypto liquidity providers directly with borrowers who need small loans for micro-business growth or urgent personal needs. The protocol is designed to start within Coxygen and Zonke community environments as an “intranet” RealFi pilot, and later expand to additional communities through a federation model.

Coxy Fi prioritizes privacy and minimal personal data handling. Users do not publish names, phone numbers, or email addresses on-chain, and the system is designed to reduce reliance on centralized identity and custody.


## 2. Vision and Aim: Financial Inclusion

The primary aim of Coxy Fi is **financial inclusion**: enabling access to micro-credit for community members who may not qualify for bank loans due to lack of collateral, limited credit history, or bureaucratic screening processes.

Coxy Fi also aims to create a productive opportunity for stablecoin holders. Many stablecoin holders keep idle balances, and Coxy Fi enables them to earn yield by funding real needs within trusted community domains, while borrowers gain faster access to capital.

The long-term ambition is to help stablecoin holders expand beyond crypto-native opportunities and participate in broader RealFi opportunities, including future integrations with tokenized real-world markets, subject to appropriate controls and compliance.

## 3. Problem Statement

In many communities, micro-businesses and students face a gap between urgent capital needs and available credit options. Traditional lenders often require extensive paperwork, formal employment records, or collateral. Informal lending markets can be expensive, unsafe, and non-transparent.

At the same time, global crypto markets hold deep liquidity, including stablecoin balances that are often under-utilized. Bridging these two realities requires a mechanism that can:

* match lenders and borrowers with minimal friction,
* protect privacy,
* incentivize repayment without relying on heavy legal enforcement, and
* operate without requiring a central custodian of funds.

## 4. Core Principles

Coxy Fi is designed around the following principles:

1. **Peer-to-peer:** Lenders and borrowers interact directly. Lenders self-custody assets until a loan is executed.
2. **Privacy-first:** No names, phone numbers, or email addresses are placed on-chain; identity is pseudonymous and community-bound.
3. **Community enforcement:** Repayment incentives and consequences are anchored to community membership benefits and reputation rather than traditional KYC enforcement.
4. **Low volatility funding:** Loans can be denominated and repaid in stablecoins to reduce volatility and remove the need for price oracles in the core loan logic.
5. **Progressive trust:** Eligibility and risk pricing improve with time in the community and verifiable on-chain learning credentials.
6. **No central custody:** Protocol contracts enforce rules; the platform does not act as a custodian of user funds.

## 5. Scope: Intranet RealFi Pilot and Community Domains

Coxy Fi begins as an intranet pilot within the Coxygen/Zonke ecosystem. In this design, a “community domain” is represented on-chain by a membership credential (e.g., **CC-NFT**) that identifies the participant as part of the domain.

Future communities may launch their own domains (e.g., “B-NFT” for Community B). Each domain maintains its own reputation environment, while a long-term federation can allow interoperability under a shared standard.

## 6. Supported Assets and Rationale (Stablecoins and ADA)

Coxy Fi supports both stablecoin lending and ADA lending, with the rule that the borrower must repay in the **same asset** they borrowed.

### 6.1 Stablecoins

Stablecoins are supported to reduce volatility and simplify loan accounting. The protocol intends to support Cardano-native stablecoins such as **USDM** (Moneta/Mehen), **USDA** (Anzens), and **DJED** (COTI/IOG), and may also support other stablecoin variants introduced on Cardano over time. ([Moneta][1])
Where relevant and available, stablecoin infrastructure expansions (e.g., USDC-backed variants) may be considered for integration. ([Yahoo Finance][2])

### 6.2 ADA

ADA loans are also allowed for community members who prefer ADA-denominated borrowing and repayment. ADA lending is subject to volatility risk and is typically priced accordingly by lenders.

## 7. Participants and Roles

### 7.1 Borrowers

Borrowers are community members (initially students and enrolled members) who request micro-loans for micro-business growth or personal needs. Borrowers accept loan offers and commit to repayment schedules.

### 7.2 Lenders (Liquidity Providers)

Lenders supply ADA or stablecoins to borrowers and set terms such as interest rate, duration, and risk preferences. Lenders benefit from interest income and may also participate in reputation-building within the community.

### 7.3 Community Domain (Coxygen/Zonke)

The community provides membership benefits (training access, jobs network, positions, further loan eligibility) that serve as the non-financial enforcement layer.

### 7.4 Protocol and Smart Contracts

Smart contracts coordinate loan offers, loan acceptance, repayment accounting, and the on-chain credit standing records used for eligibility gating.

## 8. Identity, Privacy, and the Coxy DID / CFDID

Coxy Fi introduces a pseudonymous identifier called the **Coxy Fi DID (CFDID)** to represent a user in the credit system.

### 8.1 “Computed on the fly”

The system is designed so that sensitive identity elements are not stored in a recoverable form. A user’s CFDID can be derived when needed rather than being stored as plain personal information.

### 8.2 Strong derivation requirements

To protect users from credential guessing or brute-force attacks, the CFDID derivation should use a modern, memory-hard function such as **Argon2id**, which is standardized for password hashing and is intended to make large-scale guessing expensive. ([RFC Editor][3])

### 8.3 DID alignment

While Coxy Fi uses a DID concept internally, it also aligns with the broader idea that decentralized identifiers are controlled via cryptographic proofs rather than centralized registries. ([W3C][4])

In the intranet pilot, identity is additionally anchored by a domain membership credential (e.g., CC-NFT), allowing reputation and enforcement to remain community-bound.

## 9. Credit Profile and Eligibility Rules

Coxy Fi relies on a credit profile built from “digital gains” and community reputation, rather than traditional KYC credit checks.

### 9.1 Eligibility (Pilot Rules)

Borrowers qualify to participate in the loan scheme when they satisfy at least the following:

* The borrower has been enrolled in the Coxygen/Zonke community for **six months or more**.
* The borrower has completed at least **37 on-chain learning progress credentials**, used as a readiness threshold for further training and reliability.
* The borrower maintains acceptable internal reputation and has not been suspended for unresolved arrears.

### 9.2 Credit score inputs

Credit scoring can include: time in community, repayment history, lender ratings, training completions, and participation credentials. These signals form a **credit standing** that drives eligibility and can influence the interest rate lenders demand.


## 10. Lending and Borrowing Flow (P2P Marketplace)

Coxy Fi uses a P2P marketplace model:

1. A lender creates a loan offer specifying asset type (stablecoin or ADA), principal, duration, interest terms, and risk requirements (minimum standing/score).
2. An eligible borrower accepts a loan offer.
3. The loan is executed through a smart contract state that tracks obligations and deadlines.
4. Repayment occurs according to the selected repayment method (on-chain or off-chain confirmation).
5. Loan completion improves borrower standing and unlocks larger opportunities over time.

Because the marketplace is P2P, the protocol does not mandate a single universal interest rate. Lenders may price risk as they see fit, and borrowers select offers that match their needs.

## 11. Repayment Methods

Coxy Fi supports multiple repayment modes:

### 11.1 On-chain repayment (preferred for the pilot)

Borrowers repay directly in the borrowed asset (stablecoin or ADA). This mode is automatable and reduces disputes.

### 11.2 Fiat repayment (later phases)

Borrowers may repay via EFT, eWallet/mobile money, or debit orders. In early designs, borrowers submit proof and lenders confirm receipt. Over time, the protocol can add a multi-party confirmation model to reduce the risk of dishonest confirmations.

## 12. Default, “Three Chances,” and Decentralized Punishment

Coxy Fi’s enforcement is primarily **reputational and access-based**, not identity-based KYC enforcement.

### 12.1 Three chances

If a borrower misses a payment, the protocol provides up to **three opportunities** to resolve arrears within defined grace windows. Late repayment is allowed, and the borrower can restore good standing by clearing arrears.

### 12.2 Suspension (blacklisting) and consequences

If arrears remain unresolved after the allowed opportunities, the borrower’s account is placed into **Suspended** standing for the community domain. Suspension includes loss of access to community benefits such as further loans, training access, jobs and opportunities, and positions.

### 12.3 Reinstatement

A suspended borrower can return by repaying arrears and satisfying the reinstatement policy. The borrower may begin “clean” again, but prior suspension can still influence risk pricing and future eligibility thresholds.

This approach makes default economically irrational for many borrowers because the value of community access exceeds the value of a micro-loan.

## 13. Fees and Economics

Coxy Fi is designed to be lightweight and transparent.

### 13.1 Network fees

Users pay Cardano transaction fees for on-chain actions.

### 13.2 Protocol and service fees (illustrative)

The pilot may include limited fees to support sustainable operation, such as:

* a small protocol fee to cover operational and development costs,
* optional conversion or cash-out service fees when off-chain settlement or cash access is used.

Fees should be disclosed clearly before execution of any transaction.

## 14. Governance and Upgrades

Coxy Fi begins as an intranet pilot with a defined policy set and evolves toward stronger decentralization as adoption grows.

Governance can be anchored to community credentials and on-chain voting. Upgrades may include improvements to risk scoring, dispute resolution, federation across communities, and stronger compliance controls for expansion beyond the intranet pilot.

## 15. Security and Technical Architecture

### 15.1 Wallet integration

Coxy Fi can integrate with Cardano wallets through the dApp-wallet bridge standard, enabling secure user authorization and transaction signing. ([cips.cardano.org][5])

### 15.2 Efficient shared state

Credit standing and domain credentials can be referenced efficiently using Cardano primitives such as **reference inputs** (and related tooling), supporting scalable validation without consuming shared UTxOs each time. ([cips.cardano.org][6])

### 15.3 Privacy by design

Coxy Fi avoids placing personal identifiers on-chain. The system favors pseudonymous identifiers and credential proofs, with secure derivation approaches for any off-chain identifiers. ([RFC Editor][3])

## 16. Risks and Mitigations

Coxy Fi acknowledges these major risks:

* **Smart contract risk:** Bugs or vulnerabilities may cause fund loss. Mitigation includes audits, formal testing, staged rollouts, and conservative limits.
* **Stablecoin risk:** Stablecoins may de-peg or have issuer risk. Even widely-used models can fail. ([Moneta][1])
* **Default risk:** Borrowers may default. Mitigation includes community-based enforcement, eligibility gating, and progressive trust.
* **Dispute risk (fiat repayment):** Proof/confirmation disputes can occur. Mitigation includes on-chain repayment preference and later multi-party confirmation models.
* **Regulatory risk:** Requirements differ by jurisdiction. Mitigation includes limiting scope during the intranet pilot and adding licensing/compliance where expansion requires it.
* **Privacy risk:** Weak secrets can lead to identity guessing. Mitigation includes memory-hard derivation methods and strong local secrets. ([RFC Editor][3])

## 17. Roadmap

### Phase 1: Intranet Pilot (Coxygen/Zonke)

* Stablecoin and ADA P2P loans within CC membership domain.
* Credit standing based on 6-month membership and 37+ credentials.
* On-chain repayment focus to minimize disputes.
* Suspension and reinstatement policies for defaulters.

### Phase 2: Enhanced Repayment Options

* Add structured support for fiat repayment confirmations.
* Add dispute resolution mechanisms that reduce reliance on any single party.

### Phase 3: Federation Across Communities

* Support additional community domains (e.g., B-NFT) with local credit standing.
* Enable interoperable credit signals across domains under shared standards.

### Phase 4: Broader RealFi Expansion

* Explore regulated integrations that allow stablecoin holders to participate in broader traditional markets through tokenized RealFi opportunities, subject to compliance and risk controls.

## 18. Glossary of Terms

* **ADA:** Cardano’s native cryptocurrency used for fees and value transfer.
* **Stablecoin:** A crypto asset designed to track a stable value (often USD), used to reduce volatility in loans. Examples considered include USDM, USDA, and DJED. ([Moneta][1])
* **USDM:** A fiat-backed stablecoin project presented as Cardano-native. ([Moneta][1])
* **USDA:** A USD-backed stablecoin initiative associated with Anzens. ([anzens.com][7])
* **DJED:** An overcollateralized stablecoin model on Cardano associated with COTI/IOG. ([djed.xyz][8])
* **CFDID (Coxy Fi DID):** A pseudonymous identifier used to build a credit profile without publishing personal data.
* **CC-NFT:** A membership credential representing participation in the Coxygen/Zonke community domain.
* **Credit Standing:** A status (e.g., Good, Late, Suspended) used to gate borrowing privileges.
* **P2P (Peer-to-Peer):** A model where lenders and borrowers interact directly without a central custodian.
* **CIP-30:** Cardano standard interface for dApps to interact with wallets. ([cips.cardano.org][5])
* **CIP-31:** Cardano mechanism for reference inputs (reading UTxOs without consuming them). ([cips.cardano.org][6])
* **Argon2id:** A memory-hard function recommended for password hashing and resistant to large-scale guessing. ([RFC Editor][3])
* **DID:** Decentralized Identifier, an identifier controlled via cryptographic proofs rather than centralized registries. ([W3C][4])
* **Default:** Unresolved arrears after allowed grace opportunities, resulting in suspension of borrowing privileges and community benefits.
* **Reinstatement:** The process of restoring good standing by repaying arrears and meeting policy requirements.


[1]: https://moneta.global/?utm_source=chatgpt.com "Mehen - Moneta - USDM Stablecoin | Cardano's Premier Fiat-Backed Stablecoin"
[2]: https://finance.yahoo.com/news/cardano-sets-february-target-usdcx-183043518.html?utm_source=chatgpt.com "Cardano Sets February Target for USDCx Stablecoin Launch to Boost Liquidity"
[3]: https://www.rfc-editor.org/rfc/rfc9106.html?utm_source=chatgpt.com "RFC 9106: Argon2 Memory-Hard Function for Password Hashing and Proof-of ..."
[4]: https://www.w3.org/TR/did-1.0/?utm_source=chatgpt.com "Decentralized Identifiers (DIDs) v1.0"
[5]: https://cips.cardano.org/cip/CIP-30?utm_source=chatgpt.com "CIP-30 | Cardano dApp-Wallet Web Bridge"
[6]: https://cips.cardano.org/cip/CIP-31?utm_source=chatgpt.com "CIP-31 | Reference inputs - cips.cardano.org"
[7]: https://www.anzens.com/?utm_source=chatgpt.com "Anzens USDA Stablecoin"
[8]: https://www.djed.xyz/?utm_source=chatgpt.com "Djed"

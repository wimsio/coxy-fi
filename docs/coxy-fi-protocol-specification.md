## Appendix A: Protocol Specification (Intranet Pilot)

### A1. Purpose and Scope

This appendix specifies the minimum technical and operational rules required to implement Coxy Fi as a peer-to-peer micro-loan marketplace within the Coxygen/Zonke community domain (“the Domain”). The design prioritizes stablecoin-denominated loans to reduce volatility and avoid price oracle dependencies, while still allowing ADA loans when a borrower explicitly requests ADA and agrees to repay in ADA.

This specification describes a pilot architecture that can function in an intranet environment and later be extended to broader federation. Where this appendix mentions “must” and “shall,” it defines protocol requirements for the pilot.

### A2. Asset Support and Denomination Rules

Coxy Fi supports lending and borrowing in two categories of assets: (a) Cardano-native stablecoins approved by the Domain, and (b) ADA. Every loan shall be denominated in exactly one asset type. Repayments shall occur in the same asset type as the principal, and the protocol shall not automatically convert between assets. This rule avoids reliance on external price feeds and eliminates the need for oracle-based accounting in the core loan life cycle.

The Domain may publish and update an allow-list of stablecoin asset identifiers that are considered acceptable for the community. Lenders may offer only assets from this allow-list and ADA.

### A3. Participants and Roles

Coxy Fi includes the following participant roles:

**Borrower.** A borrower is a Domain member who requests and receives a micro-loan and is obligated to repay it according to the accepted terms. A borrower must meet eligibility rules defined by the Domain before accepting any loan offer.

**Lender.** A lender is a participant who provides ADA or approved stablecoins to fund loans. Lenders set loan terms, including interest rate, duration, and risk requirements. Lenders self-custody their assets up until the moment a loan offer is accepted and executed via an on-chain transaction.

**Domain (Coxygen/Zonke).** The Domain is a credentialed community environment that issues membership credentials and learning credentials, and provides community benefits that may be gated by credit standing. The Domain does not act as a custodian of funds.

**Credit Registry Updaters.** In the pilot, certain designated keys or a committee may be authorized to update the credit standing registry. Over time, this may evolve toward broader governance, but in the pilot it shall remain constrained to avoid spam and manipulation.

**Dispute Participants.** For off-chain repayments, the borrower and lender participate in a confirmation process. The protocol may optionally include an arbitration committee in later phases, but in the pilot the lender confirmation process is the baseline mechanism.

### A4. Identity Model and Privacy Requirements

Coxy Fi operates without publishing personal identifiers on-chain. The protocol does not require on-chain names, phone numbers, or email addresses.

Identity is expressed in two layers:

**(1) On-chain Borrower Identifier.** Each borrower has an on-chain identifier derived from cryptographic control of a wallet within the Domain. This identifier is used to associate loans and repayment history with a persistent pseudonymous identity inside the Domain.

**(2) Off-chain Login Alias.** The platform may allow users to log in via a primary email and a secret (PIN/passphrase). If an email-based login is used, the system shall not store raw email or a reversible form of email. Instead, it shall compute an alias using a memory-hard derivation approach, and shall require a user secret that is strong enough to resist guessing attacks. In practice, this is best achieved by generating a device-stored random secret and protecting it locally with a PIN, rather than using a short PIN directly as the sole cryptographic salt.

The central requirement is that a database compromise must not reveal user identities from stored records, and the system should minimize retained personal data.

### A5. Eligibility and Credit Standing Rules

Borrower eligibility in the pilot shall be defined by Domain participation and learning credentials. A borrower shall be eligible to accept loans only if:

1. The borrower has remained enrolled in the Domain for at least six months, measured according to Domain credential timestamps or Domain enrollment attestations.
2. The borrower has completed at least 37 qualifying on-chain learning progress credentials as defined by the Domain.
3. The borrower is not currently suspended due to unresolved arrears.

The protocol shall maintain a credit standing state for each borrower. Credit standing shall include at minimum: Good Standing, Late, Delinquent, Suspended, and Reinstated (or Good Standing again after repayment). The Domain may compute and display an internal “credit score,” but the minimum enforcement logic shall rely on standing states.

### A6. On-chain Objects and Minimal Data Requirements

The protocol can be implemented with three principal on-chain objects:

**(1) Loan Offer Object.** A UTxO representing a lender’s offer to lend a particular asset type under specified terms. The datum must capture principal bounds, interest rate or fixed return, loan duration, repayment cadence (e.g., monthly), and minimum borrower standing/requirements. The lender must retain the ability to cancel the offer prior to acceptance.

**(2) Active Loan Object.** A UTxO representing the state of a specific loan between a lender and borrower. The datum must capture: the asset type, principal, interest terms, duration, borrower identifier, lender identifier, repayment schedule, amount paid so far, outstanding balance, and a structured set of late windows (“three chances”).

**(3) Credit Registry Object.** A UTxO (or set of UTxOs) representing borrower standing and eligibility markers. In the pilot, this object may be updated by authorized Domain keys or a committee. Loan validation shall reference this registry when validating borrower eligibility and when enforcing standing updates after missed payments.

### A7. Loan Lifecycle and State Machine

A Coxy Fi loan follows a controlled state machine that governs transitions:

**Offer Created.** A lender posts a loan offer that is available for acceptance by eligible borrowers.

**Offer Accepted and Loan Activated.** A borrower accepts an offer, and the offer transitions into an active loan state. The transaction that activates the loan must bind the borrower identifier and lender identifier into the loan datum, and it must move the loan funds to the borrower under the agreed terms.

**Repayment In Progress.** The borrower repays according to the schedule. Each repayment updates the loan datum to increase the paid amount and decrease the outstanding balance.

**Late Windows (Three Chances).** If a scheduled payment is missed, the loan moves into a late window with defined grace time. The protocol supports three chances. Each chance is a period during which the borrower may repay arrears and return to Good Standing without being suspended.

**Suspended (Default).** If the borrower fails to cure arrears after the third chance window expires, the borrower is marked Suspended in the Credit Registry. The protocol shall then prevent the borrower from accepting new loans within the Domain while suspended.

**Reinstatement.** If a suspended borrower later repays all arrears (and any defined late fees), the borrower shall be reinstated to Good Standing or a Reinstated state, and may become eligible again subject to Domain policy. The Domain may also apply a score penalty even after reinstatement to reflect repayment reliability.

### A8. Late and Default Policy Definition

The “three chances” policy shall be encoded deterministically so that all participants can anticipate consequences. A recommended pilot definition is:

* A scheduled payment becomes “Late” when it is not fully received by the due date.
* Chance 1 window begins immediately after the due date and lasts a defined grace interval.
* Chance 2 begins after Chance 1 expires and lasts a second grace interval.
* Chance 3 begins after Chance 2 expires and lasts a third grace interval.
* Suspension becomes eligible only after Chance 3 expires without curing arrears.

The specific grace interval durations may be configured by Domain policy for different loan durations, but the policy must be visible before acceptance so that borrowers and lenders understand it.

### A9. Repayment Modes

Coxy Fi supports two repayment modes.

**(1) On-chain repayment.** This is the preferred pilot mode for simplicity. In this mode, repayment is executed by sending the loan asset to the repayment script/state transition and updating the active loan state. Completion is objective and automatic.

**(2) Off-chain (fiat) repayment with confirmation.** In this mode, the borrower repays via EFT, eWallet, mobile money, debit order, or other acceptable rails. The borrower submits proof to the platform and requests confirmation. The lender confirms receipt, after which the loan state is updated to reflect repayment. The pilot acknowledges that off-chain proofs can be disputed; therefore, a time-bound confirmation window and an escalation mechanism to an arbitration committee is recommended for later phases.

### A10. Interest and Pricing Model

Coxy Fi is a marketplace and does not impose a single universal interest rate. Lenders set their own terms and can price according to demand and borrower standing. Borrowers select offers that suit their needs and perceived affordability. The protocol may display indicative “risk tiers” based on standing and community achievements, but lenders remain responsible for pricing risk.

The protocol shall clearly disclose the total repayment amount and timing before a borrower accepts a loan. Extremely high interest configurations should be treated as high-risk and may be restricted by Domain policy if required for user safety and long-term sustainability.

### A11. Credit Score Inputs and Updates

Credit standing and score signals shall be derived from community participation and repayment behavior. In the pilot, the following inputs are recommended:

* time enrolled in the Domain,
* completion count of qualifying on-chain credentials,
* repayment history (on-time vs late vs suspended),
* lender ratings (where applicable and fraud-resistant),
* successful loan completion count and progressive loan sizing.

Credit updates shall be deterministic and auditable. The protocol should avoid subjective manual scoring where possible.

### A12. Limits and Safety Controls (Pilot)

The pilot shall impose conservative limits, including principal range constraints (e.g., $200–$600 equivalent in the selected stablecoin, or a domain-defined ADA range), limits on the number of concurrent active loans per borrower, and limits on maximum duration and payment cadence. These constraints reduce systemic risk while the protocol is being validated in real usage.

### A13. Governance and Upgrades

Coxy Fi governance begins with Domain-based control for safety and evolves toward community governance over time. In the pilot, certain keys or a committee may be allowed to update registry parameters, stablecoin allow-lists, and operational limits.

Any upgrades to smart contracts shall be disclosed, tested, and rolled out with cautious limits. Users should be able to verify the on-chain contract addresses and policies associated with the Domain.

### A14. Federation Across Communities

The protocol anticipates a future federation model in which multiple communities operate parallel “domains” with their own membership credentials and registries. Federation shall not assume email matching across databases. Instead, interoperability should be based on cryptographic proof of control and on-chain credential references, preserving privacy and avoiding dependence on centralized personal identity data.

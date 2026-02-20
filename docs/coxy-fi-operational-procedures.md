## Appendix F: Coxy Fi Operational Procedures (Pilot Runbook)

### F1. Purpose

This appendix defines operational procedures for running the Coxy Fi intranet pilot safely and consistently. It is written as a practical runbook for the Domain operators, credential issuers, committee members, and community moderators who support the pilot. These procedures are designed to preserve the “no central custody” principle while still allowing responsible administration, user safety, and dispute handling.

This runbook does not create a central custodian. It defines how the Domain coordinates credentialing and standing updates while lenders and borrowers remain fully responsible for their own funds and repayment decisions.

### F2. Operating Roles and Separation of Duties

To reduce abuse and conflicts of interest, the pilot separates roles into distinct responsibilities.

1. **Domain Membership Issuer:** Issues and revokes Domain membership credentials (e.g., CC-NFT) according to published enrollment rules. This role does not control user funds.
2. **Learning Credential Issuer:** Issues learning progress credentials (including the “37 credentials” qualification threshold) based on objective completion criteria.
3. **Credit Registry Committee:** Updates credit standing and handles exceptional standing operations (such as reinstatement confirmation when off-chain proof is disputed). This role should be a multi-person committee and should not be a single individual.
4. **Support and Moderation Team:** Handles user questions, education, and abuse reports. This team cannot seize funds and cannot unilaterally rewrite repayment state.
5. **Smart Contract Stewardship Team:** Manages upgrade planning, testnet deployments, and emergency procedures. This team must follow published governance processes for upgrades.

The pilot should implement a policy that prevents the same individual from holding all roles simultaneously, unless the pilot is extremely small and explicitly discloses such limitations to participants.

### F3. Enrollment, Membership, and Credential Issuance

#### F3.1 Enrollment procedure

When a user enrolls in the Domain, the membership issuer shall:

1. verify enrollment according to the Domain’s published rules (e.g., student enrollment verification within the intranet environment),
2. create or facilitate creation of the user’s wallet/address within the intranet model if that is part of the Domain’s onboarding, and
3. issue a Domain membership credential (e.g., CC-NFT) to the user’s wallet.

The Domain shall record an enrollment timestamp or enrollment credential that can be used to measure the six-month eligibility rule.

#### F3.2 Learning credential issuance

Learning credential issuers shall:

1. issue credentials only when objective completion criteria are met,
2. avoid manual issuance without evidence, and
3. ensure credential issuance is consistent and auditable.

The “37 credentials” threshold shall be computed from the on-chain credential set defined by the Domain.

### F4. Eligibility Verification in the Pilot

The system shall verify borrower eligibility before loan acceptance using the following checks:

1. the borrower holds a valid Domain membership credential,
2. the borrower’s enrollment age meets the minimum (six months),
3. the borrower’s on-chain learning credentials meet the threshold (at least 37), and
4. the borrower’s credit standing is not Suspended.

These checks may be performed automatically by the dApp interface and/or validated by smart contract logic.

### F5. Loan Offer Moderation and Abuse Prevention

Because the marketplace is open to lender-defined terms, the Domain must reduce predatory or abusive listings during the pilot.

1. The Domain shall publish marketplace conduct guidelines requiring clear disclosure of principal, repayment amounts, and due dates.
2. The interface should warn users when rates are extremely high or when loan terms appear inconsistent.
3. The Domain may restrict or hide offers that are clearly malicious, fraudulent, or abusive in presentation, while acknowledging that this is not a guarantee of safety.

Moderation shall focus on abuse prevention and safety rather than controlling market pricing.

### F6. Repayment Operations (On-chain)

#### F6.1 Standard on-chain repayment procedure

When a borrower repays on-chain:

1. the borrower submits a repayment transaction that updates the loan state,
2. the system records the repayment on-chain, and
3. the borrower’s standing is updated automatically through protocol logic or through registry updates that reference the repayment state.

On-chain repayment is considered complete when the transaction is finalized on-chain.

#### F6.2 Payment reminders and education

The Domain may provide reminders, education, and budgeting guidance, but reminders do not alter repayment obligations and do not pause due dates unless a formal restructure is agreed by both parties.

### F7. Repayment Operations (Off-chain Fiat Proofs – Pilot Mode)

Because fiat repayment introduces disputes, the pilot must apply a clear process.

#### F7.1 Borrower submission procedure

A borrower who repays via EFT/eWallet/mobile money/debit order shall:

1. submit proof through the designated intranet channel,
2. include a reference code or unique transaction identifier where available, and
3. submit within a defined time window after payment (e.g., within 48 hours), to reduce confusion.

#### F7.2 Lender confirmation procedure

The lender shall:

1. confirm receipt honestly and promptly through the designated confirmation interface,
2. confirm within the confirmation window (e.g., 72 hours), and
3. if rejecting, provide a reason such as “payment not received” or “incorrect reference” and supply supporting evidence where feasible.

The pilot should treat repeated dishonest confirmation behavior as abuse.

#### F7.3 Escalation procedure (recommended)

If a borrower claims repayment and the lender does not confirm within the window, or disputes the claim, the case may be escalated to the Credit Registry Committee for review.

Committee review should follow three steps:

1. request evidence from both parties,
2. verify consistency of proofs and references, and
3. decide whether the credit registry should reflect repayment.

The committee should not claim to have legal enforcement power. Its role is to maintain community integrity and prevent misuse of standing rules.

### F8. Late Payments, “Three Chances,” and Standing Updates

#### F8.1 Late handling procedure

If a borrower misses a due date, the system flags Late standing and begins Chance Window 1. The Domain should provide a standardized reminder and education message explaining:

1. the current standing,
2. the time remaining in the current chance window, and
3. how to cure arrears.

#### F8.2 Strike progression procedure

If arrears are not cured by the end of Chance 1, standing progresses to Delinquent and Strike 1 is recorded. The same process repeats for Chance 2 and Chance 3.

The Domain should ensure the policy is applied consistently and cannot be arbitrarily modified on a per-user basis without published governance authority.

#### F8.3 Suspension procedure

If the borrower fails to cure arrears after Chance 3 expires, the borrower’s standing is set to Suspended. Suspended standing triggers gating across Domain benefits.

### F9. Reinstatement Procedure

A suspended borrower can return by repaying all arrears according to policy.

Reinstatement shall follow this procedure:

1. the borrower repays arrears (on-chain repayment is preferred where possible),
2. the borrower submits a reinstatement request if required by the interface,
3. the system verifies arrears are cleared, and
4. standing is updated to Reinstated or Good Standing, with tier limits reset to entry-level for at least one successful cycle.

Reinstatement shall not erase historical records. It is a restoration of eligibility, not a deletion of repayment history.

### F10. Loan Restructuring Procedure (Optional in Pilot)

If the Domain allows restructuring, it must be explicit, consent-based, and recorded.

A restructure requires:

1. mutual agreement between lender and borrower,
2. a clear new schedule and total repayment amount, and
3. an on-chain update (where feasible) to prevent misunderstandings.

The Domain should limit restructuring frequency to reduce repeated “evergreen” debt.

### F11. Incident Handling and Emergency Procedures

Even without central custody, emergencies can arise (e.g., a discovered smart contract vulnerability).

#### F11.1 Emergency pause (interface-level)

The Domain may temporarily pause the interface’s ability to create new offers or accept new loans if a severe vulnerability is discovered. This does not seize funds; it only prevents new commitments.

#### F11.2 Smart contract deprecation and migration

If a contract must be replaced:

1. the Domain announces the reason and the new contract addresses,
2. the Domain provides a migration guide, and
3. the Domain sets conservative transition limits.

The Domain should avoid forced migrations that could trap funds.

#### F11.3 Communication protocol

All incidents should be communicated through the Domain’s official channels. The message must include:

1. what happened,
2. what users should do immediately, and
3. what changes are being made.

### F12. Audit, Monitoring, and Reporting (Pilot)

The Domain should operate a minimal transparency dashboard (intranet is acceptable) that reports:

1. total loans issued (count and volume),
2. repayment rates, late rates, suspension rates,
3. average loan size, duration, and interest ranges, and
4. stablecoin usage distribution.

The purpose of reporting is to help users understand risk and to guide policy tuning.

### F13. Staff and Committee Conduct Rules

To maintain trust:

1. committee members must disclose conflicts of interest where possible,
2. committee members should not use their position to pressure users, and
3. actions that affect standing must be traceable and auditable.

### F14. Data Minimization Operations

Operational processes should minimize personal data exposure:

1. avoid collecting unnecessary personal identifiers,
2. limit access to off-chain repayment proofs to authorized reviewers,
3. redact or delete proofs after the retention window when no dispute remains, and
4. prefer on-chain repayment methods when feasible.

### F15. Continuous Improvement Process

The pilot shall run a structured feedback process:

1. collect community feedback on usability and fairness,
2. publish proposed policy changes,
3. test changes in a limited scope, and
4. roll out changes with transparent communication.

This process supports safe scaling and prepares the protocol for federation beyond the intranet.

## Appendix E: Risk Scoring and Loan Limits Policy (Pilot)

### E1. Purpose

This appendix defines a practical, transparent risk scoring and loan limits policy for the Coxy Fi intranet pilot. Its purpose is to protect lenders from excessive default risk, prevent borrowers from over-borrowing, and support responsible growth of the marketplace. This policy is designed to be strict enough to reduce systemic risk while remaining accessible enough to encourage adoption and participation.

The policy is intentionally modular. The Domain may update thresholds as more data becomes available, provided changes are disclosed before borrowers accept loans under the updated rules.

### E2. Core Risk Concepts

Coxy Fi uses a blended risk approach that combines (a) community stability and learning progress, and (b) repayment behavior. The model assumes that the Domain’s benefits and reputation systems create strong incentives to repay.

In the pilot, risk is represented by two linked measures:

1. **Credit Standing (State-Based):** A small set of enforceable states used for eligibility and punishment.
2. **Risk Score (Numeric):** A score used to determine limits and guide lender pricing in the marketplace.

Credit Standing shall always override the numeric score. A borrower who is Suspended is not eligible regardless of numeric score.

### E3. Credit Standing Definitions

The following Credit Standing states are used in the pilot:

1. **Good:** The borrower has no unresolved arrears and is eligible for loans subject to score tier rules.
2. **Late:** A payment is overdue but within the first grace window. The borrower may cure arrears without suspension.
3. **Delinquent:** The borrower is overdue beyond the first grace window and has incurred at least one “chance strike.”
4. **Suspended:** The borrower failed to cure arrears after three chances and is restricted from borrowing and from Domain benefits gated by standing.
5. **Reinstated:** The borrower was previously Suspended but has repaid arrears and returned to eligibility. This state may carry tighter limits until trust is rebuilt.

### E4. Borrower Eligibility Gate (Pilot Minimum)

A borrower may accept loans only if all conditions below are met:

1. The borrower has remained enrolled in the Domain for at least six months.
2. The borrower has completed at least 37 qualifying on-chain learning progress credentials.
3. The borrower’s Credit Standing is Good or Reinstated (and not Late, Delinquent, or Suspended at acceptance time).
4. The borrower does not exceed concurrent loan limits defined in this appendix.

### E5. Risk Score Model (Pilot)

The pilot uses a score range of **0 to 100**, where higher scores represent lower risk. The score is computed from verifiable Domain signals and loan repayment history.

#### E5.1 Base score components

The borrower’s initial score starts from a base and then adjusts:

1. **Membership longevity factor:** Time enrolled beyond the minimum six months increases score gradually.
2. **Learning credential factor:** Completion beyond the 37-credential threshold increases score gradually.
3. **Repayment performance factor:** Each successfully completed loan improves score. Late payments reduce score. Suspensions reduce score significantly.
4. **Lender rating factor:** Where ratings exist, only fraud-resistant ratings may be included. A single counterparty rating cannot dominate the score.

#### E5.2 Pilot scoring philosophy

The pilot prioritizes behavior over promises. A borrower who repays consistently should become eligible for larger principal and better rates. A borrower who becomes late repeatedly should be constrained even if their membership and learning credentials are strong.

The pilot should avoid “hidden scoring.” The system should display the borrower’s standing and tier in a simplified manner (e.g., Tier 1 to Tier 5), even if the full numeric score is not shown publicly.

### E6. Risk Tiers and Borrowing Limits

Risk tiers translate standing and score into borrowing limits. In the pilot, tiers are defined as follows:

#### Tier 0: Suspended (Score irrelevant)

A borrower in Suspended standing cannot accept new loans. Domain benefits gated by standing are restricted until arrears are cleared and reinstatement conditions are met.

#### Tier 1: Entry Tier (Score 40–54, Standing Good/Reinstated)

Tier 1 is for borrowers who have just become eligible or who have recently been reinstated. Borrowing is limited to prevent early over-extension.

* **Maximum principal per loan:** $200 equivalent (stablecoin) or a Domain-defined ADA equivalent.
* **Maximum concurrent loans:** 1
* **Maximum duration:** 30 days (or 30–45 days if Domain allows)
* **Repayment cadence:** single payment or monthly
* **Suggested interest band:** lender-set, but the UI should warn that very high rates carry borrower stress risk.

#### Tier 2: Growth Tier (Score 55–64)

Tier 2 is for borrowers who have demonstrated at least one successful repayment cycle.

* **Maximum principal per loan:** $300 equivalent
* **Maximum concurrent loans:** 1
* **Maximum duration:** up to 60 days
* **Repayment cadence:** monthly or end-of-term
* **Late policy:** standard three chances

#### Tier 3: Trusted Tier (Score 65–74)

Tier 3 is for borrowers with consistent repayment performance and stronger domain engagement.

* **Maximum principal per loan:** $450 equivalent
* **Maximum concurrent loans:** 2 (only if both are stablecoin-denominated or if Domain allows ADA risk separately)
* **Maximum duration:** up to 90 days
* **Repayment cadence:** monthly
* **Additional requirement:** must have no late events in the most recent completed loan cycle (Domain can define this window).

#### Tier 4: Advanced Tier (Score 75–84)

Tier 4 is for borrowers with repeated successful repayments and minimal late history.

* **Maximum principal per loan:** $600 equivalent
* **Maximum concurrent loans:** 2
* **Maximum duration:** up to 120 days
* **Repayment cadence:** monthly
* **Optional benefit:** access to lower marketplace fees or priority listing.

#### Tier 5: Exceptional Tier (Score 85–100)

Tier 5 is reserved for top borrowers with strong repayment history and high internal reputation.

* **Maximum principal per loan:** $600–$1,000 equivalent (only if Domain authorizes expansion)
* **Maximum concurrent loans:** up to 3 (pilot should only enable this if default rates remain low)
* **Maximum duration:** up to 180 days
* **Repayment cadence:** monthly
* **Special safety rule:** Tier 5 borrowers should still be blocked from rapid compounding borrowing (see E8).

### E7. Interest Guidance and Marketplace Safety

Coxy Fi allows lenders to set their own interest rates. However, the pilot should include responsible disclosure mechanisms:

1. The borrower must see the total repayment amount before acceptance.
2. The UI should display an effective monthly cost and a warning banner for extremely high rates.
3. The Domain may impose a maximum rate cap during the intranet pilot to reduce harm and stabilize repayment rates, while still allowing market pricing within a reasonable band.

If the Domain allows very high interest rates for low-score borrowers, the protocol should treat such loans as high-risk and may limit their principal or duration automatically.

### E8. Anti-Overborrowing Controls

To prevent borrowers from stacking debt irresponsibly, the pilot shall implement these controls:

1. **Cooldown period:** After completing a loan, a borrower must wait a short cooldown period (e.g., 3–7 days) before accepting a new loan in the same tier.
2. **No rapid step-jumps:** A borrower may not jump more than one tier upward per completed loan cycle.
3. **Debt-to-standing limit:** Even if Tier allows multiple concurrent loans, the borrower’s total outstanding principal must not exceed the maximum allowed for their tier.

These controls reduce default risk and encourage gradual trust building.

### E9. Strike System and Score Penalties

The strike system is connected to the “three chances” policy.

1. A missed due date triggers **Late** standing and may apply a small score penalty.
2. Failure to cure within Chance 1 triggers **Strike 1** and a larger score penalty.
3. Failure to cure within Chance 2 triggers **Strike 2** and a larger score penalty.
4. Failure to cure within Chance 3 triggers **Suspended** standing and a major score penalty.

Reinstatement does not erase history automatically. The protocol may mark borrowers as Reinstated and apply tighter limits until sufficient successful repayments rebuild trust.

### E10. Reinstatement Conditions (Pilot)

A suspended borrower may be reinstated only when:

1. all arrears and agreed late fees (if any) are fully paid,
2. the borrower accepts reinstatement rules and any cooldown waiting period, and
3. the borrower returns initially to Tier 1 limits for at least one successful cycle.

This approach allows forgiveness while maintaining a strong deterrent.

### E11. Lender Protections and Transparency

The protocol should provide lenders with transparent risk information that does not compromise borrower privacy. In the pilot, lenders should be able to view:

1. borrower tier and standing,
2. number of completed loans,
3. number of late events and suspensions (in aggregated form),
4. domain membership duration category (e.g., 6–9 months, 9–12 months, 12+ months), and
5. learning credential completion category (e.g., 37–50, 50–70, 70+).

This information should be shown without revealing personal identity.

### E12. Stablecoin and ADA Risk Considerations

Stablecoin loans reduce volatility but introduce stablecoin issuer and de-pegging risk. ADA loans introduce volatility risk and may require more conservative limits or higher lender pricing. The Domain may enforce separate ADA tier caps if volatility begins to affect repayment success.

### E13. Policy Updates

The Domain may update tier thresholds, principal limits, cooldown rules, and scoring weights during the pilot. Any changes must be disclosed before new loans are accepted under the updated policy. Existing loans continue under the terms accepted at activation unless both parties agree to restructure.




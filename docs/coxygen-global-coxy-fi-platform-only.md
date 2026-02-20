## Coxygen Global – Coxy Fi - Platform Only V1

## Platform-Only Marketplace Procedure (Direct Contracting + Self-Custody)

### 1) Purpose

To operate Coxy Fi as a **technology platform** that enables **peer-to-peer lending** between community lenders and borrowers, while ensuring:

* **Coxygen is not the lender, borrower, agent, broker, or custodian**
* **Crypto transfers are wallet-to-wallet (self-custody)**
* **Fiat repayments (if used) are executed via licensed payment partners**
* Clear auditability, dispute process, and compliance-ready documentation


## 2) Roles and Responsibilities

### 2.1 Coxygen (Platform Operator)

Coxygen provides:

* User accounts, profiles, verification workflows (where permitted)
* Loan listing/matching interface
* Contract templates and digital signing workflow (optional)
* Education, risk warnings, and recordkeeping tools
* Support and dispute intake (not adjudication of credit terms)

Coxygen **does not**:

* Lend or borrow
* Hold funds (crypto or fiat)
* Control keys/seed phrases
* Move funds on behalf of users
* Participate in interest/spread (no revenue share from interest)

### 2.2 Lender (User)

* Creates offers and sets terms
* Performs their own suitability checks where required
* Sends crypto directly from their own wallet to borrower wallet
* Receives repayments directly (crypto or fiat via partner rails)

### 2.3 Borrower (User)

* Accepts terms and signs contract directly with lender
* Provides repayment proof
* Repays directly to lender (or via licensed intermediary if fiat)

### 2.4 Payment Partner (Fiat only)

* Handles EFT/debit orders/card/wallet payouts and collections (where applicable)
* Performs required KYC/AML and mandate authentication (partner-controlled)
* Settles **directly** to lender or to a regulated intermediary (not to Coxygen)


## 3) Mandatory Platform Statement (Use in T&Cs + Onboarding Screen)

**Platform Status & Community Statement (recommended text):**

> “Coxygen Global (Coxy Fi) provides a technology platform that helps lenders and borrowers connect and transact directly. Coxygen Global is **not** a lender, borrower, credit provider, financial intermediary, agent, broker, payment processor, or custodian, and does not hold or control user funds or private keys. All crypto transfers occur **wallet-to-wallet** under self-custody by users.
> Where fiat repayments are used, these are handled through **licensed payment partners** and settled directly to the lender or a regulated intermediary.
> Coxy Fi is a global community platform: our students and community members are located across **10+ countries worldwide**, and they will participate in this **Cardano-based project** as part of learning and innovation.
> As adoption grows and the platform matures into a commercial business, Coxygen may progressively implement additional compliance frameworks and apply for relevant registrations/licences (including CASP where applicable).”


## 4) Operating Procedure (End-to-End)

### Step 1 — User Onboarding

1. User creates an account and accepts:

   * Terms of Service (platform-only statement)
   * Risk warnings (default/crypto volatility/consumer protection limits)
   * Privacy policy (data handling)
2. Platform collects basic profile info (minimum needed).
3. If fiat rails are enabled in a country:

   * User is redirected to the **payment partner onboarding/KYC** (Coxygen does not perform the regulated verification unless legally permitted and designed for it).

**Control:** users must tick explicit acknowledgements:

* “I understand Coxygen is not a lender/borrower/custodian.”
* “I understand crypto transfers are self-custody wallet-to-wallet.”
* “I understand disputes are between lender and borrower.”


### Step 2 — Listing and Matching

1. Lenders publish loan offers with standardized fields:

   * Amount range ($200–$600 equivalent)
   * Currency type (crypto asset / stable / fiat repayment option)
   * Interest/fee terms (lender-defined)
   * Repayment schedule and penalties (if any)
   * Collateral (if any) and enforcement method (if any)
2. Borrowers apply to a lender offer with:

   * Requested amount, term, purpose, repayment plan
   * Proof-of-income/identity documents *only if lender requires* (shared peer-to-peer; platform stores minimal copies if possible)

**Control:** Coxygen must display:

* “Terms are set by the lender.”
* “Coxygen does not recommend loans or provide investment advice.”


### Step 3 — Direct Contract Creation (Lender ↔ Borrower)

1. Platform generates a **Loan Agreement** for lender and borrower to sign:

   * Parties: lender and borrower legal names
   * Principal, term, repayment schedule
   * Interest/fees
   * Wallet addresses for disbursement + repayment
   * Default terms and dispute process
   * Governing law and jurisdiction (choose based on parties)
2. Both parties digitally sign (or external signing is linked).

**Control:** Contract must include:

* Coxygen is not a party to the agreement
* No custody by Coxygen
* Each party responsible for tax/reporting obligations


### Step 4 — Funding (Crypto Wallet-to-Wallet Only)

1. Borrower provides a **self-custody receiving address**.
2. Lender sends crypto from their wallet directly to borrower’s address.
3. Borrower confirms receipt by:

   * Providing transaction hash (txid)
   * Platform fetches chain confirmation (read-only)

**Control:** Platform must not:

* Provide hosted wallets
* Hold recovery keys
* Offer “send on behalf of” functionality


### Step 5 — Repayment

**Option A: Crypto Repayment (Preferred for platform-only)**

1. Borrower repays to lender wallet address as per schedule.
2. Borrower uploads txid; platform verifies on-chain (read-only).
3. Loan status updates automatically.

**Option B: Fiat Repayment (Only via Licensed Partner)**

1. Borrower selects a licensed payment partner option (EFT/debit order etc.).
2. Borrower signs mandates **with the payment partner** (not Coxygen).
3. Partner collects and settles **directly to lender** (or regulated intermediary).
4. Platform receives payment confirmation via partner webhook/API and updates status.

**Control:** Coxygen never receives or holds fiat repayments.


### Step 6 — Platform Fees (No Interest Participation)

Allowed fee models:

* **Listing fee** charged to lenders
* **Subscription fee** for access/tools
* **Fixed platform service fee** per successful match (flat fee, not a % of interest)
* **Optional premium tools** (analytics, education modules)

Not allowed (for platform-only posture):

* Taking a % of interest (“spread”)
* Charging success fees tied to loan performance
* Collecting repayments and forwarding (custody/agency risk)


### Step 7 — Records, Disputes, and Enforcement

1. Platform stores:

   * Signed loan agreement hash/version
   * On-chain tx hashes (funding + repayment)
   * Limited communications audit log
2. Dispute process:

   * Party-to-party resolution first (48–72 hours)
   * Platform provides evidence pack export (contract + tx + messages)
   * Escalation to mediator/arbitration (optional) chosen in contract

**Control:** Coxygen does not decide who is right; it only provides records.


## 5) Growth Plan: “Platform-Only → Gradual CASP Readiness”

### Phase 1 (Now): Platform Only

* Self-custody wallet-to-wallet transfers
* Fiat through licensed partners only
* Strong disclaimers + records + risk warnings

### Phase 2: Compliance Build-Out (When traction is proven)

* Dedicated compliance officer/consultant
* Formal AML/KYC strategy (where required)
* Enhanced transaction monitoring (still read-only if platform-only)

### Phase 3: Apply for Licences (If/When needed)

* Move toward CASP/FSP licensing if Coxygen starts doing any of:

  * custody, escrow control, transfers on behalf of users
  * integrated swaps/on-ramp as intermediary
  * managed wallets or key control


## 6) Non-Negotiable “Red Lines” (To stay platform-only)

Coxygen must not:

* Touch/hold funds (fiat or crypto)
* Control keys / seed phrases / multisigs
* Execute transfers for users
* Collect repayments and redistribute
* Set lending terms, underwrite, or act as lender of record


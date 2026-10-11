# Assignment 3 — Loan Origination & Approval System

## Scope
Start: applicant submits an application with documents. End: loan disbursed, rejected, withdrawn, or lapsed/expired.

## Participants / lanes
Applicant; Loan Officer; Underwriter / Credit Committee; Fraud & Compliance; Credit Bureau (external participant); Operations / Disbursement; Core Banking System.

## Main sequence (happy path)
1. **Message Start Event / User Task:** receive application and documents.
2. **Business Rule Task:** check document completeness.
3. **Parallel Gateway (split):** KYC verification; credit-bureau score retrieval; income/employment verification.
4. **Parallel Gateway (join):** continue when required checks are complete.
5. **Business Rule Task:** calculate eligibility and risk score.
6. **Exclusive Gateway:** auto-approve, manual review, or reject.
7. **User Task:** underwriter reviews and approves.
8. **Service/Script Task:** generate loan offer.
9. **Send Task:** send offer to applicant.
10. **Receive Task:** wait for applicant acceptance; timer boundary handles expiry.
11. **User Task:** complete e-signature.
12. **Service Task:** verify receiving account and disburse funds.
13. **Service Task:** create loan account and notify applicant.
14. **End Event:** Loan Disbursed.

## Gateway conditions
- **Exclusive:** documents complete? KYC resolved? risk route? offer accepted? disbursement succeeded?
- **Parallel:** independent KYC, bureau, and income checks execute together and join before risk scoring.
- **Inclusive:** activate one or more extra checks when policy conditions require them.
- **Event-based:** optional modeling choice for waiting on applicant response versus offer-expiry timer; use only if the diagram represents competing events rather than a simple deadline.

## Intermediate events and boundary events
- **Timer boundary:** seven-day document-response limit; offer validity (e.g., 15 days).
- **Error boundary:** credit bureau API timeout and disbursement integration failure.
- **Escalation:** fraud/compliance investigation or senior credit committee review.
- **Message intermediate events:** request missing documents; receive applicant acceptance/withdrawal.
- **Compensation:** reverse processing fees/release holds on withdrawal; reverse loan-account creation if disbursement cannot complete.

## Critical path
Application → document validation → parallel KYC/credit/income checks → risk scoring → underwriting approval → offer sent → acceptance → e-signature → account verification → disbursement and account creation → applicant notification → Loan Disbursed.

## Alternate paths
- Missing/illegible documents: request corrections; seven-day timer; no response means Application Lapsed.
- KYC mismatch: manual review; unresolved mismatch means rejection with reason code.
- Fraud/AML flag: investigation; confirmed issue means reject, record internal report, and terminate the active case as appropriate.
- Credit bureau unavailable: retry three times; manual check or park with timer.
- Low score: reject or counter-offer (guarantor, collateral, or lower amount).
- Income/DTI issue: adjust amount/tenure and rescore once; otherwise reject.
- High-value/borderline case: escalate to senior committee and add policy-required checks.
- Collateral valuation/title issue: revalue/re-underwrite; reject if title remains unclear.
- Offer not accepted: timer expires and process ends as Offer Expired.
- Applicant withdraws: compensate completed work where appropriate, release holds, end as Withdrawn.
- E-signature mismatch: resend/remind; cancel offer after two failed attempts.
- Disbursement failure: verify account and retry; hold funds/contact applicant; reverse account creation if still unsuccessful.

## Modeling checks
- Keep the credit bureau as an external participant when representing cross-organization communication.
- Do not use sequence flow across pool boundaries; use message flow between participants.
- Label decision conditions explicitly and ensure every route reaches review, recovery, rejection, withdrawal, or expiry.
- Limit retries and rescore loops.

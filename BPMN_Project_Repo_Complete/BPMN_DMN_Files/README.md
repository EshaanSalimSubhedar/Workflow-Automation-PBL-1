# Camunda 8 BPMN + DMN Model Files

These four model files are included unchanged from the latest supplied package for Camunda Modeler 5.49.0.

## Files

- `logistics/logistics_exception_management.bpmn` — Logistics and shipment exception process.
- `logistics/logistics_booking_decision.dmn` — Logistics booking decision.
- `loan/loan_origination_approval.bpmn` — Loan origination and approval process.
- `loan/loan_risk_decision.dmn` — Loan risk decision.

## Open in Modeler

Open each file in Camunda Modeler 5.49.0 using the Camunda 8/Zeebe format. Review the diagram, decision table, and **Problems** panel. If a file still reports parsing errors, do not assume it is valid merely because it is included here; resolve the errors before submission.

## Decision inputs and outputs

### LogisticsBookingDecision

Inputs: `addressValid` (boolean), `weightKg` (number), `serviceLevel` (string such as `EXPRESS` or `STANDARD`), `remoteArea` (boolean).

Outputs: `bookingValid`, `surcharge`, `decisionMessage`.

### LoanRiskDecision

Inputs: `creditScore` (number), `debtToIncome` (number from 0 to 1), `fraudFlag` (boolean), `requestedAmount` (number).

Outputs: `riskRoute` (`AUTO_APPROVE`, `MANUAL_REVIEW`, or `REJECT`), `maxApprovedAmount`, `reason`.

## Runtime requirements

These are process/decision models, not a fully deployed application. End-to-end execution may require:

1. Deploying the BPMN processes and DMN decisions to a Camunda 8 runtime.
2. Implementing workers for service-task job types.
3. Supplying process variables used by DMN decisions and gateway conditions.
4. Configuring message subscriptions and correlation keys where applicable.
5. Testing happy paths and alternate/failure paths in the target runtime.

## Validation status

Successful opening in Camunda Modeler 5.49.0, deployment, and runtime execution have **not** been independently confirmed. Validate the files in the target environment before treating them as functional or submitting them as verified models.

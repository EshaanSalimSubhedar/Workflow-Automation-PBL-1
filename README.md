# BPMN 2.0 and DMN Workflow Modeling Project

**Assignments:**
- **Assignment 2 — Logistics & Shipment Exception Management**
- **Assignment 3 — Loan Origination & Approval System**

**Modeling environment:** Camunda Modeler 5.49.0, targeting Camunda 8 / Zeebe.

> **Validation notice:** This repository includes the latest supplied BPMN and DMN files, supporting design documents, failure-path registers, a modeling checklist, a presentation, and the assignment brief. XML-level checks have been performed during preparation, but successful opening of every file in the target Modeler, deployment to a Camunda 8 runtime, and end-to-end execution have not been independently confirmed. Do not describe the models as fully functional or production-ready until those checks have been completed.

## 1. Project purpose

This academic project uses Business Process Model and Notation (BPMN) to describe workflow behavior and Decision Model and Notation (DMN) to represent decision logic in tables. The selected scenarios focus on two business processes that need both a normal route and explicit handling of exceptions:

1. **Logistics and shipment exception management:** represent shipment booking and progression, along with relevant tracking and shipment exceptions.
2. **Loan origination and approval:** represent the flow of a loan application through checks, risk routing, approval or rejection, and subsequent steps represented in the model.

The repository is intended to make the models, their design rationale, failure scenarios, and evaluation material easy to review together. It is a modeling assignment, not a complete logistics platform or lending application.

## 2. Assignment objectives

The two assignments are documented with the following objectives:

- Show a clear **happy path** from process start to a meaningful end state.
- Use BPMN task types to distinguish work that is performed by a person, a service, or an incoming message where applicable.
- Use gateways to make branching and routing conditions explicit.
- Identify failure cases, alternate paths, timeouts, and recovery behavior where represented in the design.
- Use appropriate BPMN events and sequence flows while keeping the diagram readable.
- Use DMN tables to express decision rules separately from the process flow.
- Document design choices and review the model against the assignment rubric before submission.

The assignment brief and its marking rubric are included in `reference/BPMN_Project_Assignments.pdf`. The rubric covers happy path, task types, gateways, failure identification, solutions, and notation/readability. Use the original brief as the final authority for submission requirements.

## 3. Repository map

```text
BPMN_Project_Repo_Complete/
├── README.md
├── BPMN_DMN_Files/
│   ├── README.md
│   ├── logistics/
│   │   ├── logistics_exception_management.bpmn
│   │   └── logistics_booking_decision.dmn
│   └── loan/
│       ├── loan_origination_approval.bpmn
│       └── loan_risk_decision.dmn
├── assignment-2-logistics/
│   ├── process-design.md
│   └── failure-path-register.csv
├── assignment-3-loan/
│   ├── process-design.md
│   └── failure-path-register.csv
├── docs/
│   └── modeling-checklist.md
├── presentation/
│   └── BPMN_Project_Presentation.pptx
└── reference/
    └── BPMN_Project_Assignments.pdf
```

### What each folder contains

| Path | Purpose |
|---|---|
| `BPMN_DMN_Files/` | The four supplied model files intended to be opened in Camunda Modeler. |
| `assignment-2-logistics/process-design.md` | Written overview of the logistics process and its modeling intent. |
| `assignment-2-logistics/failure-path-register.csv` | Tabular register of logistics failure/exception scenarios and their proposed handling. |
| `assignment-3-loan/process-design.md` | Written overview of the loan process and its modeling intent. |
| `assignment-3-loan/failure-path-register.csv` | Tabular register of loan failure/exception scenarios and their proposed handling. |
| `docs/modeling-checklist.md` | Review checklist for model logic, notation, and readability. |
| `presentation/BPMN_Project_Presentation.pptx` | Editable slide deck for explaining the project. |
| `reference/BPMN_Project_Assignments.pdf` | Original assignment brief and rubric supplied for this project. |

## 4. Assignment 2 — Logistics & Shipment Exception Management

### Business problem

A shipment workflow must coordinate booking, validation, movement, tracking, and delivery while accounting for exceptions that can prevent the expected progression. A diagram should make it possible to identify the normal route and understand what happens when required information or a shipment milestone is missing or delayed.

### Modeling focus

Refer to the actual process and failure register for the exact tasks and paths represented. The documented design covers shipment booking and validation, pickup and transit, delivery/proof-of-delivery, closure, and exception scenarios such as missing scans, customs delays, and lost shipments where specified.

The companion DMN file, `logistics_booking_decision.dmn`, is intended to express booking-related decisions separately from the process flow. Its documented inputs are:

- `addressValid` — boolean
- `weightKg` — number
- `serviceLevel` — string, for example `EXPRESS` or `STANDARD`
- `remoteArea` — boolean

Its documented outputs are `bookingValid`, `surcharge`, and `decisionMessage`. Verify these names and all rule conditions against the DMN decision table in Modeler before relying on them at runtime.

### Files for this assignment

- BPMN: `BPMN_DMN_Files/logistics/logistics_exception_management.bpmn`
- DMN: `BPMN_DMN_Files/logistics/logistics_booking_decision.dmn`
- Design notes: `assignment-2-logistics/process-design.md`
- Failure register: `assignment-2-logistics/failure-path-register.csv`

### Review questions

- Is the normal shipment path easy to trace from start to end?
- Are the booking and validation outcomes explicit?
- Are timers, missing-scan handling, customs delays, and loss scenarios represented as modeled rather than only described in documentation?
- Are exception paths connected to meaningful follow-up or end states?
- Do the DMN rules and BPMN process use compatible input and output variable names?

## 5. Assignment 3 — Loan Origination & Approval System

### Business problem

A loan application moves through information collection and checks before an outcome can be reached. The workflow needs to distinguish ordinary progression from incomplete information, risk-related routing, withdrawal, or other exceptions represented by the design.

### Modeling focus

Refer to the BPMN model and written design for the exact task sequence. The documented design discusses application intake, document validation, KYC and credit checks, risk routing, underwriting, offer acceptance, and disbursement. These descriptions explain the intended process; they do not imply that external identity, credit bureau, fraud, or banking integrations have been implemented.

The companion DMN file, `loan_risk_decision.dmn`, is intended to express loan-risk routing. Its documented inputs are:

- `creditScore` — number
- `debtToIncome` — number from 0 to 1
- `fraudFlag` — boolean
- `requestedAmount` — number

Its documented outputs are `riskRoute` (`AUTO_APPROVE`, `MANUAL_REVIEW`, or `REJECT`), `maxApprovedAmount`, and `reason`. Confirm the actual rules, data types, and output values in the DMN file before using these as executable business policy.

### Files for this assignment

- BPMN: `BPMN_DMN_Files/loan/loan_origination_approval.bpmn`
- DMN: `BPMN_DMN_Files/loan/loan_risk_decision.dmn`
- Design notes: `assignment-3-loan/process-design.md`
- Failure register: `assignment-3-loan/failure-path-register.csv`

### Review questions

- Can a reviewer follow the application from intake to its final outcome?
- Are the gateway conditions clear and based on defined process variables?
- Are missing documents, checks that fail, withdrawal, timeouts, and other exceptions represented consistently with the documentation?
- Are rejection, manual review, approval, and disbursement outcomes distinct where applicable?
- Does the BPMN model reference the intended DMN decision and map its results into variables used by the process?

## 6. BPMN and DMN: how they fit together

**BPMN** describes the process flow: activities, events, gateways, and the sequence in which work proceeds. **DMN** describes decision logic using inputs, rules, and outputs. Separating decision logic from process routing can make the rules easier to inspect and maintain. In Camunda, a decision table can be evaluated by a process when the BPMN model is configured to call that decision and supplies the required inputs.

Official references:
- [Camunda 8 — BPMN, DMN, and FEEL](https://docs.camunda.io/docs/components/concepts/bpmn-dmn-feel/)
- [Camunda 8 — DMN in Modeler](https://docs.camunda.io/docs/components/modeler/dmn/)
- [Camunda 8 — Decision tables](https://docs.camunda.io/docs/8.8/components/modeler/dmn/decision-table/)

## 7. Open the models in Camunda Modeler

The target environment reported for this project is **Camunda Modeler 5.49.0** in a Camunda 8 getting-started bundle. Follow these steps:

1. Download or clone the repository and extract it if it is a ZIP.
2. Open Camunda Modeler.
3. Open each `.bpmn` and `.dmn` file from `BPMN_DMN_Files/` individually.
4. Inspect the diagram or decision requirements diagram and the **Problems** panel.
5. For a DMN file, inspect the decision requirements diagram and open the decision table itself.
6. If the file reports a parsing error, preserve the complete error message and fix the file before treating it as validated.
7. Review diagram readability: labels, sequence-flow direction, crossings, gateways, boundary events, and end states.
8. Use `docs/modeling-checklist.md` to record the outcome of the review.

The latest supplied model files are included as-is. Their inclusion in this repository is not proof that they open cleanly in every installation.

## 8. Validation and runtime requirements

Validation has several distinct levels. Record each separately rather than treating one as proof of another.

| Validation level | What it establishes | Current status |
|---|---|---|
| XML well-formedness | The XML is syntactically well-formed. | XML checks were performed during preparation. |
| Modeler compatibility | Camunda Modeler opens the file without parsing errors and renders the diagram/table. | Not independently confirmed in the user's Modeler installation. |
| Model review | The paths, gateways, events, rule conditions, and diagram layout are correct. | Requires manual review using the checklist. |
| Deployment | The target Camunda 8 runtime accepts the BPMN and DMN definitions. | Not confirmed. |
| Execution | Test instances follow expected paths and produce expected decisions. | Not confirmed. |

Before end-to-end execution, the target environment may require:

- Deploying the BPMN and DMN models to the same appropriate Camunda 8 environment.
- Implementing and running job workers for service tasks that require external work.
- Supplying all process variables used by conditions and decision tables with the expected types.
- Configuring message names, subscriptions, correlation keys, and message payloads for message events where used.
- Checking timer durations and testing both timer-triggered and normal paths.
- Verifying BPMN decision invocation settings, decision IDs, result-variable mappings, and DMN input names.
- Testing successful, rejected, missing-data, timeout, and exception scenarios as applicable.

Do not state that a scenario works until a test demonstrates it in the target runtime.

## 9. Evaluation and marking rubric

Use the original assignment PDF as the authoritative source. The rubric represented in the project materials has these areas:

| Area | Marks | What to demonstrate |
|---|---:|---|
| Happy path | 4 | A clear, complete normal process path. |
| Task types | 3 | Appropriate task types and a clear explanation of their purpose. |
| Gateways | 3 | Correct and understandable decision/branching logic. |
| Failure identification | 4 | Relevant failure scenarios are identified. |
| Solutions | 4 | Alternate paths and recovery/handling behavior address those failures. |
| Notation/readability | 2 | Correct, readable BPMN notation and a clean layout. |
| **Total** | **20** | **20 marks** |

For each assignment, cross-check the BPMN against the process design and failure-path register. The presentation should explain not just which BPMN symbols are present, but what each important branch means for the business process.

## 10. Suggested submission review

Before submission:

- [ ] Read the original assignment brief and confirm the selected assignments meet the instructor's requirements.
- [ ] Open both BPMN files in the intended Camunda Modeler version.
- [ ] Open both DMN files and inspect the decision tables.
- [ ] Resolve all parsing errors and investigate warnings that affect model correctness.
- [ ] Confirm each BPMN/DMN ID is unique where required and decision references match.
- [ ] Check the happy path and each documented failure path against the diagram.
- [ ] Check that gateway conditions use defined variables and correct data types.
- [ ] Check diagram readability and reduce crossing or overlapping sequence flows.
- [ ] If runtime functionality is required, deploy and test representative normal and exception scenarios.
- [ ] Update the validation status based on actual test evidence; do not claim unperformed tests.
- [ ] Review the presentation and speaker explanation against the final files.
- [ ] Ensure no secrets or unrelated personal files are committed to a public repository.

## 11. Presentation

The editable slide deck is located at `presentation/BPMN_Project_Presentation.pptx`. Use it as a supporting explanation of the two workflows, BPMN concepts, DMN decision logic, failure scenarios, and validation status. If the model files change after the slides are created, update the presentation so screenshots and claims match the submitted models.

## 12. Limitations and disclaimer

This repository is for academic workflow modeling and demonstration. It is not production shipping software, a loan underwriting service, a credit scoring policy, or a substitute for regulatory, security, financial, or operational review. Any risk thresholds or example decision rules must be reviewed by the relevant instructor or domain owner before being treated as real policy.

The README and supporting documentation describe the intended design and the contents of this repository. They do not certify that the BPMN/DMN files are deployment-ready or that integrations and runtime workers exist.

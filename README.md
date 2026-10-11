# BPMN 2.0 and DMN Workflow Modeling Project

**Project type:** Academic workflow modeling assignment  
**Platform:** Camunda 8 / Camunda Modeler 5.49.0  
**Selected assignments:**
1. Assignment 2 — Logistics & Shipment Exception Management
2. Assignment 3 — Loan Origination & Approval System

## Project Overview

This repository presents two business-process modeling scenarios using Business Process Model and Notation (BPMN 2.0) and Decision Model and Notation (DMN). The aim is to demonstrate how a business process can be represented through activities, events, gateways, sequence flows, and exception paths, while keeping decision rules in separate decision tables where appropriate.

The logistics assignment models a shipment workflow and its handling of exceptions such as missing tracking scans, customs delays, and shipment loss where represented in the model. The loan assignment models the progression of a loan application through validation, risk routing, approval or rejection, and subsequent steps where represented in the model.

The repository includes the four model files, written process-design documents, failure-path registers, a modeling checklist, the assignment brief, and a presentation.

## Project Objectives

- Model the normal process flow for each selected business scenario.
- Use BPMN events, tasks, gateways, and sequence flows to communicate process behavior.
- Identify relevant failure scenarios and document their intended handling.
- Represent decision logic in DMN decision tables, separate from the overall process flow.
- Provide supporting documentation that explains the design and supports review against the assignment rubric.
- Organize the models and documentation in a single repository for assessment and future refinement.

## Repository Structure

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

## Assignment 2 — Logistics & Shipment Exception Management

### Purpose

This assignment represents a shipment-related process with a normal progression from booking and validation through shipment handling and completion. It also considers exception situations that can interrupt the expected flow.

### Modeling focus

The BPMN model is intended to communicate the shipment workflow, the responsibilities and activities involved, and the handling of relevant exceptions. The accompanying DMN model separates booking-related decision logic from the process diagram.

### Included files

- `BPMN_DMN_Files/logistics/logistics_exception_management.bpmn` — BPMN process model.
- `BPMN_DMN_Files/logistics/logistics_booking_decision.dmn` — DMN booking decision model.
- `assignment-2-logistics/process-design.md` — process design notes.
- `assignment-2-logistics/failure-path-register.csv` — register of identified failure and exception scenarios.

## Assignment 3 — Loan Origination & Approval System

### Purpose

This assignment represents a loan application workflow in which application information is checked and a risk-related decision supports subsequent routing. The model distinguishes the intended normal flow from alternate outcomes and exceptions represented in the process.

### Modeling focus

The BPMN model communicates the workflow and its branches. The companion DMN model is intended to express loan-risk routing rules separately from the process flow. External credit, identity, fraud, or banking integrations should not be assumed to be implemented merely because their activities or scenarios appear in the model or documentation.

### Included files

- `BPMN_DMN_Files/loan/loan_origination_approval.bpmn` — BPMN process model.
- `BPMN_DMN_Files/loan/loan_risk_decision.dmn` — DMN risk decision model.
- `assignment-3-loan/process-design.md` — process design notes.
- `assignment-3-loan/failure-path-register.csv` — register of identified failure and exception scenarios.

## BPMN and DMN

BPMN is used to represent process behavior, including tasks, events, gateways, and the flow between activities. DMN is used to express decision logic in a decision table. Keeping these concerns separate can make a process easier to read and decision rules easier to review. For executable integration, the BPMN process must be configured to invoke the relevant DMN decision and pass the expected input variables.

## Supporting Materials

- `docs/modeling-checklist.md` provides a structured review checklist for the models.
- `presentation/BPMN_Project_Presentation.pptx` contains the project presentation.
- `reference/BPMN_Project_Assignments.pdf` contains the supplied assignment brief and rubric.

## Assessment Alignment

The project materials are organized to support review of the following rubric areas described in the assignment brief:

| Assessment area | Marks | Evidence to review |
|---|---:|---|
| Happy path | 4 | Normal route through each BPMN process. |
| Task types | 3 | Use and purpose of task types in the models. |
| Gateways | 3 | Branching and routing logic. |
| Failure identification | 4 | Failure scenarios in the process models and registers. |
| Solutions | 4 | Intended handling, alternate routes, and recovery paths. |
| Notation/readability | 2 | BPMN notation and diagram clarity. |
| **Total** | **20** | **Both selected assignments** |

The original assignment brief remains the authoritative source for assessment requirements.

## Validation Status and Scope

The model files have been subject to XML-level checks during preparation. This is not equivalent to confirming that every file opens without errors in Camunda Modeler, that the definitions deploy successfully to a Camunda 8 runtime, or that process instances execute correctly.

At the time of packaging, the following remain unconfirmed:

- Successful opening and rendering of all four files in the target Camunda Modeler installation.
- Successful deployment of the BPMN and DMN definitions to the target Camunda 8 runtime.
- End-to-end execution of normal and exception paths.
- Runtime integration with service-task workers or external systems.

Accordingly, the repository should be understood as an academic workflow-modeling submission and supporting documentation, not as a verified production implementation. Any future validation claims should be based on observed Modeler, deployment, and execution results.

## References

- [Camunda 8 documentation: BPMN, DMN, and FEEL](https://docs.camunda.io/docs/components/concepts/bpmn-dmn-feel/)
- [Camunda 8 documentation: DMN in Modeler](https://docs.camunda.io/docs/components/modeler/dmn/)
- Original assignment brief included at `reference/BPMN_Project_Assignments.pdf`.

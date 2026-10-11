# BPMN 2.0 Project Repository — Logistics and Loan Origination

This repository contains assignment documentation, the presentation, reference assignment brief, and the latest supplied BPMN/DMN model files for **Assignment 2: Logistics & Shipment Exception Management** and **Assignment 3: Loan Origination & Approval System**.

## Repository contents

```text
BPMN_Project_Repo_Complete/
├── README.md
├── assignment-2-logistics/
│   ├── process-design.md
│   └── failure-path-register.csv
├── assignment-3-loan/
│   ├── process-design.md
│   └── failure-path-register.csv
├── docs/modeling-checklist.md
├── presentation/BPMN_Project_Presentation.pptx
├── BPMN_DMN_Files/
│   ├── README.md
│   ├── logistics/
│   │   ├── logistics_exception_management.bpmn
│   │   └── logistics_booking_decision.dmn
│   └── loan/
│       ├── loan_origination_approval.bpmn
│       └── loan_risk_decision.dmn
└── reference/BPMN_Project_Assignments.pdf
```

## Assignment overview

### Assignment 2 — Logistics & Shipment Exception Management

The process design documents shipment booking, validation, pickup, transit, delivery, proof of delivery, closure, and exception handling. See `assignment-2-logistics/process-design.md` and its failure-path register.

### Assignment 3 — Loan Origination & Approval System

The process design documents application intake, document validation, KYC and credit checks, risk routing, underwriting, offer acceptance, and disbursement. See `assignment-3-loan/process-design.md` and its failure-path register.

## Opening the model files

Use Camunda Modeler 5.49.0 with the Camunda 8/Zeebe format:

1. Extract this repository to a local folder.
2. Open each `.bpmn` and `.dmn` file under `BPMN_DMN_Files/`.
3. Inspect the Modeler **Problems** panel and visually review each diagram and decision table.
4. Follow `docs/modeling-checklist.md` before submitting.

The four BPMN/DMN files are copied unchanged from `BPMN_DMN_Project_Files_Camunda8_Fixed_v3.zip`. This repository does not claim that they have been successfully opened in your exact Modeler installation, deployed, or executed end to end.

## Runtime status and requirements

**Runtime execution is not verified.** Opening a file or parsing its XML is not proof that a process or decision is functional. Full execution may require:

- Deploying the BPMN processes and DMN decisions to a Camunda 8 runtime.
- Implementing workers for service-task job types.
- Supplying the process variables expected by gateways and DMN inputs.
- Configuring message subscriptions and correlation keys where message events are used.
- Testing normal paths, timers, retries, and exception paths.

See `BPMN_DMN_Files/README.md` for the DMN input/output names and runtime notes.

## Evaluation alignment

The documents and presentation address the assignment rubric: happy path, task types, gateways, failure identification, failure solutions, and notation/readability. Use the failure-path registers to cross-check the BPMN diagrams and the modeling checklist to review layout and routing.

## Reference material

`reference/BPMN_Project_Assignments.pdf` contains the assignment brief and rubric used to prepare the documentation.

## Disclaimer

This is an academic workflow-design project, not production shipping, lending, banking, legal, or compliance software.

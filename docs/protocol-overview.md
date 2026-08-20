# R.E.T.N.A.™ Protocol Overview

**Public Technical Review Artifact — Draft v0.1**

R.E.T.N.A.™ — **Real-Time Execution Trust and Notarization Architecture** — is a model-agnostic and agent-agnostic Decision Governance Protocol developed by **Value Intelligence Solutions Inc. (ValueIO)**.

The Protocol introduces an enforceable governance layer between **Decision Construction** and **Decision Execution** for AI, agentic, autonomous, and model-driven systems capable of producing consequential digital, financial, operational, legal, security, or physical effects.

> **Governance Must Precede Execution.**

> **This Protocol governs decisions, not models.**

This public overview describes the protocol-level architecture, governance flow, principal artifacts, and conformance direction without disclosing proprietary production implementation logic.

---

## 1. Purpose

Modern AI systems increasingly progress from recommendation to action.

A model or agent may:

- propose a transaction;
- modify a system record;
- invoke a tool;
- control a device;
- allocate a resource;
- initiate a workflow;
- trigger an external service;
- produce a physical or operational state change.

R.E.T.N.A. addresses the point at which a proposed action becomes a **governed commitment to act**.

The Protocol does not treat model output, agent intent, workflow routing, or tool invocation as sufficient authorization for consequential execution.

Instead, governed execution is conditioned on explicit evaluation at a **Governance Boundary**.

---

## 2. Architectural Principle

The core architectural separation is:

```text
Decision Construction
        ↓
Candidate Decision
        ↓
Governance Boundary
        ↓
Governance Outcome
        ↓
Decision Receipt
        ↓
Governed State Transition
        ↓
Decision Execution
```

This separation establishes an explicit distinction between:

- **what a system proposes to do**; and
- **what the system is authorized to do**.

R.E.T.N.A. therefore treats output generation and execution authorization as separate protocol concerns.

---

## 3. The Governance Boundary

The **Governance Boundary** is the enforceable transition point between a candidate decision and consequential execution.

At this boundary, the proposed action may be evaluated against protocol-relevant conditions including:

- actor identity and role;
- execution authority;
- decision classification;
- applicable policies and constraints;
- evidence references;
- evidence admissibility;
- decision formation requirements;
- risk context;
- state-transition eligibility;
- persistence and audit requirements.

A candidate decision does not acquire execution authority merely because it has been produced, routed, forwarded, or accepted by another component.

**Transport is not authorization.**

**Forwarding is not a governed state transition.**

---

## 4. Governance Chain

A governed decision may be understood through the following protocol chain:

```text
Authority
    ↓
Decision Formation
    ↓
Evidence
    ↓
Admissibility
    ↓
Governance Boundary
    ↓
Governance Outcome
    ↓
Decision Receipt
    ↓
Governed State Transition
    ↓
Execution Consequence
```

Each stage addresses a different governance question.

### Authority

Does the actor or system possess valid authority to propose, authorize, or execute the action?

### Decision Formation

Was the candidate decision formed in a manner that satisfies the requirements applicable to the governed action?

### Evidence

What evidence supports the decision?

### Admissibility

Is the referenced evidence acceptable for the governed decision under the applicable policy and protocol context?

### Governance Outcome

What explicit authorization state results from governance evaluation?

### Decision Receipt

What durable artifact records the governed determination?

### Governed State Transition

What state change, if any, is authorized to occur as a consequence of the governed decision?

---

## 5. Canonical Governance Outcomes

R.E.T.N.A. defines five baseline governance outcomes:

| Outcome | Protocol Meaning |
|---|---|
| **ALLOW** | The governed decision is authorized for execution. |
| **DENY** | Execution is prohibited. |
| **ESCALATE** | Higher authority or human review is required. |
| **DEFER** | Execution is postponed pending evidence, time, or another required condition. |
| **DEGRADE** | Execution may proceed only under reduced authority, scope, capability, or autonomy. |

Governance outcomes are intended to be:

- explicit;
- machine-readable;
- reproducible;
- auditable;
- interoperable;
- accompanied by structured Reason Codes.

Undefined or ambiguous authorization states are not intended to substitute for a canonical governance outcome.

---

## 6. Decision Classification

R.E.T.N.A. treats decision classification as an input to governance evaluation.

The current protocol model uses three principal dimensions:

```text
Risk Class
    +
Action Type
    +
Decision Mode
    =
Decision Classification
```

Classification provides structured context for evaluating the authority, policy, evidence, timing, and conformance requirements applicable to a governed decision.

The assigned classification is intended to remain stable during a single governance evaluation and to be represented within the corresponding Decision Receipt.

---

## 7. Protocol Actors

R.E.T.N.A. distinguishes roles so that decision construction, governance, and execution do not collapse into a single implicit authority surface.

Protocol roles may include:

### Producer

Creates or proposes the candidate decision.

### Governor

Evaluates the candidate decision against applicable governance requirements and determines the governance outcome.

### Executor

Performs an authorized state transition or action.

### Evidence Source

Provides evidence referenced during governance evaluation.

### Policy Authority

Provides or governs applicable policy and constraint material.

### Auditor / Validator

Examines Decision Receipts, protocol artifacts, or conformance behavior without requiring access to proprietary model internals.

A single implementation may map these roles to different services, agents, processes, or trust domains, but the protocol preserves their logical distinction.

---

## 8. Decision Receipts

The **Decision Receipt** is the primary governance artifact of R.E.T.N.A.

A Decision Receipt provides structured evidence of the governed determination.

A conforming receipt may represent information concerning:

- protocol version;
- receipt identity;
- decision identity;
- actor and role information;
- authority context;
- decision classification;
- evidence references;
- policy references;
- governance outcome;
- Reason Codes;
- state-transition status;
- integrity metadata;
- trace and audit references;
- timestamps and persistence information.

Conceptually:

```text
WHO
proposed / governed / executed

        +

WHAT
action or state transition was proposed

        +

UNDER WHAT AUTHORITY

        +

BASED ON WHICH EVIDENCE

        +

AGAINST WHICH POLICY / CONSTRAINTS

        +

WITH WHAT OUTCOME

        +

WITH WHAT INTEGRITY / PERSISTENCE EVIDENCE

        =

DECISION RECEIPT
```

The Decision Receipt is intended to support verification of the governance event without requiring disclosure of proprietary model reasoning, private scoring formulas, or implementation-specific internal logic.

---

## 9. Reason Codes

Canonical **Reason Codes** provide structured explanations for governance outcomes and protocol-relevant state-transition determinations.

Reason Codes are intended to support:

- machine-readable interpretation;
- audit reconstruction;
- cross-system observability;
- conformance testing;
- deterministic failure handling;
- independent validation.

Reason Codes communicate why a governance result occurred without requiring exposure of proprietary internal reasoning.

A dedicated public Reason Code artifact is planned for this repository.

---

## 10. Governed State Transitions

R.E.T.N.A. distinguishes **message or output transport** from **governed consequence**.

A message may be routed.

An output may be forwarded.

A tool call may be constructed.

None of those events, by themselves, establish that a consequential state transition is authorized.

A governed state transition represents the point at which a valid governance determination is permitted to produce an external, operational, legal, financial, physical, security, or other material system consequence.

The protocol therefore treats state-transition integrity as distinct from transport integrity.

---

## 11. Fail-Closed Governance

For governed decision classes, unresolved governance requirements must not silently become authorization.

Conditions that may prevent governed execution include:

- unavailable or unverifiable authority;
- failed authentication or authorization;
- incomplete decision formation;
- inadmissible or insufficient evidence;
- policy violation;
- unresolved state-transition requirements;
- required integrity failure;
- Decision Receipt persistence failure;
- invalid governance result.

The intended default is:

```text
No valid governance determination
            ↓
No governed authority to execute
```

Availability and authority are separate concerns.

---

## 12. Interoperability Model

R.E.T.N.A. is intended to be implementable across heterogeneous systems.

The Protocol does not require:

- a specific foundation model;
- a specific agent framework;
- a specific programming language;
- a specific database;
- a specific cloud provider;
- a specific orchestration platform;
- a specific hardware environment.

Protocol interoperability centers on shared governance semantics and observable artifacts, including:

- canonical governance outcomes;
- Decision Receipt fields;
- Reason Codes;
- declared protocol versions;
- integrity metadata;
- conformance behavior.

A third-party validator should not require access to proprietary model internals merely to interpret the protocol-level result of a governed decision.

---

## 13. Conformance Direction

R.E.T.N.A. is intended to support behavior-based conformance.

Conformance is therefore concerned with observable protocol guarantees such as:

- Governance Boundary integrity;
- mandatory Decision Receipt emission;
- receipt completeness;
- required evidence and policy references;
- canonical outcome behavior;
- deterministic handling of equivalent governance conditions;
- fail-closed negative cases;
- integrity and persistence behavior;
- audit replay;
- independent validation.

The long-term objective is for governance claims to be **demonstrable through artifacts and tests**, rather than accepted as unverified assertions.

No formal third-party certification authority is claimed by the v0.1 public repository.

---

## 14. Relationship to Governed Autonomous Intelligence

R.E.T.N.A. forms the governance layer within ValueIO's broader **Governed Autonomous Intelligence (GAI)** architecture.

The architectural model separates:

```text
Layer 1 — Physical State
Deterministic Ground Truth
        ↓
Layer 2 — Orchestration
Decision Formation
        ↓
Layer 3 — Governance
Execution Authorization
        ↓
Governed Execution
```

Within ValueIO's reference architecture:

- **Smart-I-Shelf™** represents deterministic physical-state validation;
- **HomeSphere AI™** represents distributed multi-agent orchestration;
- **R.E.T.N.A.™** represents Decision Governance Infrastructure.

R.E.T.N.A. is intended to remain architecturally independent from these specific reference components and applicable across other AI and autonomous-system environments.

---

## 15. What R.E.T.N.A. Does Not Standardize

The Protocol does not seek to standardize:

- model architecture;
- model weights;
- prompts;
- chain-of-thought or private model reasoning;
- agent planning algorithms;
- proprietary scoring formulas;
- internal decision trees;
- application-specific business logic;
- vendor-specific orchestration internals.

R.E.T.N.A. governs the **authorization and accountability surface around consequential decisions**.

---

## 16. Public vs. Controlled Technical Surface

This document is part of the **public technical review surface**.

The public repository is intended to expose sufficient protocol structure to support:

- technical evaluation;
- research;
- interoperability discussion;
- conformance review;
- investor and enterprise diligence;
- legal and regulatory analysis;
- public understanding of the protocol architecture.

The complete **R.E.T.N.A. Protocol Specification — Institutional Edition**, **Governed Autonomous Intelligence Whitepaper — Institutional Edition**, and selected supporting materials remain available through controlled review.

[Request R.E.T.N.A. Controlled Review Access](https://valueintelligence.io/retna-protocol/#controlled-review-access)

Public availability of this overview does not grant unrestricted implementation, certification, commercialization, sublicensing, or trademark rights.

See [`NOTICE.md`](../NOTICE.md) for the repository's public disclosure and rights boundary.

---

## 17. Related Repository Artifacts

Current root-level repository documents:

- [`README.md`](../README.md) — public introduction and repository front door;
- [`STATUS.md`](../STATUS.md) — current protocol status and explicit non-claims;
- [`NOTICE.md`](../NOTICE.md) — public disclosure, rights, and controlled-review boundary.

Planned technical artifacts include:

```text
docs/
├── normative-language.md
├── governance-boundary.md
├── system-invariants.md
├── decision-receipts.md
├── reason-codes.md
├── conformance-model.md
├── interoperability.md
└── controlled-review.md

examples/
└── sample-decision-receipt.json

conformance/
└── README.md
```

---

## 18. Protocol Status

This public overview reflects the **R.E.T.N.A. v0.1 Draft Specification** and may evolve as implementation validation, conformance testing, interoperability work, legal review, security review, and external technical feedback continue.

Breaking semantic changes should be reflected through explicit version treatment rather than silent modification.

For current protocol status, see [`STATUS.md`](../STATUS.md).

---

## 19. Stewardship

R.E.T.N.A. is developed and stewarded by:

**Value Intelligence Solutions Inc.**

The long-term objective is to advance Decision Governance Infrastructure as a vendor-neutral, enforceable, testable, and interoperable layer for autonomous and model-driven systems.

---

© 2026 Value Intelligence Solutions Inc. All rights reserved.

**R.E.T.N.A.™ — Trademark Pending**  
**HomeSphere AI™ — Trademark Pending**  
**Smart-I-Shelf™ — Patent Pending / Trademark Pending**

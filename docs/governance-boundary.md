# R.E.T.N.A.™ Governance Boundary

**Public Technical Review Artifact — Draft v0.1**

The **Governance Boundary** is the mandatory interface between **Decision Construction** and **Decision Execution** in the R.E.T.N.A.™ Decision Governance Protocol.

Its purpose is to ensure that a candidate decision does not become a consequential action merely because a model, agent, workflow, tool, or orchestration system produced, routed, forwarded, persisted, or acknowledged it.

> **Governance Must Precede Execution.**

> **Output is not authorization.**

> **Transport is not governed consequence.**

This public artifact explains the protocol-level Governance Boundary, the conditions it resolves, the artifacts it produces, and the observable behaviors that support external technical review and conformance analysis.

The controlled **R.E.T.N.A. Protocol Specification — Institutional Edition** remains the authoritative source for v0.1 normative requirements.

---

## 1. Boundary Definition

R.E.T.N.A. defines the Governance Boundary as the mandatory control interface at which a candidate decision is evaluated before consequential execution.

Conceptually:

```text
DECISION CONSTRUCTION
        │
        │ Candidate Decision
        ▼
┌──────────────────────────────────────┐
│          GOVERNANCE BOUNDARY         │
│                                      │
│  Payload / Decision Classification   │
│  Authority + Edge Policy             │
│  Formation Integrity                 │
│  Evidence + Admissibility            │
│  Policy + Constraint Evaluation      │
│  Governance Outcome                  │
│  Governed State Transition           │
└──────────────────┬───────────────────┘
                   │
                   ▼
            Decision Receipt
                   │
                   ▼
          Receipt Persistence
                   │
                   ▼
             EXECUTION
                   │
                   ▼
        Execution Consequence
```

The Governance Boundary is not an observability hook placed after execution.

It is an **authorization boundary positioned before governed consequence**.

---

## 2. Core Boundary Requirement

For a governed decision class, execution authority is not implied by successful decision construction.

A system implementing the R.E.T.N.A. governance model must preserve the separation:

```text
Decision Construction ≠ Decision Execution
```

The protocol's v0.1 design requires governed actions capable of altering external state to pass through governance evaluation and receive an explicit authorization outcome before execution.

The execution interface therefore acts as an enforcement point, not merely as a logging surface.

---

## 3. What Counts as Governed Consequence

The Governance Boundary applies where a decision is capable of producing a materially consequential effect.

Examples include:

- digital state change;
- financial commitment;
- operational action;
- physical actuation;
- security-relevant action;
- legal or compliance-relevant consequence;
- environmental or infrastructure consequence;
- other material system state transition.

The protocol distinguishes such consequence from informational output.

A model may generate text.

An agent may construct a proposal.

A router may forward a message.

An orchestrator may complete a workflow.

Those events do not independently establish authority for governed consequence.

---

## 4. Transport Is Not Authorization

R.E.T.N.A. explicitly separates transport semantics from governance semantics.

The following events do **not** independently authorize governed execution:

```text
Successful routing
Successful forwarding
Message delivery
Acknowledgement
Orchestration completion
Output generation
Tool-call construction
Persistence alone
Transport success
```

The relevant distinction is:

```text
Transport Success
      ≠
Governed Execution Authorization
```

A governed action becomes eligible for consequential execution only after the required governance conditions have been resolved.

This prevents infrastructure success signals from being mistaken for authorization signals.

---

## 5. Boundary Inputs

The Governance Boundary evaluates a governed decision using protocol-relevant context.

Depending on the applicable decision class, Payload Kind, policy, risk posture, and compliance profile, that context may include:

### 5.1 Candidate Decision

The proposed commitment to act.

### 5.2 Payload Kind

The semantic category of the decision request used to route governance behavior and applicable policy evaluation.

### 5.3 Decision Classification

The decision's governance classification, including protocol-defined dimensions such as:

```text
Risk Class
Action Type
Decision Mode
Payload Kind
```

### 5.4 Authority Context

Information sufficient to determine whether the actor or system asserting authority possesses valid authority for the proposed action.

### 5.5 Edge Policy

Governance rules defining which actors or systems are authorized to issue or execute specific categories of decisions.

### 5.6 Formation Context

Governance-relevant information describing how the candidate decision was shaped before admissibility evaluation and Governance Boundary enforcement.

### 5.7 Evidence

Inputs used in decision construction or policy evaluation, which may include:

- state deltas;
- sensor signals;
- user commands;
- retrieved documents;
- derived signals;
- other referenced Evidence Artifacts.

### 5.8 Admissibility

The explicit determination of whether the candidate decision satisfies the governance conditions required for consequential execution.

### 5.9 Policy and Constraints

Applicable Policy Bundles, policy constraints, risk conditions, execution restrictions, and other governance rules.

---

## 6. Boundary Evaluation Chain

The public technical model can be represented as:

```text
Candidate Decision
        ↓
Payload Kind + Classification
        ↓
Authority / Edge Policy
        ↓
Formation Context
        ↓
Evidence
        ↓
Admissibility
        ↓
Policy + Constraint Evaluation
        ↓
Governance Outcome
        ↓
Governed State Transition Resolution
        ↓
Decision Receipt
        ↓
Receipt Persistence
        ↓
Execution Eligibility
```

This is the point at which governance becomes operational rather than descriptive.

---

## 7. Authority Integrity

Authority must be explicit enough to verify who or what is asserting execution authority and under what scope.

The protocol's authority-integrity model preserves sufficient information to evaluate matters such as:

- the actor or system asserting authority;
- authority scope;
- applicable Edge Policy;
- delegated authority;
- authority validity at governance-evaluation time;
- authority validity at execution-commitment time.

Unresolved, unverifiable, contradictory, expired, or inadmissible authority conditions must not silently become execution permission.

Where authority materially affects the governance determination, the authorization basis is expected to remain traceable through the Decision Receipt.

---

## 8. Formation Integrity

Governance may need visibility into how a candidate decision was formed before it reached the Governance Boundary.

Where formation context is materially relevant or required, the protocol may preserve information identifying:

- upstream shaping path;
- materially participating actors;
- orchestration influences;
- tools or models materially involved;
- constraints influencing proposal formation;
- basis upon which the candidate decision was constructed.

Formation visibility is distinct from admissibility.

Knowing **how a decision was formed** does not by itself mean the decision is **permissible to execute**.

---

## 9. Admissibility Requirement

A governed decision is not execution-eligible merely because it exists and has provenance.

The Governance Boundary evaluates whether the candidate decision is admissible under the applicable governance conditions.

Admissibility may consider:

- policy constraints;
- authority validity;
- evidence sufficiency;
- formation integrity;
- execution scope;
- risk posture;
- Edge Policy restrictions;
- anomaly conditions.

Where admissibility cannot be established, governed execution fails closed.

Admissibility is therefore a precondition of consequential execution, not a post-execution explanation.

---

## 10. Policy and Constraint Evaluation

The Governance Boundary evaluates applicable policy before execution.

Policy evaluation may resolve:

- whether execution is permitted;
- whether execution is prohibited;
- whether higher authority is required;
- whether additional evidence is required;
- whether execution must be delayed;
- whether execution must occur under reduced authority or reduced autonomy;
- whether the action must be invalidated.

Passive logging alone does not satisfy this control function.

The governance layer must be capable of affecting whether and how an action proceeds.

---

## 11. Canonical Governance Outcomes

Boundary evaluation resolves to a canonical Governance Outcome.

| Outcome | Boundary Meaning |
|---|---|
| **ALLOW** | The governed decision may proceed subject to the recorded authorization context. |
| **DENY** | Consequential execution is prohibited. |
| **ESCALATE** | Additional or higher authority / human review is required. |
| **DEFER** | Execution is postponed pending evidence, time, dependency, or another required condition. |
| **DEGRADE** | Execution may proceed only under reduced scope, capability, authority, or autonomy. |

A governance result must not be inferred from transport success.

The outcome is an explicit protocol artifact.

---

## 12. Decision Receipt as Authorization Artifact

The **Decision Receipt** is the canonical governance artifact associated with a governed decision.

It records the governance determination in a form designed to support audit, verification, interoperability, and execution authorization.

A receipt may preserve or reference:

- candidate decision;
- actor identities and roles;
- authority context;
- decision classification;
- formation context;
- state context;
- Evidence References;
- policy-evaluation results;
- admissibility result;
- Governance Outcome;
- Reason Codes;
- integrity metadata;
- persistence metadata;
- Dispatch Trace information.

For governed execution, the Decision Receipt is not merely retrospective evidence.

It is part of the authorization chain.

---

## 13. Receipt Persistence

Governance does not end when a receipt is constructed.

Where the applicable posture requires durable receipt persistence, execution eligibility depends on successful preservation of the governance artifact.

Conceptually:

```text
Governance Outcome
        ↓
Governed State Transition
        ↓
Decision Receipt
        ↓
Receipt Persistence
        ↓
Execution
```

If required receipt persistence fails under a fail-closed posture, consequential execution must not proceed.

This ensures that the system does not create consequences that cannot later be reconstructed through the required governance record.

---

## 14. Governed State Transition Integrity

R.E.T.N.A. distinguishes successful transport from successful governed consequence.

A **Governed State Transition** is a governance-resolved transition between prior state and resulting state that has satisfied the governance conditions applicable to the consequential action.

The protocol model preserves sufficient information to reason about:

- prior state;
- candidate state;
- resulting state;
- Governance Outcome;
- authority basis;
- formation context;
- admissibility outcome;
- Evidence References;
- receipt reference;
- receipt persistence status;
- execution authorization conditions;
- applicable Reason Codes.

The critical rule is:

```text
Forwarded ≠ Executed
Delivered ≠ Authorized
Persisted ≠ Permitted
Generated ≠ Governed
```

Governed consequence derives from explicit governance resolution.

---

## 15. Boundary Bypass

A Governance Boundary that can be silently bypassed is not an enforceable governance boundary.

For governed decision classes:

- the Executor must not act merely because it received a decision;
- a valid Governance Outcome must authorize execution;
- required Decision Receipt conditions must be satisfied;
- applicable governed state transition conditions must be resolved;
- required persistence conditions must be satisfied;
- attempts to bypass governance should be observable through canonical governance artifacts and Reason Codes.

The purpose is to prevent an alternate path from converting advisory governance into optional governance.

---

## 16. Fail-Closed Boundary Behavior

The Governance Boundary is designed to fail closed where required governance conditions remain unresolved.

Examples include:

- missing authority;
- invalid authority;
- expired authority;
- missing required formation context;
- failed admissibility;
- insufficient evidence;
- policy violation;
- contradictory governance outcome;
- invalid state-transition result;
- missing required Decision Receipt;
- receipt persistence failure;
- integrity failure.

The governing principle is:

```text
Unresolved Governance
        ↓
No Execution Authority
```

This is distinct from system availability.

An execution system may be technically available while execution authority remains absent.

---

## 17. Boundary Actors and Separation of Duties

The Governance Boundary preserves logical role separation among protocol actors.

### Producer

Constructs or proposes the candidate decision.

### Governor

Evaluates governance requirements and produces the Governance Outcome.

### Executor

Carries out an authorized action or governed state transition.

### Receipt Store

Persists Decision Receipts for audit and verification.

Optional supporting roles may include:

- Policy Authority;
- Evidence Store;
- Attestor;
- independent validator or auditor.

Implementations may compose roles differently, but conformance depends on preserving the protocol guarantees associated with those roles.

---

## 18. Boundary Invariant Mapping

The Governance Boundary is directly connected to multiple R.E.T.N.A. System Invariants.

| Invariant | Boundary Relationship |
|---|---|
| **I1 — Governance Boundary Integrity** | No governed execution without passing through the Governance Boundary. |
| **I2 — Mandatory Receipt Emission** | Every governed decision produces a Decision Receipt regardless of outcome. |
| **I3 — Trace Completeness** | Materially participating actors remain identifiable. |
| **I4 — Evidence Referencing** | Governance decisions preserve sufficient evidence references or summaries. |
| **I5 — Structured Policy Disclosure** | Applicable policy evaluation remains reconstructable at the required level. |
| **I6 — Outcome Determinism** | Equivalent governance conditions resolve predictably. |
| **I7 — Tamper Awareness** | Receipt and integrity mechanisms expose unauthorized alteration. |
| **I8 — Separation of Duties** | Decision construction, governance, and execution roles remain governable. |
| **I9 — Authority Integrity** | Governed execution depends on valid authority provenance and scope. |
| **I10 — Admissibility Requirement** | Consequential execution requires explicit admissibility determination. |
| **I11 — Formation Integrity** | Required decision-formation context remains inspectable. |
| **I12 — Governed State Transition Integrity** | Transport success cannot substitute for explicit state-transition authorization. |

A dedicated public [`system-invariants.md`](system-invariants.md) artifact will describe these invariants in greater detail.

---

## 19. Boundary Conformance Signals

The Governance Boundary is intended to be externally testable through observable behavior.

A reviewer should be able to evaluate conditions such as:

### Boundary Integrity

Attempt to execute a governed decision without valid governance authorization.

**Expected behavior:** execution is refused.

### Authority Failure

Submit a governed decision with unresolved or invalid authority.

**Expected behavior:** consequential execution does not proceed.

### Admissibility Failure

Submit a decision that cannot establish required admissibility.

**Expected behavior:** execution fails closed and the result is observable.

### Formation Failure

Remove formation metadata where formation integrity is required.

**Expected behavior:** the governed decision is rejected, invalidated, deferred, or otherwise prevented from consequential execution according to applicable policy.

### Governed State Transition Failure

Produce successful routing, forwarding, or orchestration while state-transition authorization remains unresolved.

**Expected behavior:** transport succeeds, but governed consequence remains blocked.

### Receipt Persistence Failure

Simulate required receipt-storage or persistence failure.

**Expected behavior:** consequential execution is refused under the applicable fail-closed posture.

These testable behaviors are the bridge between doctrine and conformance.

---

## 20. Boundary vs. Post-Hoc Logging

The difference between logging and governance can be stated simply:

| Post-Hoc Logging | Governance Boundary |
|---|---|
| Records events after execution | Evaluates permission before consequence |
| Describes what happened | Determines what is allowed to happen |
| Does not necessarily block execution | Can block, defer, degrade, escalate, or deny |
| May be advisory | Must be enforceable for governed decision classes |
| Execution may precede artifact creation | Governance artifact participates in authorization chain |

R.E.T.N.A. therefore treats observability as useful but insufficient for consequential authorization.

---

## 21. Implementation Independence

The Governance Boundary is defined by protocol behavior rather than a mandatory vendor architecture.

A conforming implementation is not required to use a specific:

- model;
- agent framework;
- programming language;
- policy engine;
- database;
- cloud environment;
- orchestration platform;
- hardware system.

Independent implementations may realize the Governance Boundary differently provided the required protocol guarantees remain observable and enforceable.

---

## 22. What External Reviewers Can Verify

The public technical surface is designed so that an external reviewer can determine whether R.E.T.N.A. defines more than a governance narrative.

A reviewer can evaluate whether the protocol has:

- a defined execution boundary;
- explicit authorization semantics;
- structured authority handling;
- formation and admissibility controls;
- canonical governance outcomes;
- a portable Decision Receipt artifact;
- receipt-persistence expectations;
- governed state-transition semantics;
- fail-closed behavior;
- explicit invariants;
- observable conformance tests.

The deeper controlled specification provides the full normative treatment and implementation context.

---

## 23. Public and Controlled Review

This document is part of the **public R.E.T.N.A. technical review surface**.

Related public artifacts:

- [`protocol-overview.md`](protocol-overview.md)
- [`normative-language.md`](normative-language.md)
- [`STATUS.md`](../STATUS.md)
- [`NOTICE.md`](../NOTICE.md)

The complete **R.E.T.N.A. Protocol Specification — Institutional Edition**, the **Governed Autonomous Intelligence Whitepaper — Institutional Edition**, and selected supporting materials remain available through controlled review.

[Request R.E.T.N.A. Controlled Review Access](https://valueintelligence.io/retna-protocol/#controlled-review-access)

Public availability of this document does not grant unrestricted implementation, certification, commercialization, sublicensing, patent, or trademark rights.

---

## 24. Protocol Status

This document reflects the public technical surface of the **R.E.T.N.A. v0.1 Draft Specification**.

It may evolve through explicit repository and protocol versioning as implementation validation, conformance testing, interoperability work, security review, legal review, and external technical feedback continue.

See [`STATUS.md`](../STATUS.md) for current protocol status.

---

## 25. Stewardship

R.E.T.N.A. is developed and stewarded by:

**Value Intelligence Solutions Inc.**

The long-term objective is to advance Decision Governance Infrastructure as a vendor-neutral, enforceable, testable, and interoperable control layer for autonomous and model-driven systems.

---

© 2026 Value Intelligence Solutions Inc. All rights reserved.

**R.E.T.N.A.™ — Trademark Pending**  
**HomeSphere AI™ — Trademark Pending**  
**Smart-I-Shelf™ — Patent Pending / Trademark Pending**

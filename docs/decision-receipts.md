# R.E.T.N.A.™ Decision Receipts

**Public Technical Review Artifact — Draft v0.1**

The **Decision Receipt** is the canonical governance artifact of the R.E.T.N.A.™ Decision Governance Protocol.

It records the governed determination associated with a candidate decision and preserves sufficient structured context to support:

- execution authorization;
- audit and investigation;
- policy verification;
- evidence traceability;
- authority verification;
- admissibility reconstruction;
- governed state-transition verification;
- interoperability across compliant systems.

> **Receipts over narratives.**

> **Governance must be reconstructable without requiring access to proprietary model internals.**

A Decision Receipt is not merely a post-execution log.

For governed decision classes, it participates directly in the authorization chain that determines whether consequential execution may occur.

The controlled **R.E.T.N.A. Protocol Specification — Institutional Edition** remains the authoritative source for complete v0.1 normative requirements.

---

## 1. Decision Receipt Purpose

A Decision Receipt provides a structured record of:

```text
WHAT was proposed
        +
WHO participated
        +
UNDER WHAT authority
        +
HOW the decision was formed
        +
WHICH evidence was relied upon
        +
WHICH policies and constraints were evaluated
        +
WHETHER the decision was admissible
        +
WHICH governance outcome was produced
        +
WHAT governed state transition was permitted or refused
        +
WHETHER execution occurred
        +
HOW integrity and retention were preserved
```

The receipt therefore acts as a portable governance record for consequential decisions constructed by AI, agents, orchestration systems, or other model-driven infrastructure.

---

## 2. Mandatory Receipt Emission

Every governed decision is expected to produce a Decision Receipt regardless of outcome.

This includes decisions that are:

- **ALLOW**
- **DENY**
- **ESCALATE**
- **DEFER**
- **DEGRADE**
- blocked before execution;
- never executed.

This requirement reflects **System Invariant I2 — Mandatory Receipt Emission**.

Conceptually:

```text
Governed Decision
        ↓
Governance Evaluation
        ↓
Decision Receipt
        ↓
Execution or Refusal
```

The receipt is therefore not conditioned on success.

It records both actions permitted and actions prevented.

---

## 3. Receipt as Authorization Artifact

For governed execution, the Decision Receipt is part of the execution-authorization chain.

A valid execution path can be represented as:

```text
Candidate Decision
        ↓
Governance Boundary
        ↓
Governance Outcome
        ↓
Governed State Transition Resolution
        ↓
Decision Receipt
        ↓
Required Receipt Persistence
        ↓
Executor Verification
        ↓
Consequential Execution
```

An Executor must not treat the mere arrival of a decision as authorization.

Execution must remain consistent with the authorization context represented by the receipt.

---

## 4. Receipt Requirements

The v0.1 protocol model requires Decision Receipts to be suitable for both:

- machine verification; and
- human inspection.

A receipt must preserve enough information to explain:

- what was proposed;
- why the decision was evaluated;
- how the governance outcome was determined;
- whether execution was authorized or refused;
- what authority conditions applied;
- why the decision was admissible, inadmissible, deferred, degraded, escalated, or denied;
- what state transition was authorized, constrained, blocked, or refused;
- what governance conditions materially affected execution eligibility.

Receipts must remain interpretable without requiring:

- proprietary model weights;
- unrestricted chain-of-thought;
- private scoring formulas;
- vendor-specific reasoning artifacts.

---

## 5. Receipt Lifecycle

Every Decision Receipt progresses through a logical lifecycle.

```text
PROPOSED
   ↓
EVALUATED
   ↓
RESOLVED
   ↓
EXECUTED (optional)
   ↓
FINALIZED
```

### Proposed

The candidate decision has entered governance evaluation.

### Evaluated

Applicable policies, constraints, evidence, authority, and other required governance conditions have been assessed.

### Resolved

A canonical Governance Outcome has been determined.

### Executed — Optional

The authorized action or governed state transition has been applied.

### Finalized

The receipt has been sealed for audit and retained according to the applicable policy or compliance profile.

A lifecycle transition must preserve trace continuity.

Prior receipt state must not be silently erased.

---

## 6. Canonical Receipt Architecture

The public v0.1 receipt model is organized into canonical governance blocks.

```text
Decision Receipt
│
├── Receipt Header
├── Identity Block
├── Authority Context Block
├── Decision Envelope
├── Formation Context Block
├── State Context
├── Participants
├── Evidence Block
├── Policy Evaluation Block
├── Admissibility Block
├── Outcome Block
└── Integrity and Audit Block
```

This ordering reflects the governance chain:

```text
Identity
   ↓
Authority
   ↓
Decision
   ↓
Formation
   ↓
State
   ↓
Evidence
   ↓
Policy
   ↓
Admissibility
   ↓
Outcome
   ↓
Integrity / Audit
```

Serialization format may vary, but the canonical semantics must remain stable.

---

## 7. Receipt Header

The Receipt Header identifies the governance artifact and protocol version.

Publicly relevant fields include:

| Field | Purpose |
|---|---|
| `receipt_id` | Globally unique receipt identifier |
| `version` | R.E.T.N.A. protocol version |
| `created_at` | Receipt creation timestamp |
| `expires_at` | Optional expiry information, including deferred-decision contexts |

Stable receipt identity supports:

- cross-receipt correlation;
- audit;
- version-aware validation;
- chaining;
- lifecycle reconstruction.

---

## 8. Identity Block

The Identity Block identifies the primary protocol actors associated with the receipt.

Typical actor classes include:

### Producer

The actor responsible for constructing the candidate decision.

### Governor

The authoritative governance actor that evaluates the proposal and emits the Decision Receipt.

### Executor

The actor capable of applying an authorized action to the environment.

Actor identity records are expected to preserve stable identifiers sufficient for:

- provenance;
- cross-receipt correlation;
- audit and investigation.

---

## 9. Authority Context Block

The **Authority Context Block** records the authority basis under which the governed decision was evaluated for admissibility and execution eligibility.

Where authority materially affects governance, the receipt may preserve information such as:

| Field | Public Meaning |
|---|---|
| `authority_id` | Identifier for the relevant authority source |
| `authority_type` | Category of authority |
| `authority_scope` | Scope within which authority applies |
| `delegation_chain` | Optional delegated-authority lineage |
| `edge_policy_result` | Optional Edge Policy result |
| `verification_status` | Authority-verification state |
| `authority_expiration` | Optional expiry boundary |

Authority metadata must remain coherent with the Governance Outcome.

Ambiguous, unverifiable, contradictory, expired, or delegated-beyond-scope authority must not independently authorize governed execution.

This block makes **System Invariant I9 — Authority Integrity** inspectable.

---

## 10. Decision Envelope

The Decision Envelope describes the candidate decision independently of proprietary internal reasoning.

Publicly relevant fields include:

| Field | Purpose |
|---|---|
| `decision_id` | Stable decision identifier |
| `risk_class` | Governance Risk Class |
| `action_type` | Action Type classification |
| `decision_mode` | Decision Mode classification |
| `payload_kind` | Semantic request category where supported |
| `proposed_action` | Structured candidate-action summary |
| `target` | Affected entity, system, resource, or environment |

The Decision Envelope answers:

> **What consequential action is actually being governed?**

---

## 11. Payload Kind

Where supported, **Payload Kind** identifies the semantic category of the governed request.

It supplements the core classification triad:

```text
Risk Class
    +
Action Type
    +
Decision Mode
```

Payload Kind may be used for:

- routing governance evaluation;
- policy applicability;
- privilege determination;
- distinguishing execution requests from evidence, observational, or governance artifacts.

Payload Kind does not replace Risk Class.

For privileged categories, ambiguous Payload Kind resolution must not silently become execution authority.

---

## 12. Formation Context Block

The **Formation Context Block** preserves governance-relevant information describing how the candidate decision was shaped before admissibility evaluation and Governance Boundary enforcement.

Formation context may include:

- formation identifier;
- formation trace reference;
- orchestration lineage;
- materially participating models;
- materially participating tools;
- governance constraints applied during formation;
- formation-integrity status.

Formation preservation may vary according to:

- Compliance Profile;
- Risk Class;
- Payload Kind;
- Action Type;
- domain-specific policy;
- transition sensitivity.

The protocol does **not** require unrestricted chain-of-thought disclosure.

Only governance-relevant formation context necessary for auditability and execution-integrity verification is expected.

This block supports **System Invariant I11 — Formation Integrity**.

---

## 13. State Context

The State Context records the state relevant to governance evaluation.

Publicly relevant concepts include:

| Field | Purpose |
|---|---|
| `state_snapshot_ref_before` | Optional reference to prior state |
| `state_snapshot_ref_after` | Optional reference to resulting state |
| `state_delta_summary` | Structured summary of actual or expected change |
| `environment_context` | Relevant environmental context, subject to redaction |

The State Context should make it possible to understand:

```text
What was true before?
        ↓
What was proposed to change?
        ↓
What changed or would change?
```

Sensitive raw state data should be represented through bounded summaries or references where appropriate.

---

## 14. Participants and Dispatch Trace

All materially participating entities involved in Decision Construction should remain identifiable.

The Participants surface may include:

- `agents_involved`
- `models_involved`
- `tools_invoked`
- `external_services`

Each participant should carry enough stable identification to support provenance and audit.

The participation path may also be represented through a **Dispatch Trace**, provided the receipt remains independently interpretable.

This supports **System Invariant I3 — Trace Completeness**.

---

## 15. Evidence Block

The Evidence Block references the evidence used during Decision Construction and governance evaluation.

Public evidence semantics may include:

| Field | Purpose |
|---|---|
| `evidence_id` | Stable evidence identifier |
| `type` | Evidence category |
| `source` | Evidence source |
| `timestamp` | Evidence time context |
| `hash` | Integrity value where profile-required |
| `location_ref` | Non-public retrieval reference |
| `summary` | Bounded audit-oriented summary |

The preferred design is:

```text
Reference evidence when possible
        ↓
Avoid unnecessary raw-data replication
        ↓
Preserve retrieval + integrity + auditability
```

This supports **I4 — Evidence Referencing** and **I7 — Tamper Awareness**.

---

## 16. Policy Evaluation Block

The Policy Evaluation Block records the governance rules applied to the candidate decision.

A public receipt model may identify:

### Policy Bundles

- bundle identifier;
- bundle version;
- authority.

### Applied Constraints

- constraint identifier;
- result;
- severity;
- Reason Codes.

### Optional Risk Assessment

- risk score;
- risk factors.

Where applicable, Edge Policy results may also be represented.

The Policy Evaluation Block should remain structured and machine-readable.

This supports:

- **I5 — Policy Disclosure (Structured)**
- **I6 — Outcome Determinism**

---

## 17. Admissibility Block

The **Admissibility Block** records whether the candidate decision satisfied the governance conditions required for governed consequence.

Publicly relevant semantics may include:

| Field | Purpose |
|---|---|
| `admissibility_status` | Admissibility determination |
| `admissibility_reason_codes` | Structured explanation |
| `blocking_constraints` | Constraints preventing admissibility |
| `authority_validation_result` | Authority-related evaluation result |
| `formation_integrity_result` | Formation-related result |
| `evidence_sufficiency_result` | Evidence-sufficiency result |
| `execution_eligibility` | Execution-eligibility state where represented |
| `admissibility_timestamp` | Time of determination |

Admissibility answers:

> **Did the candidate decision satisfy the governance conditions required to become eligible for governed consequence?**

A decision that cannot establish required admissibility must not proceed to governed execution.

This supports **I10 — Admissibility Requirement** and **I12 — Governed State Transition Integrity**.

---

## 18. Outcome Block

The Outcome Block records the canonical result of governance evaluation.

The canonical Governance Outcomes are:

```text
ALLOW
DENY
ESCALATE
DEFER
DEGRADE
```

The public outcome surface may represent:

- Governance Outcome;
- outcome Reason Codes;
- required human confirmation;
- fallback path;
- execution status;
- human override where applicable.

At least one Reason Code accompanies every canonical outcome.

Human review, fallback, or override behavior should remain explicit rather than implicit.

---

## 19. Governed State Transition Context

A Decision Receipt must support verification of governed consequence, not merely transport.

The receipt should preserve enough state-transition context to determine whether the consequential action was:

- authorized;
- denied;
- deferred;
- degraded;
- blocked;
- invalidated;
- refused.

The relevant doctrine is:

```text
Forwarded ≠ Executed
Delivered ≠ Authorized
Persisted ≠ Permitted
Generated ≠ Governed
```

Where consequential execution is permitted, the receipt participates in proving that the associated state transition crossed the Governance Boundary under valid authority and admissibility conditions.

---

## 20. Integrity and Audit Block

The Integrity and Audit Block records the integrity protections and retention controls associated with the receipt.

Publicly relevant fields include:

| Field | Purpose |
|---|---|
| `receipt_hash` | Canonical receipt integrity value |
| `previous_receipt_hash` | Optional receipt-chain continuity |
| `signature` | Required where the applicable profile requires cryptographic attestation |
| `retention_class` | Retention policy category |
| `access_class` | Access-control category |

Integrity metadata must be sufficient to expose unauthorized receipt modification.

Where receipt chaining is used, previous-receipt references can preserve continuity across related governance events.

---

## 21. Canonicalization and Serialization

R.E.T.N.A. does not require every implementation to use the same physical serialization format.

It does require deterministic canonicalization sufficient to support:

- stable hashing;
- reproducible verification;
- consistent signature or attestation behavior;
- interoperable audit export.

For JSON, a conforming canonicalization profile may use principles such as:

```text
UTF-8
Canonical field names
Deterministic key ordering
No insignificant whitespace
```

Where a receipt hash is stored inside the receipt, the hashing procedure must avoid circular self-hashing by blanking or excluding the receipt-hash field before computing the canonical hash.

Validators must be able to identify which canonicalization profile was used.

---

## 22. Receipt Immutability and Lifecycle Updates

Receipt lifecycle progression must not permit silent historical rewriting.

If execution state or other post-issuance information is added, implementations may:

- update receipt state under a verifiable lifecycle mechanism; or
- emit a linked follow-on receipt.

In either case:

```text
Original Governance Event
        ↓
Explicit Linkage / Chaining
        ↓
Later Receipt State
```

Prior receipt state must remain reconstructable.

---

## 23. Decision Receipt and Receipt Store

The **Receipt Store** is the durable system responsible for preserving Decision Receipts.

A Receipt Store may be implemented using:

- databases;
- append-only logs;
- audit ledgers;
- compliance data stores;
- equivalent durable mechanisms.

The storage layer must preserve integrity according to the declared Compliance Profile.

Receipt deletion or alteration remains subject to governance policy.

---

## 24. Receipt Persistence as Execution Gate

For consequential execution, receipt construction alone may be insufficient where the applicable posture requires durable persistence.

Conceptually:

```text
Governance Resolved
        ↓
Receipt Constructed
        ↓
Receipt Persisted
        ↓
Execution Eligible
```

If required persistence fails under a fail-closed governance posture:

```text
Persistence Failure
        ↓
No Execution Authority
```

This ensures that consequential system change does not outrun the governance record required to reconstruct it.

---

## 25. Receipt Integrity by Compliance Profile

R.E.T.N.A. supports progressively stronger integrity expectations.

A public summary is:

| Profile | Receipt Integrity Direction |
|---|---|
| **RETNA-A** | Foundational receipt and governance controls |
| **RETNA-B** | Stronger tamper-evident governance and audit expectations |
| **RETNA-C** | Critical-consequence posture with stronger cryptographic / attestation expectations |

The complete controlled specification defines the applicable profile requirements.

---

## 26. Minimal Receipt

R.E.T.N.A. supports a minimal receipt concept for foundational governance adoption.

A minimal receipt should still preserve enough canonical information to establish:

- receipt identity;
- decision identity;
- primary actors;
- decision classification;
- evidence references;
- policy result;
- Governance Outcome;
- Reason Codes;
- integrity metadata required by the applicable profile.

Minimal does not mean optional governance.

It means a reduced canonical surface that still preserves the protocol's essential accountability guarantees.

---

## 27. Receipt and System Invariant Mapping

Decision Receipts make multiple System Invariants externally inspectable.

| Invariant | Receipt Evidence Surface |
|---|---|
| **I2** | Receipt existence |
| **I3** | Participants / Dispatch Trace |
| **I4** | Evidence Block |
| **I5** | Policy Evaluation Block |
| **I6** | Outcome + Reason Codes + context |
| **I7** | Integrity and Audit Block |
| **I9** | Authority Context Block |
| **I10** | Admissibility Block |
| **I11** | Formation Context Block |
| **I12** | State Context + governed-state-transition metadata |

This is why the Decision Receipt functions as a **governance evidence surface**, not merely a transaction log.

---

## 28. Receipt Conformance Signals

A reviewer should be able to test:

### Receipt Emission

Does every governed decision produce a receipt?

### Receipt Completeness

Are required governance blocks present for the applicable profile and decision class?

### Authority Reconstruction

Can the execution-authority basis be reconstructed?

### Evidence Traceability

Can referenced evidence be identified and verified?

### Policy Reconstruction

Can the applied Policy Bundles and material constraints be identified?

### Admissibility Reconstruction

Can the admissibility basis be determined?

### State-Transition Verification

Can the governed consequence be distinguished from mere message transport?

### Integrity Validation

Can unauthorized receipt modification be detected?

### Lifecycle Continuity

Do lifecycle updates preserve the prior governance record?

These tests turn the receipt model into an externally reviewable protocol surface.

---

## 29. Interoperability Role

The Decision Receipt is designed to function as the primary portable unit of governance interoperability.

Independent systems should be able to interpret:

- the governed decision;
- actor identity;
- classification;
- governance outcome;
- Reason Codes;
- evidence references;
- policy references;
- integrity metadata;
- protocol version;

without requiring access to proprietary model internals.

This allows governance evidence to move across:

- vendors;
- runtimes;
- audit systems;
- policy systems;
- orchestration environments;
- regulatory or enterprise review surfaces.

---

## 30. What a Decision Receipt Is Not

A Decision Receipt is not:

- unrestricted chain-of-thought;
- a prompt transcript;
- a raw model trace;
- a proprietary scoring dump;
- a replacement for domain-specific records;
- proof that every underlying model statement is correct;
- mere post-hoc logging.

It is a structured governance artifact recording the authorization context and observable basis of a governed decision.

---

## 31. Public Illustrative Shape

A public receipt may be represented conceptually as:

```json
{
  "receipt_id": "retna_example_001",
  "version": "0.1",
  "identities": {
    "producer": "...",
    "governor": "...",
    "executor": "..."
  },
  "authority_context": {
    "verification_status": "..."
  },
  "decision_envelope": {
    "decision_id": "...",
    "risk_class": "...",
    "action_type": "...",
    "decision_mode": "...",
    "payload_kind": "...",
    "proposed_action": "...",
    "target": "..."
  },
  "formation_context": {
    "formation_trace_ref": "..."
  },
  "state_context": {
    "state_delta_summary": "..."
  },
  "evidence": [
    {
      "evidence_id": "...",
      "summary": "..."
    }
  ],
  "policy_evaluation": {
    "policy_bundles": ["..."],
    "constraints": ["..."]
  },
  "admissibility": {
    "admissibility_status": "...",
    "admissibility_reason_codes": ["..."]
  },
  "outcome": {
    "governance_outcome": "...",
    "outcome_reason_codes": ["..."],
    "execution_status": "..."
  },
  "integrity": {
    "receipt_hash": "...",
    "retention_class": "...",
    "access_class": "..."
  }
}
```

This is an **illustrative public shape**, not the complete controlled schema.

A separate synthetic example receipt is planned under:

```text
examples/sample-decision-receipt.json
```

---

## 32. Public and Controlled Review

This document is part of the **public R.E.T.N.A. technical review surface**.

Related public artifacts:

- [`protocol-overview.md`](protocol-overview.md)
- [`normative-language.md`](normative-language.md)
- [`governance-boundary.md`](governance-boundary.md)
- [`system-invariants.md`](system-invariants.md)
- [`STATUS.md`](../STATUS.md)
- [`NOTICE.md`](../NOTICE.md)

The complete **R.E.T.N.A. Protocol Specification — Institutional Edition**, the **Governed Autonomous Intelligence Whitepaper — Institutional Edition**, and selected supporting materials remain available through controlled review.

[Request R.E.T.N.A. Controlled Review Access](https://valueintelligence.io/retna-protocol/#controlled-review-access)

Public availability of this document does not grant unrestricted implementation, certification, commercialization, sublicensing, patent, or trademark rights.

---

## 33. Next Public Artifact

The next planned technical artifact is:

```text
docs/reason-codes.md
```

It will describe the canonical Reason Code model, baseline categories, usage rules, governance-control semantics, authority and admissibility codes, state-transition codes, and vendor-extension boundaries.

---

## 34. Protocol Status

This document reflects the public technical surface of the **R.E.T.N.A. v0.1 Draft Specification**.

The controlled specification remains authoritative for complete normative requirements and canonical field definitions.

See [`STATUS.md`](../STATUS.md) for current protocol status.

---

## 35. Stewardship

R.E.T.N.A. is developed and stewarded by:

**Value Intelligence Solutions Inc.**

The long-term objective is to advance Decision Governance Infrastructure as a vendor-neutral, enforceable, testable, and interoperable control layer for autonomous and model-driven systems.

---

© 2026 Value Intelligence Solutions Inc. All rights reserved.

**R.E.T.N.A.™ — Trademark Pending**  
**HomeSphere AI™ — Trademark Pending**  
**Smart-I-Shelf™ — Patent Pending / Trademark Pending**

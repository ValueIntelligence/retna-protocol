# R.E.T.N.A.™ Canonical Reason Codes

**Public Technical Review Artifact — Draft v0.1**

Canonical **Reason Codes** are the machine-readable governance assertions used by the R.E.T.N.A.™ Decision Governance Protocol to explain why a governed decision produced a particular outcome or execution posture.

Reason Codes form part of the **Decision Receipt Outcome Block** and provide a standardized interpretation layer between:

```text
Policy Evaluation
        +
Authority / Formation / Admissibility
        +
Evidence / Risk / System State
        +
Governed State Transition Resolution
        ↓
Canonical Reason Codes
        ↓
Governance Outcome
        ↓
Execution Posture + External Observability
```

All systems claiming R.E.T.N.A. compliance are expected to support the canonical baseline Reason Codes defined by the Protocol.

Implementations may extend the baseline set, but extensions must not redefine or suppress applicable canonical meanings.

> **Reason Codes are not narrative explanations.**

> **They are stable, machine-readable assertions about the governance conditions that materially influenced the decision.**

The controlled **R.E.T.N.A. Protocol Specification — Institutional Edition** remains the authoritative source for complete v0.1 normative requirements.

---

## 1. Purpose

Canonical Reason Codes serve four principal functions:

1. consistent interpretation of governance outcomes across systems;
2. support for automated audit, analytics, alerting, and validation;
3. review without disclosure of proprietary model reasoning;
4. stable signals for downstream workflows such as escalation, retry, fallback, remediation, degradation, persistence handling, or governed state-transition authorization.

Reason Codes are designed to identify material governance conditions such as:

- policy results;
- evidence sufficiency;
- confidence;
- risk;
- safety;
- regulatory restriction;
- system state;
- dependency failure;
- human oversight;
- authority integrity;
- admissibility;
- formation integrity;
- governed state-transition status;
- continuity or state drift.

---

## 2. Reason Codes vs. Governance Outcomes

Reason Codes and Governance Outcomes perform different protocol functions.

### Governance Outcomes

The five baseline Governance Outcomes are:

```text
ALLOW
DENY
ESCALATE
DEFER
DEGRADE
```

They answer:

> **What governance posture resulted?**

### Reason Codes

Canonical Reason Codes answer:

> **Which governance condition materially explains that posture?**

Conceptually:

```text
Governance Outcome
        =
What happened

Reason Code(s)
        =
Why the governance system resolved that way
```

A Decision Receipt may contain multiple Reason Codes where multiple governance conditions materially influenced the result.

---

## 3. Canonical Namespace

Baseline R.E.T.N.A. Reason Codes use the canonical prefix:

```text
RC_
```

Examples:

```text
RC_POLICY_PASS
RC_AUTHORITY_INVALID
RC_ADMISSIBILITY_FAIL
RC_STATE_TRANSITION_BLOCKED_NO_RECEIPT
```

Canonical codes should remain:

- concise;
- enumerable;
- stable;
- deterministic;
- interpretable without proprietary system context.

---

# 4. Policy Evaluation Codes

These codes describe policy-constraint evaluation.

| Code | Meaning |
|---|---|
| `RC_POLICY_PASS` | All applicable constraints evaluated successfully. |
| `RC_POLICY_FAIL` | One or more blocking constraints failed. |
| `RC_POLICY_PARTIAL` | Non-blocking constraints failed or warnings were issued. |

Policy evaluation codes should accompany Decision Receipts unless a higher-level governance failure prevented policy evaluation.

### Interpretation

```text
RC_POLICY_PASS
        ↓
Applicable policy constraints passed

RC_POLICY_FAIL
        ↓
At least one blocking constraint failed

RC_POLICY_PARTIAL
        ↓
Evaluation completed with non-blocking failures or warnings
```

A policy code alone does not replace the canonical Governance Outcome.

---

# 5. Evidence and Confidence Codes

These codes describe deficiencies or governance conditions involving evidence availability, freshness, confidence, or integrity.

| Code | Meaning |
|---|---|
| `RC_INSUFFICIENT_EVIDENCE` | Required evidence was missing or incomplete. |
| `RC_LOW_CONFIDENCE` | A confidence threshold required for action was not met. |
| `RC_EVIDENCE_STALE` | Evidence used during evaluation was outdated or expired. |
| `RC_EVIDENCE_INTEGRITY_FAIL` | Evidence integrity verification failed. |

Evidence codes should be emitted when an evidence deficiency materially influenced the Governance Outcome.

These codes allow systems to distinguish:

```text
Evidence Missing
Evidence Too Weak
Evidence Too Old
Evidence Integrity Failed
```

without exposing unnecessary raw evidence.

---

# 6. Risk and Safety Codes

These codes describe governance decisions materially influenced by risk evaluation, safety controls, or regulatory restrictions.

| Code | Meaning |
|---|---|
| `RC_RISK_THRESHOLD_EXCEEDED` | Computed risk exceeded the allowed policy threshold. |
| `RC_SAFETY_GUARDRAIL` | A safety constraint or guardrail was triggered. |
| `RC_REGULATORY_RESTRICTION` | A regulatory or compliance rule prevented execution. |

Risk and safety codes are expected where safety, compliance, or risk thresholds materially influenced the governance decision.

---

# 7. System and Dependency Codes

These codes describe operational system conditions or environmental dependencies that influenced the outcome.

| Code | Meaning |
|---|---|
| `RC_EXTERNAL_DEPENDENCY_FAILURE` | A required external system was unavailable or failed. |
| `RC_RATE_LIMITED` | Execution was deferred due to rate limiting or throughput constraints. |
| `RC_SYSTEM_DEGRADED` | System health conditions triggered reduced autonomy. |

These codes distinguish governance restrictions caused by operational state from restrictions caused by policy, evidence, authority, or risk.

---

# 8. Governance Control Codes

These codes describe governance conditions involving confirmation, escalation, fallback, or human override.

| Code | Meaning |
|---|---|
| `RC_REQUIRES_CONFIRMATION` | Human confirmation is required before execution. |
| `RC_ESCALATION_REQUIRED` | Escalation to a higher authority is required. |
| `RC_FALLBACK_APPLIED` | A safe fallback path was selected. |
| `RC_HUMAN_OVERRIDE` | A human operator overrode the governance outcome. |

Governance control codes are required where the governance result materially depends on escalation, confirmation, fallback, or override behavior.

These codes make human involvement explicit rather than implicit.

---

# 9. Authority Integrity Codes

These codes describe governance conditions related to authority disclosure, verification, delegation, expiry, and execution scope.

| Code | Meaning |
|---|---|
| `RC_AUTHORITY_REQUIRED` | Required authority disclosure was missing. |
| `RC_AUTHORITY_INVALID` | Authority failed structural or verification requirements. |
| `RC_AUTHORITY_UNVERIFIED` | Authority could not be verified. |
| `RC_AUTHORITY_SCOPE_VIOLATION` | Authority exceeded the declared execution scope. |
| `RC_AUTHORITY_EXPIRED` | Authority context expired before execution authorization. |
| `RC_AUTHORITY_ESCALATED` | Higher-authority review is required. |

Authority Reason Codes are expected where authority materially influenced governance eligibility or execution authorization.

The public authority model therefore distinguishes:

```text
Authority Missing
Authority Invalid
Authority Unverified
Authority Out of Scope
Authority Expired
Authority Escalated
```

This supports **System Invariant I9 — Authority Integrity**.

---

# 10. Admissibility and Formation Codes

These codes describe governance conditions involving admissibility and candidate-decision formation.

| Code | Meaning |
|---|---|
| `RC_ADMISSIBILITY_REQUIRED` | Required admissibility disclosure is missing. |
| `RC_ADMISSIBILITY_FAIL` | The candidate decision failed admissibility evaluation. |
| `RC_FORMATION_REQUIRED` | Required formation metadata is missing. |
| `RC_FORMATION_INVALID` | Formation metadata is malformed or insufficient. |
| `RC_FORMATION_CONTEXT_LOST` | Required proposal-shaping context is unavailable. |

These codes should be emitted where proposal permissibility, provenance, or shaping integrity materially influenced governance.

They preserve a key R.E.T.N.A. distinction:

```text
Formation
How was the candidate decision shaped?

        ≠

Admissibility
Is the candidate decision permitted to cross into governed consequence?
```

These codes support:

- **I10 — Admissibility Requirement**
- **I11 — Formation Integrity**

---

# 11. Governed State Transition Codes

These codes describe authorization, refusal, degradation, blocking, or invalidation of consequential state transitions.

They explicitly distinguish **successful transport** from **governed consequence**.

| Code | Meaning |
|---|---|
| `RC_STATE_TRANSITION_AUTHORIZED` | Candidate decision is authorized for governed state transition. |
| `RC_STATE_TRANSITION_DENIED` | Candidate decision is denied state transition. |
| `RC_STATE_TRANSITION_DEFERRED` | Candidate decision is deferred pending additional governance resolution. |
| `RC_STATE_TRANSITION_DEGRADED` | Candidate decision is allowed only under a degraded posture. |
| `RC_STATE_TRANSITION_BLOCKED_NO_AUTHORITY` | Required authority is missing. |
| `RC_STATE_TRANSITION_BLOCKED_NO_FORMATION` | Required formation metadata is missing or invalid. |
| `RC_STATE_TRANSITION_BLOCKED_NO_ADMISSIBILITY` | Required admissibility is missing or invalid. |
| `RC_STATE_TRANSITION_BLOCKED_NO_RECEIPT` | Required Decision Receipt is unavailable. |
| `RC_STATE_TRANSITION_BLOCKED_PERSISTENCE_FAILURE` | Receipt persistence is unavailable under the applicable fail-closed posture. |
| `RC_STATE_TRANSITION_INVALID_RESULT` | The resulting state is invalid for the current governance posture. |

Governed state-transition codes are expected where an action is capable of producing:

- operational consequence;
- legal consequence;
- financial consequence;
- physical consequence;
- security consequence;
- other material system consequence.

The governing distinction is:

```text
Successful Transport
        ≠
Governed Execution Authorization
```

Governed state-transition authorization remains traceable to a valid Decision Receipt, Governance Outcome, and applicable persistence posture.

These codes support **I12 — Governed State Transition Integrity**.

---

# 12. Continuity and State Drift Codes — Reserved Canonical Set

The v0.1 specification reserves a continuity-sensitive Reason Code set for implementations that validate whether the governance assumptions existing at authorization time remain valid at execution opportunity.

These codes address conditions where:

- authority posture changes;
- admissibility context expires;
- dependencies drift;
- telemetry continuity fails;
- environmental assumptions become invalid;
- the allowed authorization-to-execution window expires.

The reserved codes are:

| Code | Meaning |
|---|---|
| `RC_ADMISSIBILITY_CONTEXT_EXPIRED` | Admissibility context expired before consequential execution authorization could be completed. |
| `RC_CONTINUITY_REVALIDATION_REQUIRED` | Governance revalidation is required because of elapsed continuity window, changed conditions, or degraded execution confidence. |
| `RC_DEPENDENCY_STATE_DRIFT` | Required dependency state materially changed after governance authorization. |
| `RC_CONTINUITY_WINDOW_EXCEEDED` | The maximum allowed interval between authorization and execution opportunity was exceeded. |
| `RC_CONTINUITY_DRIFT_DETECTED` | Material execution-context drift was detected before consequential execution. |
| `RC_AUTHORITY_CONDITION_DRIFT` | Authority conditions changed after authorization and require re-evaluation before execution. |
| `RC_ENVIRONMENTAL_ASSUMPTION_INVALIDATED` | Execution assumptions were invalidated by environmental, operational, or contextual change. |
| `RC_TELEMETRY_CONTINUITY_FAILURE` | Required telemetry continuity became unavailable, corrupted, incomplete, or insufficient to support execution. |

### Reserved does not mean inactive by default

An implementation may introduce continuity-sensitive enforcement gradually.

However, a reserved continuity code must not be emitted as an active enforcement result unless the runtime can actually:

- detect the corresponding condition;
- validate it;
- explain why the code applies.

This prevents semantic claims from outrunning runtime enforcement.

---

# 13. Constraint Severity

Reason Codes are also associated with evaluated policy constraints.

The canonical constraint-severity levels are:

| Priority | Severity | Meaning |
|---:|---|---|
| **1** | `BLOCK` | Outcome must be denied or escalated. |
| **2** | `DEFER` | Outcome must be deferred pending evidence or time. |
| **3** | `DEGRADE` | Outcome is allowed only with reduced autonomy. |
| **4** | `WARN` | Outcome may remain allowed but is flagged. |
| **5** | `INFO` | Informational only; no effect on Governance Outcome. |

The normative precedence is:

```text
BLOCK
  ↓
DEFER
  ↓
DEGRADE
  ↓
WARN
  ↓
INFO
```

When multiple constraints influence one governed decision, the most restrictive applicable severity governs according to the protocol's severity semantics.

Constraint severity is recorded within the Decision Receipt Policy Evaluation Block.

---

# 14. Reason Code Usage Rules

The public v0.1 Reason Code model preserves the following rules:

1. At least one outcome Reason Code appears in every Decision Receipt.
2. Reason Codes remain reproducible and validator-consistent under identical governance conditions.
3. Governed consequential actions should include sufficient Reason Codes to reconstruct:
   - authority posture;
   - admissibility basis;
   - governed state-transition outcome.
4. Reason Codes are deterministic given identical inputs, Policy Bundles, and configuration state.
5. Reason Codes are sufficient to justify the Governance Outcome.
6. Reason Codes do not expose proprietary model internals or private reasoning artifacts.
7. Multiple Reason Codes may be emitted when multiple factors influenced the outcome.

Reason Codes should remain:

- concise;
- enumerable;
- stable across protocol versions;
- interpretable without system-specific context.

---

# 15. Multiple Reason Codes

A single Governance Outcome may be influenced by more than one material condition.

Illustrative public example:

```text
Governance Outcome:
DEFER

Reason Codes:
RC_INSUFFICIENT_EVIDENCE
RC_REQUIRES_CONFIRMATION
RC_STATE_TRANSITION_DEFERRED
```

This conveys three separate facts:

```text
Evidence is insufficient
        +
Human confirmation is required
        +
The governed state transition is deferred
```

The example is illustrative; applicable codes depend on the actual governance evaluation.

---

# 16. Reason Codes in the Decision Receipt

Canonical Reason Codes are represented through the Decision Receipt.

Relevant receipt surfaces may include:

```text
Policy Evaluation Block
        ↓
constraint.reason_code

Admissibility Block
        ↓
admissibility_reason_codes

Outcome Block
        ↓
outcome_reason_codes

Governed State Transition Context
        ↓
state-transition Reason Codes
```

Reason Codes therefore connect:

```text
Governance Evaluation
        ↓
Decision Receipt
        ↓
Executor / Validator
        ↓
Audit / Compliance / Observability
```

See [`decision-receipts.md`](decision-receipts.md).

---

# 17. Reason Codes and Deterministic Authorization

Reason Codes are part of R.E.T.N.A.'s reproducibility model.

For equivalent governance conditions, validators should be able to determine whether:

- the same canonical conditions were identified;
- the Governance Outcome is consistent;
- the Reason Codes remain coherent with that outcome;
- implementation-specific extensions did not suppress required baseline semantics.

This supports:

- deterministic replay;
- validator parity;
- governance debugging;
- audit reconstruction;
- conformance testing.

---

# 18. Vendor Extensions

Implementations may define additional Reason Codes.

Vendor extensions must preserve the canonical protocol surface.

Extension requirements include:

- canonical codes remain present when applicable;
- baseline meanings are not redefined;
- extended codes are namespaced;
- extended codes remain clearly distinguishable from canonical R.E.T.N.A. codes.

Recommended pattern:

```text
VENDORNAME_REASON_CODE
```

Illustrative examples from the specification:

```text
ACME_MODEL_TIMEOUT
ACME_SENSOR_DRIFT
```

A vendor extension must not replace an applicable canonical code merely because the vendor prefers different terminology.

---

# 19. Canonical vs. Extended Codes

Conceptually:

```text
Canonical R.E.T.N.A. Code
        ↓
Stable cross-system semantics

Vendor Extension
        ↓
Additional implementation-specific detail
```

A receipt may therefore contain:

```text
RC_EXTERNAL_DEPENDENCY_FAILURE
ACME_MODEL_TIMEOUT
```

where the canonical code provides interoperable governance meaning and the vendor extension provides optional implementation-specific detail.

---

# 20. Audit and Compliance Role

Canonical Reason Codes support:

- cross-system audit correlation;
- automated compliance validation;
- regulator-friendly inspection;
- post-incident root-cause analysis;
- validator parity;
- runtime reproducibility;
- governance testability;
- deterministic replay of authorization posture.

Because the codes are standardized, a reviewer does not need prior knowledge of proprietary system internals merely to interpret the governance condition represented by the receipt.

---

# 21. Reason Codes as an Interoperability Layer

Reason Codes provide a portable semantic layer between heterogeneous implementations.

```text
Vendor A
        │
        ├── RC_AUTHORITY_EXPIRED
        │
        └── RC_STATE_TRANSITION_BLOCKED_NO_AUTHORITY
        ↓
Canonical Receipt Semantics
        ↑
Vendor B
        │
        ├── Same canonical meanings
        │
        └── Different internal implementation
```

This allows governance evidence to remain interpretable across:

- model providers;
- agent frameworks;
- orchestration systems;
- audit platforms;
- enterprise governance systems;
- validators;
- regulators;
- domain implementations.

---

# 22. Conformance Signals

A Reason Code implementation can be externally tested.

### Presence

**Test:** produce a Decision Receipt.

**Expected:** at least one applicable outcome Reason Code exists.

### Determinism

**Test:** replay identical governance conditions.

**Expected:** canonical Reason Codes remain validator-consistent within the protocol's deterministic requirements.

### Sufficiency

**Test:** compare Reason Codes to the Governance Outcome.

**Expected:** the codes are sufficient to explain the material governance basis of the outcome.

### Non-Disclosure

**Test:** inspect Reason Code content.

**Expected:** codes identify governance conditions without exposing proprietary model internals.

### Canonical Preservation

**Test:** add vendor-specific extensions.

**Expected:** applicable canonical codes remain present.

### State-Transition Semantics

**Test:** allow transport to succeed while withholding governed state-transition authorization.

**Expected:** Reason Codes reflect the blocked or unresolved governed consequence rather than reporting transport success as authorization.

### Reserved Continuity Semantics

**Test:** emit a reserved continuity code.

**Expected:** the runtime has corresponding detection and validation capability.

---

# 23. Public Canonical Code Registry

The current public v0.1 canonical surface can be summarized as:

```text
POLICY
├── RC_POLICY_PASS
├── RC_POLICY_FAIL
└── RC_POLICY_PARTIAL

EVIDENCE / CONFIDENCE
├── RC_INSUFFICIENT_EVIDENCE
├── RC_LOW_CONFIDENCE
├── RC_EVIDENCE_STALE
└── RC_EVIDENCE_INTEGRITY_FAIL

RISK / SAFETY
├── RC_RISK_THRESHOLD_EXCEEDED
├── RC_SAFETY_GUARDRAIL
└── RC_REGULATORY_RESTRICTION

SYSTEM / DEPENDENCY
├── RC_EXTERNAL_DEPENDENCY_FAILURE
├── RC_RATE_LIMITED
└── RC_SYSTEM_DEGRADED

GOVERNANCE CONTROL
├── RC_REQUIRES_CONFIRMATION
├── RC_ESCALATION_REQUIRED
├── RC_FALLBACK_APPLIED
└── RC_HUMAN_OVERRIDE

AUTHORITY
├── RC_AUTHORITY_REQUIRED
├── RC_AUTHORITY_INVALID
├── RC_AUTHORITY_UNVERIFIED
├── RC_AUTHORITY_SCOPE_VIOLATION
├── RC_AUTHORITY_EXPIRED
└── RC_AUTHORITY_ESCALATED

ADMISSIBILITY / FORMATION
├── RC_ADMISSIBILITY_REQUIRED
├── RC_ADMISSIBILITY_FAIL
├── RC_FORMATION_REQUIRED
├── RC_FORMATION_INVALID
└── RC_FORMATION_CONTEXT_LOST

GOVERNED STATE TRANSITION
├── RC_STATE_TRANSITION_AUTHORIZED
├── RC_STATE_TRANSITION_DENIED
├── RC_STATE_TRANSITION_DEFERRED
├── RC_STATE_TRANSITION_DEGRADED
├── RC_STATE_TRANSITION_BLOCKED_NO_AUTHORITY
├── RC_STATE_TRANSITION_BLOCKED_NO_FORMATION
├── RC_STATE_TRANSITION_BLOCKED_NO_ADMISSIBILITY
├── RC_STATE_TRANSITION_BLOCKED_NO_RECEIPT
├── RC_STATE_TRANSITION_BLOCKED_PERSISTENCE_FAILURE
└── RC_STATE_TRANSITION_INVALID_RESULT

CONTINUITY / STATE DRIFT — RESERVED
├── RC_ADMISSIBILITY_CONTEXT_EXPIRED
├── RC_CONTINUITY_REVALIDATION_REQUIRED
├── RC_DEPENDENCY_STATE_DRIFT
├── RC_CONTINUITY_WINDOW_EXCEEDED
├── RC_CONTINUITY_DRIFT_DETECTED
├── RC_AUTHORITY_CONDITION_DRIFT
├── RC_ENVIRONMENTAL_ASSUMPTION_INVALIDATED
└── RC_TELEMETRY_CONTINUITY_FAILURE
```

---

# 24. What Reason Codes Are Not

Canonical Reason Codes are not:

- unrestricted natural-language explanations;
- chain-of-thought;
- raw model reasoning;
- proprietary scoring formulas;
- internal decision trees;
- substitutes for Evidence References;
- substitutes for Policy Bundle identification;
- substitutes for the Governance Outcome.

They are compact governance semantics designed for stable interpretation.

---

# 25. Public and Controlled Review

This document is part of the **public R.E.T.N.A. technical review surface**.

Related public artifacts:

- [`protocol-overview.md`](protocol-overview.md)
- [`normative-language.md`](normative-language.md)
- [`governance-boundary.md`](governance-boundary.md)
- [`system-invariants.md`](system-invariants.md)
- [`decision-receipts.md`](decision-receipts.md)
- [`STATUS.md`](../STATUS.md)
- [`NOTICE.md`](../NOTICE.md)

The complete **R.E.T.N.A. Protocol Specification — Institutional Edition**, **Governed Autonomous Intelligence Whitepaper — Institutional Edition**, and selected supporting materials remain available through controlled review.

[Request R.E.T.N.A. Controlled Review Access](https://valueintelligence.io/retna-protocol/#controlled-review-access)

Public availability of this document does not grant unrestricted implementation, certification, commercialization, sublicensing, patent, or trademark rights.

---

# 26. Next Public Artifact

The next planned technical artifact is:

```text
docs/conformance-model.md
```

It will describe the public conformance model, mandatory validation categories, negative tests, profile-specific testing, audit replay, independent verification, and the doctrine-to-test relationship between System Invariants and observable runtime behavior.

---

# 27. Protocol Status

This document reflects the public technical surface of the **R.E.T.N.A. v0.1 Draft Specification**.

The controlled specification remains authoritative for complete normative Reason Code requirements and future registry evolution.

See [`STATUS.md`](../STATUS.md) for current protocol status.

---

# 28. Stewardship

R.E.T.N.A. is developed and stewarded by:

**Value Intelligence Solutions Inc.**

The long-term objective is to advance Decision Governance Infrastructure as a vendor-neutral, enforceable, testable, and interoperable control layer for autonomous and model-driven systems.

---

© 2026 Value Intelligence Solutions Inc. All rights reserved.

**R.E.T.N.A.™ — Trademark Pending**  
**HomeSphere AI™ — Trademark Pending**  
**Smart-I-Shelf™ — Patent Pending / Trademark Pending**

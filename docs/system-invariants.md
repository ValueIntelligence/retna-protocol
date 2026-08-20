# R.E.T.N.A.™ System Invariants

**Public Technical Review Artifact — Draft v0.1**

The **System Invariants** define the protocol-level guarantees that any implementation claiming R.E.T.N.A.™ conformance for an affected decision class is expected to preserve.

They are not implementation preferences.

They define the behavioral properties that make the protocol enforceable, auditable, and interoperable across different models, agents, runtimes, vendors, and deployment environments.

> **Governance Must Precede Execution.**

> **A governance system is only as strong as the guarantees that cannot be bypassed.**

This public artifact summarizes the twelve v0.1 System Invariants and their observable implications. The controlled **R.E.T.N.A. Protocol Specification — Institutional Edition** remains the authoritative source for the complete normative requirements.

---

## 1. Why Invariants Exist

R.E.T.N.A. separates implementation freedom from protocol guarantees.

An implementation may vary in:

- programming language;
- model provider;
- agent framework;
- deployment architecture;
- policy engine;
- storage technology;
- hardware environment;
- orchestration topology.

But those implementation choices must not weaken the protocol guarantees applicable to governed decisions.

Conceptually:

```text
Implementation Freedom
        +
Mandatory Governance Guarantees
        =
R.E.T.N.A. Conformance Surface
```

The System Invariants define those mandatory guarantees.

---

## 2. Invariant Set — v0.1

The current public invariant set is:

| ID | Invariant |
|---|---|
| **I1** | Governance Boundary Integrity |
| **I2** | Mandatory Receipt Emission |
| **I3** | Trace Completeness |
| **I4** | Evidence Referencing |
| **I5** | Policy Disclosure (Structured) |
| **I6** | Outcome Determinism |
| **I7** | Tamper Awareness |
| **I8** | Separation of Duties |
| **I9** | Authority Integrity |
| **I10** | Admissibility Requirement |
| **I11** | Formation Integrity |
| **I12** | Governed State Transition Integrity |

Together, these invariants define the minimum governance properties expected from a conforming implementation.

---

# I1 — Governance Boundary Integrity

A governed decision must pass through the R.E.T.N.A. Governance Boundary before consequential execution.

The invariant protects the structural separation:

```text
Decision Construction
        ≠
Decision Execution
```

Observable implications include:

- the Governance Boundary is positioned before governed execution;
- the Executor does not act solely because it received a decision;
- a valid Governance Outcome is required before execution;
- bypass attempts result in refusal rather than silent execution;
- bypass events should remain observable through governance artifacts and Reason Codes.

### Why it matters

Without an enforced Governance Boundary, governance becomes advisory logging rather than authorization infrastructure.

### Public verification signal

Attempt to execute a governed decision without valid governance authorization.

**Expected result:** execution is refused.

See [`governance-boundary.md`](governance-boundary.md).

---

# I2 — Mandatory Receipt Emission

Every governed decision produces a **Decision Receipt**, regardless of outcome.

Receipt emission is not limited to successful execution.

The governance record also covers decisions that are:

- denied;
- deferred;
- escalated;
- degraded;
- blocked;
- otherwise prevented from execution.

### Why it matters

Accountability requires visibility into both:

```text
Actions Authorized
        +
Actions Prevented
```

A governance system that records only successful actions cannot reconstruct its own decision-control behavior.

### Public verification signal

Submit a governed decision that resolves to a non-executing outcome.

**Expected result:** a Decision Receipt still exists.

---

# I3 — Trace Completeness

Decision Receipts preserve sufficient trace information to identify the materially participating entities involved in the decision pathway.

Trace information may include:

- Producers;
- Governors;
- Executors where execution was attempted;
- models materially involved in Decision Construction;
- tools materially involved in Decision Construction;
- other materially participating actors.

Participating entities are represented through stable identifiers sufficient to support correlation and audit.

The **Dispatch Trace** may be used to represent this participation path.

### Why it matters

Partial traces undermine:

- provenance;
- accountability;
- audit reconstruction;
- incident analysis;
- cross-system correlation.

### Public verification signal

Inspect a governed Decision Receipt.

**Expected result:** materially participating entities can be identified and correlated.

---

# I4 — Evidence Referencing

Governance must remain auditable without requiring unnecessary replication of sensitive source data.

A Decision Receipt therefore preserves either:

- structured evidence summaries; or
- references to externally stored Evidence Artifacts.

Evidence references must be sufficiently specific for retrieval and verification under the applicable compliance profile.

Where references are sufficient, raw sensitive data need not be embedded directly in the receipt.

### Why it matters

Evidence must be:

```text
Traceable
        +
Verifiable
        +
Privacy-Aware
```

The protocol seeks auditability without unnecessary data exposure.

### Public verification signal

Inspect the Evidence Block or evidence references associated with a governed receipt.

**Expected result:** the governance evidence basis is identifiable without requiring indiscriminate embedding of raw sensitive data.

---

# I5 — Policy Disclosure (Structured)

Decision Receipts preserve structured information describing the policy basis of the governance determination.

This may include:

- the Policy Bundle or Bundles applied;
- applicable Policy Bundle versions;
- Policy Constraints evaluated;
- constraints that materially influenced the Governance Outcome.

Policy disclosure is intended to be structured and machine-readable.

### Why it matters

Trust requires more than knowing the final result.

A reviewer must be able to understand:

```text
What happened?
        +
Which rules governed it?
```

This does not require disclosure of proprietary internal rule-engine logic where structured policy references and material constraint results are sufficient.

### Public verification signal

Inspect the policy-evaluation portion of a receipt.

**Expected result:** applicable policy references and materially relevant constraint results are reconstructable at the required level.

---

# I6 — Outcome Determinism

Equivalent governance conditions should produce reproducible governance results within declared bounds of nondeterminism.

Relevant conditions may include:

- Payload Kind;
- inputs;
- Evidence References;
- Policy Bundles;
- configuration state;
- other declared evaluation context.

Where nondeterminism exists, it must be explicitly represented and traceable through governance artifacts.

Reason Codes must remain consistent with the resulting governance outcome.

### Why it matters

Determinism — or explicitly bounded nondeterminism — supports:

- debugging;
- audit replay;
- regulatory review;
- cross-system comparison;
- reproducible conformance testing.

### Public verification signal

Replay materially equivalent governance conditions.

**Expected result:** the Governance Outcome is reproducible within the implementation's declared bounds, and associated Reason Codes remain coherent with that result.

---

# I7 — Tamper Awareness

Decision Receipts require integrity mechanisms appropriate to the declared compliance profile.

The v0.1 profile direction includes:

| Profile | Integrity Expectation |
|---|---|
| **RETNA-A** | Basic integrity awareness; append-only or equivalent protections are recommended. |
| **RETNA-B** | Tamper-evident mechanisms are required. |
| **RETNA-C** | Cryptographic attestation or strongly equivalent integrity guarantees are required. |

Detected integrity failures must be surfaced rather than silently ignored.

### Why it matters

A receipt that can be altered without detection cannot reliably function as a governance trust artifact.

### Public verification signal

Alter or invalidate protected receipt integrity data.

**Expected result:** the integrity failure becomes detectable and is recorded or flagged according to the applicable profile.

---

# I8 — Separation of Duties

Decision Construction and Decision Governance remain logically separable functions.

They may exist within the same runtime or service, but the protocol does not require governance logic to be embedded inside model inference or private reasoning.

Conceptually:

```text
Model / Agent Reasoning
        ↓
Candidate Decision
        ↓
Independent Governance Evaluation
```

### Why it matters

Separation of duties supports:

- independent validation;
- reduced conflicts of interest;
- modular governance;
- multi-vendor interoperability;
- model independence.

### Public verification signal

Replace or change the underlying model or agent implementation.

**Expected result:** protocol-level governance can remain enforceable without requiring governance semantics to be embedded in that model's private reasoning process.

---

# I9 — Authority Integrity

Privileged or consequential execution requires an explicit and inspectable authority basis.

Authority integrity preserves sufficient information to determine matters such as:

- which actor or system asserted execution authority;
- the scope under which authority was granted;
- applicable Edge Policy constraints;
- delegated authority status;
- authority validity during governance evaluation;
- authority validity at execution commitment.

Authority conditions that are unresolved, unverifiable, contradictory, expired, or otherwise inadmissible do not silently become authorization.

Where authority materially affects the governance determination, the authorization basis remains traceable through the Decision Receipt.

### Why it matters

Execution authority cannot safely derive from:

```text
Network Position
Orchestration Topology
Transport Success
System Adjacency
```

Authority requires verifiable provenance and scope.

### Public verification signal

Submit a governed decision with missing, expired, or invalid authority.

**Expected result:** governed execution does not proceed.

---

# I10 — Admissibility Requirement

A governed decision is not execution-eligible until admissibility is explicitly evaluated and represented through canonical governance metadata.

Admissibility may evaluate:

- policy constraints;
- authority validity;
- evidence sufficiency;
- formation integrity;
- execution scope;
- risk posture;
- Edge Policy restrictions;
- anomaly conditions.

The admissibility result must remain traceable through the Decision Receipt and associated Reason Codes.

### Why it matters

A decision may be:

- well formed;
- well traced;
- evidence-backed;

and still not be permissible to execute.

Admissibility answers a separate question:

> **Is this candidate decision allowed to cross into governed consequence under the applicable conditions?**

### Public verification signal

Remove or invalidate a required admissibility determination.

**Expected result:** governed execution fails closed.

---

# I11 — Formation Integrity

Where materially relevant or required, the system preserves sufficient context describing how the candidate decision was formed before Governance Boundary enforcement.

Formation context may identify:

- upstream shaping path;
- materially participating actors;
- orchestration influences;
- tools or models materially involved;
- constraints influencing proposal formation;
- the basis upon which the candidate decision was constructed.

Formation may be represented through:

- Dispatch Trace structures;
- formation metadata blocks;
- orchestration lineage references;
- equivalent governance artifacts.

Formation requirements may vary by:

- Compliance Profile;
- Risk Class;
- Payload Kind;
- domain-specific governance policy.

### Why it matters

Formation visibility and admissibility are different governance surfaces.

```text
How was the decision formed?
        ≠
Is the decision admissible?
```

Both may be necessary for consequential governance.

### Public verification signal

Remove required formation context from a formation-sensitive governed decision.

**Expected result:** the action does not proceed unless the applicable governance requirements can still be satisfied.

---

# I12 — Governed State Transition Integrity

A governed action is not considered complete merely because it was:

- forwarded;
- routed;
- delivered;
- acknowledged;
- persisted;
- emitted as output;
- successfully transported.

Actions capable of operational, legal, financial, physical, security, or other material consequence resolve through an explicit **Governed State Transition** before execution commitment.

State-transition integrity preserves sufficient information to reason about:

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
- applicable canonical Reason Codes.

The critical distinction is:

```text
Forwarded ≠ Executed
Delivered ≠ Authorized
Persisted ≠ Permitted
Generated ≠ Governed
```

### Why it matters

R.E.T.N.A. governs consequential state transition authorization — not transport semantics.

### Public verification signal

Complete successful routing or forwarding while governed state-transition authorization remains unresolved.

**Expected result:** transport may succeed, but consequential execution remains blocked.

---

## 15. Invariant Enforcement Scope

The v0.1 System Invariants apply across:

- governed decision classes;
- RETNA-A;
- RETNA-B;
- RETNA-C;
- cloud deployments;
- edge deployments;
- embedded deployments;
- hybrid deployments.

Implementations may introduce stronger protections.

They must not weaken or bypass the invariant guarantees applicable to the claimed conformance surface.

---

## 16. Invariant Violation Semantics

Where an applicable System Invariant is violated:

```text
Invariant Violation
        ↓
Affected Decision Is Non-Compliant
        ↓
R.E.T.N.A. Conformance Must Not Be Claimed
        ↓
Remediation Should Remain Auditable
```

The invariant model therefore makes conformance falsifiable.

A system cannot preserve a conformance claim merely by logging that a mandatory invariant was violated.

---

## 17. Constitutional Role of the Invariants

The System Invariants sit above implementation details.

They constrain the behavior of:

- Producers;
- Governors;
- Executors;
- Receipt Stores;
- Policy Authorities;
- Evidence Stores;
- Attestors;
- validators;
- vendor-specific components.

This ordering is intentional.

The protocol first establishes the guarantees that must hold.

Only then does it define how actors, artifacts, flows, and implementations satisfy those guarantees.

---

## 18. Invariants as a Doctrine-to-Test Bridge

Each invariant can be mapped to observable tests.

| Invariant | Example Observable Test |
|---|---|
| **I1** | Attempt Governance Boundary bypass |
| **I2** | Verify receipt emission for non-executing outcome |
| **I3** | Verify materially participating actor trace |
| **I4** | Verify retrievable Evidence References |
| **I5** | Verify structured Policy Bundle / constraint disclosure |
| **I6** | Replay equivalent governance context |
| **I7** | Tamper with protected receipt integrity |
| **I8** | Validate governance independently of model internals |
| **I9** | Remove or expire execution authority |
| **I10** | Remove admissibility outcome |
| **I11** | Remove required formation context |
| **I12** | Allow transport while withholding state-transition authorization |

This mapping is central to the R.E.T.N.A. thesis:

```text
Doctrine
    ↓
Invariant
    ↓
Observable Behavior
    ↓
Conformance Test
    ↓
Evidence Artifact
```

---

## 19. Invariant Interdependence

The invariants are not isolated controls.

They reinforce one another.

For example:

```text
I1  Governance Boundary Integrity
        ↓
I9  Authority Integrity
        ↓
I10 Admissibility Requirement
        ↓
I12 Governed State Transition Integrity
        ↓
I2  Mandatory Receipt Emission
        ↓
I7  Tamper Awareness
```

A valid boundary without valid authority is insufficient.

Authority without admissibility is insufficient.

Admissibility without state-transition integrity is insufficient for consequential action.

A governance decision without a durable receipt weakens reconstructability.

A receipt without tamper awareness weakens trust.

The protocol therefore treats governance as a system of mutually reinforcing guarantees.

---

## 20. Invariants and Decision Receipts

Decision Receipts serve as the principal observable artifact through which many invariant guarantees become inspectable.

Examples include:

| Invariant | Receipt-Relevant Evidence |
|---|---|
| **I2** | Receipt existence |
| **I3** | Participants / Dispatch Trace |
| **I4** | Evidence Block / Evidence References |
| **I5** | Policy Evaluation Block |
| **I6** | Governance Outcome + Reason Codes + evaluation context |
| **I7** | Integrity and Audit metadata |
| **I9** | Authority Context |
| **I10** | Admissibility Block |
| **I11** | Formation Context |
| **I12** | State Context + governed state-transition metadata |

This is why the Decision Receipt is more than a log record.

It is the protocol's primary governance evidence surface.

---

## 21. Invariants and External Review

An external technical reviewer should be able to ask:

- Can governance be bypassed?
- Are denied decisions still represented?
- Can participating actors be reconstructed?
- Can evidence be verified?
- Can applied policy be identified?
- Are equivalent evaluations reproducible?
- Can receipt tampering be detected?
- Can governance remain independent of private model reasoning?
- Is execution authority explicit?
- Is admissibility explicit?
- Is decision formation visible where required?
- Is state change distinguishable from message transport?

The invariant set converts those questions into testable protocol expectations.

---

## 22. Public and Controlled Review

This document is part of the **public R.E.T.N.A. technical review surface**.

Related public artifacts:

- [`protocol-overview.md`](protocol-overview.md)
- [`normative-language.md`](normative-language.md)
- [`governance-boundary.md`](governance-boundary.md)
- [`STATUS.md`](../STATUS.md)
- [`NOTICE.md`](../NOTICE.md)

The complete **R.E.T.N.A. Protocol Specification — Institutional Edition**, the **Governed Autonomous Intelligence Whitepaper — Institutional Edition**, and selected supporting materials remain available through controlled review.

[Request R.E.T.N.A. Controlled Review Access](https://valueintelligence.io/retna-protocol/#controlled-review-access)

Public availability of this document does not grant unrestricted implementation, certification, commercialization, sublicensing, patent, or trademark rights.

---

## 23. Next Public Artifact

The next planned technical artifact is:

```text
docs/decision-receipts.md
```

It will describe the public Decision Receipt model, lifecycle, major canonical blocks, integrity expectations, and the relationship between receipts, authorization, audit, interoperability, and governed state transitions.

---

## 24. Protocol Status

This document reflects the public technical surface of the **R.E.T.N.A. v0.1 Draft Specification**.

The controlled specification remains authoritative for the complete normative requirements.

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

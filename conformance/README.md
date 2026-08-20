# R.E.T.N.A.™ Public Conformance Surface

**Public Verification Artifact — Draft v0.1**

This directory is the public entry point for R.E.T.N.A.™ conformance and validation artifacts.

Its purpose is to show how the protocol's doctrine, System Invariants, Decision Receipts, Reason Codes, and Governance Boundary can be evaluated through **observable tests and evidence artifacts**.

> **Governance trust should be demonstrable, not merely asserted.**

The public conformance surface is intentionally independent of proprietary implementation internals. It is designed so that reviewers can understand what a conforming implementation must prove without requiring access to private model reasoning, production policy logic, internal scoring methodologies, customer data, or controlled deployment code.

The controlled **R.E.T.N.A. Protocol Specification — Institutional Edition** remains authoritative for complete v0.1 normative conformance requirements.

---

## 1. Public Conformance Objective

The conformance surface connects:

```text
Doctrine
   ↓
Protocol Requirement
   ↓
System Invariant
   ↓
Runtime Enforcement
   ↓
Decision Receipt
   ↓
Canonical Reason Codes
   ↓
Conformance Test
   ↓
Evidence Artifact
```

This directory will hold public artifacts that make those relationships inspectable.

---

## 2. Current Public Verification Set

The current repository exposes:

```text
docs/
├── protocol-overview.md
├── normative-language.md
├── governance-boundary.md
├── system-invariants.md
├── decision-receipts.md
├── reason-codes.md
└── conformance-model.md

examples/
└── sample-decision-receipt.json

conformance/
└── README.md
```

The synthetic sample receipt is available at:

[`../examples/sample-decision-receipt.json`](../examples/sample-decision-receipt.json)

The public conformance model is available at:

[`../docs/conformance-model.md`](../docs/conformance-model.md)

---

## 3. What This Directory Is Intended to Prove

A mature R.E.T.N.A. implementation should be capable of producing evidence that:

- governed execution cannot bypass the Governance Boundary;
- every governed decision emits a Decision Receipt;
- required receipt fields and blocks are present;
- policy constraints materially affect Governance Outcomes;
- equivalent governance conditions are reproducible within declared bounds;
- malformed or integrity-invalid receipts are rejected;
- invalid authority cannot authorize governed execution;
- missing admissibility cannot authorize governed execution;
- required formation context is preserved;
- transport success cannot substitute for governed state-transition authorization;
- required receipt-persistence failure cannot silently fail open;
- profile-specific integrity protections are testable;
- negative conditions remain fail-closed;
- governance events can be replayed;
- independent parties can validate protocol artifacts without proprietary model access.

---

## 4. Core Conformance Test Families

The public v0.1 conformance model includes the following principal test families:

| Test Family | Primary Purpose |
|---|---|
| Governance Boundary Integrity | Verify no governed execution without prior governance |
| Receipt Emission | Verify every governed decision produces a receipt |
| Receipt Completeness | Verify required receipt structures are present |
| Policy Trigger | Verify policy constraints materially affect outcomes |
| Deterministic Outcome | Verify reproducible governance behavior |
| Receipt Validator | Verify valid receipts pass and invalid receipts fail |
| Authority Integrity | Verify invalid or expired authority cannot authorize execution |
| Admissibility Enforcement | Verify unresolved admissibility blocks execution |
| Formation Integrity | Verify required formation context remains preserved |
| Governed State Transition Blocking | Verify transport success cannot authorize consequence |
| Receipt Persistence Refusal | Verify required persistence failure blocks execution |
| Runtime Governance Validation | Verify enforcement exists at runtime rather than only in documentation |

See:

[`../docs/conformance-model.md`](../docs/conformance-model.md)

---

## 5. System Invariant Coverage

The public test surface maps to the twelve v0.1 System Invariants.

| Invariant | Public Verification Question |
|---|---|
| **I1 — Governance Boundary Integrity** | Can a governed action execute without governance? |
| **I2 — Mandatory Receipt Emission** | Does every governed evaluation emit a receipt? |
| **I3 — Trace Completeness** | Can materially participating actors be reconstructed? |
| **I4 — Evidence Referencing** | Can the evidence basis be identified and verified? |
| **I5 — Policy Disclosure (Structured)** | Can the applied policy and material constraints be reconstructed? |
| **I6 — Outcome Determinism** | Are equivalent governance conditions reproducible? |
| **I7 — Tamper Awareness** | Can receipt or evidence tampering be detected? |
| **I8 — Separation of Duties** | Can governance remain independent of private model reasoning? |
| **I9 — Authority Integrity** | Can invalid authority authorize execution? |
| **I10 — Admissibility Requirement** | Can missing admissibility authorize execution? |
| **I11 — Formation Integrity** | Is required decision-formation context preserved? |
| **I12 — Governed State Transition Integrity** | Can transport success produce consequence without state-transition authorization? |

See:

[`../docs/system-invariants.md`](../docs/system-invariants.md)

---

## 6. Public Test Case Structure

A public R.E.T.N.A. conformance case should identify enough information for repeatable review.

Recommended public structure:

```text
test_id
protocol_version
compliance_profile
governed_scope
invariant_mapping
preconditions
input_artifact
expected_governance_outcome
expected_reason_codes
expected_execution_posture
actual_result
receipt_ref
validator_result
evidence_refs
timestamp
```

Future machine-readable fixtures may use JSON or another deterministic format.

The public structure is intended to support repeatability, not disclose production secrets.

---

## 7. Test Result Semantics

A public conformance result may use a simple status vocabulary such as:

```text
PASS
FAIL
NOT_APPLICABLE
NOT_RUN
```

A `PASS` should mean that:

- the test preconditions were satisfied;
- observable behavior matched the expected protocol behavior;
- required governance artifacts were present;
- no prohibited side effect occurred.

A `FAIL` should identify the relevant test condition and preserve enough evidence for remediation.

---

## 8. Negative Testing

Negative tests are required to determine whether governance remains enforceable under invalid or degraded conditions.

Representative public negative cases include:

```text
missing evidence
malformed receipt
unauthorized Producer
unavailable Governor
invalid authority
expired authority
authority-scope violation
missing admissibility
failed admissibility
missing required formation context
invalid governed state transition
receipt persistence failure
receipt integrity failure
```

Expected posture:

```text
Required Governance Condition Fails
        ↓
No Silent Allow
        ↓
Governed Execution Does Not Proceed
        ↓
Failure Remains Observable
```

---

## 9. Fail-Closed Verification

The conformance surface explicitly separates:

```text
Technical Availability
        ≠
Execution Authority
```

Examples:

- a healthy model does not imply valid authority;
- a healthy router does not imply admissibility;
- a callable tool does not imply state-transition authorization;
- an online Executor does not imply a valid Decision Receipt;
- a healthy orchestration path does not imply receipt persistence.

The public test model therefore attempts to break governance at the point where availability could otherwise be mistaken for permission.

---

## 10. Synthetic Decision Receipt

The repository includes a synthetic public Decision Receipt:

[`../examples/sample-decision-receipt.json`](../examples/sample-decision-receipt.json)

The example is designed to illustrate how protocol concepts can be represented together:

```text
Receipt Identity
        +
Actor Identity
        +
Authority Context
        +
Decision Classification
        +
Formation Context
        +
State Context
        +
Participants / Trace
        +
Evidence
        +
Policy Evaluation
        +
Admissibility
        +
Governance Outcome
        +
Governed State Transition
        +
Integrity / Audit
```

The sample is:

- synthetic;
- non-production;
- non-customer;
- non-certifying;
- intentionally incomplete relative to the controlled schema.

It exists to provide a concrete public verification surface.

---

## 11. Decision Receipt Validation Direction

A public validator should eventually be capable of testing whether a receipt:

- contains required structures;
- declares protocol version;
- declares applicable profile information where required;
- contains a canonical Governance Outcome;
- contains required Reason Codes;
- preserves authority information where applicable;
- preserves admissibility information where applicable;
- preserves formation context where required;
- preserves governed state-transition context where applicable;
- contains required integrity metadata;
- satisfies canonicalization requirements.

The validator should reject materially invalid receipts without requiring access to proprietary model internals.

---

## 12. Reason Code Validation Direction

A public Reason Code validator should be able to determine whether:

- required canonical codes are present;
- codes are syntactically valid;
- codes remain coherent with the Governance Outcome;
- vendor extensions do not suppress applicable canonical codes;
- governed-state-transition codes reflect governed consequence rather than transport success;
- reserved continuity codes are not asserted without corresponding runtime capability.

See:

[`../docs/reason-codes.md`](../docs/reason-codes.md)

---

## 13. Compliance Profile Direction

The public conformance surface recognizes the three baseline profiles:

```text
RETNA-A
RETNA-B
RETNA-C
```

Higher profiles strengthen integrity and verification expectations.

Public examples include:

### RETNA-B

- evidence-integrity testing;
- tamper-evident receipt-storage testing.

### RETNA-C

- attestation verification;
- human-override recording;
- third-party verifiability.

The controlled specification remains authoritative for complete profile requirements.

---

## 14. Independent Verification

A key R.E.T.N.A. design objective is that a third party can inspect protocol artifacts without needing access to proprietary model internals.

An independent validator should be able to evaluate:

```text
Decision Receipt
        ↓
Structure
        ↓
Protocol Version
        ↓
Governance Outcome
        ↓
Reason Codes
        ↓
Integrity Metadata
        ↓
Profile-Specific Requirements
```

This supports review by:

- enterprise governance teams;
- auditors;
- regulators;
- insurers;
- technical diligence teams;
- incident-response teams;
- research organizations.

---

## 15. Audit Replay Direction

Conformance evidence should support later reconstruction of a governance event.

A public replay package may include references to:

- candidate decision;
- decision classification;
- Evidence References;
- Policy Bundles;
- constraint results;
- authority context;
- formation context;
- admissibility;
- Governance Outcome;
- Reason Codes;
- receipt integrity;
- execution or refusal state.

Where full replay is impossible because of volatile external dependencies, that limitation should remain explicit.

---

## 16. Evidence Artifact Preservation

A mature public conformance run should preserve:

```text
protocol version
compliance profile
governed scope
test identifier
test inputs
expected result
actual result
Decision Receipt
Reason Codes
validator output
integrity result
execution side-effect result
evidence references
timestamp
unresolved gaps
```

This converts a governance demonstration into a repeatable evidence package.

---

## 17. CI / Automated Validation Direction

Future public conformance artifacts may support automated validation of:

- receipt structure;
- canonical fields;
- receipt hashes;
- Reason Codes;
- authority requirements;
- admissibility requirements;
- formation requirements;
- state-transition blocking;
- receipt-persistence refusal;
- profile-specific integrity requirements.

A future repository structure may include:

```text
conformance/
├── README.md
├── fixtures/
│   ├── valid/
│   └── invalid/
├── tests/
└── reports/
```

These directories are **planned**, not implied to exist until they are actually published.

---

## 18. Public Conformance Evidence vs. Certification

This directory documents protocol validation and conformance concepts.

It does **not** itself establish:

- an accredited certification body;
- an approved certification program;
- a regulatory approval;
- a third-party accreditation regime;
- permission to claim "R.E.T.N.A. Certified."

Public conformance evidence and formal certification remain distinct.

See:

[`../NOTICE.md`](../NOTICE.md)

---

## 19. What This Public Surface Does Not Expose

This directory is not intended to publish:

- production governance test harnesses;
- private Policy Bundles;
- production credentials;
- customer data;
- confidential evidence;
- proprietary scoring logic;
- exploit-sensitive security details;
- private validator internals;
- controlled certification material;
- customer- or OEM-specific conformance packages.

Those materials may remain controlled or separately licensed.

---

## 20. Reviewer Quick Path

A reviewer evaluating the public R.E.T.N.A. technical surface can follow this sequence:

```text
1. README.md
        ↓
2. docs/protocol-overview.md
        ↓
3. docs/governance-boundary.md
        ↓
4. docs/system-invariants.md
        ↓
5. docs/decision-receipts.md
        ↓
6. docs/reason-codes.md
        ↓
7. docs/conformance-model.md
        ↓
8. examples/sample-decision-receipt.json
        ↓
9. conformance/README.md
```

This sequence moves from:

```text
Thesis
  ↓
Architecture
  ↓
Mandatory Guarantees
  ↓
Governance Artifact
  ↓
Machine Semantics
  ↓
Verification
  ↓
Concrete Example
```

---

## 21. Controlled Review

The complete **R.E.T.N.A. Protocol Specification — Institutional Edition**, **Governed Autonomous Intelligence Whitepaper — Institutional Edition**, and selected supporting technical, implementation, legal, regulatory, and diligence materials remain available through controlled review.

[Request R.E.T.N.A. Controlled Review Access](https://valueintelligence.io/retna-protocol/#controlled-review-access)

Public availability of this directory does not grant unrestricted implementation, certification, commercialization, sublicensing, patent, or trademark rights.

---

## 22. Protocol Status

This public conformance surface reflects the **R.E.T.N.A. v0.1 Draft Specification**.

It may evolve as implementation validation, conformance testing, interoperability work, security review, legal review, and external technical feedback continue.

See:

[`../STATUS.md`](../STATUS.md)

---

## 23. Stewardship

R.E.T.N.A. is developed and stewarded by:

**Value Intelligence Solutions Inc.**

The long-term objective is to advance Decision Governance Infrastructure as a vendor-neutral, enforceable, testable, independently verifiable, and interoperable control layer for autonomous and model-driven systems.

---

© 2026 Value Intelligence Solutions Inc. All rights reserved.

**R.E.T.N.A.™ — Trademark Pending**  
**HomeSphere AI™ — Trademark Pending**  
**Smart-I-Shelf™ — Patent Pending / Trademark Pending**

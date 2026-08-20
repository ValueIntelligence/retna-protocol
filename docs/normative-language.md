# R.E.T.N.A.™ Normative Language

**Public Technical Review Artifact — Draft v0.1**

This document explains how requirement language is used in the **R.E.T.N.A.™ Decision Governance Protocol**.

R.E.T.N.A. v0.1 contains both **Normative** and **Informative** material. Normative provisions define requirements relevant to protocol behavior and conformance. Informative material provides explanation, context, examples, rationale, or implementation guidance without independently creating a protocol requirement.

The controlled R.E.T.N.A. Protocol Specification states that the key words:

**MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **SHOULD NOT**, **RECOMMENDED**, **MAY**, and **OPTIONAL**

are to be interpreted as described in **RFC 2119** and **RFC 8174** when, and only when, they appear in all capital letters.

> Use of RFC 2119 / RFC 8174 requirement terminology does **not** mean that R.E.T.N.A. is an IETF RFC, an IETF standard, a government standard, or a formally adopted industry standard.

---

## 1. Why Normative Language Matters

R.E.T.N.A. is intended to define observable and testable Decision Governance behavior.

A protocol requirement must therefore communicate more than general intent. It must make clear whether an implementation:

- is required to perform a behavior;
- is prohibited from performing a behavior;
- is strongly recommended to perform a behavior;
- is strongly recommended not to perform a behavior; or
- may optionally support a behavior.

Normative language provides that distinction.

In R.E.T.N.A., requirement strength is especially important where protocol behavior affects:

- Governance Boundary enforcement;
- authority;
- policy evaluation;
- evidence handling;
- Decision Receipt construction;
- canonical governance outcomes;
- Reason Codes;
- governed state transitions;
- integrity and persistence;
- conformance claims.

---

## 2. Normative and Informative Material

R.E.T.N.A. documentation may explicitly identify sections as **Normative** or **Informative**.

### Normative

Normative material defines protocol requirements, prohibitions, required behaviors, or permitted implementation choices relevant to conformance.

Examples of normative subject matter include:

- whether a governed action may execute;
- whether a Governance Boundary may be bypassed;
- whether a Decision Receipt is required;
- whether an authorization result is valid;
- what an implementation must preserve for conformance.

### Informative

Informative material explains the protocol without independently imposing a conformance obligation.

Informative content may include:

- architectural rationale;
- historical context;
- examples;
- deployment guidance;
- adoption guidance;
- explanatory diagrams;
- strategic or research context.

An informative explanation does not override a normative requirement.

---

## 3. Requirement Keywords

The following table summarizes how requirement keywords are used by R.E.T.N.A. in accordance with RFC 2119 and RFC 8174 / BCP 14.

| Keyword | R.E.T.N.A. Requirement Level |
|---|---|
| **MUST** | An absolute protocol requirement. |
| **REQUIRED** | Equivalent in requirement strength to **MUST**. |
| **SHALL** | Equivalent in requirement strength to **MUST**. |
| **MUST NOT** | An absolute protocol prohibition. |
| **SHALL NOT** | Equivalent in prohibition strength to **MUST NOT**. |
| **SHOULD** | A strong recommendation; a different course may be justified only after its implications are understood and weighed. |
| **RECOMMENDED** | Equivalent in recommendation strength to **SHOULD**. |
| **SHOULD NOT** | A strong recommendation against a behavior; exceptions require careful consideration of the implications. |
| **MAY** | An optional protocol capability or behavior. |
| **OPTIONAL** | Equivalent in optionality to **MAY**. |

These summaries are provided for public technical review. The governing external definitions remain RFC 2119 and RFC 8174.

---

## 4. Uppercase Requirement Semantics

RFC 8174 clarifies the ambiguity between ordinary English usage and normative requirement keywords.

Within R.E.T.N.A. normative text, the special requirement meanings apply **only when the defined key words appear in all capital letters**.

For example:

```text
MUST
MUST NOT
SHOULD
SHOULD NOT
MAY
```

carry normative requirement meaning when used as requirement keywords.

By contrast, ordinary lowercase or mixed-case uses such as:

```text
must
should
may
```

should be read according to their ordinary language context unless the document expressly defines otherwise.

This distinction helps prevent explanatory prose from being mistaken for a conformance requirement.

---

## 5. Requirement Strength

Normative requirements can be understood as a hierarchy of obligation:

```text
Absolute requirement
        │
        ├── MUST
        ├── REQUIRED
        └── SHALL

Absolute prohibition
        │
        ├── MUST NOT
        └── SHALL NOT

Strong recommendation
        │
        ├── SHOULD
        └── RECOMMENDED

Strong recommendation against
        │
        └── SHOULD NOT

Optional behavior
        │
        ├── MAY
        └── OPTIONAL
```

The presence of an implementation preference does not weaken a **MUST** or **MUST NOT** requirement.

Similarly, an optional implementation choice introduced by **MAY** does not create permission to violate another mandatory protocol requirement.

---

## 6. Normative Language and R.E.T.N.A. Conformance

R.E.T.N.A. conformance is intended to be evaluated against observable protocol behavior.

Accordingly:

- a **MUST** requirement identifies behavior required for the applicable conformance claim;
- a **MUST NOT** requirement identifies behavior prohibited for the applicable conformance claim;
- a **SHOULD** requirement identifies expected behavior from which deviation requires a justified implementation reason;
- a **SHOULD NOT** requirement identifies behavior that is generally expected to be avoided;
- a **MAY** requirement identifies an implementation choice that is optional unless another applicable requirement makes it necessary.

A system cannot cure failure to satisfy a mandatory requirement merely by documenting that failure after execution.

R.E.T.N.A. treats governance as an enforceable protocol layer rather than a passive reporting convention.

---

## 7. Examples of Normative Structure

The examples below illustrate how requirement language operates in R.E.T.N.A.-style protocol statements.

### Mandatory Behavior

```text
A governed execution interface MUST verify that the required
governance outcome exists before consequential execution.
```

Meaning:

The behavior is required for the applicable protocol requirement.

### Prohibited Behavior

```text
A governed execution path MUST NOT silently bypass the
Governance Boundary.
```

Meaning:

The behavior is prohibited.

### Recommended Behavior

```text
An implementation SHOULD preserve sufficient evidence
references to support later governance reconstruction.
```

Meaning:

The behavior is strongly recommended. A different design requires careful consideration of the consequences.

### Optional Behavior

```text
An implementation MAY expose additional non-normative
diagnostic metadata.
```

Meaning:

The implementation may support the feature, but the feature is not independently mandatory by virtue of this statement.

> These examples are illustrative public examples and do not replace the controlled specification text.

---

## 8. Normative Language Does Not Standardize Implementation Internals

Requirement keywords define **protocol obligations**, not a mandatory internal software architecture unless the specification expressly makes an architectural property necessary for conformance.

R.E.T.N.A. does not generally use normative terminology to prescribe:

- model weights;
- prompts;
- private reasoning;
- chain-of-thought;
- programming language;
- database technology;
- cloud provider;
- agent framework;
- proprietary scoring formula;
- internal decision tree;
- vendor-specific orchestration design.

The protocol is intended to constrain the governance behavior surrounding consequential decisions while allowing heterogeneous implementations.

---

## 9. Normative Outcomes vs. Requirement Keywords

R.E.T.N.A. governance outcomes and normative requirement keywords serve different functions.

### Requirement Keywords

Terms such as:

```text
MUST
SHOULD
MAY
```

define the obligation level of a protocol requirement.

### Governance Outcomes

Terms such as:

```text
ALLOW
DENY
ESCALATE
DEFER
DEGRADE
```

represent the result of governance evaluation for a governed decision.

They are not interchangeable.

For example:

```text
The specification may state that an implementation MUST emit
a canonical governance outcome.
```

Here:

- **MUST** defines the protocol obligation;
- **ALLOW / DENY / ESCALATE / DEFER / DEGRADE** define possible governance results.

---

## 10. Normative Reason Codes and Registries

Where the Protocol requires canonical Reason Codes, Payload Kinds, receipt fields, outcome values, or other registered protocol terms, normative language determines whether support or emission is mandatory.

A registry entry and a requirement keyword therefore perform different roles:

```text
Registry
Defines the canonical term or value

        +

Normative requirement
Defines when or whether that value MUST, SHOULD, or MAY be used
```

This separation is important for machine-readable conformance.

---

## 11. Conflict and Precedence

Where public explanatory material differs from the controlled R.E.T.N.A. Protocol Specification, the controlled specification remains the authoritative source for the current v0.1 normative requirements.

Within the specification itself:

- explicit normative requirements govern applicable conformance behavior;
- informative examples do not override normative requirements;
- ordinary prose should not be interpreted as silently replacing an explicit all-uppercase requirement keyword;
- later protocol versions may revise requirements through explicit version treatment.

Public repository documentation is intended to explain the protocol surface, not silently create a different specification.

---

## 12. Standards-Body Status

R.E.T.N.A. uses established requirement terminology to improve precision and interoperability of technical interpretation.

That use does not imply:

- IETF authorship;
- IETF endorsement;
- publication as an RFC;
- ISO adoption;
- government adoption;
- regulatory certification;
- formal industry-standard status.

R.E.T.N.A. v0.1 remains an independently developed **Draft Specification** stewarded by **Value Intelligence Solutions Inc.**

See [`STATUS.md`](../STATUS.md) for the current protocol status and explicit non-claims.

---

## 13. External Normative References

R.E.T.N.A. v0.1 references the following external documents for requirement-keyword interpretation:

- **RFC 2119 — Key words for use in RFCs to Indicate Requirement Levels**  
  https://www.rfc-editor.org/rfc/rfc2119

- **RFC 8174 — Ambiguity of Uppercase vs Lowercase in RFC 2119 Key Words**  
  https://www.rfc-editor.org/rfc/rfc8174

Together, RFC 2119 and RFC 8174 are associated with **BCP 14** requirement terminology.

These external references define requirement-keyword semantics; they do not make R.E.T.N.A. an IETF specification.

---

## 14. Public and Controlled Review

This document is part of the **public technical review surface**.

The complete **R.E.T.N.A. Protocol Specification — Institutional Edition** remains available through controlled review.

[Request R.E.T.N.A. Controlled Review Access](https://valueintelligence.io/retna-protocol/#controlled-review-access)

Public availability of this document does not grant unrestricted implementation, certification, commercialization, sublicensing, patent, or trademark rights.

See:

- [`protocol-overview.md`](protocol-overview.md) — public protocol architecture overview;
- [`NOTICE.md`](../NOTICE.md) — public disclosure and rights boundary;
- [`STATUS.md`](../STATUS.md) — current protocol status.

---

## 15. Stewardship

R.E.T.N.A. is developed and stewarded by:

**Value Intelligence Solutions Inc.**

This public artifact reflects the R.E.T.N.A. v0.1 Draft Specification and may evolve through explicit repository and protocol versioning.

---

© 2026 Value Intelligence Solutions Inc. All rights reserved.

**R.E.T.N.A.™ — Trademark Pending**  
**HomeSphere AI™ — Trademark Pending**  
**Smart-I-Shelf™ — Patent Pending / Trademark Pending**

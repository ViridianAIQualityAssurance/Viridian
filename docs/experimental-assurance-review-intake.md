# Viridian Experimental Assurance Review — Async Intake

Use this intake for **one bounded experimental decision**.

The purpose is to determine whether the evidence supporting that decision is complete, comparable, reconstructable, and strong enough for the claim being made.

A live call is not required.

## Before submitting

Please avoid sending:

- passwords or API keys;
- unnecessary personal data;
- production secrets;
- customer-confidential data that is not needed for the review.

Prefer sanitized, synthetic, redacted, or public artifacts where they are sufficient.

## Required questions

### 1. What decision are you trying to make?

Examples:

- promote Candidate B over Baseline A;
- ship a new agent version;
- accept a benchmark claim;
- close a regression;
- replace an evaluator;
- treat an observed improvement as confirmed.

**Required response**

Describe the exact decision in one or two sentences.

---

### 2. What exact claim would you make if the review passes?

Examples:

> Candidate B improves task success over Baseline A under evaluation protocol P.

> Regression R is fixed and can be closed.

> Evaluator E can replace the current grader for release decisions.

**Required response**

Write the strongest claim the current evidence is expected to support.

This matters because Viridian reviews evidence **against the claim**, not just the score.

---

### 3. What evidence currently supports that claim?

Please identify the available artifacts.

Useful examples include:

- baseline/candidate run outputs;
- per-case scores;
- evaluator outputs and rationales;
- model/checkpoint identities;
- dataset or benchmark version;
- prompt/rubric identity;
- code commit;
- environment/dependency version;
- failure/timeout records;
- repeated-run results;
- held-out confirmation;
- logs or trace artifacts;
- existing postmortem or issue.

**Required response**

List what exists and what is missing.

Do not hide missing evidence. UNKNOWN is a valid input to an assurance review.

---

### 4. What changed between the relevant runs or versions?

Examples:

- model/checkpoint;
- prompt/system instruction;
- evaluator;
- benchmark;
- dataset split;
- tools;
- timeout/retry policy;
- environment;
- code/harness;
- sampling settings;
- context budget.

**Required response**

List every known material change.

If you do not know whether something changed, write **UNKNOWN**.

---

### 5. What would a useful written outcome look like?

Choose the most relevant result:

- **Claim supported within stated scope**
- **Claim contradicted / protected regression found**
- **UNKNOWN / insufficient evidence**
- **Comparator not valid**
- **Evaluator evidence not qualified**
- **Historical evidence needs remeasurement**
- **Specific remediation / next experiment required**

Then explain what internal decision the report would unlock.

## Optional metadata

These fields improve triage but are not required for the first contact:

- organization;
- team;
- role;
- public website/domain;
- relevant repository/issue;
- approximate experiment volume;
- whether the case is development, release, research publication, or production;
- whether procurement/security review would be required after technical validation.

## Triage criteria

A case is a strong fit for a Viridian review when:

- there is a concrete experimental/release decision;
- the team can supply enough artifact identity to inspect the evidence;
- comparator/evaluator/provenance/confirmation uncertainty matters;
- the result would change a real technical or commercial decision.

A case is a weak fit when:

- the request is only general advice;
- there is no concrete claim;
- no evidence can be supplied;
- the desired outcome is a guarantee of truth, safety, or compliance;
- the team expects unlimited unpaid custom engineering.

## Review output

A bounded Experimental Assurance Review should return:

1. the requested claim;
2. evidence inventory;
3. identity/provenance findings;
4. comparator/evaluator findings;
5. missingness/UNKNOWN;
6. affected and surviving evidence;
7. strongest currently admissible claim;
8. remediation / next evidence required;
9. explicit scope and capability limitations.

## Commercial boundary

Public Viridian checklists and examples are free.

Customer-specific analysis, qualification, integration, or a live workflow pilot is separately scoped.

The purpose of the intake is to determine the **smallest bounded engagement** that can answer a material decision, not to create an open-ended consulting project.

## Existing public intake

Viridian's current public Google Form remains the intake surface while this question set is adopted:

[Request an Experimental Assurance Audit](https://docs.google.com/forms/d/e/1FAIpQLScRhl7hZfzJbxi2ittQ2nNGawK9X_c67ERjhBrIVsmPuxsGxg/viewform)

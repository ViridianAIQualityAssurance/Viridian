# Viridian Sample Assurance Output v1

> Synthetic public fixture. This document demonstrates the output shape of a bounded Viridian assurance review. It is not a real customer result and does not claim that the underlying models or organizations exist.

## Case

**Proposed claim**

> Candidate B improves task success over Baseline A and is ready for promotion.

**Requested decision**

Can the supplied evidence support that promotion claim?

## Determination

# UNKNOWN — CLAIM NOT YET ADMISSIBLE

The candidate's observed score is higher, but the supplied evidence does not establish a valid comparative promotion claim.

Viridian preserves the positive observation while bounding the conclusion.

## 1. Observed evidence

| Evidence item | Baseline | Candidate | Status |
|---|---|---|---|
| Aggregate score | 0.71 | 0.79 | OBSERVED |
| Raw delta | — | +0.08 | OBSERVED |
| Model identity | model-A@rev-44 | model-B@rev-19 | PRESENT |
| Dataset name | eval-set | eval-set | PRESENT |
| Dataset version | v3 | **missing** | UNKNOWN |
| Evaluator | judge-v5 | judge-v6 | NON-COMPARABLE |
| Evaluator rubric | rubric-12 | rubric-12 | PRESENT |
| Repeated trials | 3 | 3 | PRESENT |
| Protected confirmation | none | none | MISSING |

## 2. Findings

### F-001 — Evaluator identity changed

**Type:** comparator qualification  
**Severity:** material  
**Evidence:** baseline used `judge-v5`; candidate used `judge-v6`.

A score difference cannot be attributed to the candidate model alone while the measurement system changed materially between arms.

**Effect on claim:** blocks the comparative improvement claim.

### F-002 — Candidate dataset version is unknown

**Type:** evidence identity / population  
**Severity:** material  
**Evidence:** candidate run identifies the dataset name but not the required version.

Viridian cannot establish that both arms evaluated the same population.

**Effect on claim:** blocks comparator qualification.

### F-003 — No protected confirmation

**Type:** confirmation boundary  
**Severity:** material for promotion  
**Evidence:** the supplied runs are development/selection evidence only.

A promising development result is not the same thing as independent confirmation.

**Effect on claim:** blocks final promotion authority.

## 3. Evidence lineage

```text
baseline run
 ├─ model-A@rev-44
 ├─ eval-set@v3
 ├─ judge-v5
 └─ score 0.71
                     X  comparator qualification blocked
          /
candidate run
 ├─ model-B@rev-19
 ├─ eval-set@UNKNOWN
 ├─ judge-v6
 └─ score 0.79
```

The raw observations remain in the record.

The blocked comparison is a statement about **authority**, not deletion.

## 4. Claim analysis

### Proposed claim

> Candidate B improves task success over Baseline A and is ready for promotion.

**Status:** NOT ADMISSIBLE FROM CURRENT EVIDENCE

### Strongest currently supportable statement

> Candidate B produced a score of 0.79 versus 0.71 for Baseline A in the supplied runs. Because evaluator identity changed and the candidate dataset version is missing, the evidence does not yet establish that the +0.08 difference represents a valid model improvement. No protected confirmation was supplied.

## 5. What would change the determination?

At minimum:

1. establish the exact candidate dataset version;
2. rerun baseline and candidate with materially equivalent evaluator identity/configuration, or independently qualify evaluator equivalence;
3. preserve exact run/evaluator/dataset identities;
4. execute the frozen candidate on protected confirmation evidence not used to select it;
5. confirm that no protected regression gate fails.

## 6. Decision table

| Gate | Result | Consequence |
|---|---|---|
| Evidence identity complete | UNKNOWN | Cannot fully reconstruct candidate population |
| Comparator fairness | FAIL | Improvement attribution blocked |
| Repeated-run evidence | PASS | Useful development evidence retained |
| Protected regression | UNKNOWN | No final promotion authority |
| Protected confirmation | FAIL / missing | Promotion claim blocked |
| Final claim eligibility | UNKNOWN | Do not promote on supplied evidence alone |

## 7. Machine-readable summary

```json
{
  "case_id": "public-fixture-001",
  "requested_claim": "Candidate B improves task success over Baseline A and is ready for promotion.",
  "verdict": "UNKNOWN",
  "observations": {
    "baseline_score": 0.71,
    "candidate_score": 0.79,
    "raw_delta": 0.08
  },
  "blocking_findings": [
    {
      "id": "F-001",
      "type": "comparator",
      "reason": "evaluator_identity_changed"
    },
    {
      "id": "F-002",
      "type": "evidence_identity",
      "reason": "candidate_dataset_version_missing"
    },
    {
      "id": "F-003",
      "type": "confirmation",
      "reason": "protected_confirmation_missing"
    }
  ],
  "claim_status": "NOT_ADMISSIBLE",
  "next_evidence": [
    "candidate dataset version",
    "equivalent or qualified evaluator regime",
    "protected confirmation run"
  ]
}
```

## 8. Scope disclosures

This sample does not claim to:

- prove either score is wrong;
- perform statistical significance testing;
- rerun the model;
- independently qualify arbitrary judges;
- certify regulatory compliance;
- prove Candidate B is unsafe;
- prove Candidate B is worse;
- convert UNKNOWN into FAIL merely because evidence is incomplete.

## 9. Why this output shape matters

The output separates four things that dashboards often collapse:

1. **what happened** — the raw observations;
2. **what is missing or non-comparable** — the findings;
3. **what the evidence may support** — the claim ceiling;
4. **what would change the answer** — the next evidence requirement.

That is the core role of experimental assurance.

# EIR-002 — Evidence Misassociation in Asynchronous Evaluation

**Series:** Viridian Experimental Integrity Reports  
**Case:** Memgraph AI Toolkit context-graph evaluation  
**Failure class:** result-to-example misassociation  
**Severity:** High experimental-integrity exposure  
**Status:** Public-source analysis

## Executive summary

Memgraph AI Toolkit documented an evaluation bug in which judge results were paired with goldens by list position even though the evaluator returned results in **asynchronous completion order**.

That meant a score and judge rationale could be attached to the wrong question while the aggregate run still looked plausible.

Memgraph's issue reports that:

- a reproduced 12-case concurrent run returned results out of input order;
- in saved 100-question runs, **11–24 questions** had a Contextual Recall reason quoting a different question's expected answer;
- aggregate run totals were roughly preserved by the within-group permutation;
- **every per-question and per-type result was wrong**;
- the fix changed result association to use the golden's stable name rather than completion position;
- the regression test fails on the old implementation and passes on the fix.

Primary sources:

- [Issue #387 — judge scores were attributed to the wrong questions](https://github.com/memgraph/ai-toolkit/issues/387)
- [PR #388 — match judge scores to their question](https://github.com/memgraph/ai-toolkit/pull/388)
- [Issue #390 — corrected-scoring follow-on map](https://github.com/memgraph/ai-toolkit/issues/390)
- [Issue #391 — corrected hybrid-retrieval measurement](https://github.com/memgraph/ai-toolkit/issues/391)

## 1. Observed public facts

Memgraph reports that `runner._judge_group` paired Deepeval `result.test_results` with input goldens using positional `zip(...)`.

Under async concurrency, Deepeval returned results in completion order rather than the input order.

A fake metric with random latency reproduced the ordering mismatch.

Memgraph also reports that saved runs showed judge reasons referring to another question's expected answer.

The important distinction is:

- the **judge output itself could be valid** for the case it actually evaluated;
- the **association between that output and the recorded question identity was invalid**.

That is a provenance failure rather than merely a bad score.

## 2. Why aggregate metrics can hide the failure

A positional permutation can preserve an aggregate count while destroying case-level meaning.

Memgraph explicitly notes that totals were roughly preserved because results were permuted within judged groups, although a later retrieval-floor operation prevented perfect preservation.

This is a dangerous failure shape because a dashboard may look numerically stable while:

- case-level failure analysis is wrong;
- category/type breakdowns are wrong;
- regression localization is wrong;
- decisions about which cases improved or regressed are unsupported.

## 3. Affected and surviving evidence

### Affected

According to Memgraph's issue:

- every per-question result from the affected runs;
- every per-type result derived from those question associations;
- prior readings that depended on question-level pass rates or stability.

### Potentially surviving

Subject to reconstruction:

- underlying question/golden definitions;
- raw judge outputs;
- aggregate totals to the limited extent they are invariant to the permutation;
- raw model outputs;
- historical run identities;
- corrected runs after the association fix.

Surviving artifacts remain useful only if their identities allow the correct relationship to be reconstructed.

## 4. Viridian Advanced V5 mapping

### 4.1 Stable evidence identity

Every evaluation case should receive a stable identity before execution.

Every downstream artifact should carry that identity:

- model output;
- evaluator request;
- evaluator result;
- rationale;
- score;
- failure state;
- derived aggregate.

Completion order should not be permitted to substitute for evidence identity.

### 4.2 Evidence-association validation

An assurance layer can require that:

- each expected case ID appears exactly once where required;
- unknown case IDs are rejected;
- duplicate IDs are rejected;
- missing IDs remain explicit;
- result-to-case joins are keyed on identity rather than position.

### 4.3 Evaluator provenance

The record should preserve the evaluator/judge identity and configuration separately from the evaluated system.

This matters because the evaluator is part of the evidence-producing apparatus, not an oracle outside the experiment.

### 4.4 Historical taint

Once the association defect is discovered, affected historical per-case evidence should not silently remain authoritative.

The appropriate response is to mark or bound the affected lineage and remeasure the claims that depend on it.

### 4.5 Reconstruction

If raw outputs and stable identities were preserved, some affected evidence may be repairable without rerunning the expensive model generation step.

If stable identity was never retained, rerunning may be the only defensible way to restore case-level evidence.

## 5. What Viridian cannot infer from the public case

This report does not claim:

- every aggregate score from the affected Memgraph runs was unusable;
- the evaluator model itself was wrong;
- Viridian would automatically repair arbitrary third-party evaluator outputs;
- every asynchronous evaluation framework has this failure;
- the corrected retrieval method is objectively better outside the measured benchmark.

The public issue itself distinguishes approximately preserved totals from invalid per-question and per-type attribution.

## 6. Corrective action taken by Memgraph

PR #388 changed the matching behavior so test cases carry the golden's name and results are matched by that identity.

Memgraph reports:

- a regression test that fails on the old implementation;
- two consecutive successful evaluation-suite runs on the same instance;
- **246 passing tests**;
- additional changes to use fixed judge rubric steps and minimum supported effort.

The fix is important because it changes the evidence relationship from:

> input position → completion position

to:

> stable case identity → returned result identity

## 7. Why this is commercially relevant

No financial-loss estimate is asserted.

The commercial exposure class includes:

- wasted analysis on corrupted per-case evidence;
- invalid regression localization;
- incorrect product/research prioritization by category;
- expensive reruns when raw evidence cannot be reconstructed;
- reduced confidence in benchmark claims.

## 8. Verification questions for other teams

1. Does every test case have a stable immutable ID before async execution begins?
2. Does every evaluator result carry that ID back?
3. Are joins performed by identity rather than ordering?
4. What happens to missing, duplicate, or unknown IDs?
5. Can every aggregate score be traced back to its exact per-case evidence?
6. If a mapping bug is found, can historical evidence be reconstructed?
7. Which downstream claims must be remeasured rather than merely relabeled?

## 9. Viridian determination

**Failure class:** evidence/result misassociation  
**Experimental severity:** High  
**Primary affected authority:** per-case and per-type conclusions  
**Primary control:** stable evidence identity + provenance-preserving joins + historical taint/reconstruction

---

This case is materially different from EIR-001. EIR-001 is a **control/comparator identity failure**. EIR-002 is an **evidence-association/provenance failure**.

Together they demonstrate why experimental assurance cannot be reduced to a single aggregate score.

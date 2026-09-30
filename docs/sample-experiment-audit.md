# Sample Viridian Experiment Audit

> Illustrative assurance report. This example shows the structure of a Viridian review; it is not a claim about a real customer or model.

## Proposed claim

**Candidate B improves task success over Baseline A and is ready for promotion.**

## Assurance decision

**NOT YET SUPPORTED**

The observed result may be promising, but a higher score alone is not enough to support the promotion claim. The evidence package below separates what was observed from what can defensibly be concluded.

## Evidence reviewed

| Control | Status | Audit question |
|---|---|---|
| Exact candidate identity | PASS | Is the candidate model/code/config identity frozen and reconstructable? |
| Exact baseline identity | PASS | Is the comparator identity frozen rather than described loosely? |
| Dataset / task identity | PASS | Are inputs and versions pinned? |
| Comparator fairness | REVIEW | Were both arms given equivalent budgets, tools, prompts and stopping rules? |
| Repeated trials | REVIEW | Is the apparent gain larger than run-to-run variation? |
| Evaluator integrity | REVIEW | Can scores be traced to the correct examples and evaluator version? |
| Negative evidence | PASS | Are failures retained rather than silently excluded? |
| Held-out confirmation | MISSING | Was the final claim confirmed on evidence not used during iteration? |
| Provenance / reconstruction | PASS | Can the run be reconstructed from recorded artifacts? |

## Why promotion is blocked

### 1. Discovery is not confirmation

If Candidate B was selected because it performed best on the same tasks now being used to justify promotion, those results are discovery evidence. They are useful for choosing what to test next, but they are not independent confirmation.

### 2. Variance has not been bounded

A single aggregate score does not distinguish a real improvement from stochastic variation. Repeat both arms under the same protocol and preserve the full outcome distribution.

### 3. Comparator fairness must be explicit

Before interpreting the delta, verify that Baseline A and Candidate B received materially equivalent conditions: tool access, token/time budget, evaluator, task set, retries, stopping rules and environment.

### 4. Evaluator integrity is part of the experiment

A judge can produce plausible numbers while associating results with the wrong example, using a changed rubric, or silently failing. Preserve per-example evidence and evaluator identity so aggregate scores can be audited back to source outcomes.

### 5. Final confirmation is still missing

Freeze the candidate and protocol, then run a held-out confirmation that was not used to choose Candidate B. Promotion should depend on that result, not on the discovery run.

## Required next experiment

1. Freeze Baseline A and Candidate B identities.
2. Freeze the comparison protocol and evaluator.
3. Run repeated, interleaved trials under equivalent conditions.
4. Preserve per-trial outcomes, failures and evaluator evidence.
5. Estimate the candidate-baseline effect together with its uncertainty.
6. Run one untouched held-out confirmation after the candidate is frozen.
7. Promote only if the predeclared confirmation rule passes.

## Claim ceiling

Until the missing controls are satisfied, the strongest defensible statement is:

> Candidate B produced a promising observed improvement under the current experiment, but the evidence is not yet sufficient to claim a confirmed improvement or authorize promotion.

That distinction is the purpose of experiment assurance: preserve useful results without allowing an experiment to claim more than its evidence supports.

---

Viridian is an experimental-assurance layer for AI teams. It sits around existing training and evaluation stacks to make improvement claims reproducible, auditable and defensible.

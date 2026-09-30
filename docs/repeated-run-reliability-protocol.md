# Repeated-Run Reliability Protocol

A single successful evaluation run is evidence that a system *can* succeed. It is not evidence that the system is reliable.

This protocol is a lightweight way to decide whether an apparent model, prompt, agent, or harness improvement survives repeated execution.

## 1. Freeze the comparison before running

Record, for both baseline and candidate:

- model/provider and exact version where available
- prompt/system-instruction identity
- agent code commit
- tool and dependency versions
- evaluator/judge identity and configuration
- dataset or case-set identity
- sampling settings
- environment/runtime identity
- retry, timeout, fallback, and missing-result policy

Do not change these during the comparison without starting a new comparison identity.

## 2. Define the claim

Write the claim before looking at results.

Examples:

- "Candidate B improves task success without increasing critical failures."
- "The new prompt reduces tool-selection errors."
- "The new model is no worse on the protected regression set."

Define the primary metric, protected metrics, failure conditions, and promotion rule in advance.

## 3. Run both arms repeatedly

Use the same cases and equivalent execution conditions for baseline and candidate.

For stochastic systems, one run per case is usually insufficient. Choose a repeat count appropriate to cost and consequence, and record it before execution.

Where ordering or infrastructure drift could bias results, interleave baseline and candidate runs rather than completing one arm first.

## 4. Preserve run-level evidence

For every run retain enough evidence to reconstruct what happened:

- case ID
- arm (baseline/candidate)
- attempt number
- inputs
- outputs
- tool calls / trace where applicable
- evaluator result and rationale where applicable
- errors, retries and timeouts
- latency/cost if relevant
- exact identities from section 1

Do not retain only the final aggregate score.

## 5. Treat missingness as evidence

A timeout, evaluator failure, malformed result, exhausted retry budget, or unavailable tool is not automatically a pass and should not silently disappear from the denominator.

Declare the missing-result policy before the run and report missingness by arm.

## 6. Separate capability from reliability

Report both:

- whether the system succeeds at least sometimes
- how consistently it succeeds across repeats

A candidate that raises best-case performance while increasing variance may be worse for a production workflow.

At minimum report per-arm success rate, failure rate, missing rate, and dispersion across repeats. For material decisions, add an uncertainty interval or an appropriate statistical comparison.

## 7. Inspect regressions, not just the mean

Before promotion, check:

- protected/critical cases
- newly introduced failure modes
- cases that flip repeatedly between pass and fail
- evaluator disagreement or instability
- performance changes hidden by aggregate improvements

A higher average score does not erase a critical regression.

## 8. Confirm on held-out evidence

If the candidate was selected using the same cases used to declare victory, the result is discovery evidence.

Use a held-out or otherwise protected confirmation set for the final promotion claim where feasible. Preserve its identity and keep it outside iterative tuning.

## 9. Promotion record

A defensible promotion record should state:

- exact baseline and candidate identities
- predeclared claim and decision rule
- repeat count and case count
- aggregate results plus uncertainty
- missing/error counts
- protected-case results
- held-out confirmation result
- known limitations
- final promote / reject / unknown decision

If the evidence is insufficient, record **UNKNOWN** rather than forcing a winner.

---

This protocol is intentionally framework-agnostic. It can sit around an existing evaluation stack rather than replace it.

Related Viridian resources:

- [Experiment Validity Checklist](experiment-validity-checklist.md)
- [Benchmark Evidence Manifest Template](benchmark-evidence-manifest-template.md)
- [Evaluator Integrity Failure Modes](evaluator-integrity-failure-modes.md)
- [Sample Experiment Audit](sample-experiment-audit.md)

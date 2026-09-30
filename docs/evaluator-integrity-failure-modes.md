# Evaluator Integrity Failure Modes

A model-evaluation pipeline can execute successfully and still produce evidence that should not support a release or improvement claim.

This checklist focuses on failures in the evaluator itself: cases where the scoring or evidence pipeline silently changes what a result means.

## 1. Result-to-example misassociation

**Failure:** asynchronous or parallel evaluation results are joined to examples by completion order, list position, or another unstable key.

**Why it matters:** a correct score can become evidence for the wrong prompt, expected answer, or test case.

**Control:** assign an immutable example ID before execution and require every score, trace, judge rationale, and artifact to carry it through the full pipeline. Reject joins with missing, duplicated, or unknown IDs.

## 2. Judge identity drift

**Failure:** the judge model, prompt, decoding settings, rubric, or provider revision changes between compared runs.

**Why it matters:** an apparent model improvement may actually be an evaluator change.

**Control:** persist judge identity and configuration with every result. Treat a changed judge as a new evaluation regime unless equivalence is independently established.

## 3. Comparator asymmetry

**Failure:** candidate and baseline do not receive the same task set, preprocessing, tool availability, retry policy, context, timeout, or scoring path.

**Why it matters:** the comparison measures multiple changes at once.

**Control:** freeze shared experimental conditions and record intentional differences explicitly. Prefer interleaved or paired comparisons when practical.

## 4. Missingness hidden as success

**Failure:** timeouts, parser failures, judge errors, dropped rows, or unavailable artifacts disappear from aggregate metrics.

**Why it matters:** the reported denominator no longer represents the attempted experiment.

**Control:** make missingness typed and visible. Report attempted, completed, failed, excluded, and unknown outcomes separately. Never silently convert missing evidence into a pass.

## 5. Stale evidence after a fix

**Failure:** an evaluator bug is corrected, but historical scores produced by the broken evaluator remain mixed with corrected results.

**Why it matters:** downstream summaries and decisions can continue relying on invalid evidence.

**Control:** preserve evaluator version and evidence lineage. Taint affected historical results and require re-evaluation before they can support new claims.

## 6. Aggregate-only evidence

**Failure:** only a final average, pass rate, or leaderboard score is retained.

**Why it matters:** it becomes difficult to reconstruct which examples moved, identify corrupted rows, audit judge behavior, or test alternative aggregation rules.

**Control:** retain per-example outcomes, stable identities, relevant traces, evaluator outputs, exclusions, and configuration alongside aggregates.

## 7. Unmeasured evaluator variance

**Failure:** a stochastic judge or nondeterministic harness is treated as deterministic.

**Why it matters:** small apparent gains can be evaluator noise.

**Control:** measure repeated-run variance where nondeterminism exists. Define the promotion threshold before observing the candidate result and require the claimed effect to clear the relevant uncertainty.

## 8. Evidence that cannot be reconstructed

**Failure:** a result cannot be reproduced because model, dataset, prompt, code, environment, or evaluator identities were not retained.

**Why it matters:** the number may be real, but its experimental meaning cannot be independently checked.

**Control:** store immutable or content-addressed identities for the evidence-producing components and enough provenance to reconstruct the run.

## Minimal promotion gate

Before a result is allowed to support a model or agent promotion, ask:

- Can every score be traced to the exact example that produced it?
- Are candidate and baseline evaluator conditions equivalent?
- Are failures and missing results explicit?
- Is evaluator identity frozen and recorded?
- Has evaluator variance been measured where relevant?
- Are affected historical results tainted after evaluator defects?
- Can the evidence be reconstructed from retained artifacts?

If any answer is **unknown**, the safest conclusion is not “fail.” It is **insufficient evidence for the claim**.

---

Viridian is an experimental-assurance layer for AI teams. This document is a reusable engineering checklist, not a claim that any particular evaluation framework is defective.

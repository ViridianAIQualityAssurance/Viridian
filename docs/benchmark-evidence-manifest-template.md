# Benchmark Evidence Manifest Template

A compact, tool-agnostic manifest for recording enough evidence to make an AI benchmark result inspectable, comparable, and reconstructable.

This is not a benchmark runner. It is a record of **what was actually compared, under which conditions, with which evaluator, and what evidence survived the run**.

## 1. Run identity

- Run ID:
- Timestamp (UTC):
- Repository / project:
- Code commit:
- Runner / harness version:
- Environment image or lockfile digest:
- Hardware / accelerator:
- Operator or automation identity:

## 2. Subject under test

- Model / agent name:
- Exact model identifier:
- Model revision / checkpoint digest:
- Adapter / system prompt / policy revision:
- Inference configuration:
- Tool configuration:
- External service versions:

## 3. Benchmark identity

- Benchmark name:
- Benchmark version / commit:
- Dataset revision / digest:
- Split:
- Number of eligible cases:
- Number attempted:
- Number completed:
- Number excluded:
- Exclusion reasons:
- Missing-result policy:

A score without the exact benchmark and split identity is not a reconstructable result.

## 4. Comparator fairness

For every arm being compared, record whether these were identical or intentionally different:

- Dataset and split
- Case ordering / sampling
- Token / time / tool budgets
- Retry policy
- Temperature / sampling policy
- System instructions
- Tool access
- Environment
- Evaluator
- Failure handling

Document every intentional asymmetry and why it does not invalidate the comparison.

## 5. Evaluator identity

- Evaluator type:
- Judge model / version:
- Rubric version / digest:
- Parser / scorer version:
- Randomness settings:
- Calibration or control cases:
- Known evaluator limitations:

If evaluation is asynchronous, verify that outputs are associated with cases by stable identity rather than completion order.

## 6. Repetition and variance

- Number of independent trials:
- Seed policy:
- Per-trial scores:
- Mean / median:
- Dispersion measure:
- Confidence interval or uncertainty estimate:
- Known nondeterministic components:

Do not collapse repeated trials into one number before preserving the individual outcomes.

## 7. Failure accounting

Count and retain:

- Model failures
- Tool failures
- Timeouts
- Harness failures
- Evaluator failures
- Missing outputs
- Invalid outputs
- Retries
- Exclusions

A failed run is evidence. Do not silently turn infrastructure failures into missing rows or successful zeros.

## 8. Held-out confirmation

- Was the final claim checked on data not used for tuning or selection?
- Was the holdout identity protected before promotion?
- Who or what could access it?
- Was the final candidate evaluated once or repeatedly?
- Did the held-out result agree with the selection result?

## 9. Preserved artifacts

Record paths, object IDs, or digests for:

- Raw model outputs
- Per-case evaluator outputs
- Per-case scores
- Logs
- Configurations
- Environment manifest
- Dataset manifest
- Failure records
- Summary report

Prefer immutable or content-addressed evidence where practical.

## 10. Promotion decision

- Candidate:
- Baseline:
- Observed delta:
- Uncertainty:
- Regression checks:
- Held-out confirmation:
- Decision: PROMOTE / REJECT / INCONCLUSIVE
- Decision reason:
- Known limitations:

**INCONCLUSIVE is a valid result.** If evidence is missing, comparators are unfair, evaluator integrity is uncertain, or the result cannot be reconstructed, do not force a positive/negative claim.

---

Viridian treats experimental assurance as a layer around existing training and evaluation stacks: preserving identities, evidence, comparison validity, failure semantics, and promotion logic so that an apparent improvement can be defended later.

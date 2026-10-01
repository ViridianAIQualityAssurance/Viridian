# Viridian

Viridian is an experimental-assurance layer for AI teams.

Evaluation systems can tell you the scores. Viridian asks a different question:

> **Does the evidence actually support the conclusion you are about to make?**

It sits around existing training and evaluation stacks and focuses on evidence identity, comparability, evaluator integrity, reproducibility, regressions, provenance, confirmation boundaries, and claim scope.

## Experimental Assurance Audit

The clearest public example is a synthetic model comparison where the candidate scores **0.79** and the baseline scores **0.71**.

Viridian preserves the +0.08 observation, but returns **INSUFFICIENT_EVIDENCE** because the evaluator identity/version differs between runs and the required dataset version is missing.

**[Read the Experimental Assurance Audit sample](docs/experimental-assurance-audit-model-comparison.md)**

The point is simple: a higher score is not automatically a defensible improvement claim.

## Public technical resources

- [Experimental Assurance Audit — model comparison sample](docs/experimental-assurance-audit-model-comparison.md)
- [Sample experiment audit](docs/sample-experiment-audit.md)
- [Experiment validity checklist](docs/experiment-validity-checklist.md)
- [Evaluator integrity failure modes](docs/evaluator-integrity-failure-modes.md)
- [Benchmark evidence manifest template](docs/benchmark-evidence-manifest-template.md)
- [Repeated-run reliability protocol](docs/repeated-run-reliability-protocol.md)

## Bounded written audits

Have one evaluation, model-comparison, regression, benchmark, or release claim you do not completely trust?

Viridian can assess one bounded case asynchronously from the supporting artifacts and return a written assurance determination.

No live demo or meeting is required.

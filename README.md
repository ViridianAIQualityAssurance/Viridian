# Viridian

Viridian is an experimental-assurance layer for AI teams.

Evaluation systems can tell you the scores. Viridian asks a different question:

> **Does the evidence actually support the conclusion you are about to make?**

It sits around existing training and evaluation stacks and focuses on evidence identity, comparability, evaluator integrity, reproducibility, regressions, provenance, confirmation boundaries, and claim scope.

## Experimental Assurance Audit

The clearest public example is a synthetic model comparison where the candidate scores **0.79** and the baseline scores **0.71**.

Viridian preserves the +0.08 observation, but returns **INSUFFICIENT_EVIDENCE** because the evaluator identity/version differs between runs and the required dataset version is missing.

**[Read the Experimental Assurance Audit sample](docs/experimental-assurance-audit-model-comparison.md)**

**[Request an Experimental Assurance Audit](https://docs.google.com/forms/d/e/1FAIpQLScRhl7hZfzJbxi2ittQ2nNGawK9X_c67ERjhBrIVsmPuxsGxg/viewform)**

The point is simple: a higher score is not automatically a defensible improvement claim.

## Experimental Integrity Reports

Viridian also analyzes public experimental failures as evidence-governance cases.

The reports separate:

- observed public facts;
- affected evidence;
- affected claims;
- evidence that still survives;
- the relevant assurance control;
- what Viridian cannot infer from the case.

Current reports:

- [EIR-001 — DEBEDb control-set omission and comparator invalidity](docs/eir-001-debedb-control-set-omission.md)
- [EIR-002 — Memgraph asynchronous evidence misassociation](docs/eir-002-memgraph-evidence-misassociation.md)

These are technical case analyses, not security vulnerability disclosures.

## Advanced V5 qualification and diligence

- [Advanced V5 Qualification Evidence Pack — public summary](docs/advanced-v5-qualification-evidence-pack.md)
- [Security & Diligence Overview](docs/security-and-diligence-overview.md)
- [Security Policy](SECURITY.md)
- [NIST AI RMF evidence crosswalk](docs/nist-ai-rmf-crosswalk.md)

The qualification material states both what has been tested and what remains explicitly outside scope.

## What a Viridian result looks like

- [Canonical sample assurance output v1](docs/sample-assurance-output-v1.md)
- [Experimental Assurance Review — async intake](docs/experimental-assurance-review-intake.md)
- [CI Assurance Gate specification](docs/ci-assurance-gate-spec.md)

## Public technical resources

- [Experimental Assurance Audit — model comparison sample](docs/experimental-assurance-audit-model-comparison.md)
- [Sample experiment audit](docs/sample-experiment-audit.md)
- [Experiment validity checklist](docs/experiment-validity-checklist.md)
- [Evaluator integrity failure modes](docs/evaluator-integrity-failure-modes.md)
- [Benchmark evidence manifest template](docs/benchmark-evidence-manifest-template.md)
- [Repeated-run reliability protocol](docs/repeated-run-reliability-protocol.md)

## Bounded written reviews

Have one evaluation, model-comparison, regression, benchmark, or release claim you do not completely trust?

Viridian can assess one bounded case asynchronously from the supporting artifacts and return a written assurance determination.

A bounded review is intended to answer one material decision rather than become an open-ended consulting project.

**[Request an Experimental Assurance Audit](https://docs.google.com/forms/d/e/1FAIpQLScRhl7hZfzJbxi2ittQ2nNGawK9X_c67ERjhBrIVsmPuxsGxg/viewform)**

No live demo or meeting is required.

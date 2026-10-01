# Viridian Experimental Assurance Audit — Model Comparison Example

> Synthetic public sample generated to demonstrate Viridian Experimental Assurance Audit v0.1. This is not a claim about a real company, customer, model, or production experiment.

## The claim

> **Candidate model improved evaluation performance over baseline.**

## What the team observed

| Run | Score |
|---|---:|
| Baseline | 0.71 |
| Candidate | 0.79 |
| Raw delta | **+0.08** |

At first glance, this looks like an improvement.

## Viridian determination

# INSUFFICIENT_EVIDENCE

The numerical increase is preserved as an observation, but the supplied evidence does not establish the comparative claim.

## Why the score increase is not enough

Viridian identified two material evidence problems:

### F-001 — Comparability

**Material limitation:** the evaluator identity and version differ between the baseline and candidate runs.

A comparison cannot safely treat a score delta as evidence of model improvement when the measurement system itself changed materially between arms.

### F-002 — Dataset identity

**Unknown:** the dataset version required to establish the evaluated population is missing.

The runs name the same nominal dataset, but without the required version identity Viridian cannot establish that both scores were produced against the same evaluation population.

Neither finding says that either score is wrong.

The issue is narrower: **the evidence supplied does not justify the stronger comparative conclusion yet.**

## Observation vs. qualified conclusion

**OBSERVATION**

Candidate score is 0.08 higher than baseline.

**QUALIFIED CONCLUSION**

Not established.

A raw score difference is not automatically comparative support. Material run identities must be complete and comparable before the delta can carry that authority.

## What evidence would change the determination?

The claim could be reassessed with evidence establishing, at minimum:

- evaluator identity/configuration equivalence across both runs;
- dataset version identity for both runs; and
- materially comparable experimental conditions for the baseline and candidate.

## What Viridian did

Audit v0.1 performed the checks available for this structured case, including:

- evidence artifact identity and SHA-256 manifesting;
- declared run-identity checks;
- structured baseline/candidate score observation;
- claim-aware comparability checks; and
- deterministic claim-status generation.

## What Viridian did not do

This version of the Audit does **not** claim to:

- assess statistical significance;
- rerun the experiment;
- independently qualify arbitrary evaluators;
- interpret arbitrary evidence formats;
- certify regulatory compliance; or
- prove that either model is objectively better.

Unavailable checks are scope disclosures, not findings against the evidence.

## Why this matters

AI teams often compare scores across changes to models, prompts, judges, datasets, environments, and evaluation protocols.

A numerical improvement can be real while the evidence needed to support the conclusion is incomplete.

Viridian separates **what was observed** from **what the evidence is qualified to support**.

## What a Viridian Experimental Assurance Audit returns

For one bounded evaluation, model-comparison, regression, benchmark, or release claim, the Audit produces a written assurance determination with:

- typed findings;
- evidence references and identities;
- evidence gaps;
- the evidence required to strengthen or change the determination;
- explicit capability and scope disclosures; and
- a reproducibility record for the evidence assessed.

## Have a result you don't completely trust?

> Send one bounded evaluation, model-comparison, regression, benchmark, or release claim together with the artifacts supporting it. Viridian can assess the evidence and return a written assurance determination.

Viridian works asynchronously in writing.

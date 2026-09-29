# Experiment Validity Checklist

A compact pre-promotion checklist for AI experiments. The goal is not to make experiments heavier; it is to stop a plausible-looking score change from becoming a claim that the evidence does not support.

## 1. Define the claim before reading the result
- Write down the exact claim the experiment could support.
- Define the primary metric and the smallest improvement that would matter.
- Separate exploratory measurements from promotion criteria.
- Record what result would count as no improvement or a regression.

## 2. Freeze the identities that matter
Record enough information to reconstruct both arms:
- model and checkpoint identity
- code / commit identity
- dataset or task-set identity
- prompt, rubric and grader identity
- environment and dependency versions
- relevant inference / sampling settings

If an identity can silently change between runs, the comparison is not yet controlled.

## 3. Check comparator fairness
Before comparing A with B:
- verify both arms receive equivalent inputs and opportunities;
- make resource, tool, timeout and retry differences explicit;
- distinguish intended treatment differences from accidental harness differences;
- verify missing or failed trials are handled by the same policy.

A comparison can be numerically precise and still answer the wrong question.

## 4. Preserve negative evidence
Do not keep only successful runs.
Record:
- failures and timeouts
- missing outputs
- invalid trials
- evaluator failures
- infrastructure failures
- exclusions and their reasons

“Unknown” should remain unknown rather than silently becoming pass, fail or absent.

## 5. Measure variability
For nondeterministic systems, one run is an observation, not a distribution.
- repeat trials when variance can affect the decision;
- report denominators and missingness;
- compare the observed effect with run-to-run noise;
- avoid promoting a change whose apparent gain is smaller than the experiment can reliably resolve.

## 6. Protect held-out confirmation
If changes were chosen using a set of examples, that set is no longer independent confirmation.
- keep a held-out or lockbox set away from the optimization loop;
- do not repeatedly select changes against the same “test” set;
- distinguish development evidence from confirmation evidence.

## 7. Audit the evaluator
Ask whether the measurement system can fail independently of the model:
- Is the grader stable on repeated judgments?
- Is the oracle independent of the system being tested?
- Can the agent grade its own misunderstanding as correct?
- Are rubric changes versioned?
- Are evaluator errors distinguishable from model errors?

## 8. Preserve provenance and reconstruction
A result should be traceable back to the evidence that produced it.
Keep:
- inputs
- outputs / traces
- scores
- evaluator decisions
- run identities
- configuration
- exclusions
- relevant logs

A future reviewer should be able to answer: “Why did this number exist?”

## 9. Reproduce the promoted result cleanly
Before treating a development win as established:
- rerun from a clean process or environment where practical;
- verify the intended configuration is actually the one executed;
- confirm the result is not dependent on stale state, cached artifacts or accidental leakage;
- check that the reconstructed result agrees with the recorded evidence.

## 10. Make the promotion decision explicit
Finish with a decision, not just a score:
- **Promote** — evidence supports the defined claim.
- **Reject** — evidence supports no improvement or a regression.
- **Unknown** — evidence is insufficient, invalid, contradictory or too noisy.

For every decision, state the scope. Evidence for one model, task class, environment or trust boundary should not silently become a universal claim.

---

### Minimal promotion record

For a lightweight workflow, record at least:

```text
Claim:
Baseline identity:
Candidate identity:
Dataset/task-set identity:
Evaluator identity:
Primary metric:
Repeated-trial result:
Missing/failed trials:
Held-out confirmation:
Known limitations:
Decision: PROMOTE / REJECT / UNKNOWN
Decision scope:
```

This checklist is part of the public technical material for **Viridian**, an experimental-assurance project for AI teams. It is intended to complement existing training and evaluation stacks, not replace them.

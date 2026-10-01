# Viridian CI Assurance Gate — Specification v0.1

**Status:** Design specification  
**Target surface:** GitHub Actions first  
**Goal:** Make a bounded Viridian assurance decision available inside an existing CI/release workflow without reducing the result to a meaningless green check.

## 1. Product principle

The CI gate must separate:

- **technical runner status** — did the Viridian check execute correctly?
- **assurance verdict** — what is the evidence allowed to support?

These are not the same thing.

A broken adapter is not evidence that the candidate failed.

Missing evidence is not evidence that the candidate failed.

## 2. Assurance verdicts

The initial public contract is:

- `PASS`
- `FAIL`
- `UNKNOWN`

### PASS

All configured evidence requirements for the requested claim are satisfied inside the selected assurance profile.

PASS is always scoped.

It means:

> The supplied evidence satisfies the configured gate for this claim and scope.

It does not mean:

> The model is universally correct, safe, or better.

### FAIL

The evidence affirmatively violates a configured requirement.

Examples:

- a protected regression exceeds its permitted boundary;
- candidate and comparator are demonstrably non-equivalent under a gate that requires equivalence;
- the configured confirmation result fails the frozen promotion rule.

FAIL should be used for **negative evidence**, not merely for missing evidence.

### UNKNOWN

The evidence cannot support either PASS or FAIL under the configured rules.

Examples:

- missing dataset version;
- missing evaluator identity;
- judge failure;
- incomplete run;
- comparator identity cannot be established;
- required confirmation does not exist;
- evidence is tainted or outside the profile's qualified scope.

UNKNOWN is a first-class outcome.

## 3. Runner status

Separate field:

- `OK`
- `ERROR`

`ERROR` means the Viridian adapter/gate itself did not complete correctly.

Examples:

- malformed input bundle;
- unsupported schema;
- storage failure;
- internal exception;
- unavailable required file.

An ERROR must never be converted into a model FAIL.

## 4. Exit-code policy

Recommended initial CLI contract:

| Condition | Exit code | GitHub Actions effect |
|---|---:|---|
| PASS + runner OK | 0 | success |
| FAIL + runner OK | 10 | blocks job |
| UNKNOWN + runner OK | 20 | blocks job by default |
| runner ERROR | 30 | blocks job |

The action may later support a policy input such as:

`unknown_policy: block | warn`

Default should be **block** for a gate explicitly used to authorize promotion.

The Markdown/JSON artifacts must always preserve the full verdict even if a workflow owner chooses a non-blocking policy.

## 5. Minimal inputs

The Action should not expose the whole Advanced V5 implementation.

A thin public Action should call a stable, versioned Viridian interface.

Proposed inputs:

```yaml
with:
  evidence_bundle: path/to/evidence
  requested_claim: path/to/claim.json
  assurance_profile: development-promotion-v1
  output_dir: .viridian
  unknown_policy: block
```

Optional future inputs:

- expected programme identity;
- expected manifest digest;
- protected-regression profile;
- confirmation requirement;
- adapter type.

## 6. Evidence bundle contract

The minimum bundle should be able to express:

- case/run ID;
- baseline identity;
- candidate identity;
- model/checkpoint identity;
- dataset/benchmark identity;
- evaluator identity;
- code/harness identity;
- environment identity;
- score/observation;
- failure/missing states;
- repeated-trial outcomes;
- protected confirmation state;
- preserved artifacts/references.

The bundle format must be versioned.

Unknown fields should not silently gain authority.

## 7. Outputs

### Step outputs

Proposed:

```text
verdict=PASS|FAIL|UNKNOWN
runner_status=OK|ERROR
claim_status=ADMISSIBLE|BLOCKED|NOT_ADMISSIBLE|UNRESOLVED
blocking_findings=3
report_path=.viridian/report.md
json_path=.viridian/result.json
```

### Job summary

The GitHub Actions summary should show:

1. requested claim;
2. verdict;
3. scope;
4. blocking findings;
5. strongest admissible statement;
6. next evidence required.

### Artifact

Upload:

- `result.json`;
- `report.md`;
- optional evidence manifest;
- optional checksums.

The artifact is part of the audit trail. The checkmark alone is not.

## 8. Example result

```text
Viridian Assurance Gate: UNKNOWN

Requested claim:
Candidate B improves task success over Baseline A.

Blocking findings:
- evaluator identity differs between arms
- candidate dataset version missing
- protected confirmation missing

Observed:
candidate 0.79
baseline 0.71
delta +0.08

Strongest admissible statement:
Candidate B produced a higher observed score in the supplied runs,
but the evidence does not establish a valid comparative improvement.
```

## 9. Marketplace packaging

GitHub currently requires a Marketplace Action to:

- live in a public repository;
- contain one root `action.yml` or `action.yaml` for the listed action;
- use a unique action name;
- be published through a release;
- satisfy GitHub Marketplace publishing requirements.

The Viridian Action should therefore be a **small dedicated repository** rather than embedding multiple unrelated public actions in the main Viridian repository.

Reference: [GitHub — Publishing actions in GitHub Marketplace](https://docs.github.com/en/actions/how-tos/create-and-publish-actions/publish-in-github-marketplace)

## 10. Security design

The thin Action should:

- use least-privilege workflow permissions;
- avoid long-lived tokens where possible;
- pin the Viridian CLI/package version;
- produce an exact tool/version identity in every result;
- avoid transmitting evidence externally unless the selected deployment explicitly requires it;
- redact secrets from logs;
- fail closed on malformed evidence for a blocking promotion gate.

A future packaged Action must be tested for actual network behavior before any no-phone-home claim is made.

## 11. Qualification boundary

The CI Action is an **integration surface**.

Publishing the Action does not automatically qualify every workflow, model, evaluator, or customer environment.

The Action should state:

- Viridian version;
- adapter version;
- evidence-schema version;
- selected assurance profile;
- relevant qualification scope.

## 12. Initial implementation milestone

Do not build ten integrations first.

The first implementation is complete when:

1. one public fixture repository can run the gate;
2. PASS, FAIL, UNKNOWN, and runner ERROR are distinguishable;
3. UNKNOWN does not silently become FAIL;
4. a Markdown and JSON report are preserved;
5. the sample from `sample-assurance-output-v1.md` can be reproduced from structured input;
6. an external engineer can understand why the job blocked without reading Viridian source code.

## 13. Non-goals for v0.1

- replacing GitHub Actions;
- running arbitrary model training;
- becoming a general policy engine;
- universal model qualification;
- remote SaaS hosting;
- proving scientific truth;
- hiding evidence behind a proprietary green check.

The wedge is simple:

> Put experimental-evidence authority next to the CI decision that already promotes the change.

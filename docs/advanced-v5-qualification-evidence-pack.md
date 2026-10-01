# Advanced V5 Qualification Evidence Pack — Public Summary

**Status:** Public-safe human-readable summary  
**Product:** Viridian Advanced V5  
**Purpose:** Technical diligence and qualification-scope disclosure

This document summarizes the qualification evidence that may be stated publicly about the frozen Advanced V5 architecture.

It is intentionally conservative. It does not replace the frozen machine-readable manifests, internal qualification databases, implementation digests, or release-specific checksums.

## 1. What Advanced V5 is

Advanced V5 is an **experimental-assurance architecture** for AI/ML research and development.

It sits around an existing experiment, training, benchmark, or evaluation stack and governs questions such as:

- what evidence exists;
- which identities produced it;
- whether candidate and comparator are legitimately comparable;
- whether evidence is DEVELOPMENT, DISCOVERY, protected confirmation, historical, synthetic, or another declared class;
- whether evidence is tainted, missing, contradictory, or otherwise non-qualifying;
- whether a result has replicated or been independently confirmed;
- what scope a claim may legitimately have.

Advanced V5 is not presented as a replacement for PyTorch, MLflow, benchmark harnesses, LLM judges, or training frameworks.

## 2. Core authority invariant

A central architectural rule is:

`AUTHORITY_DELTA=NONE`

The intended meaning is:

> Adding capability to the Advanced layer or to an alternate execution substrate must not silently grant additional scientific/epistemic authority.

This does **not** mean arbitrary agents have zero operational permissions, nor does it establish universal prevention of agentic drift.

## 3. Evidence integration

The final evidence-integration qualification recorded:

- **30 vector outcomes — PASS**

The purpose of this campaign was to verify that Advanced components preserved the evidence semantics expected by the trusted V5 core across the tested vectors.

## 4. Resident R3 execution profile

The resident execution profile is identified as:

`k2-resident-execution-profile-candidate-v3`

The corresponding trusted-local profile is:

`custom-model-code-profile-k2-horizon-3.7b-v1`

The qualified model was:

**K2 Horizon 3.7B**

### Qualification scope

R3 qualification is deliberately narrow.

The evidence applies only to the exact pinned qualification envelope, including the relevant:

- model identity;
- trusted-local DEVELOPMENT profile;
- implementation identity/digest;
- trust-profile identity/digest;
- loader and version assumptions;
- environment;
- qualification policy.

A materially changed model, loader, environment, trust profile, or implementation does **not** automatically inherit this qualification.

## 5. Clean-process equivalence

The clean-process reference path and R3 were compared across the frozen equivalence campaign.

Result:

- **20 / 20** cases were recorded as **exact or declared-equivalent**.

This establishes equivalence only for the tested qualification cases inside the frozen envelope.

It does not establish universal equivalence for arbitrary workloads or customer stacks.

## 6. Live soak

The resident profile was subjected to sustained live execution.

Recorded campaign:

- **3,390 observations**
- approximately **3,600.76 seconds** of soak time

The soak was intended to expose issues such as state accumulation, cross-run contamination, recovery problems, drift, and resource degradation within the tested environment.

No soak test can prove the absence of every possible long-duration failure.

## 7. Fault injection

Recorded campaign:

- **84 injected failures**
- **84 corresponding sentinels**

The fault campaign tested whether the system preserved expected failure/evidence semantics under the injected conditions.

This does not imply coverage of every production fault class.

## 8. Persistence, restart, recovery, and reconstruction

Advanced V5 is not stateless.

The current architecture uses persistent local SQLite stores for evidence/provenance/reconstruction/recovery/qualification state.

Qualification work covered:

- persistence;
- shutdown/restart;
- restore;
- reconstruction;
- historical identity preservation;
- derived-state rebuilding.

Recorded restart/recovery testing included:

- **10 / 10** cases passing

The overall persistence/recovery/reconstruction qualification passed within its frozen scope.

## 9. HumanEvidenceVisibilityLedger

Result:

**PASS WITH LIMITATION**

The tested scope included:

- temporal visibility;
- evidence-class filtering;
- hidden/protected evidence treatment;
- reconstruction;
- unknown-class rejection.

Explicit limitation:

> Human intent is not fully observable from software-visible evidence.

Viridian can reason about evidence exposed through controlled interfaces and recorded actions. It cannot prove what a person knew from unrecorded or out-of-band sources.

## 10. Security composition

Result:

**PASS WITH TRUSTED-LOCAL LIMITS**

The qualified posture assumes a trusted-local environment for the resident/custom-model-code path.

Explicit non-claim:

- hostile native-code containment is outside the qualified scope.

Advanced V5 therefore must not be marketed as a hardened sandbox for arbitrary malicious native code.

## 11. Anti-self-deception audit

The final anti-self-deception campaign passed within the frozen scope.

Test themes included:

- negative-result preservation;
- UNKNOWN preservation;
- evidence-taint propagation;
- comparator fairness;
- historical identity preservation;
- protected-evidence leakage;
- evidence-class laundering;
- future-evidence leakage;
- synthetic-to-real laundering;
- shadow-to-executed laundering;
- DEVELOPMENT-to-confirmation laundering.

The purpose is not to make error impossible.

The purpose is to make it mechanically harder for invalid evidence to acquire authority silently.

## 12. CUDA out-of-memory limitation

CUDA OOM qualification remained:

**SIMULATED ONLY**

The simulated fault provides evidence about logic and failure handling.

It does **not** establish equivalence to every real GPU out-of-memory condition on physical hardware.

## 13. Frozen regression status

The recorded final frozen regression suite was:

- **295 / 295 — PASS**

Earlier sub-campaign counts and the final frozen suite are different qualification snapshots and should not be summed as if they were one test run.

## 14. Canonical R3 adoption

After technical qualification, the R3 path underwent a human canonical-adoption step.

Recorded transaction state:

**ADOPTED**

This permits routing into R3 only for requests matching the qualified envelope.

It does not universalize the profile.

The clean-process path remains the fallback outside scope.

## 15. Evidence classes and claim governance

The architecture recognizes materially different classes of evidence rather than treating all stored results as equivalent.

The public conceptual model includes classes such as:

- DEVELOPMENT;
- DISCOVERY;
- PROTECTED_CONFIRMATION;
- HELD_OUT_QUALIFICATION;
- HISTORICAL;
- SYNTHETIC;
- EXTERNAL_PRIOR.

The class of evidence constrains what it may support.

For example:

- DEVELOPMENT evidence does not become independent confirmation by being summarized;
- synthetic fault evidence does not become real-hardware qualification;
- historical evidence remains bound to the identity that produced it.

## 16. Public claim boundaries

### Safe

- Advanced V5 preserves and qualifies structured experimental evidence.
- It separates discovery from confirmation.
- It binds evidence to identities and provenance.
- It preserves explicit missing/UNKNOWN states.
- It can block or bound a claim when configured evidence requirements are unmet.
- R3 was qualified in a narrow K2 trusted-local DEVELOPMENT envelope.
- persistence/recovery/reconstruction passed within the tested qualification scope.

### Not supported

- Viridian proves scientific truth.
- Viridian proves causality automatically.
- Viridian makes all AI evaluation deterministic.
- Viridian guarantees every model stack is qualified.
- R3 automatically supports any customer model.
- Viridian is a hardened zero-trust native-code sandbox.
- the persistence layer is a cryptographic append-only ledger.
- simulated CUDA OOM testing is the same as real-hardware OOM qualification.

## 17. Machine-readable release evidence

This human-readable document should eventually be accompanied by a release-specific public artifact bundle containing, where safe to disclose:

- exact release/tag identity;
- frozen manifest;
- SHA-256 checksums;
- SBOM;
- exact full implementation/trust-profile digests;
- selected qualification outputs;
- versioned limitations statement.

Those artifacts must be exported from the frozen release itself rather than manually reconstructed from prose.

## 18. Diligence question this pack is meant to answer

The correct buyer question is not:

> "Is Viridian perfect?"

It is:

> "What has this version actually been qualified to do, under which identities and trust assumptions, and what remains explicitly outside scope?"

That is the standard Advanced V5 applies to its own claims.

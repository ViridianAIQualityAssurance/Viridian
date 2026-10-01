# Viridian Advanced V5 — Threat Model

**Status:** Public technical threat model  
**Scope:** Current Advanced V5 assurance architecture and planned bounded-review deployment

This threat model describes what Viridian is intended to protect, the assumptions under which its qualification evidence applies, and the failure classes that remain outside the qualified boundary.

## 1. Security objective

Viridian's primary objective is **experimental-evidence integrity**, not general host security.

The system is designed to reduce the chance that:

- the wrong evidence is attached to a claim;
- a materially changed comparator is treated as equivalent;
- missing/failed evidence becomes silent positive support;
- protected confirmation leaks into development authority;
- historical evidence is rewritten under a newer identity;
- derived summaries gain more authority than their source evidence;
- an alternate execution substrate silently gains scientific authority.

## 2. Assets

Assets whose integrity matters include:

- evidence artifacts;
- run/case identities;
- model/checkpoint identities;
- dataset/benchmark identities;
- evaluator/rubric identities;
- environment/configuration identities;
- evidence classes;
- taint/missingness state;
- decision/promotion rules;
- qualification manifests;
- recovery/reconstruction state;
- assurance outputs and their scope.

Confidentiality may also matter for:

- customer artifacts;
- prompts;
- outputs/traces;
- API credentials;
- non-public model/configuration information.

Confidentiality guarantees are deployment-dependent and are not inferred automatically from this threat model.

## 3. Trust boundaries

### Trusted / qualified boundary

The current resident/custom-model-code security qualification assumes a **trusted-local** environment.

The V5 core, canonical stores, and qualified identities are expected to operate inside this boundary.

### Adapter boundary

Adapters may ingest evidence from external experiment/evaluation systems.

External data is treated as **input evidence**, not as automatically authoritative truth.

Adapters must not silently extend the scientific authority of the system.

### External integration boundary

Optional integrations may include:

- model/evaluator providers;
- GitHub or CI systems;
- artifact stores;
- experiment trackers;
- telemetry/lineage systems.

Each integration introduces its own identity, availability, confidentiality, and network assumptions.

## 4. Threats in scope

### T-001 — Evidence identity substitution

An artifact from model/dataset/evaluator identity B is recorded as if it came from identity A.

**Controls:** explicit identities, manifests/digests where implemented, provenance relationships, qualification envelope.

### T-002 — Comparator drift

Candidate and baseline are compared despite a material unrecorded change to task population, evaluator, environment, resource policy, or another controlled condition.

**Controls:** comparator-fairness checks, frozen programme identity, explicit intentional differences.

### T-003 — Missingness laundering

Timeouts, judge failures, malformed outputs, dropped rows, or unavailable artifacts disappear from the denominator or become favorable evidence.

**Controls:** typed missingness/UNKNOWN, negative-evidence preservation, explicit failure state.

### T-004 — Evidence-class laundering

DEVELOPMENT, SYNTHETIC, historical, or shadow evidence is relabeled or summarized into a stronger class.

**Controls:** evidence-class preservation, authority rules, taint propagation, anti-self-deception tests.

### T-005 — Future evidence leaks backward

Evidence revealed later is allowed to influence reconstruction of an earlier decision state.

**Controls:** temporal evidence visibility and reconstruction policy.

### T-006 — Historical identity rewriting

Old evidence becomes implicitly associated with a newer model/loader/environment merely because the semantic name stayed the same.

**Controls:** historical identity preservation, explicit version/configuration identity.

### T-007 — Derived-state corruption

A cache/index/summary becomes inconsistent with canonical evidence and is treated as the source of truth.

**Controls:** canonical-vs-derived separation, reconstruction from persistent canonical state.

### T-008 — Persistence/recovery corruption

A restart or failure loses, duplicates, or mutates evidence relationships.

**Controls:** persistent structured stores, restart/recovery testing, reconstruction qualification.

### T-009 — Alternate execution authority expansion

A faster/resident/agentic execution path gains additional claim authority merely because it can do more.

**Controls:** `AUTHORITY_DELTA=NONE`, narrow qualification envelope, clean-process fallback.

### T-010 — Evaluator integrity failure

Judge identity changes, outputs are attached to the wrong case, or evaluator failures are mistaken for model outcomes.

**Controls:** evaluator identity, stable evidence IDs, UNKNOWN preservation, comparator/evaluator qualification.

## 5. Threats explicitly outside or only partially covered

### O-001 — Hostile native code

Advanced V5 is **not qualified as a hardened sandbox** for arbitrary malicious native code.

Hostile native-code containment is outside the trusted-local security qualification.

### O-002 — Compromised operating system / administrator

A malicious host administrator may be able to bypass application-level controls, modify files/databases, inspect memory, or alter the runtime.

No claim of resistance to a fully compromised host is made.

### O-003 — Out-of-band human knowledge

Viridian cannot prove what a human knew from unrecorded external channels.

HumanEvidenceVisibilityLedger qualification explicitly retains this limitation.

### O-004 — Unmeasured network exfiltration

No universal no-phone-home/exfiltration claim is made before the packaged deployment is measured.

### O-005 — Arbitrary third-party adapter correctness

An adapter may be wrong or incomplete.

Adapter output must remain attributable to its source and must be qualified before it is allowed to support a stronger claim.

### O-006 — General scientific truth

The system can govern evidence authority; it cannot independently guarantee that the study design, metric, domain assumption, or causal theory is correct.

## 6. Abuse and bypass cases

A technically capable operator may attempt to:

- delete inconvenient evidence;
- relabel evidence classes;
- alter thresholds after seeing results;
- rerun until a favorable result appears;
- change the comparator;
- bypass the intended write path;
- substitute a different evaluator;
- copy evidence into a new programme without its original limitations.

The architecture should preserve enough provenance, historical identity, programme freezing, and decision rules to make these operations detectable or to reduce the authority of the affected evidence.

A fully malicious operator with unrestricted host/database access remains outside the strongest application-level guarantees.

## 7. Confidentiality and secrets

A customer deployment must separately define:

- which evidence artifacts are sensitive;
- who can read canonical stores;
- where credentials are sourced;
- whether credentials ever enter evidence/logs;
- retention policy;
- backup encryption;
- network egress;
- access-control/tenancy model.

These are deployment controls, not automatic consequences of the V5 evidence model.

## 8. Supply-chain threats

Risks include:

- compromised dependencies;
- compromised CI/release workflow;
- substituted release artifacts;
- stale vulnerable dependencies.

Target mitigations for public/package releases include:

- pinned dependencies;
- CI checks;
- SBOM;
- release checksums;
- signed artifacts/provenance where implemented;
- least-privilege workflow permissions;
- explicit supported versions.

## 9. Residual risk

A PASS from Viridian should never be interpreted as "no risk."

Residual risks may include:

- unmodeled experimental assumptions;
- external evaluator/model behavior;
- deployment-specific security gaps;
- compromised infrastructure;
- human/out-of-band contamination;
- insufficient domain coverage;
- untested failure classes.

## 10. Threat-model rule

> When a threat is outside the qualified boundary, the correct output is a limitation—not a marketing extrapolation.

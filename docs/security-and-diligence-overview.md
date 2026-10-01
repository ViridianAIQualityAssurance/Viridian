# Viridian Security & Diligence Overview

**Status:** Public-safe diligence summary  
**Scope:** Current Advanced V5 architecture and the public Viridian assurance workflow

This document is for technical/security diligence. It states what is currently supported, what is deployment-dependent, and what is explicitly not claimed.

## 1. Product category

Viridian is **experimental-assurance infrastructure**.

It is security-adjacent because evidence integrity, identity, provenance, failure handling, and trust boundaries matter to its operation.

It is **not** currently represented as:

- an endpoint-security product;
- a malware sandbox;
- a general-purpose zero-trust enforcement platform;
- a compliance-certification product.

## 2. Current trust boundary

The qualified Advanced V5 security-composition result is:

**PASS WITH TRUSTED-LOCAL LIMITS**

The resident/custom-model-code path assumes trusted-local code within the qualified envelope.

### Out of scope

Hostile native-code containment is outside the qualified security scope.

A buyer requiring execution of untrusted malicious code should not treat Viridian as a substitute for a hardened sandbox or isolation platform.

## 3. Data persistence

Advanced V5 is not stateless.

The current architecture writes durable structured experimental state to persistent local SQLite stores used for:

- evidence;
- provenance;
- reconstruction;
- recovery;
- qualification.

The architecture also preserves identities, frozen manifests, digests, and audit artifacts where implemented.

## 4. What the persistence layer is not

The current persistence design should not be described as:

- blockchain;
- a cryptographic append-only ledger;
- tamper-proof under every threat model.

Hashes and digests can bind exact artifacts/identities. They do not alone prove every database transition is cryptographically immutable.

## 5. High-level data flow

A representative bounded assurance flow is:

```text
Customer experiment/eval artifacts
        ↓
Adapter / structured intake
        ↓
Identity + provenance checks
        ↓
Evidence classification
        ↓
Comparator / evaluator / qualification gates
        ↓
Canonical local evidence state
        ↓
Written / machine-readable assurance output
```

A production data-flow diagram must be generated for the **actual packaged deployment** and integrations being proposed to the customer.

## 6. Network behavior

No universal "does not phone home" claim is currently made.

The correct procedure for a packaged release is to measure:

- DNS activity;
- outbound connections;
- package/update checks;
- model/provider calls;
- telemetry;
- integration-specific network paths.

A network-behavior report should be tied to an exact release and deployment configuration.

## 7. Privacy / PII

PII handling is deployment-dependent.

Viridian should request only the evidence required for the assurance decision and should prefer:

- sanitized artifacts;
- synthetic/public fixtures;
- local processing;
- minimal retention

where those are sufficient.

No universal claim is made that every future integration can never process third-party PII.

## 8. Secrets

A production integration should document:

- which credentials exist;
- where they are supplied;
- whether they are persisted;
- how they are redacted from evidence/logs;
- which adapters require them;
- how access is revoked.

No customer secret should be requested merely for convenience if the assurance case can be reproduced with sanitized evidence.

## 9. Software supply chain

The target public-release hygiene programme includes:

- `SECURITY.md`;
- supported-version policy;
- pinned dependencies / lockfiles;
- CI/regression checks;
- release SHA-256 checksums;
- CycloneDX SBOM;
- artifact signing where packaging supports it;
- build provenance where the release pipeline supports it.

These controls provide inspectability and release provenance.

They are not a substitute for product qualification or external security review.

## 10. Vulnerability reporting

Sensitive security issues should not be posted publicly with exploit details.

Use GitHub private vulnerability reporting where available. If no private path is available, request a private channel without publishing the sensitive reproduction.

See the root [SECURITY.md](../SECURITY.md).

## 11. Security/compliance certifications

Viridian is not currently represented as:

- SOC 2 certified;
- ISO 27001 certified;
- ISO/IEC 42001 certified;
- NIST certified.

A NIST AI RMF crosswalk can describe how selected Viridian evidence supports selected framework activities. That is **not** certification or full organizational compliance.

## 12. Reliability evidence

Current public qualification statements include:

- 20/20 clean-vs-R3 exact/declared-equivalent cases;
- 3,390 live soak observations over approximately 3,600.76 seconds;
- 84 injected failures with 84 corresponding sentinels;
- persistence/recovery/reconstruction qualification passing within scope;
- 10/10 recorded restart/recovery cases;
- a final frozen 295/295 regression suite;
- security composition passing within trusted-local limits.

See [Advanced V5 Qualification Evidence Pack](advanced-v5-qualification-evidence-pack.md).

## 13. Known technical limitations

The current public limitations include:

1. hostile native-code containment is not qualified;
2. real CUDA OOM behavior remains unqualified; OOM testing was simulated;
3. human intent and out-of-band knowledge cannot be perfectly reconstructed;
4. networking/privacy properties must be measured for the packaged deployment;
5. R3 qualification does not transfer to arbitrary customer models;
6. SQLite concurrency/scaling claims should be based on measured deployment load, not assumption;
7. causal/scientific truth is not independently proven by the assurance layer.

## 14. Pilot-stage security package

Before a serious paid pilot, the minimum diligence set should include:

- this overview;
- qualification scope and limitations;
- threat model;
- exact package identity;
- install/uninstall path;
- data-flow diagram;
- measured network behavior for the package;
- dependency manifest/SBOM where packaging exists;
- customer-specific data/credential inventory;
- explicit support and incident-contact path.

## 15. Enterprise-stage additions

Larger production deployments may additionally require:

- tested backup/restore procedure;
- concurrency/load envelope;
- RBAC/tenancy model where relevant;
- vulnerability-management workflow;
- external penetration/security review;
- formal licence and support terms;
- organization-specific compliance evidence;
- certifications where they are a genuine procurement requirement.

Those are roadmap/procurement requirements, not properties that should be claimed before they exist.

## 16. Diligence principle

Viridian's security posture should be evaluated the same way as its experimental evidence:

> distinguish what is measured, what is qualified, what is deployment-dependent, and what is still unknown.

# Security Policy

Viridian is an experimental-assurance project for AI teams. This policy covers the public Viridian repository and the security claims that may be made about Advanced V5.

## Reporting a security issue

Please do **not** publish exploit details, secrets, credentials, private customer data, or other sensitive reproduction material in a public issue.

If GitHub private vulnerability reporting is enabled for this repository, use that channel. If it is not available, open a minimal public issue asking the repository owner to establish a private contact path **without including the sensitive technical details**.

For ordinary bugs, documentation errors, or non-sensitive assurance questions, use the normal GitHub issue workflow.

## Supported security posture

The current qualified Advanced V5 security boundary is **trusted-local**.

That means:

- security-composition testing passed within the frozen trusted-local qualification scope;
- hostile native-code containment is **outside** the qualified scope;
- Advanced V5 must not be described as a hardened sandbox for arbitrary malicious code;
- a customer deployment's network behavior, data flows, credential handling, and privacy properties must be verified for that packaged deployment rather than inferred from architectural intent.

## Persistence and integrity

Advanced V5 is not stateless. The current implementation writes durable structured experimental state to persistent local SQLite stores used for evidence, provenance, reconstruction, recovery, and qualification.

The system also preserves hashes/digests, frozen manifests, identities, and audit artifacts where implemented.

These properties **must not** be described as a cryptographic append-only ledger or blockchain-style store. A digest can bind an artifact to an identity; it does not by itself prove that every state transition is cryptographically immutable.

## Qualification boundaries

Resident R3 is qualified only inside its exact pinned qualification envelope, including the specific K2 Horizon 3.7B model, trusted-local DEVELOPMENT profile, implementation/trust identities, loader/version assumptions, and environment used by the qualification campaign.

Changing the model, loader, environment, execution substrate, or another material identity does not automatically inherit R3's qualification.

## Known limitations

The public security and assurance posture currently includes these explicit limitations:

- hostile native-code containment is not qualified;
- real CUDA out-of-memory behavior was not directly qualified; the OOM path was simulated;
- human intent and out-of-band information exposure cannot be perfectly reconstructed from software-visible evidence;
- no universal "no phone home" claim should be made until the shipped package and its integrations have a measured network-behavior report;
- privacy and PII claims are deployment-dependent;
- Viridian is not currently represented as SOC 2 certified, ISO 27001 certified, NIST certified, or otherwise formally certified by a standards body.

## Release hygiene target

Public/releasable Viridian components should progressively provide:

- pinned dependencies or lockfiles;
- CI/regression checks;
- release checksums;
- a CycloneDX SBOM for packaged releases;
- signed artifacts and provenance where the release pipeline supports them;
- explicit supported-version and upgrade policies;
- a public qualification-scope and limitations statement.

These are software-supply-chain and diligence controls. They do not prove that an AI experiment is scientifically correct.

## Disclosure principle

Viridian applies the same rule to its own security claims that it applies to experimental claims:

> A claim must not be stronger than the evidence that supports it.

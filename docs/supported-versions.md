# Supported Versions and Qualification Scope

This document separates **software support** from **scientific/assurance qualification**.

Those are not the same thing.

## Public documentation

The public Viridian repository is currently an early technical surface.

Unless a release explicitly says otherwise:

- the latest public documentation on `main` is the maintained public documentation set;
- historical reports and examples remain useful as historical artifacts, but later corrections may supersede their interpretation;
- a document's publication does not imply that every described product capability is generally available as a packaged production release.

## Advanced V5 qualification

Advanced V5 qualification statements apply only to the exact frozen implementation and qualification envelope referenced by the qualification evidence.

A later change to:

- model;
- loader;
- execution substrate;
- trust profile;
- environment;
- evaluator;
- persistence behavior;
- authority logic;
- evidence schema;
- another material identity

does not inherit the earlier qualification automatically.

Material changes require requalification appropriate to the changed scope.

## Resident R3

R3 is qualified only for its exact pinned K2 Horizon 3.7B trusted-local DEVELOPMENT envelope.

It is not a universal execution profile.

## Security support

Security reports should identify the exact artifact/version they affect whenever possible.

Until a formal production release train exists:

- no long-term support window is promised;
- no automatic upgrade compatibility promise is made;
- no security-fix SLA is promised;
- no package should be assumed supported merely because a similarly named architecture is documented.

## Release policy target

A production-ready Viridian release should identify:

1. version/tag;
2. build/package digest;
3. dependency/SBOM identity;
4. qualification scope;
5. known limitations;
6. supported upgrade path;
7. security-support window;
8. end-of-support date where applicable.

## Compatibility principle

> A semantic name is not a qualification identity.

Evidence and support must remain bound to the exact implementation and environment that earned them.

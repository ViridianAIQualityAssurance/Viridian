# Network Behavior Verification Plan

**Status:** Test procedure, not a completed result.

Viridian should not claim that a packaged deployment "does not phone home" until the exact package and enabled integrations have been measured.

This plan defines the minimum evidence required for such a statement.

## 1. Test objective

For an exact packaged Viridian release, determine:

- whether the process performs DNS resolution;
- whether it creates outbound TCP/UDP connections;
- whether it checks for updates;
- whether dependencies emit telemetry;
- whether adapters contact model/evaluation providers;
- whether package installation performs external fetches;
- whether runtime behavior differs between default and optional integrations.

## 2. Freeze the test identity

Record:

- Viridian version/tag;
- package/container digest;
- OS/base-image identity;
- dependency/SBOM digest;
- enabled adapters;
- environment variables;
- configuration;
- test fixture digest;
- network-capture tooling/version.

If any of these change materially, the result belongs to a new test identity.

## 3. Test phases

### Phase A — installation

Observe network activity during:

- package installation;
- dependency installation;
- container pull/build where applicable;
- first-run initialization.

Installation network access must be distinguished from runtime network access.

### Phase B — idle startup

Start Viridian with:

- no external adapters;
- a local/public synthetic evidence fixture;
- no model-provider credentials.

Observe for a fixed interval.

### Phase C — bounded assurance run

Run the public sample assurance fixture.

Capture:

- DNS queries;
- destination IP/host;
- destination port;
- protocol;
- process responsible;
- timestamp;
- reason if known.

### Phase D — optional integrations

Repeat separately for each adapter that intentionally requires network access.

Examples:

- remote evaluator/model provider;
- GitHub API;
- cloud artifact store;
- remote telemetry endpoint.

The final report must distinguish **core runtime** from **optional integration traffic**.

## 4. Linux example instrumentation

Possible tools include:

```bash
sudo tcpdump -i any -nn -w viridian-network-test.pcap
```

and process/socket inspection such as:

```bash
ss -tpuna
```

A containerized test may additionally run with an isolated Docker network or an egress-deny policy to observe failure behavior.

## 5. Windows example instrumentation

Use a combination of:

- Windows Firewall outbound rules;
- Resource Monitor / TCPView or equivalent process-aware connection viewer;
- packet capture such as Wireshark/Npcap where available.

The specific tool choice is less important than preserving a reproducible capture tied to the package identity.

## 6. Offline execution check

Run the same bounded fixture with outbound networking blocked.

Record whether Viridian:

- completes normally;
- fails explicitly;
- silently degrades;
- changes its assurance result;
- attempts retries.

A networking failure must not silently change experimental evidence semantics.

## 7. Pass criteria for a "local/no-phone-home" claim

A release may only make a bounded claim such as:

> The tested core package completed the public fixture without observed outbound runtime connections under configuration X.

when:

1. the package identity is frozen;
2. capture tooling observed the full process/network namespace;
3. no unexplained outbound connections occurred;
4. optional integrations are separately documented;
5. the offline run did not silently alter assurance semantics.

Do **not** generalize this result to another release or integration automatically.

## 8. Required output

The final test report should contain:

- exact package identity;
- test environment;
- capture method;
- observed DNS/connections;
- expected integration traffic;
- unexpected traffic;
- offline result;
- limitations;
- packet-capture/checksum references.

## 9. Explicit non-claim

Until this procedure is executed against a real packaged release, Viridian should state:

> Network behavior is deployment-dependent and has not yet been universally verified.

That is more credible than an unmeasured privacy promise.

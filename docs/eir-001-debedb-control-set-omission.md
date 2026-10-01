# EIR-001 — Control-Set Omission and Comparator Invalidity in DEBEDb

**Series:** Viridian Experimental Integrity Reports  
**Case type:** Public technical postmortem analysis  
**Severity:** High experimental-integrity exposure  
**Status:** Public-source analysis; not a security vulnerability report  
**Source date:** September 2026

## Executive summary

DEBEDb published a postmortem describing a benchmark-control failure in which its "full repository dump" baseline silently omitted files.

The packing loop accepted files until one did not fit, skipped that file, and continued. According to DEBEDb, the resulting baseline contained **69 of 97 files** and omitted large files including the classes needed to answer one architecture question.

After the control was corrected, the reported baseline changed from **6.60 to 10.80 out of 12**.

DEBEDb states that every published cross-strategy comparison in the earlier write-up had been anchored to that incorrect control.

This is a strong example of a **control-set identity and comparator-validity failure**: the benchmark executed, produced plausible scores, and still supported comparisons whose denominator was materially wrong.

Primary source: [DEBEDb — "Our Control Group Was Broken and It Cost Us 4.2 Points"](https://blog.debedb.com/2026/09/22/our-control-group-was-broken-and-it-cost-us-4-2-points/)

## 1. Observed public facts

The following points are reported by DEBEDb:

1. The "full repository dump" baseline used a skip-and-continue packing policy.
2. When a file did not fit the context budget, the packer skipped it and continued rather than treating the control as incomplete.
3. The resulting baseline admitted 69 of 97 files.
4. Important large files were omitted, including the three classes needed for an architecture question.
5. The model correctly reported those classes as absent from the supplied files.
6. The original baseline score was **6.60/12**.
7. The corrected baseline score was **10.80/12**.
8. DEBEDb states that earlier cross-strategy comparisons were anchored to the incorrect baseline.

This report does **not** infer that every historical DEBEDb result is invalid. The affected scope is the set of claims that depend on the broken control or on comparisons normalized against it.

## 2. Failure mechanism

### 2.1 Nominal identity differed from effective identity

The run was described as a full-repository baseline, but the effective input set was not the full repository.

That creates two different identities:

- **nominal control:** full repository;
- **effective control:** the subset that survived skip-and-continue packing.

If the experimental system records only the nominal label, downstream analysis can treat materially different evidence as if it came from the intended control.

### 2.2 The control failed silently

The important failure was not merely that files were missing.

The stronger problem was that the benchmark still executed and produced a plausible score without elevating the omission into a qualification failure.

A successful process exit therefore did not imply a valid comparator.

### 2.3 Comparator validity propagated downstream

Once the incorrect baseline was accepted, downstream statements such as "strategy X reaches N% of full-context quality" inherited the broken denominator.

The raw observations from the treatment arms may still be useful. What changes is the authority of claims that compare those observations to the invalid control.

## 3. Evidence classification

### Affected evidence

- the original 6.60/12 baseline as evidence for the intended full-repository control;
- comparisons normalized against that baseline;
- per-strategy relative-quality claims whose denominator depended on the broken control.

### Evidence that can still survive

Subject to DEBEDb's own retained artifacts and later verification:

- raw treatment-arm outputs;
- raw scores that do not depend on the broken comparator;
- the corrected 10.80/12 baseline;
- the observed failure mechanism itself;
- any conclusion whose truth does not depend on the invalid comparator.

## 4. Claim ceiling after the failure

Before remeasurement, a defensible claim is narrower than:

> Strategy X achieves N% of full-context quality.

A safer statement is:

> Strategy X produced the recorded result under the original benchmark execution, but comparisons to the intended full-repository baseline require remeasurement because the baseline input set was incomplete.

That preserves the observation without laundering it into a stronger comparison.

## 5. Viridian Advanced V5 mapping

This section describes how an **appropriately configured** Advanced V5 programme could govern this failure class. It is not a claim that Viridian was present in DEBEDb's system or that the exact omission would have been automatically detected without the relevant identities being configured.

### 5.1 Frozen comparator identity

A V5 programme can bind a comparison to exact evidence-producing identities.

For this failure class, the relevant identity should include the **effective benchmark/control input set**, not merely the label "full repository."

A material change to that set should either:

- produce a new experimental identity; or
- make the evidence ineligible to support the original comparator claim.

### 5.2 Comparator-fairness gate

If the candidate/treatment arm and baseline are not evaluated against the intended, qualified input populations, the comparison should fail comparator qualification even when both runs produce numeric scores.

### 5.3 Provenance and reconstruction

The evidence record should make it possible to reconstruct:

- which files were eligible;
- which files were included;
- which files were omitted;
- why they were omitted;
- the exact packer/harness identity;
- the score produced from that effective input set.

### 5.4 Taint propagation

Once the baseline is found to be materially invalid for the intended claim, downstream comparison evidence should carry that limitation until it is remeasured or explicitly superseded.

The original treatment evidence need not be deleted. Its **claim authority** changes.

### 5.5 Protected confirmation

After fixing the control, the strongest comparative claims should be rerun against a frozen corrected baseline and, where appropriate, confirmed on evidence that was not already consumed during iterative correction.

## 6. What Advanced V5 cannot claim from this case

This case does **not** establish that Viridian:

- would have made the file omission mathematically impossible;
- automatically detects every missing benchmark input;
- proves that the corrected 10.80/12 score is the unique true baseline;
- retroactively knows which human decisions used the broken result;
- prevents every comparator bug in an arbitrary unconfigured stack.

Those stronger statements require evidence this public case does not provide.

## 7. Commercial and research exposure hypothesis

No financial-loss estimate is made here.

The plausible exposure class is:

- wasted reruns and engineering time;
- incorrect prioritization of compression/retrieval strategies;
- publication or product claims that require correction;
- downstream decisions made from relative metrics whose control was invalid.

The magnitude depends on how widely the affected comparator was used.

## 8. Verification questions for an assurance review

A team facing a similar incident should be able to answer:

1. What is the exact effective control/input identity?
2. Can the system prove which artifacts were actually included?
3. Are exclusions typed and reconstructable?
4. Does a missing or changed control input force a new comparison identity?
5. Which downstream claims depend on the affected comparator?
6. Which evidence can survive without re-execution?
7. What corrected run is required before promotion/publication resumes?

## 9. Viridian determination

**Failure class:** control-set omission / comparator invalidity  
**Experimental severity:** High  
**Security vulnerability:** Not established  
**Primary remediation:** re-establish the exact control identity, remeasure affected comparisons, preserve the broken evidence as historically bounded rather than silently overwriting it.

---

Viridian Experimental Integrity Reports analyze public experimental failures through an evidence-governance lens. They separate **observed public facts**, **Viridian interpretation**, **affected claims**, **surviving evidence**, and **what Viridian can or cannot actually enforce**.

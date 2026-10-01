# Viridian × NIST AI RMF — Evidence Crosswalk

**Status:** Technical mapping, not certification  
**Framework:** NIST AI Risk Management Framework 1.0  
**Companion context:** NIST Generative AI Profile (NIST AI 600-1)

NIST describes the AI RMF as a voluntary framework for helping organizations manage AI risk. Viridian can provide **technical experimental-assurance evidence** relevant to selected activities in that broader risk-management process.

Viridian is **not NIST certified**, and this document is **not** a statement of full organizational compliance.

Primary references:

- [NIST AI Risk Management Framework 1.0](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-ai-rmf-10)
- [NIST AI RMF — Generative AI Profile](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence)

## 1. Crosswalk legend

- **Strong technical support** — Viridian directly produces evidence relevant to the function.
- **Partial technical support** — Viridian can contribute evidence, but the function includes broader organizational responsibilities outside the product.
- **Not covered** — the requirement should not be inferred from Viridian's architecture.

## 2. GOVERN

**Viridian coverage:** Partial technical support

Relevant Viridian capabilities:

- frozen experimental-programme identity;
- authority boundaries;
- evidence-class policy;
- decision provenance;
- qualification-scope disclosure;
- explicit limitations and UNKNOWN states;
- installation/extension authority constraints.

Evidence Viridian can provide:

- programme/configuration identity;
- recorded decision rules;
- qualification envelope;
- blocked/unknown decision records;
- historical identity/provenance;
- limitations statement.

What Viridian does **not** provide by itself:

- board/executive governance;
- organization-wide AI policy;
- legal accountability structure;
- workforce roles and training;
- risk appetite;
- enterprise compliance management.

**Safe language**

> Viridian can provide technical evidence relevant to selected AI RMF GOVERN activities, particularly around experimental authority, decision provenance, and qualification scope.

## 3. MAP

**Viridian coverage:** Strong technical support for experimental context; partial organizational coverage

Relevant Viridian capabilities:

- model/checkpoint identity;
- code/harness identity;
- dataset/benchmark identity;
- evaluator identity;
- environment/dependency identity;
- experimental scope;
- claim scope;
- provenance relationships;
- historical identity preservation.

Evidence Viridian can provide:

- what exact system was tested;
- what evidence population was used;
- which evaluator produced the score;
- which environment produced the run;
- what changed between candidate and comparator;
- what claim the evidence is intended to support.

What Viridian does not independently determine:

- all affected human populations;
- social/legal context;
- organizational risk tolerance;
- downstream harms outside the available evidence.

**Safe language**

> Viridian can strengthen the experimental/system-context evidence available to AI RMF MAP activities.

## 4. MEASURE

**Viridian coverage:** Strong technical support

This is the closest conceptual fit.

Relevant Viridian capabilities:

- comparator fairness;
- evaluator identity and qualification;
- explicit missingness/UNKNOWN;
- repeated-run evidence;
- variance/sensitivity;
- protected regressions;
- evidence taint;
- protected confirmation;
- held-out qualification;
- causal/claim gates;
- reconstruction.

Evidence Viridian can provide:

- whether compared runs are materially comparable;
- whether evaluator identity changed;
- whether the required evidence is complete;
- whether a claimed effect survives repeated observation;
- whether protected constraints regressed;
- whether a final claim has independent confirmation;
- which evidence is non-qualifying or outside scope.

What Viridian does not guarantee:

- that every metric is substantively correct;
- that every evaluator is truthful;
- that the chosen metric reflects every relevant real-world risk;
- that passing an experimental gate implies overall system safety.

**Safe language**

> Viridian provides structured experimental-assurance evidence directly relevant to measurement and evaluation activities within an AI risk-management programme.

## 5. MANAGE

**Viridian coverage:** Partial technical support

Relevant Viridian capabilities:

- deterministic claim/admissibility rules under fixed inputs;
- PASS / FAIL / UNKNOWN-style decision semantics;
- protected-regression blocking;
- research-debt tracking;
- failure classification;
- remediation evidence requirements;
- clean-process fallback;
- historical taint and requalification.

Evidence Viridian can provide:

- whether a configured promotion claim is admissible;
- why it is blocked;
- what missing evidence would change the result;
- which historical evidence is affected after a defect;
- whether the system is operating outside its qualified envelope.

What remains an organizational decision:

- whether to ship;
- whether to accept the business risk;
- how to prioritize remediation;
- whether to discontinue a system;
- legal/regulatory action.

**Safe language**

> Viridian can provide evidence and gates that support risk-treatment decisions; it does not make the organization's risk decision.

## 6. Generative AI Profile relevance

NIST's Generative AI Profile is a cross-sector companion to the AI RMF intended to help organizations manage risks specific to generative AI.

Viridian's strongest technical relevance is to activities involving:

- evaluation;
- ongoing assessment;
- reproducibility;
- documentation of evidence;
- evaluator/model identity;
- change control;
- monitoring of regressions;
- qualification of claims.

This is a **high-level mapping only**.

No clause-level or action-level GenAI Profile compliance claim should be made without a dedicated source-grounded control analysis.

## 7. Example buyer translation

### Buyer question

> How does Viridian help our AI RMF programme?

### Defensible answer

> Viridian does not implement the whole AI RMF. It provides technical evidence for a narrower layer: the identity, provenance, comparability, evaluator integrity, confirmation status, regressions, uncertainty, and claim eligibility of AI experiments. Those records can support selected GOVERN, MAP, MEASURE, and MANAGE activities.

## 8. What not to say

Do not say:

- "Viridian is NIST compliant."
- "Viridian is NIST certified."
- "Using Viridian makes your AI RMF programme compliant."
- "Viridian implements the entire AI RMF."
- "NIST endorses Viridian."

## 9. Diligence output

For an enterprise buyer, a Viridian assurance report can be attached to broader AI-governance evidence as:

- experiment identity;
- evaluator/comparator evidence;
- uncertainty/missingness record;
- confirmation status;
- protected-regression outcome;
- claim-eligibility decision;
- limitations/remediation record.

That is the correct level of integration: **technical assurance evidence inside a broader organizational risk-management system**.

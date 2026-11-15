# The AI Recommendation Changed After One Field Was Corrected. Was the Decision Ever Stable?

**Deck:** An AI output is not ready for operating use until the team knows which plausible input changes would push it across a real action boundary.

**By Jared Mastroianni**

An AI recommendation can look solid right up to the moment someone corrects one field.

A facility status changes from closed to open. A sensor value changes from observed to inferred. A note timestamp moves into the prior shift. A work order that appeared unresolved is linked to a completed inspection. The model produces a different answer, and the operating path changes with it.

That does not automatically mean the model failed. The corrected fact may deserve to change the result. The problem is discovering the dependency only after the recommendation has influenced a queue, a dispatch, a customer message or an access decision.

Before an AI-assisted recommendation crosses into facility work, the system should test its decision sensitivity: which plausible changes to the current evidence would alter the recommendation, its priority or its permitted next action? The answer belongs in the operating record, not only in an evaluation notebook.

## Stability, correctness and authority are different questions

Teams often compress four questions into one confidence score.

**Repeatability** asks whether the system produces the same output from the same input. **Sensitivity** asks whether a small, plausible change to an input produces a materially different output. **Correctness** asks whether the output is supported by the governing facts and evaluation method. **Authority** asks what the workflow may do with that output.

None answers the others.

A recommendation can be repeatable and wrong because the same stale facility record is supplied every time. It can be sensitive for a good reason because the current operating mode should change the response. It can be technically correct but still lack authority to send a message or change a facility setting. It can carry a high model score while depending on an inferred field that no operator has verified.

The [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) is voluntary, cross-sector guidance. It calls for risk management across the AI lifecycle and for testing, evaluation, validation and verification appropriate to context. It does not prescribe a self-storage sensitivity test. It supports the underlying operating principle: the system must be evaluated in the conditions and workflow where people intend to use it.

## Define the action boundary before testing the answer

Sensitivity becomes useful when the team defines what counts as a material change.

Changing punctuation in a summary may change the wording without changing the operating decision. Changing the facility operating mode may move a recommendation from routine review to immediate human attention. Those outcomes should not be treated as equivalent.

Create a short action ladder for the use case:

1. **Display evidence** without a recommendation.
2. **Propose a classification or priority** for human review.
3. **Place work in a governed queue** without executing it.
4. **Prepare an action** that still requires named approval.
5. **Execute a bounded action** only through separate, explicit authority.

Then define the boundaries between those states. A decision-sensitivity test is material when a plausible evidence change moves the output across one of those boundaries, changes the responsible reviewer, changes the required evidence, or changes the permitted time window.

The boundary evaluator should be deterministic. The model may propose a class, but code or policy should determine that a particular class requires a human, that a missing source creates a hold, or that a recommendation may not become an action. Otherwise, the same model whose sensitivity is being tested also decides whether the sensitivity matters.

## Challenge plausible fields, not random words

Random prompt noise can help with some technical tests, but it is not an operating sensitivity plan. Facility work changes along recognizable dimensions.

Build a bounded challenge set around five types of evidence:

- **Identity:** facility, unit, customer, device, vendor, work order or policy version.
- **Time:** event time, source cutoff, local time zone, business calendar, maintenance window or evidence age.
- **State:** open, closed, restricted, active, completed, canceled, acknowledged or unknown.
- **Provenance:** observed value, staff entry, vendor response, calculated field, retrieved summary or model inference.
- **Missingness:** absent, unreadable, unavailable, not applicable, not evaluated or explicitly negative.

For each selected field, define a plausible alternative before running the test. Do not let the model invent a convenient alternate history. A facility calendar can be challenged with its prior approved version. A sensor state can be replaced with `unknown` if the connection failed. An inferred work-order status can be replaced with the last verified status. A local timestamp can be challenged at the daylight-saving or business-day boundary.

The test artifact must remain clearly synthetic. A challenged value is not a corrected facility record. It is a question asked of the decision path: if this fact were different, would the operating outcome cross a boundary?

## Turn sensitive fields into evidence obligations

When a plausible field change crosses an action boundary, that field becomes decision-critical for that recommendation.

Decision-critical does not mean globally important. A field may be critical for one recommendation and irrelevant to another. The obligation is local and traceable: verify this exact value from its governing source before this exact recommendation advances.

The evidence packet should record:

- the baseline source snapshot and its digest;
- the model, prompt, retrieval, policy and configuration versions;
- the field challenged and why the alternate value was plausible;
- the baseline and challenged outputs;
- the baseline and challenged action classes;
- the boundary crossed;
- the governing source for the critical field;
- the source freshness and retrieval outcome;
- the reviewer and disposition; and
- the final operating readback, if any action is later authorized.

This is more useful than saying the model was “robust.” Robust to what, within which range, for which facility state and against which operating boundary? A bounded sensitivity record gives the operator an answer that can be reviewed.

NIST’s [Four Principles of Explainable Artificial Intelligence](https://www.nist.gov/publications/four-principles-explainable-artificial-intelligence) describes explanation, meaningfulness, explanation accuracy and knowledge limits. The publication does not require counterfactual testing or certify an explanation method. Its distinction between an explanation and one that accurately reflects the system’s process matters here. A polished reason generated after the fact is not a substitute for evidence showing what actually changed the result.

## Keep the test away from live execution

A sensitivity runner should never share the live action path.

Clone the decision input into an isolated evaluation context. Block tool credentials and write permissions. Mark every challenged field as synthetic. Capture the output without placing it in the live queue. Compare the baseline and challenged outputs through the deterministic boundary evaluator. Only the verified baseline record may return to the operating workflow, and it should return with a new decision identifier after critical evidence is resolved.

This separation prevents a test from dispatching a vendor, changing gate behavior, sending a customer message or updating a facility record. It also prevents a synthetic value from being mistaken for observed history.

Use durable identifiers rather than screenshots alone. A practical event chain might include `recommendation_created`, `sensitivity_test_started`, `field_challenged`, `boundary_crossed`, `critical_evidence_verified`, `human_disposition_recorded` and `operating_readback_completed`. The [W3C PROV data model](https://www.w3.org/TR/prov-dm/) offers a general vocabulary for entities, activities, agents, generation and responsibility. It does not authenticate a facility record, but it is useful for keeping the source snapshot, test activity, reviewer and resulting decision connected without collapsing them into one event.

## A fictional gate-maintenance example

The following portfolio, facilities, systems, records, people, values and outcomes are entirely fictional. They do not describe modSTORAGE, Facily.ai, a customer or a deployed product.

Marrow Bay Storage uses an invented AI-assisted triage workflow to propose review priority for equipment notes. At the fictional North Harbor facility, the system receives a gate-motor alert, an operator note and a facility-calendar record.

The baseline recommendation is “routine next-business-day review.” The evidence packet shows that the recommendation depends on `facility_operating_mode=closed`. The sensitivity runner challenges that field with the plausible approved state `open_for_customer_access`. The recommendation changes to “human review before the next access period,” crossing the portfolio’s review-timing boundary.

That result does not prove the gate is unsafe, the facility is open, a dispatch is required or a customer will be affected. It proves that the proposed timing depends materially on one field.

The workflow places the baseline recommendation on hold. An operator retrieves the current approved facility calendar and confirms that the source snapshot used an outdated holiday schedule. The system creates a new baseline from the corrected source, retains the original and challenged records, and routes the new recommendation to the named facility reviewer.

No remote gate change occurs. No vendor is dispatched. No customer communication is prepared. Those actions would require their own evidence and authority.

The useful outcome is not that the AI “caught” the problem. The useful outcome is that the architecture exposed a fragile dependency before the recommendation acquired operating force.

## The Facility AI Decision-Sensitivity and Evidence Challenge

Use the accompanying tool before a recommendation enters a consequential queue or prepared-action state.

| Gate | Required question | Hold condition |
|---|---|---|
| Baseline | Can the exact source snapshot and system versions be reproduced? | Snapshot, version or purpose is missing |
| Boundary | Which change would alter priority, owner, evidence or permitted action? | No action ladder or boundary rule exists |
| Challenge | Is the alternate value plausible and explicitly synthetic? | The test invents an unbounded scenario |
| Evidence | Did a challenged field cross a boundary, and what source governs it? | Critical field is inferred, stale or unavailable |
| Human review | Did the reviewer see both outputs and the evidence difference? | Reviewer sees only a generated explanation |
| Release | Does the verified baseline remain within approved authority? | Recommendation changed, expired or lacks readback |

The tool is not a lease form, safety protocol, legal determination, engineering standard or compliance certification. It is an architecture worksheet for exposing which facts carry an AI-assisted decision.

## Monitor sensitivity after release

Predeployment tests are necessary, but they cannot represent every live combination of source quality, facility state, interface behavior and human use. NIST’s 2026 report [Challenges to the Monitoring of Deployed AI Systems](https://www.nist.gov/publications/challenges-monitoring-deployed-ai-systems-center-ai-standards-and-innovation) identifies functionality, operational, human-factors, security, compliance and large-scale-impact monitoring categories, while emphasizing that validated methods and common terminology remain immature. The report is a research synthesis, not a certification or a ready-made facility-monitoring standard.

For a bounded facility workflow, monitor:

- how often a recommendation has at least one decision-critical field;
- which source types most often trigger boundary crossings;
- how often critical evidence is unavailable or stale;
- how often verification changes the baseline;
- which model, prompt or policy versions change the crossing rate;
- how long sensitive recommendations remain on hold; and
- whether an executed action lacks the required sensitivity record or readback.

Do not interpret a low crossing rate as proof of safety. The challenge set may be weak. The action boundaries may be too broad. The system may be failing to expose missing evidence. Review samples from both crossing and non-crossing cases, and revise the challenge set when source schemas, policies, facility states or models change.

The [NIST Generative AI Profile](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence) is also voluntary and cross-sector. It emphasizes risks arising from human-AI configuration, confabulation and inappropriate reliance, among other concerns. It does not validate this tool or a self-storage deployment. Its practical relevance is that generated output must be evaluated as part of the surrounding system, including the people, evidence and authority boundaries that give the output consequence.

## Make instability visible before it becomes work

An operator should not have to discover decision sensitivity by accident.

The architecture can test plausible evidence changes before release, isolate the test from live tools, identify fields that carry the decision, verify those fields from governing sources and require a human disposition when an operating boundary moves.

That does not make the AI correct. It makes one important weakness observable.

If one corrected field can change the work, the field is part of the decision. Treat it that way before the recommendation leaves the screen.

---

## Sources and limitations

- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework), accessed November 14, 2026. Voluntary, cross-sector framework currently being revised; it does not prescribe or certify this architecture.
- [NIST AI 600-1, Generative Artificial Intelligence Profile](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence), July 2024, accessed November 14, 2026. Cross-sector profile; it does not establish a self-storage requirement or deployment result.
- [NIST AI 800-4, Challenges to the Monitoring of Deployed AI Systems](https://www.nist.gov/publications/challenges-monitoring-deployed-ai-systems-center-ai-standards-and-innovation), March 2026, accessed November 14, 2026. Research synthesis identifying monitoring categories and open challenges; it does not certify a monitoring method.
- [NISTIR 8312, Four Principles of Explainable Artificial Intelligence](https://www.nist.gov/publications/four-principles-explainable-artificial-intelligence), September 2021, accessed November 14, 2026. General explainability principles; it does not require counterfactual testing or validate a generated explanation.
- [W3C PROV-DM](https://www.w3.org/TR/prov-dm/), W3C Recommendation, April 2013, accessed November 14, 2026. General provenance model; it does not authenticate, authorize or complete a facility record.

## Disclosure

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai. This article proposes an operating architecture and uses an explicitly fictional scenario. It does not describe a released product capability, customer deployment, measured result, certification, legal conclusion or industry standard.

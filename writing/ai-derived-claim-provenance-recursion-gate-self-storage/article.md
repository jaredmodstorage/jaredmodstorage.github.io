# The AI Cited Another AI Summary. Where Did the Facility Evidence Go?

**Deck:** Model-generated summaries can move quickly through an operating stack until a derived sentence looks like a direct facility fact. A provenance gate should preserve the route back to authoritative evidence—and stop when that route disappears.

**By Jared Mastroianni**

![Three self-storage leaders walk beside an urban multistory facility while discussing the property.](070-urban-multistory-property-walk.png)

*Operational intelligence should remain connected to the physical property and the evidence produced there. Editorial image; provenance and non-documentary-use limits are recorded in the package.*

<!-- BODY START -->

An overnight AI prepares a regional briefing. It says a facility has “repeated climate-control instability.” The sentence cites a weekly exception summary. That summary was written by another AI from a daily digest. The daily digest was generated from work-order notes, sensor alerts and a manager email.

By morning, the briefing looks well sourced. It may still have no defensible route to an observed facility condition.

One model may have merged duplicate alerts. Another may have converted a planned setpoint into a measured temperature. A third may have turned “technician scheduled” into “repair completed.” The final system did not invent the whole story in one step. It inherited and compressed small semantic changes until the derived statement outran the evidence.

This is a provenance-recursion problem. A model-generated artifact reenters retrieval as though it were an ordinary source, then influences another generated artifact. Each layer can cite the one before it while losing the primary evidence, its time, its facility identity, its record class and its limitations.

The safe design is not to ban AI summaries. It is to classify them correctly and require claim-level ancestry before they support an operating conclusion.

## A citation is not the same as ancestry

A citation answers, “Where did this system get the statement?” Ancestry answers a harder set of questions:

- Which records ultimately influenced the claim?
- Which of those records are direct observations, human assertions, deterministic calculations or model-generated text?
- What transformations occurred between the source and the current sentence?
- Did any step widen the scope, strengthen the certainty or change the record class?
- Are the underlying records still current, authorized and available to the decision maker?

If an AI cites `regional-summary-44`, the citation can be technically correct while operationally inadequate. The summary is a derived entity. The decision needs to know what it was derived from and whether those leaf sources can support the requested use.

The W3C PROV model offers a useful vocabulary for this structure. It distinguishes entities, activities and agents and can represent that one entity was derived from another. Its provenance ontology is a general Web standard, not a self-storage control. The transferable idea is to preserve relationships among the artifact, the transformation that produced it, the inputs used and the actors responsible.

For an operating system, that means the claim—not just the document—needs a provenance record.

## Classify evidence before letting it travel

Start with a small, explicit set of evidence classes.

**Observed record.** A governed record of something an authorized source captured or a person directly observed, with time, identity and method. This classification does not guarantee that the observation is correct; it identifies the kind of evidence.

**Human assertion.** A statement entered by a person based on knowledge, communication or judgment. It needs attribution and time. It must not silently become a sensor reading or completed work.

**Deterministic derivation.** A value produced by a defined rule from named inputs—for example, a count of open work orders under a frozen query. The rule, input set and execution time matter.

**Model-generated interpretation.** A summary, classification, extraction, prediction or recommendation produced by an AI system. It may be useful, but it remains generated output until a separate process establishes a different state.

**Authoritative operating state.** The current record the organization has designated to govern a specific decision. Authority is purpose-specific. The maintenance system may govern work-order state while the access system governs credential status. A summary does not become authoritative because it combines both.

Carry the class through every transformation. When an AI extracts “repair completed” from a technician note, record that the extracted claim is model-generated and derived from a human assertion. Do not rewrite its ancestry as a direct maintenance observation.

Human review also needs precision. A reviewer may confirm that a summary accurately reflects the cited note. That does not prove the underlying event happened. Record `summary_fidelity_verified`, not `facility_condition_verified`, unless the reviewer actually performed the evidence step required for the latter.

## Build a claim graph, not a document breadcrumb

Document-level lineage is too coarse when one paragraph contains five claims from different sources.

Give each material claim a stable identifier. Link it to the exact source spans or structured fields used. Record the generating activity: retrieval policy, model release, prompt or instruction version, transformation type, time and permitted purpose. Then connect those sources to their own parents until the graph reaches governed leaf records.

The graph should tolerate multiple parents. A claim about an unresolved door condition may depend on an open work order, a manager note and a later inspection record. It should also show disagreement. If the work order is open while a generated digest says “resolved,” the conflict cannot disappear merely because the digest is newer.

Store at least four boundaries with each derived claim:

1. **Source boundary:** the exact records and fields that influenced it.
2. **Semantic boundary:** what each source actually represents—observation, plan, request, status, forecast or generated interpretation.
3. **Scope boundary:** the facility, asset, time window and population to which the claim may apply.
4. **Use boundary:** the decisions the claim may inform and the actions it may not authorize.

This allows a system to use a generated summary for navigation while refusing to treat it as evidence for a consequential action.

## Detect recursion before it becomes confidence

The gate should inspect every retrieved artifact for generation provenance. If an item is model-generated, the system should follow its parent links and calculate the derived depth. Depth alone is not the risk; an accurate two-step transformation can be safer than a poorly governed direct note. But depth is a useful trigger because every transformation creates another place where meaning can change.

Test for these conditions:

- the artifact has no parent references;
- a parent exists but is unavailable, unauthorized or outside retention;
- the graph contains a cycle;
- two generated artifacts cite each other;
- the same original record appears through several summaries and is counted as independent corroboration;
- a transformation changed the evidence class;
- a claim widened from one unit to a facility or from one facility to a portfolio;
- uncertainty or contradiction was removed;
- the leaf evidence is stale for the proposed decision;
- a corrected source has descendants that still carry the old claim; or
- the model is citing its own prior output as the only support for a new conclusion.

When any condition is material, the system should stop the claim from advancing. The handback should identify the blocked claim, the broken or circular edge, the last trustworthy ancestor, the proposed use and the human role that can resolve it. “Low confidence” is not enough. The operator needs to know what evidence is missing and what decision remains unauthorized.

## Do not count echoes as corroboration

Recursion creates a portfolio-scale illusion: five reports appear to agree, but all five descend from one source.

Count independent leaf evidence, not the number of derived documents. If a daily digest, regional rollup, executive briefing and chatbot answer all descend from the same manager email, they form one ancestry cluster. They are not four confirmations.

The same rule applies across models. Different model vendors or prompts do not create independent evidence when they consume the same source. Model diversity may help evaluate interpretation variance. It does not multiply the underlying facility facts.

Record an ancestry fingerprint for each claim: the sorted set of governed leaf identifiers plus their relevant versions. Compare fingerprints before labeling sources independent. If two claims share material leaves, disclose the overlap. If a source is itself generated and its leaves are unknown, classify independence as unknown rather than inferred.

## Bind corrections to descendants

When an authoritative source is corrected, the architecture should identify every dependent claim, summary, queue item and decision packet.

Do not overwrite the prior output and pretend it never existed. Invalidate or supersede the affected claim, record the correction event and evaluate each descendant according to its use. A dashboard tile may be regenerated. A manager briefing may need a visible correction. A pending recommendation may need re-evaluation. An already executed action requires a separate outcome and remediation review; changing the text does not reverse the action.

This extends correction propagation beyond document replacement. The system needs a reverse index from source to descendants, including generated outputs cached in search or vector stores. Removing a bad note from the primary system does not remove an embedding, a summary or an exported decision packet that still carries it.

NIST’s Generative AI Profile describes provenance tracking as a way to trace the origin and history of content and notes that provenance metadata can include creators, time, modifications and sources. It is voluntary, cross-sector guidance. It does not prescribe this gate or certify an implementation. It does reinforce the architectural point: origin and transformation history are part of risk management, not decorative metadata.

## A fictional self-storage example

**Every organization, facility, person, system, identifier, record, time, model behavior and outcome below is fictional and exists only to demonstrate the method.**

Fictional Harbor Lattice Storage operates fictional facility `FIC-HL-008`. A generated daily digest, `FIC-DIG-118`, summarizes two temperature alerts and one work-order note. It states: “Climate issue resolved after service.” The digest links to generated extraction `FIC-EXT-77`, which interpreted “vendor visit complete; monitor before closure” as a completed repair.

A second fictional model uses the digest to produce regional briefing claim `FIC-CLM-402`: “Facility 008 resolved repeated climate-control instability.” The wording adds two unsupported ideas. “Repeated” treats duplicate alert records as separate events. “Resolved” converts monitoring into closure.

The ancestry gate follows `FIC-CLM-402` to the digest, extraction and leaf records. It finds that both alert entries share one event identifier, the work order remains open and no authorized facility observation records a stable post-service condition. It also finds that the briefing and digest share the same leaf set, so their agreement is not independent corroboration.

The gate marks the claim `blocked_for_operating_use`, retains it as a generated artifact for audit, and creates a handback to the fictional facility manager. The handback asks for the specific closure evidence required by the fictional operator’s procedure. It does not tell the manager what the physical condition is.

Later, a fictional authorized inspection record states that the assigned check was completed and gives its observed result. The work-order owner separately decides whether the work can close. The briefing is regenerated with the new lineage. The record does not claim that the fictional architecture was deployed, that any real property condition existed or that the method improved performance.

## The operator tool: AI Evidence Ancestry and Recursion Gate

The accompanying gate records the claim, proposed use, evidence class, generation activity, parent and leaf sources, ancestry depth, cycle state, independence fingerprint, semantic changes, correction state, decision eligibility and handback.

Use it first on one high-consequence claim type: access status, work-order closure, payment state, safety escalation or another conclusion where a generated echo could trigger action. Require claim-level lineage before that class can move from informational display to decision support.

Test it with synthetic and explicitly fictional cases:

- a direct authoritative record with complete ancestry;
- a faithful summary with visible parents;
- a generated summary with no leaves;
- two summaries that share the same source;
- a source correction with cached descendants;
- a circular reference;
- a unit-level note widened to the portfolio; and
- a human review that verifies wording but not the facility condition.

Measure broken ancestry, shared-leaf corroboration attempts, class changes, unsupported scope widening, stale leaves, correction-propagation gaps and handback closure. Do not call a lower error count a facility result unless a governed evaluation actually supports that claim.

The core rule is simple: model output may help people find, compare and interpret evidence. It must not become observed facility fact by repetition.

If the system cannot show where a claim came from, how it changed and whether its leaf evidence can support the proposed use, it has not earned another summary. It has earned a stop.

<!-- BODY END -->

## Sources

- [NIST AI 600-1 — Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf), National Institute of Standards and Technology.
- [NIST AI 100-1 — Artificial Intelligence Risk Management Framework (AI RMF 1.0)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf), National Institute of Standards and Technology.
- [PROV-O: The PROV Ontology](https://www.w3.org/TR/prov-o/), World Wide Web Consortium Recommendation.

## Disclosure

Harbor Lattice Storage and every facility, person, system, identifier, record, time, model behavior, test and outcome in the example are fictional. No real customer, operator, deployment, product availability, performance result, incident or facility condition is represented. NIST AI 600-1 and AI RMF 1.0 are voluntary, cross-sector resources; W3C PROV-O is a general provenance ontology. They do not establish a self-storage requirement, validate this design or confer legal, security, AI-governance or operational compliance. This article presents an operating architecture, not legal, security, engineering or records-management advice.

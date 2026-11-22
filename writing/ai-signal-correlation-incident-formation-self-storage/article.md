---
title: "The AI Combined Three Facility Signals. Did It Find an Incident—or Invent One?"
slug: "ai-signal-correlation-incident-formation-self-storage"
canonical: "https://jaredmodstorage.github.io/writing/ai-signal-correlation-incident-formation-self-storage/"
author: "Jared Mastroianni"
historical_slot: "2026-11-21 evening AI architecture"
publication_destination: "Jared Mastroianni personal authority site"
publisher_owner: "Master Personal Site Authority"
featured_image: "assets/053-ai-development-ai-sensor-operations-walk.png"
---

<!-- BODY START -->

# The AI Combined Three Facility Signals. Did It Find an Incident—or Invent One?

*Correlation can help an operator find a case worth reviewing. It cannot turn several uncertain observations into one confirmed facility condition without a governed formation decision.*

By Jared Mastroianni

![Three self-storage operations colleagues discuss facility signals while walking a corridor.](assets/053-ai-development-ai-sensor-operations-walk.png)

A corridor temperature alert arrives at 2:07 p.m. A building-control record shows a fan command at 2:09. A maintenance note entered later says the area felt warm during a walkthrough.

An AI system links the three records and opens a “climate-control failure” incident. The label appears coherent. The records share a facility, a general area and a narrow time window. A regional operator sees one case instead of three disconnected signals.

But what, exactly, has been established?

The temperature alert may be a valid reading. The fan command may be a maintenance test rather than a response. The note may describe a different corridor. Even if all three records are accurate, their combination may support several explanations: a failed component, an open exterior door, a sensor issue, planned service or a short-lived condition that already cleared.

The AI did not observe an incident. It constructed a hypothesis from observations.

That distinction matters because case formation changes work. It can page an employee, dispatch a vendor, prioritize a queue, draft a customer message, suppress separate alerts or become the basis for later analytics. Responsible architecture needs a control between “these signals may be related” and “this is one operating incident.”

## Correlation creates a new decision object

Individual signals should remain individual records. A temperature reading, controller response, image classification, access event, work-order note and customer report each have their own source, identity, time, scope and limitation.

When a system groups them, it creates something new: a **case candidate**. The candidate is a derived object with its own rule or model version, evidence set, formation time, confidence state, alternative explanations and permitted consequences. It is not a more convenient copy of the source records.

This is a practical use of provenance. The [W3C PROV-O Recommendation](https://www.w3.org/TR/prov-o/) models entities, activities, agents, derivation, attribution and invalidation. It does not define a self-storage incident or assign operating authority. It does support a crucial design boundary: the source signals, the activity that combined them and the person or service responsible for the formation decision can remain distinguishable.

If the candidate later proves wrong, the system should withdraw or revise the derived case without rewriting the original readings. If a source record is corrected, the architecture should identify which case candidates depended on it. A flattened incident record makes both tasks harder.

## Make every signal earn admission

Correlation should not begin with every field the platform can reach. It should begin with an admission contract.

For each signal class, define:

- the governing source and stable record identity;
- the facility, zone, asset or account it is allowed to describe;
- event time, observation time and ingestion time;
- freshness and clock-quality requirements;
- units, schema and valid-value rules;
- whether the record is observed, reported, inferred or commanded;
- known test, maintenance and simulation states;
- permitted correlation purposes; and
- privacy, retention and access restrictions.

A signal that fails admission may still deserve investigation. It should not silently increase the weight of an incident hypothesis.

The current [OpenTelemetry Logs Data Model](https://opentelemetry.io/docs/specs/otel/logs/data-model/) illustrates why structure matters. It distinguishes the time an event occurred from the time a collection system observed it, and it defines resource, trace and span context. Those fields can make records easier to connect. They do not prove that two records share a physical cause or belong to one business incident. A shared trace ID is technical context, not operating truth.

## Align identity, time and meaning before scoring

Three records from the same portfolio are not necessarily three records about the same facility condition.

**Identity alignment** asks whether the records refer to the same governed facility, zone and asset. A controller named `RTU-2` in one system may not be the same equipment represented by “Roof Unit 2” in another. A corridor note may use a human label that changed after construction. Resolve the mapping before using proximity as evidence.

**Temporal alignment** asks whether the times are comparable. Preserve the occurrence time at the source, the observation time and the ingestion time. A note entered at 4:00 p.m. may describe a 1:30 p.m. walkthrough. A controller record received at 2:09 may contain an earlier device time. The correlation window should use the time relevant to the hypothesis, not whichever timestamp is easiest to query.

**Semantic alignment** asks what each record actually means. “Fan on” could be a command, an accepted request, a controller state or a verified physical condition. “Warm” could be a direct observation, a tenant report or a model-generated summary. These roles cannot be blended into a single evidence count.

Until all three alignments pass, the correct state is `held_for_alignment`, not `incident_confirmed`.

## Preserve alternatives instead of forcing one story

Correlation models often reward coherence. Operations needs disciplined doubt.

The case record should preserve at least one credible alternative hypothesis and the evidence that would distinguish it. If the leading hypothesis is equipment failure, alternatives might include planned maintenance, a stale sensor, an open door, a mapping error or normal transient behavior. The goal is not to manufacture every theoretical explanation. It is to prevent the first plausible narrative from becoming the only narrative visible to the reviewer.

Contradictory evidence belongs beside supporting evidence. A current maintenance window may weaken an equipment-failure inference. A second calibrated sensor may support it. A recent asset remapping may hold the entire case. Missing evidence should remain missing rather than being converted into a neutral score.

NIST’s [SP 800-61 Revision 3](https://csrc.nist.gov/pubs/sp/800/61/r3/final) distinguishes observable events, potentially adverse events and incidents, and recommends analysis and correlation across sources in a cybersecurity context. It also notes that event fidelity varies and that additional analysis may be needed to determine whether an incident occurred. That publication does not govern self-storage operations. The transferable principle is that correlation supports a determination; it is not the determination itself.

## Use a formation state machine

One `incident=true` field hides too much. Use explicit states:

1. **signal_received** — a source record arrived; eligibility is unresolved;
2. **signal_eligible** — identity, time, meaning and permitted purpose passed admission;
3. **case_candidate** — a named rule or model grouped eligible signals into a hypothesis;
4. **review_required** — consequence or uncertainty requires a qualified person;
5. **incident_formed** — an authorized reviewer or bounded policy accepted the case definition;
6. **incident_rejected** — the candidate did not meet formation requirements;
7. **incident_split** — one candidate contained more than one operating problem;
8. **incident_merged** — separately formed cases were later governed as one; and
9. **invalidated_or_reopened** — material source or policy change requires another decision.

Each transition should record who or what made it, the policy and model versions, the evidence set, the reason and the allowed next step. Formation should never imply that the physical condition is repaired, the source cause is proven or every affected person has been notified.

## Bind authority to consequences

The stronger the downstream effect, the stronger the formation gate.

A low-consequence candidate may be allowed to appear in a review queue automatically. A candidate that would dispatch emergency service, restrict access, contact customers, change a financial record or suppress separate safety alerts should require stronger evidence and named human authority.

This is where “human in the loop” becomes specific. The human is not there to click approve on a finished AI story. The reviewer needs the eligible source records, positive and contradictory evidence, time and identity alignments, alternative hypotheses, consequence class and the exact effects approval would permit.

The review interface should offer more than approve or deny. A qualified operator may:

- accept the proposed incident boundary;
- reject the candidate;
- split the candidate into separate cases;
- merge it with an already governed incident;
- request a current readback or physical check;
- correct an identity or time mapping; or
- route it to a technical, safety, privacy or operating owner.

The [NIST AI Risk Management Framework 1.0](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-ai-rmf-10) is voluntary and use-case agnostic. Its emphasis on context, validity, reliability, monitoring, human roles and risk-proportionate controls supports this design. It does not certify a workflow or supply a self-storage incident threshold.

## Observe the formation decision, not just the model call

An inference log that records only a score and latency cannot explain why a case exists.

For every case candidate, retain:

- candidate ID and version;
- exact source-record IDs and versions;
- admission results and exclusions;
- correlation rule, feature, model and threshold versions;
- identity, time and semantic alignment results;
- supporting, contradictory and missing evidence;
- alternative hypotheses;
- proposed consequence class and prohibited effects;
- reviewer decision, authority and reason;
- formed incident ID, if any; and
- downstream consumers, readbacks and later corrections.

Monitor candidate volume, rejection, split, merge, reversal and unresolved-aging rates by signal class and consequence. A rising formation rate could mean conditions changed. It could also mean a rule widened, an asset map drifted or a source began duplicating signals. The metric is a prompt to investigate, not a facility conclusion.

## A fully fictional self-storage example

The following portfolio, facility, systems, assets, people, records, times and outcomes are entirely fictional.

At fictional **Juniper Harbor Storage**, signal `JH-TEMP-441` reports 81°F in Corridor C at 2:07 p.m. Signal `JH-CTRL-118` records a fan command associated with asset label `RTU-2` at 2:09. Note `JH-NOTE-77`, entered at 3:52, says Corridor C felt warm during a 2:20 walkthrough.

The correlation service creates candidate `JH-CASE-CAND-19`. It does not declare a climate-control failure.

Admission finds that the temperature reading is current but its calibration status is unresolved. The controller record is valid, but the command occurred inside a fictional maintenance test window. The note is a direct human observation, yet its zone label is not mapped to a sensor ID. The asset registry also shows that `RTU-2` was renamed during an unverified fictional mapping change.

The system records equipment failure as one hypothesis and planned test activity, mapping error and short-lived warm air as alternatives. Because a customer notice and emergency dispatch would be consequential, the policy requires a facilities reviewer and a current readback.

The fictional reviewer holds formation, requests the current asset mapping and a second temperature reading, and prohibits customer communication, access restriction and emergency dispatch from this candidate. The case remains `review_required`. No incident, failure, repair or customer effect is claimed.

The example demonstrates a control sequence, not a deployment or operating result.

## Use the Signal-to-Incident Formation Gate

The companion tool turns the architecture into an operator review. It asks six questions in order:

1. Are the source signals eligible for this purpose?
2. Do facility, zone, asset and subject identities align?
3. Are occurrence, observation and ingestion times comparable?
4. Do the signals have compatible meanings and evidence roles?
5. What alternatives and contradictions remain visible?
6. Who may form the incident and authorize each downstream effect?

The blank CSV supports implementation planning. The fictional example preserves each source signal as its own row while sharing one case-candidate ID. It is deliberately a formation register, not an incident-response plan, a safety procedure, a customer-communication script or proof that any AI system is deployed.

## Build the smallest safe version first

Choose one low-consequence signal family and one review queue. Define source identity, event time, observation time, eligibility, a narrow correlation window, one alternative hypothesis, an authorized reviewer and a no-action candidate state. Test stale records, duplicated signals, maintenance windows, conflicting zones, remapped assets and late human notes.

Then verify the negative path. A rejected candidate should not dispatch work. A held candidate should not disappear. A split should preserve the original formation record. A corrected source should identify dependent candidates without erasing history.

The purpose of correlation is to help operators see relationships sooner. The safeguard is to keep the relationship provisional until the evidence, authority and consequence justify more.

Several signals can point in the same direction. They still do not become one incident by arithmetic. Make incident formation a governed decision of its own.

<!-- BODY END -->

## About Jared Mastroianni

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai. He writes about multi-location operations, evidence-bound automation and responsible AI architecture for self-storage.

## Editorial production note

The Juniper Harbor Storage scenario and all related records are fictional. The article and tool describe a vendor-neutral architecture pattern and do not claim a deployed product, customer result, safety determination, legal rule, certification or measured performance.

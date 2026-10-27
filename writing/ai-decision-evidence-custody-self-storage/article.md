---
title: "The AI Record Changed After the Incident. Which Version Is Evidence?"
slug: "ai-decision-evidence-custody-self-storage"
author: "Jared Mastroianni"
description: "A responsible-AI architecture for preserving the exact evidence, model, policy, review and readback behind a self-storage operating decision without rewriting history when facts change."
canonical: "https://jaredmodstorage.github.io/writing/ai-decision-evidence-custody-self-storage/"
publication_destination: "Jared Mastroianni personal authority site"
publisher_owner: "Master Personal Site Authority"
publication_state: "publisher handoff pending"
---

# The AI Record Changed After the Incident. Which Version Is Evidence?

**By Jared Mastroianni**

*An engineering review represents the operating and technical scrutiny required around consequential AI records. Editorial, non-documentary illustration; it does not depict the fictional facility, decision, incident, evidence packet or result in this article.*

**Deck:** An editable activity screen can tell you what the system believes now. It cannot, by itself, prove what evidence the AI used, what a person reviewed or what the facility confirmed at the time. Preserve the original decision packet, then append corrections without rewriting history.

<!-- BODY START -->

An AI-assisted operations system recommends keeping an interior aisle closed after a water alert. A manager reviews the evidence and approves the hold pending inspection. Two hours later, a calibration record arrives. The sensor reading may need a different interpretation, so the AI regenerates its summary.

The current screen now looks cleaner. The new policy version appears beside the corrected explanation. The earlier wording is gone.

What, exactly, did the manager approve?

If the system retained only the latest record, the answer may be impossible to reconstruct. The interface can show the best current understanding while silently replacing the evidence, model output and policy context that shaped the original decision. That is not a harmless display problem. It can change incident review, customer communication, staff accountability, vendor follow-up and the operator’s ability to explain why work remained open.

Responsible AI architecture needs two capabilities that are easy to confuse: **correction** and **custody**. Correction lets the system adopt better information. Custody preserves the exact record that existed when a consequential decision was proposed, reviewed, executed and verified. A trustworthy system needs both.

## The current record is not the historical record

Most operational software is designed to show the latest useful state. A work order displays its current status. A tenant record shows the current contact information. A policy page shows the current approved language. That is appropriate for daily work.

An incident reconstruction asks a different question: what information existed at a specific decision point, and what happened next?

The answer cannot come from a screen that quietly overwrites prior values. It needs a versioned evidence packet that binds the material inputs and outputs used at that moment. At minimum, preserve:

- the decision and facility-safe identifiers;
- the source-record identifiers and versions;
- the retrieval or selection rule;
- the prompt, model and configuration versions;
- the policy and authority versions;
- the AI proposal and stated limitations;
- the reviewer identity or governed role and review result;
- the authorized action, provider receipt and error state;
- the facility readback or other governing outcome evidence; and
- the creation time, retention class and amendment status.

That packet is not automatically the source of truth for every field. It is the source of truth for what the workflow assembled and presented at that decision point.

## Preserve five records instead of one blended narrative

An activity log often compresses several different facts into one sentence: “AI reviewed the alert, the manager approved it and the aisle remained closed.” That sentence may be convenient, but it is weak evidence.

Keep five records separate.

**Source record.** What did each originating system record, under which identifier and version? A sensor event, work order, camera observation and manager note may disagree. None should be rewritten to make the final story cleaner.

**Derived evidence packet.** Which source versions did the workflow select? What transformations, exclusions and retrieval rules produced the review material? The packet is a derived artifact, not an observed facility fact.

**Decision record.** What proposal did the AI produce, and what did the authorized person approve, reject, narrow or defer? Preserve the exact proposal and the human disposition. Do not replace the reviewed proposal with the AI’s later explanation.

**Action record.** What command or communication was attempted, accepted, rejected or partially applied? A provider receipt proves only the state it actually reports.

**Readback record.** What governing facility or business source later established? The aisle state, work-order state, customer notice and accounting result may require different readbacks.

These records can be linked. They should not be collapsed.

## Freeze the packet at the decision boundary

Create the decision evidence packet before the approval request opens. Serialize the governed fields in a documented order, assign an artifact identifier and compute a digest over the exact bytes. The reviewer should approve the packet identifier and digest, not a mutable query that will look different tomorrow.

NIST’s Secure Hash Standard specifies algorithms including SHA-256 that produce message digests and can help determine whether content changed after the digest was generated.[^1] A digest is useful here because the system can recompute it and detect a byte-level difference.

But a hash is not a truth machine.

A matching digest does not prove the source was correct, the packet was complete, the reviewer had authority, the action occurred or the facility became safe. It does not identify the producer unless identity is bound through a separate control. It also does not protect a record if an attacker can replace both the artifact and the expected digest.

The control therefore needs more than a `sha256` field. Restrict who can create, read, amend and verify decision evidence. Store the original in a protected location. Preserve the producer and reviewer bindings. Record access and export events. Apply the approved retention rule. Test that another authorized reviewer can retrieve and verify the packet later.

NIST SP 800-53’s audit and accountability controls address protection of audit information, non-repudiation, chain of custody, retention and audit-record generation.[^2] That catalog does not prescribe this self-storage pattern or certify a private system. It does show why evidence protection, identity association and retention are separate controls.

## Correct by amendment, not substitution

New information should change the operating view when it is relevant. It should not change history.

When a calibration record, corrected payment allocation, revised access log or manager observation arrives, create an amendment with:

- its own immutable artifact identifier;
- a reference to the earlier packet identifier and digest;
- the reason for the amendment;
- the new source and policy versions;
- the claims affected and unaffected;
- the person or process that created it;
- whether the operating decision must be reviewed again; and
- the disposition of the earlier record: active, superseded for current use, invalidated or preserved with unresolved conflict.

The earlier packet remains retrievable. The current interface may lead with the amended understanding, but it must expose that the original decision used a different packet.

W3C PROV-O provides concepts for entities, activities, agents, derivation and invalidation.[^3] An operator does not need to implement that ontology to use the central idea: a corrected entity can be derived from an earlier entity without pretending the earlier one never existed. Invalidation or supersession changes whether a record should be used now. It does not erase its role in the historical decision.

## Make the amendment consequence-specific

Not every correction reopens every decision.

A spelling fix in a nonmaterial note may require an append-only correction but no operational review. A newly discovered source that changes the facility, customer, amount, access state, safety classification or authorized action should place the affected decision back into review. The amendment rule should say why.

Use three dispositions:

**Historical-only amendment.** The correction improves description or metadata but does not change the reviewed operating conclusion. Preserve it and record why no new decision was required.

**Decision-impacting amendment.** The correction can change the recommendation, scope, authority or consequence. Hold any remaining action, route the new packet to an eligible reviewer and record a new decision.

**Evidence-conflict amendment.** The new record does not resolve the issue; it creates a conflict. Present both bounded claims and keep the consequence open. Do not ask the model to choose the more convenient narrative.

NIST’s AI RMF Core emphasizes systematic documentation and includes post-deployment monitoring, appeal and override, incident response, recovery and change management.[^4] Those outcomes support disciplined review, but they do not decide which self-storage events are consequential or who has legal authority. The operator must define those boundaries.

## Logs help correlation; custody needs additional controls

Structured logs are valuable. The OpenTelemetry Logs Data Model distinguishes event time from observed time and includes fields such as trace ID, span ID, resource, instrumentation scope and attributes.[^5] Those fields can help connect a decision packet to the service activity that produced it.

They do not, by themselves, make the log complete, immutable or authoritative. Sampling may omit records. Retention may expire them. An instrumentation change may alter field meaning. A trace identifier connects activity; it does not prove business authorization or physical outcome.

Use observability data as one input to custody, not as a substitute for the governed decision artifact. A high-consequence packet may reference trace and log records while preserving its own immutable manifest, reviewer disposition and facility readback.

## A fully fictional Copper Hollow example

The following scenario and every identifier, facility, system, person and outcome in it are fictional teaching material. They do not describe modSTORAGE, Facily.ai, a customer, deployment, product feature or real incident.

Fictional Copper Hollow Storage receives water-alert record `SENSOR-FIC-88` and open work record `WORK-FIC-19`. A fictional AI workflow assembles packet `PKT-FIC-204` using model `MODEL-FIC-7.3` and policy `POL-FIC-WATER-4.1`. Its proposal is to hold aisle reopening and request human review. A fictional reviewer approves the hold pending inspection.

The packet is represented as canonical UTF-8 JSON with keys sorted lexicographically, no optional whitespace and no trailing line terminator in the hashed byte string. Its SHA-256 digest is:

`b2e5548238fb9d1eb91da8e35ba902f140c6133a444e3f562c14a593fdfb19e6`

Later, an invented calibration record becomes available and policy version `POL-FIC-WATER-4.2` applies. The workflow does not edit `PKT-FIC-204`. It creates amendment `AMD-FIC-205`, references the earlier packet and digest, records the reason and sets `review_required` to true. The amendment’s digest is:

`3e13e3ce83f8030a0f1329a8690cf45e3b9b82c5c89d3226f5d5945ce984ab40`

Recomputing both digests from the supplied fictional artifact lines produces exact matches. The amendment’s `previous_sha256` also equals the original packet digest. That establishes internal byte-level chain consistency for the example. It does not establish that the fictional sensor was accurate, the aisle was unsafe, the reviewer was authorized or a physical action occurred.

The current view may show the calibration amendment first. The incident view must still show that the earlier hold was reviewed against `PKT-FIC-204`, not against the later packet.

## Use the custody test before calling a decision explainable

An AI decision is not reconstructable merely because a narrative exists. Before a consequential workflow is released, test whether another authorized person can:

1. retrieve the exact source-version manifest used at the decision point;
2. reproduce the governed packet bytes and digest;
3. identify the model, prompt, policy and configuration versions;
4. distinguish the AI proposal from the human decision;
5. distinguish provider acceptance from facility readback;
6. detect a changed packet, broken predecessor link or missing artifact;
7. follow every amendment without losing the original;
8. see whether a correction required a new decision;
9. confirm the approved retention and access controls; and
10. state the strongest allowed claim without turning system records into observed facility fact.

If any of those steps fail, the system may still present a current operational view. It should not present the historical decision as fully reconstructed.

The goal is not to freeze operations in the past. It is to let the record improve without letting the history move underneath the people responsible for it. Preserve the original packet. Append the correction. Reopen the decision when the consequence changes. Then explain the incident from evidence that still exists.

<!-- BODY END -->

## Practical operator tool

Use the accompanying [AI Decision Evidence Custody and Amendment Test](ai-decision-evidence-custody-and-amendment-test.md), [blank CSV template](ai-decision-evidence-custody-template.csv), [explicitly fictional worked ledger](ai-decision-evidence-custody-fictional-example.csv) and [canonical fictional artifacts](ai-decision-evidence-custody-fictional-artifacts.jsonl).

## Sources

[^1]: National Institute of Standards and Technology, [FIPS 180-4, Secure Hash Standard](https://csrc.nist.gov/pubs/fips/180-4/upd1/final), August 2015; accessed October 27, 2026. NIST notes a planned revision. This article uses SHA-256 only as a change-detection component, not proof of truth, identity or authorization.
[^2]: National Institute of Standards and Technology, [SP 800-53 Rev. 5, Security and Privacy Controls for Information Systems and Organizations](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final), including AU-9, AU-10, AU-11 and AU-12; accessed October 27, 2026.
[^3]: World Wide Web Consortium, [PROV-O: The PROV Ontology](https://www.w3.org/TR/prov-o/), W3C Recommendation, April 30, 2013; accessed October 27, 2026.
[^4]: National Institute of Standards and Technology, [AI RMF Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/), including documentation and post-deployment monitoring outcomes; accessed October 27, 2026. NIST states that AI RMF 1.0 is being revised.
[^5]: OpenTelemetry, [Logs Data Model](https://opentelemetry.io/docs/specs/otel/logs/data-model/), stable specification page; accessed October 27, 2026.

## About the author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.

## Editorial disclosure

AI assistance supported source discovery, drafting, comparison, artifact construction, digest verification and editorial QA under Jared Mastroianni’s direction. The architecture, Copper Hollow scenario, identifiers, packets and test are editorial proposals and fictional teaching material, not evidence of a product feature, deployment, customer result, legal requirement, certification or industry standard.

---
title: "The AI Found One Approved Exception. Why Did It Treat It as Portfolio Policy?"
slug: "ai-policy-exception-scope-self-storage"
author: "Jared Mastroianni"
canonical: "https://jaredmodstorage.github.io/writing/ai-policy-exception-scope-self-storage/"
publication_destination: "Jared Mastroianni personal authority site"
publisher_owner: "Master Personal Site Authority"
intended_slot: "2026-11-17 evening-ai-architecture"
status: "publication-ready; handoff pending"
featured_image: "066-industry-conference-peer-roundtable.png"
---

<!-- BODY START -->

# The AI Found One Approved Exception. Why Did It Treat It as Portfolio Policy?

**By Jared Mastroianni**

An AI system searches the operating record before recommending whether a facility manager may release a temporary access credential. It finds a prior approval: another manager, at another property, was allowed to issue a credential after a controller failure. The language looks useful. The model retrieves it, summarizes it and tells the current manager that the same route is approved.

The document was real. The approval was real. The conclusion was still wrong.

The prior record authorized one response at one facility, for one controller, during one outage, through a stated expiration time. It did not amend portfolio policy. It did not establish a precedent that software could generalize. It did not give the AI authority to decide that two situations were equivalent.

This is a different problem from hallucination. The system did not invent a source. It misclassified the source's role.

For operators building retrieval-augmented generation, copilots or agents, that distinction matters. A policy, an exception, an example and an obsolete record can contain similar words while carrying completely different authority. If the retrieval layer treats them all as interchangeable context, the model may turn a narrow decision into a portfolio-wide operating rule.

## Retrieval relevance is not decision authority

Most retrieval systems optimize for relevance. They select records whose language, embeddings or metadata appear close to the request. That can be useful for finding background. It is not enough for deciding what the operator may do.

An expired exception may be highly relevant to a current controller outage. A training example may be semantically closer to the question than the governing policy. A manager's note may describe the exact symptom. None of those facts makes the record authoritative.

Before an AI uses retrieved material in an operational recommendation, the system needs a second classification: **what role may this record play in this decision?**

At minimum, separate these classes:

| Record class | What it can support | What it cannot do by itself |
|---|---|---|
| Governing policy or procedure | Establish the current baseline within its stated scope | Prove the facts of the current case |
| Active exception | Authorize a defined deviation for the named scope and term | Create policy or authorize another case |
| Case evidence | Establish observed facts if source and freshness are adequate | Grant authority |
| Example or training material | Explain how a process may work | Control a live decision |
| Superseded or expired record | Preserve history and aid review | Govern current action |
| Unverified note or model output | Identify a question or lead | Establish fact, policy or permission |

The architecture should enforce these differences before generation, not rely on the model to infer them from prose.

## An exception is an authorization object, not a paragraph

If exceptions exist only as email sentences or free-form notes, a model has to guess their boundaries. A safer design represents an exception as a structured authorization object with fields the system can test.

That object should identify:

- the governing requirement being excepted, including version;
- the exact action permitted;
- facility, asset, workflow, role and case scope;
- effective and expiration times;
- the approving person or role and their authority basis;
- required compensating controls;
- stop conditions and revocation state;
- the decision record and evidence used;
- whether reuse in another decision is prohibited, advisory or allowed under a separate rule.

The final field is important. An exception should default to **non-reusable authority**. Another system may retrieve it for comparison or audit, but it cannot inherit the permission.

That default prevents a subtle but common reasoning error: “This was approved before, so it is approved now.” A prior approval proves only that a prior decision occurred. It does not prove that today's facts, policy version, risk owner, facility configuration or customer consequence are the same.

## Bind authority to the current decision identity

Every consequential AI request should have a decision identity before the system retrieves authority. That identity is more than a ticket number. It is a compact description of the case the AI is being asked to support.

For self-storage operations, it may include:

- facility identifier;
- account, unit, vendor, asset or incident identifier as applicable;
- requested action;
- policy domain and version;
- observed state timestamp;
- consequence class;
- requesting role;
- current workflow state.

The retrieval gate compares each candidate source against that identity. An exception record for Facility A fails the facility-scope test for Facility B. A credential-release exception fails the action-scope test for a gate-hours change. An approval that expired yesterday fails the time test. A record made under policy version 4 does not silently override version 5.

Some mismatches should remove the record from the authority set while leaving it in the background set. The AI can say, “A prior case may help an operator frame the question, but it does not authorize this action.” That is more useful than hiding history, and safer than treating history as permission.

## Put the scope gate before the model's answer

The control belongs between retrieval and generation. A robust flow looks like this:

1. Construct the current decision identity from authoritative records.
2. Retrieve potentially relevant material.
3. Classify every record by authority class.
4. Test scope, version, time, status, action and approver authority deterministically.
5. Build separate evidence sets: governing authority, current case facts, background only and rejected.
6. Generate the recommendation from the permitted sets.
7. Show the operator which records controlled the result and which were background.
8. Recheck the gate immediately before any external effect.

This is not just a prompt instruction. A prompt that says “use only applicable policy” still asks the model to decide applicability. The gate should be code, rules or another testable control whose output can be inspected.

The [NIST AI Risk Management Framework Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/) says context, targeted application scope, knowledge limits and human oversight should be understood and documented. It also calls for AI output to be interpreted within its identified context. That framework does not prescribe this self-storage gate. It supports the underlying discipline: intended context and limits are part of responsible operation, not optional metadata.

## Do not let similarity manufacture precedent

Embedding similarity can make two cases appear close while omitting the difference that controls authority. Both records may mention “gate controller offline.” One may involve a staffed facility during office hours; the other may involve an unattended property after hours. One may concern a vendor credential; the other a tenant account on hold. One exception may require a regional manager's live approval; the other may have allowed a facility manager to proceed.

Similarity is useful for recall. It is not a finding of equivalence.

If an operator wants a prior exception to become a reusable rule, that change should occur through the policy process. The new or revised policy can state the qualifying conditions, decision owner, permitted actions, evidence and effective date. The AI then retrieves that approved rule as policy. It should not reverse-engineer policy from accumulated exceptions.

This mirrors a general change-control principle. [NIST Special Publication 800-53 Rev. 5](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final) describes controlled system changes through review, approval, documentation and monitoring. It is federal information-system guidance, not a self-storage mandate. The useful analogy is narrow: a baseline changes through an authorized change process, not because enough deviations happen to resemble one another.

## Preserve provenance without confusing it with permission

The recommendation record should preserve which sources were considered, how they were classified, why a source was admitted or rejected and which authority actually governed the outcome.

The [W3C PROV-O Recommendation](https://www.w3.org/TR/prov-o/) distinguishes entities, activities and agents and supplies relationships for derivation, generation, attribution and association. An operator does not need to implement the full ontology to use the principle. A durable decision record should distinguish:

- the source record from the AI-generated recommendation;
- the activity that classified and used the source;
- the person or system that approved the final action;
- a prior exception that influenced review from the policy that authorized action.

That last distinction is the heart of the problem. A record can influence a decision without governing it.

## A fictional self-storage example

**The following facility, operator, incident, dates, identifiers and outcomes are entirely fictional and exist only to demonstrate the architecture.**

North Harbor Storage operates several facilities. Its current access procedure, ACC-12 version 6, requires a regional manager to approve any temporary credential issued while account eligibility cannot be verified through the primary system.

At fictional Facility NH-04, a controller outage occurred on September 3. Exception EX-221 allowed the on-site manager to issue vendor-only credentials between 9:00 a.m. and 3:00 p.m. for that controller, after verifying the work order and recording each credential. The exception expired when the controller was restored that afternoon.

On October 11, fictional Facility NH-09 reports a different outage. A tenant asks for access after the account system returns an unknown eligibility state. The AI retrieves EX-221 because both records mention a controller outage and temporary credentials.

The scope gate classifies EX-221 as an expired exception and background-only. It fails the facility, subject, action, time and eligibility tests. ACC-12 version 6 is admitted as governing policy. The current controller alert and account-system receipt are admitted as case evidence, but the unknown eligibility result is not converted into “eligible.”

The AI tells the manager that the prior exception does not authorize credential release, identifies the current regional approval path and preserves the unresolved account state. It can summarize EX-221 as a historical comparison, but it cannot cite it as permission.

If leadership decides that certain controller outages should allow a repeatable vendor-only process, leadership can revise ACC-12 or publish an approved standard exception class. That is a governance decision, not a retrieval shortcut.

## The operator tool: Policy–Exception Scope Admission Gate

The companion tool gives operators and system designers one row per retrieved record. It records the current decision identity, source class, scope tests, admissible use, rejection reason, human owner and pre-effect recheck.

Use it during design and testing, not only after an incident. Build cases where:

- the prior exception is at the wrong facility;
- the wording is nearly identical but the action differs;
- the exception has expired or been revoked;
- the baseline policy changed after approval;
- the approver lacked authority for the current consequence;
- a record is valid background but invalid authority;
- no governing authority can be established.

The final condition should produce a hold or handback, not a creative synthesis. An AI system that cannot find applicable authority should not manufacture it from precedent-like text.

Operators need the system to find useful history. They also need it to respect the boundary between history and permission. The right question is not only, “Did the AI retrieve a real record?” It is, “What was that record allowed to mean in this decision?”

That question turns retrieval from a search feature into an operating control.

---

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.

*Editorial assistance and research support were used in preparing this article. Final claims, examples and operating recommendations were reviewed for provenance and claim boundaries.*

<!-- BODY END -->

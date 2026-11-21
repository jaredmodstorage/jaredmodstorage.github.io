---
title: "The AI Says These Records Belong to the Same Tenant. Who Authorized the Join?"
slug: "ai-entity-resolution-tenant-record-linkage-self-storage"
canonical: "https://jaredmodstorage.github.io/writing/ai-entity-resolution-tenant-record-linkage-self-storage/"
author: "Jared Mastroianni"
historical_slot: "2026-11-20 evening AI architecture"
publication_destination: "Jared Mastroianni personal authority site"
featured_image: "063-operations-metrics-roundtable.png"
---

<!-- BODY START -->

# The AI Says These Records Belong to the Same Tenant. Who Authorized the Join?

*A match score can help find candidates. It cannot decide, by itself, that two facility records represent one person or that their permissions, balances and history may be combined.*

By Jared Mastroianni

![Four self-storage leaders review operating records around a conference table overlooking storage units.](assets/063-operations-metrics-roundtable.png)

Two records look like the same tenant. The names differ by one character. The phone numbers share the same last seven digits. One record belongs to a former customer at Facility A; the other belongs to a current tenant at Facility B. An AI service assigns a 96 percent match score.

What may the system do next?

It may place the pair in a review queue. It may show the evidence that raised and lowered the score. It may ask an authorized employee to resolve the ambiguity.

It may not silently combine the records, carry an access state from one facility to another, move a balance, inherit a consent, or tell a customer that the organization has verified a single identity. Similarity is not authority.

Record linkage is already part of ordinary multi-location work. Names change. Phone numbers are recycled. Email addresses are shared. A customer can rent at more than one property, and separate platforms can assign different local identifiers to the same person. AI can make candidate generation faster. It can also make a weak assumption travel farther before anyone sees it.

The architecture should therefore separate three decisions: **candidate**, **link** and **merge**. A candidate is a possibility worth checking. A link says two source records have an approved relationship while preserving their separate identities. A merge creates or updates a governing identity and may change what downstream systems can see or do. Those states should never be compressed into one `matched=true` field.

## A score is not an identity decision

A matching system compares features: name, normalized address, phone, email, date of birth, government or account identifiers, device information, facility history, and other permitted evidence. It may use deterministic rules, a statistical model, an embedding or a combination.

The output often looks authoritative because it is numeric. But a score of 0.96 is not automatically a 96 percent probability that the records belong to one person. Its meaning depends on the training population, candidate-generation method, feature set, calibration, threshold and operating context. A score produced among records already narrowed to the same facility does not carry the same meaning across an entire portfolio.

The consequence matters too. A lower-confidence link might be acceptable for showing an employee two possible search results. The same link may be unacceptable for changing gate access, combining balances, disclosing account history, applying a legal notice, or deciding who is authorized to act for a tenant.

The system needs a decision policy above the model. That policy should identify the permitted use, required evidence, conflict rules, human authority, expiration and downstream effect. The model proposes. The policy determines what the proposal can become.

## Keep the source records intact

The fastest way to lose control is to overwrite two local identities with one portfolio identity before the relationship is settled.

Preserve each source record, its facility, source system, local identifier, observed version and effective time. Store the proposed relationship as a separate object. That object should say which records are being compared, which feature and rule versions were used, what evidence agreed, what evidence conflicted, who reviewed the case and what relationship was approved.

This design follows a practical provenance principle. The [W3C PROV overview](https://www.w3.org/TR/prov-overview/) distinguishes entities, activities and agents so that derivation and responsibility can be represented. It is not a self-storage identity standard. It does, however, support a useful boundary: source records, the matching activity and the person or service making a decision should remain distinguishable.

Preserving the originals also makes correction possible. If a reviewer later learns that two people share a family phone number, the organization can withdraw the link and identify every downstream view or action that depended on it. A destructive merge without dependency records turns a correctable judgment into a forensic problem.

## Separate identity resolution from identity verification

Finding a unique record in a population is not the same as proving that the person presenting evidence owns that identity.

[NIST SP 800-63A-4](https://pages.nist.gov/800-63-4/sp800-63a.html) separates identity resolution, evidence validation and identity verification. Its requirements govern federal digital identity contexts, not ordinary self-storage account management. The distinction is still valuable. A portfolio may resolve two records as likely referring to one person while still lacking sufficient evidence that the caller, visitor or online user is that person.

That means a cross-facility match must not become a shortcut around the current facility's verification procedure. A shared email address, familiar voice, old access code or matching last name may help route a case. None should silently grant authority over another record.

The review screen should use precise language:

- **candidate:** records may refer to the same person;
- **linked:** an authorized review approved a defined relationship;
- **verified for this interaction:** the current person met the applicable verification procedure;
- **authorized for this action:** policy permits the requested action in the stated scope; and
- **merged:** a designated governing record replaced or absorbed specified source functions under an approved change.

One state does not imply the next.

## Make disagreement visible

Matching systems are often designed to display confirming evidence and hide contradictions inside the score. Operators need both.

If the name and phone align but the date of birth conflicts, show the conflict. If an address is old, identify its effective date. If one source says the email was verified and another merely stores the same string, preserve that distinction. If a phone number appears on several active records, treat reuse as negative evidence instead of rewarding every pair.

Missing is not agreement. Two blank dates of birth are not a match. A normalized apartment address can remove meaningful unit details. A transliterated or shortened name can be legitimate without behaving like an exact identifier. The architecture needs field-specific semantics, not a generic count of matching columns.

The reviewer should also see why the pair entered the candidate set. Candidate generation can create blind spots. A rule that considers only records sharing a phone number will never surface the same customer after a number change. A broad semantic search may surface too many people with similar names. Record the blocking rule and the population searched so a later reviewer can understand what was eligible to be found.

## Bind thresholds to allowed effects

Do not publish one portfolio-wide match threshold and call the problem solved.

Create consequence classes. Search assistance, analytics deduplication, customer communication, account maintenance, financial action and access control should not share an automatic decision rule. For each class, specify whether the system may suggest, create a reversible link, require a second reviewer, or prohibit automated resolution.

High-consequence effects should require stronger, independent evidence and a current verification step. They should also have explicit conflicts that force handback regardless of score. A government identifier mismatch, an active fraud flag, incompatible dates of birth or conflicting facility ownership may be a hard stop under approved policy. The exact rules belong to the operator's legal, security, privacy and operating review; this article does not supply them.

NIST's [AI Risk Management Framework Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/) is voluntary and cross-sectoral. Its emphasis on documented context, risks, human oversight, monitoring and measurement supports this consequence-based approach without providing a self-storage threshold. The number must earn its meaning in the actual population and use.

## Limit the data before improving the model

Identity-resolution projects can become collection projects. Every additional field appears useful because it might improve separation. That is the wrong default.

Start with the minimum permitted evidence required for the decision. Record the purpose for each feature, its source, retention, authorized users and whether it can be used for model development. Keep sensitive values out of general traces and dashboards. Use protected references where the reviewer can retrieve evidence under the right role rather than copying customer data into every log.

The [NIST Privacy Framework](https://www.nist.gov/privacy-framework) is voluntary guidance for managing privacy risk; it is not a declaration of compliance and does not determine which data a storage operator may use. Its value here is managerial: data processing creates risks that should be identified, governed, controlled, communicated and monitored alongside the technical match quality.

A feature can improve a score and still be inappropriate for the purpose. A retained value can also become stale, inaccurate or unexpectedly revealing when combined with other records. Technical availability is not permission.

## Human review needs a real decision surface

A reviewer cannot independently decide if the interface shows only `96% match — approve?`

Present the source records side by side, with facility and system identity intact. Show exact agreements, normalized agreements, conflicts, missing fields, source ages, validation status and reuse counts. Identify the model, rules and threshold that produced the candidate. Display the allowed decision and the effects that would follow.

The reviewer should be able to choose:

- approve a limited link;
- reject the link;
- request defined evidence;
- refer the case to a qualified owner;
- mark the pair as known different people; or
- escalate a suspected duplicate or fraud condition under approved procedure.

Do not make “merge” the easiest or default button. Require a reason code and an evidence reference. Prevent the same person who changed the matching rule from quietly adjudicating all of its uncertain outputs when independent review is material.

Monitor reviewer disagreement, reversal rate, unresolved backlog, population coverage and downstream corrections. A high approval rate may mean the model is precise. It may also mean the screen encourages approval or the queue excludes difficult cases.

## A fictional portfolio example

The following scenario, portfolio, facilities, people, records, values and decisions are entirely fictional.

Fictional North Harbor Storage Group receives a candidate pair. Record `NH-A-1842` is a former tenant at fictional Harbor East. Record `NH-B-7710` is an active tenant at fictional Harbor North. The names differ by a middle initial. The normalized street address agrees. The phone numbers match, but the number appears on three portfolio records. The dates of birth conflict. The candidate service returns 0.94.

The review policy allows the service to suggest search candidates above its documented threshold. It does not allow automatic cross-facility linking when a core attribute conflicts or a supposedly identifying phone number is reused.

The system creates review case `ER-FIC-204`, preserves both source versions and shows the positive and negative evidence. It prohibits access, balance, consent and communication effects. The reviewer selects **request evidence** and routes the case to the authorized account-resolution owner. No records are merged, no gate state changes and no customer history crosses facilities.

A later fictional review establishes that the records belong to two relatives at the same address who share a phone plan. The candidate is rejected, the pair is marked as known different people for the scoped rule version, and no source record is rewritten.

The example demonstrates a control sequence, not a deployment or performance result.

## Use an entity-resolution decision gate

Before a candidate can change an operating record, complete a gate that ties the proposed relationship to its evidence, authority and effects.

| Gate | Required record | Hold condition |
| --- | --- | --- |
| Scope | Exact records, facilities, systems, local IDs and observed versions | Target or population is ambiguous |
| Purpose | Permitted use and consequence class | Candidate is being reused for a broader purpose |
| Method | Candidate rule, feature set, model and threshold versions | Resolved runtime cannot be reproduced |
| Evidence | Agreements, conflicts, missing values, reuse counts and source ages | Conflicting or stale required evidence |
| Decision | Candidate, limited link, reject, request evidence or merge | Interface offers only approve or deny |
| Authority | Named reviewer role, policy version and decision time | Reviewer lacks authority for the effect |
| Effects | Explicit allowed and prohibited downstream changes | Link could silently change access, money or communication |
| Recovery | Reversal path and dependency register | A wrong link cannot be withdrawn and traced |
| Monitoring | Review date, expiration and correction owner | Link is treated as permanent truth without revalidation |

The companion **AI Entity-Resolution Decision Gate** includes a blank CSV and a completed fictional record. It does not prescribe legal evidence, universal thresholds or vendor behavior.

## The operating rule

AI can help an operator find records that deserve attention. That is valuable work. It becomes dangerous when candidate generation, identity verification and operating authority collapse into one invisible step.

Keep the source records intact. Show disagreement. Bind thresholds to consequences. Require a current verification path for consequential actions. Record the person and policy that authorized a relationship. Make every link reversible and every dependent effect discoverable.

The right question is not, “How confident is the model?”

It is, “What relationship did we authorize, for which purpose, on what evidence, and what is the system now allowed to do?”

<!-- BODY END -->

## Sources

1. National Institute of Standards and Technology, [NIST Special Publication 800-63A-4: Digital Identity Guidelines — Enrollment and Identity Proofing](https://pages.nist.gov/800-63-4/sp800-63a.html), accessed November 21, 2026. Federal digital-identity guidance used for the distinction among resolution, validation and verification; it is not a self-storage account-management standard.
2. National Institute of Standards and Technology, [AI Risk Management Framework Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/), accessed November 21, 2026. Voluntary cross-sector framework used for governance, context, oversight, measurement and monitoring concepts; it does not supply identity-match thresholds.
3. National Institute of Standards and Technology, [Privacy Framework](https://www.nist.gov/privacy-framework), accessed November 21, 2026. Voluntary privacy-risk guidance; it does not establish legal compliance or authorize particular customer-data uses.
4. World Wide Web Consortium, [PROV-Overview](https://www.w3.org/TR/prov-overview/), W3C Working Group Note, April 30, 2013; accessed November 21, 2026. Provenance model used by analogy to keep source entities, matching activities and responsible agents distinct.

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.

## Editorial disclosure

North Harbor Storage Group and every facility, person, record, identifier, score, policy, review and outcome in the example are fictional. The governed image is a non-documentary editorial asset; the retained registry does not state its production method. It is not evidence of a customer, meeting, deployment, product capability or result. AI assistance supported research synthesis, drafting, tool production and editorial QA under Jared Mastroianni's direction. The article presents a proposed operating architecture, not legal, privacy, security, identity-proofing or site-specific implementation advice.

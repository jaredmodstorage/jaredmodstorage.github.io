---
title: "The Operator Approved the Batch. Which Facility Actions Were Actually Inside It?"
slug: "ai-batch-approval-action-manifest-self-storage"
canonical: "https://jaredmodstorage.github.io/writing/ai-batch-approval-action-manifest-self-storage/"
author: "Jared Mastroianni"
historical_slot: "2026-11-02 evening AI architecture"
publication_destination: "Jared Mastroianni personal authority site"
featured_image: "065-access-technology-leadership-demo.png"
---

# The Operator Approved the Batch. Which Facility Actions Were Actually Inside It?

*Human review is meaningful only when approval binds to an exact, immutable set of facility actions—and execution can be reconciled to that same set.*

By Jared Mastroianni

![Three self-storage leaders review an access-technology interface on a tablet near a facility entrance.](assets/065-access-technology-leadership-demo.png)

An operations system presents a regional manager with a clean summary: **Approve 12 preventive-maintenance actions across four facilities.** The manager reviews the reason, the total count and the expected schedule, then selects Approve.

Between that click and execution, the queue changes. One task is reprioritized. A thirteenth task is added after a new sensor alert. A facility identifier is corrected. Eleven actions succeed and one fails.

What did the manager authorize?

“The maintenance batch” is not a sufficient answer. It is a label, not an authorization boundary. If the system cannot reproduce the exact actions, targets, payloads, exclusions and conditions visible at approval time, the human-in-the-loop control is mostly theater.

The architecture needs a stronger object: an **immutable action manifest**. Approval should bind to that manifest, not to a mutable list, a dashboard summary or whatever happens to be in the queue when a worker begins.

## Batch approval is a set-membership decision

A single facility action already needs a target, purpose, authority, preconditions and an expected result. A batch adds another question: which individual actions belong to the approved set?

That sounds obvious until the list is assembled from changing records. A maintenance agent might select tasks that are due, not blocked, assigned to a qualified vendor and within a spending limit. Every one of those facts can change. The screen might say “12 actions,” while the execution service later resolves the query again and finds 13.

The dangerous design is to approve the query:

> Run all eligible preventive-maintenance tasks in the Northeast region.

The safer design approves the result of that query at a defined moment:

> Run action IDs A101 through A112, with these facility and asset targets, these payloads, these limits and these preconditions.

The difference is not cosmetic. The first statement delegates future scope to the system. The second creates a bounded authorization.

An operator may intend to approve a class of work, but software should not silently convert that intention into authority over future members of the class. A newly eligible task should become a new proposal. A changed task should require revalidation and, when the change is material, renewed approval.

## Freeze the action, not just the count

A trustworthy manifest needs more than 12 rows. Each row should carry enough information to establish what will happen and where. At minimum, record:

- a unique action ID and manifest ID;
- facility ID, asset or unit ID and any relevant customer or vendor ID;
- action type and exact payload;
- source records and their observed versions or timestamps;
- governing policy, model, prompt, tool and connector versions;
- preconditions that must still be true at execution;
- financial, communication or access limits;
- exclusions and prohibited side effects;
- the human approver, approval time and approval decision;
- the total manifest count and an integrity digest.

The digest matters because it lets the system detect whether the serialized manifest changed after approval. NIST's Secure Hash Standard describes hash algorithms that generate message digests used to detect whether messages have changed. That is useful, but the boundary must remain clear: a matching digest does not prove that the operator understood the batch, that every item was semantically correct or that execution stayed within authority. It proves only that the hashed representation matches.

The human review surface therefore matters as much as the stored manifest. Show the operator a stable count, grouped targets, material differences, exceptions, limits and a way to inspect individual rows. Do not hide 12 distinct facility actions behind a green summary card.

## Separate proposal, approval and execution

These are different events and should remain different records.

The proposal says what the system recommends. The approval says which proposal version a person authorized. Execution says what workers actually attempted. Receipts say what each target accepted, rejected or completed.

That separation follows a basic provenance principle. The W3C PROV Data Model distinguishes entities, activities and agents, along with derivations and responsibility. An action manifest is an entity. Generating it, approving it and executing it are different activities. The recommending model, approving operator and executing service are different agents. Collapsing them into one “completed batch” record destroys the relationships an investigator needs later.

NIST's AI Risk Management Framework is voluntary and domain-neutral, but its emphasis on incorporating trustworthiness into the design, use and evaluation of AI systems is directly relevant. In an operating environment, trustworthiness includes knowing what the AI proposed, what the person accepted and what the system did.

This is also where least privilege becomes operational. NIST SP 800-53 is a flexible catalog for information-system security and privacy controls, not a self-storage AI rulebook. Still, its control concepts are useful design references. A batch worker should receive only the authority needed for the approved manifest, not standing permission to act on every item that later satisfies the original query.

## New members do not inherit old approval

Suppose an operator approves 12 work orders at 10:02 a.m. At 10:04, another sensor event creates a thirteenth proposal. The new item may look identical to the approved items. It may even be more urgent.

It is still not approved.

The correct behavior is to create a new proposal or an explicit amendment. The system can say, “One additional action now qualifies. Review separately.” It cannot say, “This looks like the batch you approved, so we added it.” Similarity is not authority.

The same rule applies to substitutions. If one work order is blocked, an agent should not replace it with another eligible item to preserve the count of 12. The count was a property of the approved set; it was not a quota granting freedom to choose any 12.

Material changes to an existing row need the same discipline. A corrected typo may not affect meaning. A different facility, asset, vendor, communication recipient, amount, access level or execution payload does. The system should define which changes invalidate approval and enforce that rule before work begins.

## Preconditions must be rechecked without expanding scope

Freezing a manifest does not mean ignoring live conditions. The worker still needs to recheck time-sensitive preconditions: Is the asset still out of service? Is the vendor still authorized? Is the facility open for the planned access window? Has a manager placed the task on hold?

This creates a two-part gate:

1. **Membership gate:** Is this exact action in the approved manifest?
2. **Execution gate:** Are its approved preconditions still true?

Passing the execution gate cannot create membership. If a new task now meets every rule, it remains outside the manifest. Failing the execution gate should stop or defer the approved action, not invite the agent to invent a substitute.

The result is intentionally asymmetric: changing conditions may narrow execution, but they may not broaden approval.

## Reconcile receipts at the item level

A batch status of “partially complete” is not enough for operations. The operator needs to know which facilities and assets were affected.

For every manifest row, preserve an execution record with:

- attempted, skipped, blocked, failed or succeeded status;
- attempt time and executing service identity;
- idempotency key or equivalent duplicate-prevention control;
- connector and target-system response;
- resulting record or external receipt ID;
- observed postcondition;
- retry eligibility and next owner;
- any human correction or cancellation.

Then reconcile four counts: approved, attempted, succeeded and unresolved. Those totals should tie to the individual rows, not to a separate dashboard counter.

If 12 actions were approved, 11 succeeded and one failed, the system should show the failed action as unresolved. It should not rerun the entire batch. It should not mark 12 complete because 12 requests were sent. It should not add a replacement action so that the success count reaches 12.

Retries must also remain bound to the same approved payload and target. If the retry requires a different vendor, amount or action, it is a new proposal.

## A fictional self-storage example

The following scenario is fictional and is provided only to show the control design.

Harborline Storage Cooperative operates four fictional facilities. Its maintenance agent proposes 12 preventive-maintenance tasks: three at each property. The regional operator reviews a manifest that lists every facility ID, asset ID, work type, permitted vendor category, access window, maximum authorized amount and source work-order version.

At approval, the platform freezes manifest `HB-2026-1102-01`, records 12 members and computes a digest over the canonical manifest representation.

Two minutes later, a new inspection record makes a thirteenth task eligible. The platform displays it as a separate proposal. It does not attach the task to the approved manifest.

During execution, 11 tasks succeed. One fails because the vendor credential is no longer current. The system records 12 approved, 12 evaluated for execution, 11 attempted successfully and one blocked before vendor dispatch. The blocked item remains unresolved with a named human owner. No substitute is generated.

That outcome is less visually satisfying than a green “batch complete” badge. It is also truthful, reviewable and operationally useful.

## The batch manifest test

Before allowing an AI-assisted system to execute multiple facility actions from one approval, run this test:

| Control question | Pass condition | Failure signal |
| --- | --- | --- |
| What exactly was approved? | A versioned manifest contains every action, target, payload, limit and exclusion. | Approval points to a mutable query, queue or label. |
| Can membership change after approval? | Any added, removed or materially changed row invalidates the old approval for that row or manifest. | Workers resolve the eligible set again at execution. |
| Was the review comprehensible? | The operator saw the count, material differences, grouped targets, exceptions and drill-down rows. | A summary card concealed the underlying actions. |
| Is integrity checked? | The execution service verifies the approved manifest ID, version and digest. | Count alone is treated as proof of sameness. |
| Are live conditions respected? | Preconditions can stop or defer an approved action without adding a new one. | Failed items are silently substituted. |
| Is authority bounded? | Execution credentials and tools are limited to approved action types and targets. | The worker has standing portfolio-wide authority. |
| Can outcomes be reconciled? | Every member has an item-level receipt and the totals tie. | Only a batch-level success percentage remains. |
| Are retries controlled? | A retry preserves the approved target and payload or returns for review. | A retry changes the action while keeping the old approval. |

The accompanying template turns these questions into a working manifest and reconciliation record.

## Human approval should make the system smaller

The point of human review is not to decorate automation with a name and timestamp. It is to narrow what the system may do.

After approval, the authorized action space should be smaller than it was during proposal generation: these actions, these targets, these limits, these preconditions and no others. New information may stop work. It may trigger a new recommendation. It may justify an amendment. It should not silently enlarge the old decision.

For self-storage operators, that distinction protects more than an audit trail. Batch actions can touch access, maintenance, pricing, customer communications, vendor dispatch and money. A vague approval can spread one ambiguity across many facilities at once. An immutable manifest keeps the operator's decision attached to the actual work.

Approve the set. Execute the set. Reconcile the set. If those three sets are not identical—or if the difference is not explicitly explained—the batch is not under control.

## Sources and limits

- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework): voluntary, domain-neutral guidance for incorporating trustworthiness into AI design, development, use and evaluation. NIST states that AI RMF 1.0 is being revised; this article uses the current framework page as a risk-management reference, not as a self-storage mandate.
- [NIST SP 800-53 Rev. 5](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final): a flexible security and privacy control catalog used here as a transferable reference for least privilege, auditability and change control. It is not presented as a governing self-storage AI standard.
- [W3C PROV-DM](https://www.w3.org/TR/prov-dm/): a domain-agnostic provenance model covering entities, activities, agents, derivation and responsibility.
- [NIST FIPS 180-4](https://csrc.nist.gov/pubs/fips/180-4/upd1/final): specifies secure hash algorithms and explains that digests can detect changed messages. A digest does not prove human comprehension, semantic correctness, authorization or successful execution.

*Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.*

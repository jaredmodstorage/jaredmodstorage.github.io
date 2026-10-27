---
title: "The Operator Changed the AI Recommendation. Which Decision Did the System Record?"
description: "Human review is not a binary approval step. When an operator changes an AI proposal, the architecture must preserve the delta, recheck authority and record the human-authored decision that actually governs the work."
author: "Jared Mastroianni"
date: "2026-10-27"
historical_slot: "2026-10-24 evening AI architecture"
canonical: "https://jaredmodstorage.github.io/writing/ai-human-decision-delta-self-storage/"
publication_destination: "Jared Mastroianni personal authority site"
publisher_owner: "Master Personal Site Authority"
image: "052-ai-development-ai-engineering-design-review.png"
image_alt: "AI-generated editorial scene of Jared Mastroianni listening to two colleagues during a technology design review."
---

# The Operator Changed the AI Recommendation. Which Decision Did the System Record?

**Deck:** Human review is not a binary approval step. When an operator changes an AI proposal, the architecture must preserve the delta, recheck authority and record the human-authored decision that actually governs the work.

**By Jared Mastroianni**

![AI-generated editorial scene of Jared Mastroianni listening to two colleagues during a technology design review.](052-ai-development-ai-engineering-design-review.png)

*A responsible AI review should make the proposed fields, human changes, governing evidence and final authority visible in the same decision record. AI-generated editorial image; not a documentary photograph of a real meeting or deployment.*

<!-- BODY START -->

An AI assistant proposes restricting one fictional access credential from 10:00 p.m. to 6:00 a.m. A regional operator opens the review screen, changes the start time to 9:00 p.m., adds a second credential and includes a customer message. Then the operator clicks **Approve**.

What did the system approve?

If the audit log says only “AI recommendation approved,” it is wrong in two directions. The AI did not propose the released scope. The operator did not merely approve what the AI produced. A person authored a materially different decision, and the added fields may require different evidence, permission, review and execution controls.

Human-in-the-loop architecture often treats review as a binary event: approve or reject. Real operators edit. They narrow a recommendation, widen it, remove unsupported language, add a facility exception, change a due time or substitute a different action. Those changes are not comments around the decision. They are part of the decision.

The system should preserve that authorship instead of collapsing the whole episode into a green checkmark.

## A proposal is not the operating decision

An AI output can be useful without holding authority. It can identify candidate records, summarize evidence and prepare a structured proposal. The operating decision is the exact object an authorized person releases after reviewing the evidence and applicable rules.

Those objects may match. They often should not be assumed to match.

The architecture needs at least three separate identities:

1. **Proposal identity:** the model-generated fields, evidence references, model and workflow versions, and proposal time.
2. **Decision identity:** the exact fields a person adopts, removes, adds or changes, together with the decision time, reason and authority.
3. **Execution identity:** the command, message, work item or other effect actually sent, plus its receipt and governing readback.

This separation protects both people and systems. It prevents the AI from receiving credit for a judgment a person made. It prevents the person from being described as a rubber stamp when the decision differs materially. It also prevents an edited value from bypassing controls that applied to the original proposal.

NIST's voluntary AI Risk Management Framework treats human-AI configurations, accountability, transparency and lifecycle monitoring as connected parts of AI risk management.[^1] Its Generative AI Profile notes that generative-AI use may warrant additional human review, tracking, documentation and management oversight.[^2] Neither publication defines a self-storage approval workflow. The relevant principle is narrower: human oversight must be designed and documented, not inferred from the presence of an approval button.

## Record the delta at field level

A screenshot of the final form is not enough. The decision record should show what changed between the proposal and the released decision.

For every decision field, classify the result:

- **accepted:** the person adopted the proposed value without change;
- **modified:** the person replaced the proposed value;
- **added:** the person introduced a field or target the AI did not propose;
- **removed:** the person excluded a proposed field, target or action;
- **held:** the person left the field unresolved and prevented release; or
- **not applicable:** the field did not belong to this decision class.

Then retain the before value, after value, reason, evidence reference and human actor for every material change. A free-text note such as “adjusted based on experience” may be appropriate commentary, but it should not replace the structured delta.

The delta also needs semantic meaning. Changing a customer-message typo is different from changing a credential target. Moving a maintenance review from Tuesday to Wednesday is different from converting “inspect” into “repair.” An effective schema identifies which fields affect scope, consequence, authority, evidence, timing, communication or execution.

W3C PROV-O provides a general vocabulary for entities, activities, agents and derivation relationships.[^3] It does not decide whether a human edit is authorized. It does offer a useful pattern: the final decision can be represented as a new entity derived from the proposal through a review activity associated with a named human actor. The proposal remains intact rather than being overwritten.

## Re-run the gates after the edit

Human input does not automatically make a decision eligible. A person can make an informed correction. A person can also select the wrong facility, add a target outside the reviewer's role, rely on stale information or turn a low-consequence draft into a consequential action.

Every material edit should pass the same deterministic gates that protected the proposal:

- exact organization, facility, asset, account or credential identity;
- permitted action and consequence class;
- current source eligibility and evidence completeness;
- reviewer role, scope and expiration;
- applicable policy and version;
- duplicate-action and idempotency check;
- required separation of duties;
- current operating preconditions; and
- required handback or secondary approval.

If the reviewer adds a second credential, the system must evaluate that credential as a new target. If the reviewer changes an informational note into a customer communication, the communication policy applies. If the reviewer widens a one-facility proposal to three facilities, portfolio authority does not appear merely because the same screen contains all three names.

The safe pattern is **edit, evaluate, then authorize**. Do not validate the AI proposal, let a person change it afterward and send the changed object under the proposal's old eligibility result.

This is where many review interfaces quietly fail. The policy service evaluates version A. The person edits the screen into version B. The connector receives version B with the authorization receipt for version A. The system can show a human in the loop while breaking the binding between the reviewed evidence, the authorized object and the released effect.

## Preserve disagreement instead of cleaning it away

A human change can be valuable evidence about the AI system. If reviewers repeatedly remove the same unsupported conclusion or add the same missing operating field, the pattern may reveal a retrieval, prompt, schema or training problem.

Do not erase the proposal once the decision is final. Preserve it with its input manifest and build identity. Preserve the final human-authored decision separately. Link both to the delta and the release evaluation.

That record supports questions operators will eventually ask:

- Which fields do reviewers change most often?
- Do edits usually narrow or widen consequence?
- Which changes trigger a new handback or second approval?
- Are certain source gaps associated with repeated human correction?
- Did a later model release reduce a specific type of material edit?
- Which executed actions differ from both the proposal and the final decision?

These are operating questions, not a leaderboard for employees. A high edit rate may indicate an AI design problem, a difficult decision class or a healthy review culture. A low edit rate may indicate strong proposals, automation bias or a form that makes changes difficult. The number alone does not establish quality.

## Attribute the final language honestly

The same control applies when the output is a message rather than a system command.

Suppose the AI drafts: “Your access has been restored.” The operator changes it to: “We received your request and are verifying the current access state.” The second sentence is materially safer because it does not convert a request or attempted change into a verified result.

The record should not say the AI sent an accurate restoration notice. It should say the AI proposed one statement, the operator replaced it, the authorized workflow released the replacement and the delivery channel produced a separate receipt. If the message was only saved as a draft, that remains a draft. Human editing does not prove sending, delivery, receipt or resolution.

This boundary matters for operational intelligence. A person can approve the wording of a summary without verifying the underlying facility condition. Record `language_reviewed` when that is what happened. Reserve `condition_verified` for the evidence and authority that actually establish the condition.

NIST SP 800-53 Rev. 5 includes configuration-change controls that call for reviewing proposed changes, approving or disapproving them, documenting decisions, implementing approved changes and monitoring change-controlled activity. Its audit controls also emphasize enough event content to establish what occurred, when, where, from which source, with what outcome and under whose identity.[^4] Those controls govern federal information systems, not self-storage AI. They provide a disciplined analogy: changed objects, decisions and responsible actors should remain reconstructable.

## Make the review screen show the real decision

A good interface should not bury the delta in an audit export that no operator will read.

Before release, show three views:

**What the AI proposed.** Display the structured fields, evidence references, limitations and build identity. Generated prose should be labeled as generated.

**What the person changed.** Highlight additions, removals and modifications by decision significance, not only by text color. A changed target, action or authority field deserves more prominence than punctuation.

**What will actually happen.** Show the final executable scope, communication recipient, due time, action ceiling and any remaining unknowns. The confirmation language should describe the final effect, not the earlier proposal.

If a material edit invalidates the current authorization, disable release and explain the next bounded step: refresh evidence, obtain secondary review, resolve identity or return the case to the correct owner. “Approval failed” is less useful than “The added facility is outside this reviewer's scope; route it to the regional authority or remove it from this decision.”

The screen should also preserve accessibility. Do not rely on red and green alone to communicate changes. Use text labels, icons with accessible names, a logical heading structure and a readable summary of the material delta.

## A completely fictional review episode

**Everything in this example is fictional: the company, facility, people, identifiers, records, AI behavior, times, policies, actions and outcomes. It is teaching data, not a deployment report.**

Fictional **Blue Lantern Storage** operates fictional facility `FIC-BL-014`. An AI workflow proposes an internal maintenance-priority decision for fictional gate controller `FIC-GC-22`. The proposal is `routine_review`, due the next business day, based on one communication alert and an open diagnostic task.

A fictional regional operator reviews the source packet. The operator sees a second authorized record showing three failed entry attempts during staffed hours. The operator changes the priority to `same_shift_review`, adds that evidence reference and removes the AI's unsupported sentence that the controller “is failing.” The operator does not authorize a repair, access restriction, customer message or vendor dispatch.

The system records three deltas: priority modified, evidence added and diagnosis language removed. The priority change remains within the fictional operator's scope, but it triggers a fresh policy evaluation and a shorter due time. The unsupported diagnosis cannot survive as hidden context in the work item. The final decision is attributed to the fictional operator, derived from—but not identical to—the AI proposal.

The fictional workflow then creates a review task. A task-creation receipt proves only that the task was accepted by the fictional work system. It does not prove the controller condition, technician arrival, repair, restored access or customer outcome. No real facility or result is represented.

## Use the proposal-to-decision delta record

The accompanying **AI Proposal-to-Human-Decision Delta and Authority Record** gives architects and operators one control surface for proposal identity, field-level changes, evidence, policy re-evaluation, human authority, final decision identity, execution binding and readback.

Start with one bounded decision class. Use fictional test records to exercise:

- approval with no change;
- a typo-only edit;
- a changed target;
- a widened facility scope;
- a removed unsupported claim;
- an added action outside the reviewer's role;
- an edit that requires a second approver;
- a stale proposal that must be recomputed;
- an execution payload that differs from the final decision; and
- a correction that must reach downstream records.

The pass condition is not that a human clicked something. The pass condition is that the system can prove what the AI proposed, what the person changed, why the change was eligible, which exact object was authorized, what was sent and what the governing system later showed.

Human review is valuable because people can apply context, judgment and responsibility that a model does not possess. Architecture should make that contribution visible. When a person changes an AI recommendation, the final record should tell the truth: the AI proposed; the human decided; the policy evaluated the actual decision; and the evidence—not the interface color—determined what could happen next.

<!-- BODY END -->

## Sources

[^1]: National Institute of Standards and Technology, [*Artificial Intelligence Risk Management Framework (AI RMF 1.0)*](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf), NIST AI 100-1, January 2023, accessed October 27, 2026.
[^2]: National Institute of Standards and Technology, [*Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile*](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf), NIST AI 600-1, July 2024, page updated April 8, 2026, accessed October 27, 2026.
[^3]: World Wide Web Consortium, [*PROV-O: The PROV Ontology*](https://www.w3.org/TR/prov-o/), W3C Recommendation, April 30, 2013, accessed October 27, 2026.
[^4]: National Institute of Standards and Technology, [*Security and Privacy Controls for Information Systems and Organizations*](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final), SP 800-53 Rev. 5 Release 5.2.0, accessed October 27, 2026.

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.

## Disclosure

This article and its companion tool were developed with AI assistance under Jared Mastroianni's editorial direction and reviewed for source scope, originality, claim boundaries and publication readiness. Blue Lantern Storage and every associated facility, person, identifier, record, AI behavior, policy, action, time and outcome are explicitly fictional. No real customer, deployment, product capability, performance result, incident or facility condition is represented.

# The Same System Should Not Propose, Approve, and Verify: Separation of Duties for Self-Storage AI

**A human approval screen is not an authority control if one workflow can prepare the case, choose the approver, execute the action, and declare itself correct.**

**By Jared Mastroianni**

**Proposed destination:** Jared Mastroianni personal authority site  
**Proposed slug:** `same-system-propose-approve-verify`

<!-- BODY START -->

An AI assistant reviews an after-hours access exception, assembles the supporting records and recommends a two-hour access restriction. A manager clicks approve. The assistant sends the change, reads the provider response and closes the task as verified.

That looks human-in-the-loop. It may still be one system wearing five different badges.

If the same workflow controls the evidence packet, approval request, execution credential and success test, the human may be present without supplying an independent decision. A stale record can shape the recommendation and the approval screen. A broad service account can turn a narrow approval into a larger change. A provider receipt can be mislabeled as proof of the operating result. The workflow can then grade its own work.

For consequential facility actions, operators need separation of duties across the whole decision path. The model may propose. A qualified person may authorize. A bounded service may execute. A different person or governing source may verify. Those are four duties, not four labels on one agent session.

## Start with the duties, not the org chart

Separation of duties is often treated as an accounting or security concept. The operating principle is broader: do not give one actor enough authority to initiate, approve, complete and conceal a consequential change.

NIST Special Publication 800-53 includes AC-5, Separation of Duties, which calls for identifying duties that require separation and defining access authorizations to support that division.[^1] The catalog is written for federal information systems, not as a self-storage rule. Its useful architectural lesson is that responsibility has to be reflected in permissions. A procedure that says “another person reviews this” is weak if the application still lets the proposing service approve and execute under the same principal.

Map the operating workflow into at least four duties:

1. **Proposal:** gather admitted evidence, identify unknowns and create a bounded requested action.
2. **Authorization:** decide whether that exact action is allowed, by whom, for which subjects and until when.
3. **Execution:** perform only the authorized effect through a narrowly scoped credential.
4. **Verification:** determine from the governing operational source whether the intended effect occurred once and remained within scope.

Add a fifth duty for policy administration when consequences justify it. The person or system that edits the authorization rule should not silently approve a live exception to the same rule.

These duties do not always require four employees. They do require distinct authority, evidence and state transitions. The design question is not “How many people touched the task?” It is “Could one compromised or mistaken principal take the action from proposal to accepted history without an independent barrier?”

## Do not let the proposal design its own approval

An AI-generated approval packet can make a poor decision look complete. It may select only confirming records, compress away a conflict or describe an unknown as a likely fact. A polished summary can become the reviewer’s entire field of view.

The proposal object should therefore be immutable and inspectable. It should contain the exact requested effect, subject and facility scope, source references, evidence cutoff time, known conflicts, model and prompt versions, policy version, consequence tier and expiration. Missing fields remain missing. The model does not fill an authority gap with a confidence score.

The approver needs direct access to the material sources or a governed representation that preserves limitations. The approval interface should show what changed since the proposal was created. If a source record, target set, consequence tier, policy version or requested effect changes, the old approval is invalid. The workflow must create a new decision object instead of editing the approved object in place.

NIST's AI Risk Management Framework calls for documented roles, responsibilities and lines of communication, and for policies that differentiate responsibilities in human-AI configurations.[^2] AI RMF 1.0 is voluntary and under revision. It does not prescribe this four-duty pattern. It does support the underlying point: “human oversight” is incomplete until the human role and its authority are explicit.

## Bind the approval to an exact object

An approval should not be a reusable mood. It should be a short-lived authorization for one identified decision object.

Create a digest over the fields that define the action: decision ID, facility and subject scope, proposed effect, evidence-set identity, policy version, consequence tier, execution route and expiration. Store that digest with the approver's authenticated principal, role, decision and time. The executor accepts the action only when the current object reproduces the approved digest.

This blocks a common failure mode: the model proposes a two-hour restriction for one credential, receives approval, then expands the target list or changes the effective window before execution. The visible wording may look similar, but the operating object is different. A digest mismatch should deny execution and return a compact delta to the reviewer.

Approval also needs a permitted effect, not merely “approved.” Useful dispositions include:

- deny;
- approve exactly as proposed;
- approve a narrower scope;
- approve preparation only, with execution held;
- require a second qualified approver; or
- expire and rebuild the packet.

Free-form comments can explain a decision. They should not be parsed by the model into broader authority.

## Make independence technical

A second name in an audit log does not establish independence if both actions came through the same shared account, browser session, API key or agent credential.

Use distinct principals for the proposal service, human approver, execution service and verifier. Apply least privilege to each. The proposal service can create an approval request but cannot mint an execution credential. The approver can authorize an exact object but cannot rewrite its evidence. The executor can perform only the authorized action and cannot mark verification complete. The verifier can record readback but cannot expand the approved scope.

NIST's Zero Trust Architecture separates a policy decision point from a policy enforcement point and describes a policy engine, policy administrator and enforcement mechanism as distinct logical components.[^3] That architecture addresses access control, not facility operations, and this article uses it only as a structural analogy. The decision about permission and the mechanism that carries out the permission should not collapse into one opaque model call.

A practical implementation can issue a disposable execution token after approval. The token carries the decision ID, approved digest, action class, target scope, maximum effect, expiration and idempotency key. It cannot be used for another facility or a second action. The executor presents it once, records the provider receipt and then loses the ability to reuse it.

## A receipt cannot verify the result

The executor's HTTP 200, accepted status or job ID proves something about the delivery path. It does not necessarily prove that the governing facility state changed as intended.

Verification should query the source that controls the operational truth: the access-control record, communication delivery record, work-management object, accounting ledger or another approved system for that action class. The verifier compares intended effect, observed effect, subject count, effective time and residual exceptions. A timeout remains unknown. A partial update remains partial. A mismatch reopens the decision instead of being rewritten as success.

NIST SP 800-53A's assessment procedure for AC-5 points assessors to policies, configuration settings, access authorizations and audit records, among other evidence.[^4] That assessment guide does not validate this proposed workflow. It reinforces a useful discipline: organizational prose, technical configuration and operating records are separate forms of evidence. All three matter when testing whether duties are actually separated.

Policy decision logs can help connect those forms. Open Policy Agent's current documentation, for example, describes decision events containing inputs, results, bundle revisions, decision IDs and timestamps, with masking controls for sensitive fields.[^5] OPA is only one implementation option. Its log does not establish source truth, human qualification or successful facility change. A decision ID is valuable because it lets the approval, enforcement and readback records point to the same decision without pretending they are the same event.

## Scale the separation to consequence

Not every draft needs a committee. The separation should match the consequence and reversibility of the action.

For a low-consequence draft that cannot leave an internal workspace, one person may review and revise it. The execution boundary is still closed.

For a moderate-consequence action, require a qualified human approver who is distinct from the proposing service, plus governing-source readback. Examples may include creating a vendor-review task or scheduling a non-customer-facing inspection.

For a high-consequence action, use stronger independence: named role eligibility, a second approver or specialist when policy requires it, narrow subject scope, short expiration, separate execution credentials and independent verification. NIST AI 600-1 likewise treats risk management as use-context dependent and gives organizations room to prioritize actions according to their circumstances; it does not supply the action list or approval design here.[^6] Customer charges, delinquency notices, access restrictions, account termination, employee actions and public safety statements may belong in this tier or may retain a zero autonomous execution allowance. The operator's governing policies and qualified advisers determine the exact boundary.

Small teams should not fake four people. If staffing cannot support simultaneous separation, redesign the action. Keep it in draft, lower the maximum effect, delay execution for off-site review, require next-day independent reconciliation or remove automation from the consequential step. Temporal separation is not automatically equivalent to independent authority, but an honest compensating control is better than four labels attached to one login.

Emergency access needs its own break-glass path. Record who invoked it, the exact condition, temporary scope, expiration and mandatory independent review deadline. Break-glass authority must not train the model that bypassing the normal path was a successful policy preference.

## A fictional Ashbury Gate exercise

The following scenario is entirely fictional. Ashbury Gate Storage, its seven facilities, every person, system, record, credential, time and result are invented teaching material.

A fictional assistant finds an after-hours access exception at one facility and proposes restricting one test credential from midnight to 2:00 a.m. The proposal identifies the source records, one conflicting schedule entry, evidence cutoff, model build, prompt version, policy version and exact target. Because of the conflict, the policy service requires regional review.

The regional operator opens the source records, confirms that the conflict prevents immediate approval and chooses **prepare only**. The system records the approval digest but issues no execution token. The assistant cannot reinterpret the comment as permission to restrict access.

A fictional facility manager then corrects the schedule record. That change invalidates the proposal's evidence-set identity. The original approval cannot be reused. A new decision object requests the same two-hour restriction, now with the corrected source and a later evidence cutoff. The regional operator approves the exact object for one credential, one facility and one execution before 10:00 p.m.

A dedicated access executor receives a disposable token. It submits the change once using the approved idempotency key and records the provider job ID. It cannot mark the task verified.

A different facility manager reads the governing access record and runs the permitted test. The record shows the intended schedule, but the test credential still opens the gate during the restricted period. Verification is **mismatch**, not success. The workflow reopens with the original decision, execution receipt and readback attached. No wider restriction is attempted, and no real operating result is claimed.

The lesson is not that one approval failed. The architecture made the failure visible before a single system could turn proposal, permission, delivery and self-grading into one reassuring green check.

## Run the same-system test

Choose one consequential AI-assisted workflow and trace it from evidence to closure. Ask:

1. Can the proposer alter the evidence packet after approval?
2. Is approval bound to the exact scope, versions, effect and expiration?
3. Can the proposing principal select itself or a shared account as approver?
4. Can the executor act without a valid, narrow authorization object?
5. Can the executor also declare the governing result verified?
6. Does a changed source, target or policy invalidate the approval?
7. Can one credential cross facilities or repeat the action?
8. Does an independent readback expose partial, unknown and mismatch states?
9. Is break-glass use reviewed outside the initiating path?
10. Could one compromised principal move the workflow from proposal to accepted history?

If the answer to the last question is yes, adding another approval button will not solve the architecture. Separate the duties, bind the decision and make every handoff prove only what it actually did.

<!-- BODY END -->

## Sources

[^1]: National Institute of Standards and Technology, [*Security and Privacy Controls for Information Systems and Organizations, NIST SP 800-53 Revision 5*](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final), final publication with current supplemental-release information; accessed September 14, 2026. AC-5 and related controls are used as architectural anchors, not as a self-storage requirement, audit result or certification.
[^2]: National Institute of Standards and Technology, [*Artificial Intelligence Risk Management Framework, AI RMF 1.0*](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf), January 2023; accessed September 14, 2026. The voluntary cross-sector framework is under revision and does not prescribe this article's four-duty design.
[^3]: National Institute of Standards and Technology, [*Zero Trust Architecture, NIST SP 800-207*](https://csrc.nist.gov/pubs/sp/800/207/final), August 2020; accessed September 14, 2026. Policy-decision and enforcement components are used as a structural analogy; the publication does not govern private self-storage operations or validate this method.
[^4]: National Institute of Standards and Technology, [*Assessing Security and Privacy Controls in Information Systems and Organizations, NIST SP 800-53A Revision 5*](https://csrc.nist.gov/pubs/sp/800/53/a/r5/final), January 2022; accessed September 14, 2026. Its AC-5 evidence approach does not constitute an assessment of any operator, product or workflow described here.
[^5]: Open Policy Agent, [*Decision Logs*](https://www.openpolicyagent.org/docs/management-decision-logs), current official documentation accessed September 14, 2026. OPA is an implementation example; its logs do not establish human authority, facility truth, successful execution or compliance.
[^6]: National Institute of Standards and Technology, [*Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile, NIST AI 600-1*](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf), July 2024; accessed September 14, 2026. This voluntary cross-sector profile informs consequence-sensitive governance but does not define a self-storage approval policy or certify this architecture.

## Editorial disclosure

This article was prepared with AI-assisted research and drafting under Jared Mastroianni's byline and requires Jared's editorial approval before publication. Ashbury Gate Storage and every associated facility, person, system, record, policy, credential, time, action and result are fictional teaching material. The architecture is not represented as a Facily capability, customer deployment, legal standard, certification or measured operating result.

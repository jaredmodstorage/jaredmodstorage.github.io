# Rollback Is Not Undo: The Compensation Contract for Self-Storage AI

*An AI system can reverse a database value and still leave the real-world consequence in place. Responsible architecture classifies every action before execution as reversible, cancelable, compensatable or irreversible.*

**By Jared Mastroianni**

**Proposed slug:** `rollback-not-undo-self-storage-ai-compensation-contract`

**Publication state:** Publication-ready local draft only. No publisher handoff, submission, publication, canonical assignment, search submission, crawling, indexing, coverage or recognition has occurred.

“We can always roll it back” is one of the most dangerous sentences in operational AI.

Sometimes rollback is real. A draft record can be replaced with its prior version before anyone relies on it. A configuration release may have a tested path back to a known build. But many actions in self-storage and commercial real estate do not behave like code. A message that reached a customer cannot be undelivered. A changed access credential may be replaced, but its earlier exposure cannot be erased. A payment can be refunded, not made never to have happened. A physical dispatch can be canceled only until someone acts on it.

When an AI workflow crosses from recommendation into action, “reversible” must stop being a reassuring adjective and become a typed, testable contract.

That contract should classify each action before execution as **reversible, cancelable, compensatable or irreversible**. It should define who may authorize recovery, the deadline for using the recovery path, the evidence needed before and after it, and the residual consequence that will remain even if the compensation succeeds.

The point is not pessimism. It is operational accuracy. A system that understands the difference between restoring a value and repairing a consequence is safer to automate because it knows when human judgment cannot be replaced by a generic rollback button.

## Four recovery classes, not one

The four classes answer different questions.

**Reversible** means the original state can be restored without creating a new business transaction and without erasing valid concurrent work. Replacing an unpublished internal draft with its immediately prior version may fit this class if no downstream consumer has used it.

**Cancelable** means the action has been accepted or queued but the business effect has not yet occurred, and the receiving system offers a confirmed cancellation path. Cancellation is time-bound. A queued communication is not cancelable after delivery merely because the interface still shows a cancel control.

**Compensatable** means the original effect occurred and recovery requires a new, separately authorized action. A corrected notice, refund, reissued credential or follow-up work order may compensate for part of the consequence. Compensation does not make the history disappear.

**Irreversible** means no available action can restore or adequately offset the material effect. The system may still contain, disclose, reconcile or remediate the outcome, but it cannot truthfully describe the result as undone.

These classes are not permanent labels on API endpoints. They depend on state, time, downstream use and consequence. A draft is reversible before publication, cancelable while a publisher holds it, compensatable after public release and potentially irreversible once third parties have copied or acted on it.

Microsoft’s Compensating Transaction pattern makes a crucial distinction: recovery in an eventually consistent workflow can require business-specific actions and may not return data to the state that existed before the original operation.[^1] The guidance also notes that compensation can fail and that some steps have points of no return. It is cloud-architecture guidance, not a self-storage standard, but the underlying lesson translates directly: recovery is a new workflow, not time travel.

## Ask about the consequence before the command

The reversibility decision belongs in the pre-execution gate. It is too late to invent recovery after the system has already acted.

For every proposed action, record:

1. **The intended business effect.** Name what is supposed to change, not just the method or endpoint.
2. **The governing state.** Identify the source that proves the current condition and the source that will prove the post-action condition.
3. **The point of no return.** Define the exact provider or physical state after which cancellation is no longer credible.
4. **The recovery class.** Select reversible, cancelable, compensatable or irreversible for the current state.
5. **The recovery command.** Name the permitted inverse or compensating action, if one exists.
6. **The recovery authority.** Identify who may approve it. Original-action authority does not automatically include compensation authority.
7. **The recovery deadline.** Record how long the path remains available and what clock controls it.
8. **The residual consequence.** State what will remain after successful recovery.
9. **The verification test.** Define the independent evidence required to close the recovery.
10. **The failure owner.** Name who inherits the case if recovery is unavailable, fails or produces a mismatch.

If any consequential action lacks these fields, the system should not claim it has a rollback path. It has an assumption.

## Technical idempotency does not reverse a business effect

Teams often reach for idempotency as if it solves recovery. It solves a different problem.

HTTP semantics defines an idempotent method as one whose intended effect is the same whether an identical request is made once or several times.[^2] That can make retries safer. It does not mean the effect is reversible. Sending the same approved update twice may avoid a duplicate record, yet the first update can still be wrong. Deleting the resulting record may also be idempotent, but deletion may not repair a message, export, cache, invoice, access event or human decision already produced from it.

Keep three controls separate:

- **Deduplication** prevents multiple technical attempts from representing multiple intended actions.
- **Idempotency** limits the effect of repeating the same intended command.
- **Compensation** addresses a business effect that already occurred.

An AI orchestrator needs all three when the workflow spans systems. AWS’s saga-orchestration guidance describes compensatory transactions for multi-service workflows and warns that sagas add complexity, lack transaction isolation and require observability and idempotent participants.[^3] That pattern is useful for distributed data consistency. It does not establish that a compensating step is operationally adequate, legally sufficient or safe in a facility context.

## Preserve concurrent truth

A naïve rollback often means “write back the old value.” That can destroy valid work performed after the original action.

Assume an AI changes a fictional facility’s public phone number from version 12 to version 13. A manager then makes a separately approved correction that creates version 14. If the AI later decides its own action was wrong and blindly restores version 12, it erases the manager’s valid change.

The recovery gate should compare the exact version produced by the original action with the current governing version. If they differ, automatic reversal stops. The system must determine whether the current state includes unrelated or corrective work. Recovery may require a new proposed value built from current truth, not restoration of an old snapshot.

This is one reason provenance matters. The W3C PROV data model distinguishes entities, activities, generation, use and invalidation so that changing records can retain a history of how states came to exist.[^4] PROV does not define operational rollback or confer business authority. It does provide a vocabulary for connecting an original action, later evidence and a compensating action without overwriting the lineage.

At minimum, link the compensation record to the original intent, original attempt, observed effect, current governing version, approving authority and verification evidence. The original record remains. Its disposition changes from active to superseded, compensated, contained or unresolved.

## A fictional example: Granite Bend Storage

The following scenario is explicitly fictional. Granite Bend Storage, its facilities, people, customers, records, systems, messages, providers, policies, actions and outcomes do not describe a real company or deployment.

A fictional AI workflow prepares and releases an approved service notice for one facility. The notice is correct when approved, but a scheduling source changes before release. The message provider reports 240 messages accepted and 187 delivered before the mismatch is detected.

Calling the action “reversible” would collapse several different states.

The 53 accepted-but-not-yet-delivered messages may be **cancelable** if the provider offers cancellation and fresh readback proves those exact message identities did not deliver. The 187 delivered messages are not cancelable. They may be **compensatable** with a corrected notice approved by the communication owner. The recipients’ prior exposure to incorrect information is **irreversible**; a correction can reduce confusion, but it cannot make the first message unseen.

The workflow should stop additional delivery, preserve the original approved content and source versions, query status by message identity, and create two populations: potentially cancelable and delivered. It should not send a correction automatically. The correction is a new customer communication with its own source, wording, population, approval, accessibility, timing and delivery evidence.

The closure record should say what happened: 53 original messages canceled and verified, 187 corrected through a second approved communication, and prior exposure retained as a residual consequence. If provider state remains ambiguous for any recipient, that population stays unresolved.

No delivery performance, customer response, provider capability or actual incident is claimed. The numbers exist only to demonstrate why one “rollback” status is not enough.

## Design the compensation contract

A practical compensation contract can sit beside the action policy and command manifest. It should be generated before execution and re-evaluated at every state transition.

The contract needs five parts.

**Classification.** Record the action class, current recovery class, point of no return and prohibited recovery shortcuts. Unknown means stop, not “probably reversible.”

**Authority.** Bind the original and compensating actions to named roles. A person authorized to publish a notice may not be authorized to issue a refund, change access or approve emergency work. The AI cannot infer expanded authority from urgency.

**Evidence.** Preserve the before state, original intent, command receipt, observed effect, current state and downstream consumers. A success response is not proof that the intended business state exists. A compensation success response is not proof that the residual consequence is resolved.

**Execution.** Give each recovery action its own stable intent ID, idempotency control, preconditions and attempt log. Do not reuse the original command ID or overwrite the original outcome. If compensation fails, the case needs a resumable state and a human owner.

**Closure.** Use typed results: `reversed_and_verified`, `canceled_before_effect`, `compensated_with_residual`, `contained`, `irreversible_acknowledged` or `unresolved`. “Rolled back” is acceptable only when the governing state and downstream evidence support the reversible class.

NIST SP 800-53 includes broad control families for audit, contingency planning, incident response and system integrity.[^5] Those controls can inform evidence and recovery design, but they do not supply this domain-specific contract or make every business effect recoverable.

## Put the hard cases in the operator’s view

The most useful dashboard is not a green count of successful rollbacks. It is a queue of actions whose recovery class changed.

Surface cases where:

- a cancellation deadline is approaching;
- a downstream consumer used the changed record;
- the current version no longer matches the version created by the AI;
- the proposed compensation requires a different authority;
- the provider reports mixed or ambiguous states;
- the residual consequence exceeds the approved threshold;
- the original evidence is missing;
- or the compensation itself failed.

Do not let a model summarize those differences into “resolved.” The operator needs exact populations, states, clocks, owners and evidence.

The NIST AI Risk Management Framework organizes voluntary AI risk management around Govern, Map, Measure and Manage, with profiles adapted to the user’s context and risk tolerance.[^6] NIST states that AI RMF 1.0 is being revised. The framework supports disciplined, contextual control design; it does not certify this compensation pattern or establish a self-storage requirement.

Responsible AI architecture is not defined only by what the system can do when every step works. It is defined by what the system can truthfully say after a partial effect, a late correction or a failed recovery.

Rollback is a database word. Operations need a consequence word. Use reversible when the prior state can actually be restored, cancelable while the effect can still be prevented, compensatable when a new authorized action can repair part of the outcome, and irreversible when history cannot be made not to have happened.

That vocabulary does more than improve incident reports. It changes what the AI is allowed to do before an incident exists.

---

## Sources

[^1]: Microsoft Azure Architecture Center, [Compensating Transaction pattern](https://learn.microsoft.com/en-us/azure/architecture/patterns/compensating-transaction), current first-party guidance accessed August 31, 2026.
[^2]: Internet Engineering Task Force, [HTTP Semantics, RFC 9110](https://www.rfc-editor.org/rfc/rfc9110.html), Internet Standard accessed August 31, 2026.
[^3]: Amazon Web Services, [Saga orchestration pattern](https://docs.aws.amazon.com/prescriptive-guidance/latest/cloud-design-patterns/saga-orchestration.html), first-party prescriptive guidance accessed August 31, 2026.
[^4]: World Wide Web Consortium, [PROV-DM: The PROV Data Model](https://www.w3.org/TR/prov-dm/), W3C Recommendation accessed August 31, 2026.
[^5]: National Institute of Standards and Technology, [Security and Privacy Controls for Information Systems and Organizations, NIST SP 800-53 Rev. 5](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final), current official publication page accessed August 31, 2026.
[^6]: National Institute of Standards and Technology, [AI Risk Management Framework](https://airc.nist.gov/airmf-resources/airmf/), current official framework page accessed August 31, 2026.

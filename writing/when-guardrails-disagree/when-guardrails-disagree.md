# When Guardrails Disagree: Build a Decision Lattice for Self-Storage AI

*A system with several guardrails still needs one governed way to resolve their results. Otherwise the easiest policy to satisfy can quietly become the only policy that matters.*

**By Jared Mastroianni**

*Chief Operating Officer of modSTORAGE; CEO and Founder of Facily.ai*

*Editorial disclosure: Research synthesis, drafting and quality assurance were AI-assisted under human-directed editorial controls. The architecture and all examples are authored proposals, not evidence of a deployed product, customer implementation or operating result.*

<!-- BODY START -->

A self-storage AI assistant proposes an after-hours access update. The identity control confirms that the employee is signed in. The role policy permits that employee to prepare a draft. The communications policy allows a service notice. The privacy policy blocks one field in the proposed message. The facility-state check cannot establish whether the gate is back in normal service. The safety policy requires a named person to review any statement about restored access.

Did the request pass?

It passed three evaluations, failed one, could not complete another and triggered a human obligation. Reducing that record to `approved: true` would erase the most important facts in it. Reducing it to `approved: false` would be safer, but still incomplete: the operator would not know whether to correct the message, refresh facility state, request a qualified review or abandon the action.

This is the policy-combination problem. It appears as soon as an AI workflow has more than one real control. Identity, authorization, privacy, safety, customer communication, financial approval and local operating state may each have a legitimate decision to make. Those decisions will not always agree, and some controls will occasionally be unavailable. The architecture needs an explicit method for combining results before a model recommendation becomes visible work or an executable command.

The answer is not a longer system prompt. It is a typed decision lattice: a governed structure that preserves each policy result, applies a declared combining rule, carries required obligations forward and identifies the policy that controlled the final outcome.

## One Boolean cannot represent an operating decision

Authorization systems already recognize that policy evaluation is richer than yes or no. NIST defines attribute-based access control as evaluating attributes about the subject, object, requested operation and sometimes the environment against policy.[^1] OASIS XACML goes further: an authorization result can be `Permit`, `Deny`, `Indeterminate` or `NotApplicable`, and separate policies can be combined under a declared algorithm.[^2]

That distinction matters outside traditional access control.

- `PERMIT` means the policy evaluated the exact request and allows it within its scope.
- `DENY` means the request violates a rule that is applicable now.
- `INDETERMINATE` means the policy could not produce a reliable decision because required data, evaluation logic or a dependency failed.
- `NOT_APPLICABLE` means the policy does not govern this request.
- `REVIEW` is a proposed operating extension for cases that policy deliberately reserves for a qualified person. It is not an XACML result and should not be mislabeled as one.

These states have different operator consequences. `NOT_APPLICABLE` does not mean safe. `INDETERMINATE` does not mean denied on the merits, and it certainly does not mean permitted. `REVIEW` is not an invitation for any nearby user to click through. It identifies a bounded question, the role qualified to answer it and the evidence that person must receive.

If the application converts all five states into a Boolean before combination, the strongest control can disappear without an obvious error. A timed-out privacy check may become false and be ignored. A policy that did not apply may be counted as a pass. A review requirement may be rendered as a warning under an active Submit button.

## Evaluate first; combine second

Each policy should evaluate the same decision envelope before any result is combined. At minimum, that envelope should bind:

- the requesting human or service identity and any delegated role;
- the exact facility, account-safe reference, asset or work object;
- the proposed action, fields and destination;
- the declared purpose and consequence class;
- the governing state version and observation time;
- the applicable policy-set identity and revision; and
- the decision time and expiration.

The model may propose this envelope. It should not decide which identity, facility or authority applies by itself. Those values need to come from governed application state or be confirmed through the proper workflow.

Each control then returns its own typed result, reason code, policy version and obligations. Keeping evaluations separate makes disagreement inspectable. A privacy policy can deny inclusion of a customer field while a communications policy permits a notice. That is not a broken system; it is a request that must be narrowed before it becomes eligible.

Combining happens only after the individual results exist. XACML specifies several combining algorithms, including deny-overrides, permit-overrides, first-applicable and only-one-applicable. Under deny-overrides, a denial takes priority; the specification also preserves different forms of indeterminate results so an evaluation error with possible denying effect is not casually lost.[^2]

Self-storage operators do not need to implement XACML to learn from that precision. They do need to declare what combination means for each consequence class.

For an internal, low-consequence draft, the rule may permit content generation while masking a prohibited field and holding delivery. For a financial change, customer communication, access decision or physical-control command, any applicable deny should block the prohibited effect. An indeterminate result from a control that could deny should normally stop the action until the input is restored or a qualified authority follows a documented exception path. A missing rule should not be reclassified as permission.

“Use the strictest policy” sounds sensible but is still underspecified. Strictest by what measure? A safety policy may require immediate notification while a privacy policy forbids including personal details. The correct result may be “send a limited internal alert with mandatory fields removed,” not “send everything” or “send nothing.” The combining layer must resolve effects and obligations, not merely pick the most alarming label.

## A useful lattice preserves both outcome and work

For facility AI, the combined result should be an object, not a flag:

```text
decision = {
  result,
  controlling_policy,
  applicable_policy_results,
  unresolved_inputs,
  prohibited_effects,
  mandatory_obligations,
  permitted_scope,
  reviewer_role,
  expires_at,
  decision_id
}
```

The final `result` controls what the system may do. The other fields tell the operator why, what remains possible and how the case can move.

Consider four common outcomes.

**Permit with obligations.** The assistant may create an internal draft, but it must exclude a protected field, attach the current source record and remain unsent until a named role reviews it. The obligations are part of the decision. If the enforcement point cannot fulfill them, the permit is unusable.

**Deny with a narrower eligible action.** The request to change a gate schedule is denied, but the same user may open a maintenance exception and request review. This is not a model improvising a workaround. The alternative action must have its own policy path and new decision identity.

**Indeterminate with repair work.** The system cannot establish facility state because the governing source is unavailable. The action stays blocked. The queue records the missing attribute, source owner and refresh path. It does not ask the model to infer normal operation from yesterday’s summary.

**Review with a bounded question.** The policy allows a regional operator to decide whether a factual service notice may be prepared from verified fields. The reviewer cannot use that task to approve a financial adjustment, alter access or waive an unrelated privacy rule.

This design turns a refusal into routable work without converting review into a universal override.

## Human review cannot repair an architecture that hid the conflict

NIST’s AI Risk Management Framework treats governance as a continuous, cross-cutting function and calls for transparent policies, documented roles and clear accountability across the AI lifecycle.[^3] Its Generative AI Profile is a voluntary, cross-sector companion for identifying and managing risks in generative systems; it does not certify a particular workflow or prescribe this lattice.[^4]

The practical implication is that human involvement needs structure. Showing a reviewer a green banner that says “four of five checks passed” is not meaningful oversight. The reviewer needs the exact request, every applicable result, the unavailable or conflicting input, the effects already prohibited and the narrow question assigned to that role.

Some conditions are not reviewable in the moment. A mismatched facility identity, expired delegation, absent customer-safe reference, unavailable safety control or unknown governing state may require the request to stop. A person should not be invited to manufacture missing evidence by clicking an override.

Every override or exception also needs its own authority, reason, scope and expiration. It must not overwrite the original policy results. Otherwise the record will later suggest that the controls agreed when they did not.

## Version the combination, not only the policies

Teams often version individual policies and forget the logic that combines them. That logic can change an operating outcome even when every policy stays the same.

Moving from deny-overrides to first-applicable may make list order decisive. Changing a default from indeterminate to deny alters routing and workload. Adding a new privacy obligation may turn a usable permit into an unenforceable one. Reordering policy bundles can change which reason is shown to a reviewer.

The release artifact should therefore bind:

- each policy and its owner;
- the complete policy-set revision;
- the combining algorithm and version;
- the obligation-merging rule;
- consequence-specific defaults;
- expected results for conflict cases; and
- the prior known-good bundle and rollback condition.

Open Policy Agent provides one implementation reference, not a universal operating answer. Its bundle manifest can carry a revision, and its decision logs can include input, result, decision path and the revisions of bundles used.[^5] Those features can support replay and audit. They do not decide which facility policies should apply, whether logged data is appropriate to retain or whether an operational action was correct.

Before release, replay a fixed suite of conflict cases through the complete bundle. Test at least: explicit deny plus permit; permit plus indeterminate; no applicable policy; missing subject attribute; stale facility state; conflicting obligations; expired review authority; duplicate decision ID; policy-bundle mismatch; and enforcement unable to satisfy an obligation. Compare the full decision object, not only the final label.

## Log enough to explain, not enough to create a new exposure

A decision record should preserve the request identity, policy revisions, results, reason codes, controlling policy, obligations, reviewer disposition, enforcement receipt and governing readback. That gives the operator a path from proposal to outcome.

It does not follow that every prompt, customer field or retrieved document belongs in the log. OPA’s documentation explicitly treats policy-query inputs and decisions as potentially sensitive and supports masking or erasing selected fields in decision logs.[^5] The same discipline belongs in any architecture: retain identifiers and evidence references where possible, minimize payloads, separate restricted details and define retention by purpose.

The decision log is also not proof of effect. It can show that policy returned `PERMIT`. The enforcement receipt can show that a connector accepted a bounded command. Only an appropriate readback can establish the resulting governing state, and some physical conditions still require a qualified observation.

## A fictional facility conflict

The following case is entirely fictional. Alder Bend Storage, its people, systems, records, times and outcomes do not represent a real facility or product.

At 7:42 p.m., a fictional assistant proposes a customer service notice stating that normal gate access has been restored. The employee is authenticated and has permission to draft notices. The communications policy permits a factual service update. The privacy policy denies inclusion of the customer’s unit number in a bulk notice. The facility-state policy is indeterminate because the last governing controller read is outside the action’s freshness limit. The operating policy assigns restoration language to a regional reviewer after current state is established.

The lattice returns `INDETERMINATE_BLOCKED`, controlled by the facility-state policy. It preserves the privacy denial as a prohibited-field obligation and the review requirement as pending, not completed. The system may save a restricted internal draft with no customer delivery path. It assigns one task to refresh governing state and names the source owner. It does not let the reviewer approve around the missing controller read.

At 7:49 p.m., a new state record shows only partial restoration. The assistant generates a new request with a new decision ID. The communications policy now permits a limited notice describing the verified access window. Privacy still blocks the unit field. The regional reviewer confirms only the allowed wording. The enforcement point sends the approved text through the authorized channel, records provider acceptance, then reads back the sent-message record. The case closes as “message sent and read back; facility restoration remains partial.” It does not become “gate restored.”

The useful result is not that every policy said yes. It is that disagreement remained visible long enough to produce a narrower, supportable action.

## The operator’s release test

Before an AI-supported workflow can use multiple guardrails in production, an accountable owner should be able to answer ten questions:

1. What exact decision envelope does every policy evaluate?
2. Which typed results can each policy return?
3. Which policy set and combination version produced the outcome?
4. What happens when a control is unavailable or data is missing?
5. Which denies block the whole action, and which prohibit only a field or effect?
6. How are mandatory obligations merged and enforced?
7. What question, evidence and authority does human review actually receive?
8. What new identity is created when a denied request is narrowed or retried?
9. Can the complete conflict suite be replayed against the release candidate and rollback bundle?
10. How are decision, enforcement, readback and reconciliation recorded without exposing unnecessary data?

If those answers live only in prompt text or team memory, the guardrails are not yet an operating control system.

Multiple policies are a strength only when their disagreement has semantics. Preserve the separate results. Combine them under a versioned rule. Carry obligations to enforcement. Limit what review can resolve. Read the governing state back. That is how a facility AI system stops treating “mostly approved” as permission and starts producing decisions an operator can defend.

<!-- BODY END -->

## Practical tool

Use the accompanying **Policy Decision Reconciliation Register** to document one request, each independent policy evaluation, the combination rule, controlling result, obligations, bounded review, enforcement receipt and governing readback. It includes one blank template row and six explicitly fictional teaching rows.

## Sources

[^1]: National Institute of Standards and Technology, [*Guide to Attribute Based Access Control (ABAC) Definition and Considerations*, NIST SP 800-162](https://csrc.nist.gov/pubs/sp/800/162/upd2/final), updated August 2, 2019; accessed September 11, 2026.
[^2]: OASIS Open, [*eXtensible Access Control Markup Language (XACML) Version 3.0 Plus Errata 01*](https://docs.oasis-open.org/xacml/3.0/xacml-3.0-core-spec-en.html), OASIS Standard; accessed September 11, 2026.
[^3]: National Institute of Standards and Technology, [*Artificial Intelligence Risk Management Framework (AI RMF 1.0)*](https://www.nist.gov/itl/ai-risk-management-framework), released January 26, 2023; page accessed September 11, 2026. NIST’s page states that AI RMF 1.0 is being revised.
[^4]: National Institute of Standards and Technology, [*Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile, NIST AI 600-1*](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence), published July 26, 2024, page updated April 8, 2026; accessed September 11, 2026.
[^5]: Open Policy Agent, [*Decision Logs*](https://www.openpolicyagent.org/docs/management-decision-logs) and [*Bundles*](https://www.openpolicyagent.org/docs/management-bundles), current documentation accessed September 11, 2026.


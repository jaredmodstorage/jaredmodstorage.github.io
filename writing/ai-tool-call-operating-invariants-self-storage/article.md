# The AI Tool Call Passed Validation. Why Was the Facility Action Still Impossible?

A valid payload can still violate facility hours, authority limits, current record state, or the relationship between fields. Responsible AI needs an operating-invariant gate after schema validation and before execution.

By Jared Mastroianni

An AI agent prepares a facility access window. The tool requires a facility ID, a credential ID, a start time, an end time, a reason code, and an approver reference. Every field is present. Every value has the expected type. The payload passes the schema.

It can still be wrong.

The credential may belong to another facility. The end time may precede the start time under the facility’s local-time rule. The requested window may cross a maintenance blackout. The approver may have authority for customer access but not vendor access. The account may have changed after the agent retrieved it.

Schema validation answers an important question: does this payload have the permitted structure? It does not answer the operating question: is this action coherent, current, authorized, and possible for this facility now?

That second question deserves its own architectural control. I call it the **operating-invariant gate**.

## Valid syntax is not valid operations

[JSON Schema Draft 2020-12 validation](https://json-schema.org/draft/2020-12/draft-bhutton-json-schema-validation-00) can require properties, constrain types and values, and express relationships such as dependent requirements and conditional subschemas. It also draws a boundary between structural validation and the application’s ability to use a value correctly.

That boundary becomes consequential when a model can call tools.

A schema might require `start_time` and `end_time` to be strings matching a time format. It can restrict `action_type` to an approved enumeration. It can reject a missing facility ID. Those controls should be used. But the payload can pass them while remaining operationally incoherent.

Consider values that are individually valid but collectively unsafe:

- a start time that is later than the end time under the wrong overnight rule;
- a unit that exists and a facility that exists, but the unit does not belong to that facility;
- a credential that is active and a requested schedule that is valid, but the subject is no longer eligible for that access class;
- an approver ID that is well formed, but the approver’s current role does not cover the requested consequence;
- a work-order completion state with no required inspection result;
- a communication release date earlier than the policy version it claims to use; or
- a rate change within the numeric range but outside the authority ceiling for that reviewer.

The error lives between fields, records, time, policy, and authority. A type checker cannot infer the facility’s operating contract unless that contract is made explicit and evaluated against current evidence.

## Keep four validation layers separate

An advanced tool workflow should expose four different gates rather than compressing them into one green check.

**1. Transport validation** asks whether the request arrived in a readable form and met the protocol requirements.

**2. Schema validation** asks whether the payload matches the declared structure, types, required fields, formats, enumerations, and bounded values.

**3. Operating-invariant validation** asks whether the values agree with one another and with the current governed facility state.

**4. Authority validation** asks whether the actor or delegated agent may perform this exact action on this exact target at this consequence level now.

The [OpenAPI Specification](https://spec.openapis.org/oas/v3.1.1.html) provides a standard way to describe API operations, parameters, request bodies, responses, and schema-based data shapes. It is useful contract documentation. An OpenAPI-described request can still require application rules that depend on facility-local calendars, record ownership, current account state, or a reviewer’s authority.

Do not label all four layers `validated`. Preserve the result of each one. An operator investigating a rejected action needs to know whether the JSON was malformed, a field failed its schema, a facility invariant failed, or authority was absent.

## Write invariants as testable statements

An invariant is a condition that must remain true before the action can be released. It should be precise enough for a system to test and clear enough for an operator to challenge.

Weak rule: “The access request looks reasonable.”

Testable invariant: “The credential’s authoritative facility ID equals the action’s facility ID at evaluation time.”

Weak rule: “The manager approved it.”

Testable invariant: “The approval grant is active, covers this action class and consequence tier, names this facility scope, and expires after the proposed action window.”

Weak rule: “The schedule is valid.”

Testable invariant: “The start and end timestamps resolve unambiguously in the facility’s governed time zone; the interval is positive under the declared overnight rule; and it does not intersect a current blackout interval.”

The rule should name:

- the invariant ID and version;
- the action classes it governs;
- the authoritative fields and sources it reads;
- the comparison or calculation;
- its freshness requirement;
- the result states;
- the permitted response to failure or uncertainty; and
- the human owner who can resolve an exception.

Do not hide these rules in prompt prose. Prompts can help a model form a proposal. Enforcement belongs in deterministic controls at the tool boundary or in the authoritative service.

## Evaluate current state at release time

The agent may have assembled a valid proposal from a snapshot that is already stale.

An account changes. A unit is transferred. A blackout is added. An employee’s role is revoked. A facility moves to an emergency operating mode. None of those changes must alter the JSON shape. They alter whether the action remains permissible.

The invariant gate therefore needs a release-time evidence packet with explicit source versions or read times. For each governed dependency, capture the stable record identity, authoritative source, material state, observed or effective time, and freshness result.

If the target system supports a conditional write, include the expected record version or other approved precondition. If the current version differs, reject the release and recompute. Do not let the agent silently substitute the newer record into an older approval.

The decision state should be one of:

- `pass`: every required invariant is confirmed from current-enough governing evidence;
- `fail`: at least one invariant is conclusively false;
- `unknown`: evidence is missing, stale, conflicting, or unavailable;
- `not_applicable`: the invariant does not govern this action class, with the mapping recorded; or
- `superseded`: a newer proposal or operating state has replaced this release candidate.

Only `pass` permits unattended execution. `Unknown` is not a softer pass.

## A fictional self-storage example

The following scenario, facility, people, systems, identifiers, and data are fictional. They demonstrate the control and do not describe a modSTORAGE or Facily.ai deployment.

At fictional Silver Forge Storage, an agent prepares a temporary vendor access window for fictional credential `V-284`. The payload contains the required facility ID, credential ID, access class, start and end timestamps, work-order reference, and approver reference. Each field passes the fictional API schema.

The operating-invariant gate evaluates five rules:

| Invariant | Fictional evidence | Result |
|---|---|---|
| Credential belongs to facility | Credential record names `FIC-SILVER-FORGE` | Pass |
| Work order is active for same facility | Work order names the facility and is open | Pass |
| Window is permitted for vendor class | Requested window is 10:00 p.m.–6:00 a.m.; fictional policy requires an on-site escort after 9:00 p.m. | Fail |
| Approver covers exception | Approver grant covers daytime vendor access only | Fail |
| No blackout intersects window | Current calendar shows a fictional access-system maintenance blackout from 11:30 p.m.–12:30 a.m. | Fail |

The tool call is structurally valid and operationally rejected. The system returns the failed invariant IDs, evidence references, policy versions, and permissible next step. It does not ask the model to rewrite times repeatedly until a payload happens to execute.

The fictional facility manager can choose a daytime window, arrange the required escort through the approved process, or close the proposal. Each material change creates a new release candidate and a fresh invariant evaluation.

## Do not let the model grade its own proposal

The model that created an argument should not be the only component deciding whether the argument is safe.

A model can explain a failed invariant in natural language. It can suggest a corrected proposal within a bounded workflow. It can organize the evidence for a reviewer. Those are useful roles.

The release gate should still rely on deterministic comparisons, governed policy evaluation, current authoritative readback, and named human authority where required. If an invariant cannot be evaluated deterministically, state that limitation. Route the case to a qualified person instead of converting the model’s confidence into permission.

This separation also improves testing. Teams can generate valid-looking payloads that violate one invariant at a time: facility mismatch, expired approval, stale record version, impossible interval, blackout collision, missing prerequisite, or authority above the user’s ceiling. The expected outcome is not merely a rejected request. It is the correct reason, evidence reference, owner, and permitted next action.

## Treat rule changes as releases

An invariant library is operating logic. Changing it can expand or contract what the AI system may do.

A new exception, time-zone rule, facility mapping, authority ceiling, or prerequisite should receive a version, owner, effective time, test evidence, and rollback path. In-flight proposals must declare which rule version governs them. If a rule changes before execution, the release gate should re-evaluate rather than assuming the old pass remains valid.

The [NIST AI Risk Management Framework](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/) is voluntary and not a self-storage tool protocol. Its emphasis on governance, documented roles, systematic documentation, and lifecycle risk management supports the broader discipline here: operating controls need ownership and evidence across design, use, review, and change.

Useful measures include releases evaluated by action class, failures by invariant, unknown states past due, proposals rejected for stale evidence, rule changes without completed tests, human overrides by reason, and executed actions missing a release receipt. These measure the control. They do not prove improved revenue, occupancy, safety, customer experience, or adoption.

## Give operators the release receipt

The companion **Facility Action Invariant Matrix and Release Gate** records the schema result, each operating invariant, the evidence evaluated, rule and source versions, pass/fail/unknown state, authority result, exception owner, and final release receipt.

The receipt should answer five questions without opening developer logs:

1. What action was proposed?
2. Which facility state and policy versions governed it?
3. Which invariants were tested, and what evidence supported each result?
4. Who had authority to release or resolve it?
5. What exact payload, tool version, and target receipt were bound to execution?

If the action is materially revised, issue a new proposal ID, new payload digest, and new evaluation. A prior pass should never become a reusable permission slip.

## The final gate is operational meaning

Strong schemas are necessary. They keep malformed and out-of-contract data from reaching the tool. But operational systems fail in ways that fit neatly inside valid JSON.

The harder errors are coherent-looking combinations that are impossible for the facility, inconsistent with the governing records, stale at the moment of release, or outside the actor’s authority.

Make those conditions explicit. Evaluate them against current evidence. Keep schema, invariant, and authority results separate. Return a release receipt that an operator can inspect.

Then a green check can mean more than “the API accepted the shape.” It can mean the proposed action made sense for this facility, under this authority, at this time—and the system preserved the evidence before it acted.

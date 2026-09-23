# The Tool Schema Changed. Did the Agent’s Authority Change Too?

**A compatibility gate for artificial intelligence tool calls that binds one approved facility effect to the exact operation, argument contract, defaults and executor version.**

By Jared Mastroianni

An artificial intelligence agent prepares a narrow access-control change for one self-storage facility. The approved action is to create an internal review record. The agent supplies a facility identifier, a gate identifier and a reason code. The call passes schema validation.

During a routine software release, the tool gains an optional field called `notify_customer`. The executor treats a missing value as `true`. An older agent still sends the same three arguments, the payload still validates and the tool now reaches a customer-facing channel that was never part of the approved action.

Nothing about the model’s text had to change. The contract around the text changed.

This is an explicitly fictional failure path, not a report about a product, facility or deployment. It exposes an architecture problem that becomes more important as self-storage teams connect artificial intelligence to access, maintenance, customer communication, inventory and pricing workflows: **a valid tool call is not necessarily the same authorized business action after the tool contract changes.**

The control for that gap is a tool-contract compatibility gate. It compares the agent’s evaluated contract with the executor’s current contract and projected effect before any consequential call is released.

## Separate syntax from operating authority

A schema can determine whether an object contains allowed types, required properties and enumerated values. That work matters. It prevents malformed arguments from flowing directly into an operating system.

It answers a narrow question: does this instance satisfy this schema?

It does not establish that the named facility is the right one, that an omitted argument received a safe value, that an enum still carries the same meaning, that the executor uses the same defaults, or that the resulting side effects remain inside the approval.

[JSON Schema Draft 2020-12](https://json-schema.org/draft/2020-12/json-schema-validation) makes the distinction visible. Validation keywords impose assertions on an instance. Keywords such as `default` are annotations; they can describe a value associated with a schema without requiring every implementation to insert it during validation. The specification also explains that `format` is an annotation under the default vocabulary unless assertion behavior is deliberately enabled. A green validator therefore has to be interpreted in the context of the actual validator, dialect and application behavior.

An AI action path needs four separate compatibility findings:

1. **Structural compatibility:** the proposed arguments validate under the exact declared schema and dialect.
2. **Semantic compatibility:** every argument, enum, unit, null state and default has the same operating meaning that was evaluated.
3. **Authority compatibility:** the current tool still exposes only the action, scope and side effects covered by the approval.
4. **Outcome compatibility:** the executor’s observed result can be reconciled to the approved effect.

One finding cannot substitute for another.

## Give the operation a durable identity

Tool names are often written for people: `updateGate`, `createTask` or `sendNotice`. A familiar name can survive several incompatible implementations.

The release record needs a more exact identity:

- tool or service name;
- operation identifier;
- schema dialect and schema version;
- canonical schema digest;
- executor or adapter version;
- downstream endpoint and credential scope;
- effect class and maximum consequence;
- default-resolution policy;
- response or receipt contract; and
- deprecation and compatibility state.

The current [OpenAPI Specification](https://spec.openapis.org/oas/v3.2.1.html) defines `operationId` as a case-sensitive identifier that must be unique among operations described in the API. It also distinguishes required from optional parameters and supports schemas based on the OpenAPI dialect of JSON Schema. The specification is useful for describing an interface. Its own schema guidance warns that schemas cannot catch every specification violation.

For an agent workflow, the approved unit is not merely `operationId=updateGate`. It is the operation plus its argument meaning, executor behavior, permission scope and side-effect envelope. A schema digest helps detect byte changes. It cannot explain whether those changes are compatible. That classification needs an accountable owner.

## Treat defaults as executable policy

Defaults are easy to miss because they do not appear in the agent’s proposed payload. They can still determine the effect.

Suppose an old contract accepts:

```json
{
  "facility_id": "FAC-FIC-017",
  "gate_id": "GATE-FIC-EAST",
  "action": "create_review_record"
}
```

A new executor adds optional fields for `notify_customer`, `dispatch_vendor` and `restore_access`. If any omitted field resolves to an active behavior, the absence of text has become a command.

The compatibility gate should materialize every effective value before approval or execution. It takes the model’s proposal, applies the exact current resolution rules in a non-executing environment and produces an **effect projection**. The projection states which records, messages, access states, vendor jobs or customer-visible surfaces could change.

The release owner compares that projection with the approved effect. If a new field, default, inferred identity or hidden downstream call expands the effect, the call stops even when structural validation passes.

This is also why an adapter should not silently “help” by filling a missing facility from the current browser session, choosing the first matching customer or converting an unknown enum to a nearby value. Useful inference in a draft becomes dangerous ambiguity in an action. The proposal should return to a person or a governed resolution step with the missing fact visible.

## Reject more than malformed JSON

A tight action contract usually benefits from the following rules:

- reject undeclared properties instead of ignoring them;
- make consequential fields explicit and required;
- represent unknown, omitted and intentionally empty values separately;
- bind units and time zones to the field definition;
- version enums when their operating meaning changes;
- prevent the model from supplying server-owned receipt or approval fields;
- prohibit default values that create an external side effect;
- return machine-readable validation and compatibility failures; and
- keep the model’s original proposal beside the normalized candidate.

These rules do not make the model authoritative. They make the proposal inspectable.

The [OWASP GenAI Security Project’s Excessive Agency guidance](https://genai.owasp.org/llmrisk/llm062025-excessive-agency/) describes risk created by excessive functionality, permissions or autonomy in systems that can call tools. It recommends minimizing available functions and permissions, requiring approval for high-impact actions and enforcing authorization in downstream systems rather than relying on the language model. OWASP guidance is community security guidance, not a self-storage standard or a finding about a particular implementation. Its central architecture point is useful here: the executor must mediate the call under current policy.

## Classify change by effect, not by version label

Teams often describe a change as major, minor or patch. That label can support release planning, but it is not enough for an operating decision. A field added in a “minor” release can broaden a customer message. A spelling fix in an enum can cause every older proposal to fail. A server-side implementation change can alter behavior without changing the published schema.

Classify compatibility against the exact action class:

- **Equivalent:** same effective arguments, scope, side effects and receipt semantics. Existing evaluation may remain eligible within its original time and policy limits.
- **Narrower:** the new contract removes capability or tightens validation. Re-test because previously valid proposals may now fail, but do not assume authority expanded.
- **Broader:** new target, side effect, permission, default or downstream call becomes reachable. Require a new evaluation and approval.
- **Ambiguous:** meaning, default behavior, identity resolution or receipt semantics cannot be established. Hold the action.
- **Breaking:** an approved argument, enum, unit, response or readback path no longer carries the evaluated meaning. Migrate and re-evaluate.

The compatibility result belongs to a named contract owner and business-effect owner. Engineering can identify the code and schema difference. Operations can identify what the difference means at a facility. Security or access owners can confirm the effective permission. The accountable business owner decides whether the resulting action class is eligible for release.

## A fictional access-tool rollout

Consider an entirely fictional operator, Basin Line Storage, using a fictional tool called `prepare_access_exception`.

Version 4.1 accepts a facility ID, gate ID, evidence reference and one of three intents: `draft_review`, `hold_for_manager` or `close_no_action`. The evaluated workflow may create an internal review record. It may not change access, contact a customer or dispatch a vendor.

Version 4.2 introduces three changes:

1. `hold_for_manager` becomes `restrict_pending_review`;
2. an optional `notify_customer` argument is added; and
3. the adapter resolves a missing `facility_id` from the active user session.

The fictional agent was evaluated against 4.1. It emits a stored proposal using `hold_for_manager`, with the facility ID present and no notification field.

The 4.2 schema rejects the old enum, so the adapter maps it to `restrict_pending_review`. That mapping sounds reasonable, but it changes an internal queue state into a potentially customer-affecting restriction. The new notification field resolves to `false`, so no message is sent. The facility identity remains exact.

The gate still returns **breaking**. The risk is not only the notification default. The enum’s business effect changed. The old approval covered an internal review record, not an access restriction. The team preserves the old proposal, creates a new candidate under 4.2, projects the effect, routes the exact restriction to the authorized manager and runs a current-state readback before any release.

In a second fictional test, the agent omits `facility_id`. The adapter can infer one facility from the user session, but the gate returns **ambiguous**. Identity inference is not accepted for this consequence class. The proposal receives a handback reason and no tool call occurs.

Every organization, facility, version, field, rule and outcome in this example is invented. It demonstrates the gate; it does not claim a product, deployment or result.

## Put compatibility before the execution credential

A mature flow keeps the language model on the proposal side of the boundary:

1. Resolve authenticated subject, actor, organization and facility scope.
2. Select the allowed operation from the current tool registry.
3. Capture the exact schema, dialect, digest, executor and permission versions.
4. Validate the model’s raw proposal without executing it.
5. Normalize only through documented rules; preserve raw and normalized forms.
6. Project the complete business effect, including defaults and downstream calls.
7. Compare the current contract with the evaluated and approved contract.
8. Require the appropriate owner to approve the exact effect and digest.
9. Issue a narrow, expiring execution credential for that exact candidate.
10. Execute once, collect the provider receipt, read governing state and reconcile.

The [NIST Generative Artificial Intelligence Profile](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) discusses governance, change-management controls, monitoring, documentation and different levels of human oversight across generative-AI contexts. It does not prescribe this gate or validate an implementation. It supports the broader conclusion that a changed application or human-AI configuration belongs inside governance, not outside it as a routine technical detail.

Human approval also needs the projected effect, not a friendly tool name. “Approve `prepare_access_exception`” hides too much. “Create one internal review record for facility `FAC-FIC-017`; no access change, customer message, vendor dispatch or financial effect” gives the reviewer a bounded decision.

## Test the path that production will run

Schema comparison alone cannot prove behavior. The test suite needs the actual adapter, executor and downstream test path.

Use fixtures for prior approved proposals, current proposals, omitted fields, unknown fields, enum changes, nulls, empty strings, unit conversions, cross-facility identifiers, expired approvals and responses missing their expected receipts. Run the same candidate through the old and new contracts without releasing a real effect. Compare normalized arguments, projected effects, authorization decisions, outbound requests and resulting test readbacks.

Then challenge the negative path. Confirm that a blocked compatibility result cannot obtain an execution credential. Confirm that a stale agent cannot bypass the registry by calling an old endpoint directly. Confirm that a provider success receipt cannot close the record when the governing facility state disagrees. Confirm that rollback of the schema also restores the compatible executor and permission set rather than only the documentation.

The accompanying **AI Tool Contract Compatibility Register** keeps those facts in one review sequence. Its examples are fictional and unexecuted. It does not certify a tool, approve facility access, establish software security or replace provider-specific testing.

The practical rule is concise: **bind authority to the effect, then prove that the current contract still produces that effect.** A validator can confirm that the call is well formed. Only the compatibility gate, current authorization and operating readback can show whether it is still the action someone approved.

---

## Operator tool

Download the **AI Tool Contract Compatibility Register** as an XLSX workbook or CSV register. A passive responsive HTML reference presents the same fictional cases.

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai. His work focuses on facility operations, multi-location systems, data governance and responsible artificial intelligence.

## Editorial production note

Research synthesis, drafting, structured-tool production and quality assurance were completed with AI assistance under Jared Mastroianni’s direction. The article remains bounded by its sources, fictional-example labels and claim limitations.

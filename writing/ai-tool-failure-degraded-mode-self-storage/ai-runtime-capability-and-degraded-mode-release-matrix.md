# AI Runtime Capability and Degraded-Mode Release Matrix

Use this tool for each consequential AI-assisted workflow before release and after any change to a tool, schema, permission, model, policy, organization binding, or facility binding. One row represents one required or optional runtime capability. The matrix does not grant authority; it records the authority and controls supplied by the operator.

## Part 1: Define the capability contract

| Field | Required entry | Release question |
| --- | --- | --- |
| Workflow, run, organization, and facility IDs | Exact governed identifiers | Could this run act on the wrong business or property? |
| Decision and consequence class | Describe the intended decision and impact | What is the most consequential possible outcome? |
| Tool, operation, version, and schema digest | Exact runtime dependency | Can a reviewer reproduce which capability was expected? |
| Permission and identity scope | Read/write rights and target scope | Does the caller have the required authority for this target? |
| Required or optional | `required` or `optional` | May the workflow reach release without this capability? |
| Freshness and coverage requirements | Maximum age and required population/fields | What makes the result current and complete enough? |
| Permitted degraded mode | Exact useful behavior when unavailable | What can continue without becoming a decision? |
| Action ceiling | Maximum allowed action in that state | Which actions must remain prohibited? |
| Handback owner | Named role or person | Who owns resolution and by when? |
| Readback requirement | Authoritative post-action check | What proves the business state actually changed? |

## Part 2: Classify each runtime receipt

Use one of these states rather than a generic success/error flag:

| State | Meaning | Default control |
| --- | --- | --- |
| `not_invoked` | Required call was never attempted | Hold and investigate orchestration |
| `rejected` | Identity, permission, policy, or validation blocked the call | Hold; resolve authority, do not blind-retry |
| `timed_out` | No acceptable result arrived within the decision window | Bounded retry if transient, then hand back |
| `partial` | Coverage or required fields are incomplete | Hold decision; request missing scope |
| `stale` | Result exceeds the freshness limit | Refresh before decision |
| `empty_valid` | Authoritative source completed and validly returned no records | Preserve as a valid result; do not relabel as failure |
| `completed` | Operation met scope, coverage, and freshness requirements | Continue within declared authority |
| `completed_unverified` | Write accepted but required state readback is missing | Hold closure and customer-facing claim |

## Part 3: Apply the release gate

- [ ] Every required capability has a current `completed` or valid `empty_valid` receipt.
- [ ] Organization, facility, account, and policy identity scopes agree.
- [ ] Partial results, page limits, and stale cache paths were tested.
- [ ] No model memory, cached summary, or conversational context substituted for a missing authoritative source.
- [ ] Optional capability loss is visible and within the declared degraded mode.
- [ ] Required capability loss lowered the action ceiling and created a handback.
- [ ] Retries are bounded, semantically appropriate, and safe from duplicate writes.
- [ ] A recovered tool causes a new current read and full recomputation.
- [ ] Any consequential write has an authoritative business-state readback.
- [ ] The final workflow label distinguishes `eligible_for_release`, `executed_awaiting_readback`, and `closed`.

## Part 4: Handback packet

Record only the evidence an operator needs to resolve the exception:

1. Requested outcome and consequence class.
2. Exact organization, facility, account, and workflow identifiers.
3. Successful receipts with source, scope, age, and trace reference.
4. Missing or conflicting capability with its failure state.
5. Actions the system explicitly did not take.
6. Next authorized check or escalation.
7. Owner, due time, and required closure evidence.
8. Whether full recomputation is required after recovery.

## Release rule

If any required capability is `not_invoked`, `rejected`, `timed_out`, `partial`, `stale`, or `completed_unverified`, the workflow may not claim business completion. It may continue only within a documented degraded mode, and no customer-facing or consequential action may exceed the recorded action ceiling.

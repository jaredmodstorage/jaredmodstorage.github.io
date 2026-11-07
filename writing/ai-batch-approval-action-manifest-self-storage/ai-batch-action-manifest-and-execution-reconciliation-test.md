# AI Batch Action Manifest and Execution Reconciliation Test

Use this tool before one human approval authorizes more than one AI-assisted facility action. It tests whether the approval, execution and receipt sets can be proven identical or their differences explicitly reconciled.

## A. Manifest header

| Field | Required record |
| --- | --- |
| Manifest ID and version | Stable unique identifiers |
| Proposal created at | Timestamp with timezone |
| Created by | Model/service identity and version |
| Governing policy/tool versions | Exact versions used to form the set |
| Human approver and decision time | Named person, decision and timestamp |
| Approved member count | Count derived from manifest rows |
| Manifest digest | Digest algorithm and value over canonical representation |
| Authority boundary | Allowed action types, facilities, assets, limits and exclusions |
| Expiration | Time or condition after which unused approval is invalid |

## B. Required action row fields

Record one row per approved action in the companion CSV.

- Action ID; facility ID; asset/unit/customer/vendor target IDs.
- Action type; exact payload; amount/access/communication limits.
- Source record identifiers, versions and observed timestamps.
- Preconditions and prohibited side effects.
- Approval membership state and material-change rule.
- Attempt, result, target receipt and observed postcondition.
- Retry state, exception owner and next action.

## C. Pre-execution gates

Mark Pass only when evidence exists.

| Gate | Pass standard | Result |
| --- | --- | --- |
| Membership | Action ID is present in the approved manifest version. | Pass / Fail |
| Integrity | Recomputed digest matches the approved digest. | Pass / Fail |
| Target identity | Facility and asset identifiers resolve without ambiguity. | Pass / Fail |
| Payload identity | Executable payload matches the approved payload. | Pass / Fail |
| Authority | Credential scope fits the approved action and target only. | Pass / Fail |
| Preconditions | Current conditions satisfy all approved preconditions. | Pass / Fail |
| No substitution | Worker cannot replace a blocked member with a new item. | Pass / Fail |
| Expiration | Approval remains within its approved time/condition window. | Pass / Fail |

Any Fail stops that action. A stopped member does not authorize a substitute.

## D. Reconciliation

Calculate from row-level records:

- Approved count = manifest members.
- Attempted count = members for which a target request was issued.
- Succeeded count = members with verified accepted/completed postconditions.
- Blocked/failed count = members without successful postconditions.
- Unresolved count = blocked/failed members lacking a closed resolution.
- Unapproved attempts = attempted actions absent from the manifest; required value is zero.

The batch passes only when all attempts belong to the approved manifest, every approved member has a terminal or explicitly owned unresolved state, and totals tie to individual rows.

## E. Amendment rule

Adding or removing a member, or materially changing a facility, asset, vendor, customer, amount, communication recipient, access level, payload or governing authority, requires a new manifest version and renewed approval. A retry may reuse approval only when the exact approved target and payload remain unchanged and the retry policy was part of the approval.

## Operator signoff

- Reconciliation completed by:
- Completed at:
- Approved / attempted / succeeded / unresolved:
- Unapproved attempts (must be zero):
- Exceptions and owners:
- Final disposition:

This is an operating-control template, not legal, cybersecurity or regulatory advice. Adapt it to applicable contracts, policies, laws, system capabilities and risk.

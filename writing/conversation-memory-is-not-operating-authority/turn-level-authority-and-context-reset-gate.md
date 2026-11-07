# Turn-Level Authority and Context Reset Gate

Use this proposed gate before a consequential AI-supported action or when a material condition changes during a multi-turn workflow. It preserves durable standing approval where it remains valid. It does not require a fresh approval after every conversational turn.

## 1. Resolve the current turn

| Gate | Required evidence | Pass condition | Hold or reset condition |
| --- | --- | --- | --- |
| Principal | Authenticated user or service ID; authentication time; session state | Current principal is established | Principal is unknown, changed, expired or untrusted |
| Organization | Stable organization ID from the governing identity source | Requested work belongs to an eligible organization | Transcript label or prompt text is the only organization reference |
| Facility | Stable facility ID and approved aliases | Every shorthand reference resolves to one eligible facility | Multiple candidates remain or a display name is used as authority |
| Purpose | Declared operating job | Purpose remains inside the active grant | Follow-up introduces a new or incompatible purpose |
| Action class | Read, summarize, draft, propose, communicate, dispatch or change state | Requested action is explicit | “Same,” “do it,” or “close it” hides a more consequential action |

## 2. Validate the authority

| Gate | Required evidence | Pass condition | Hold or reset condition |
| --- | --- | --- | --- |
| Grant or role | Current grant/role ID and owner | Grant covers the principal, purpose, facility and action class | Conversation history is the only proof of permission |
| Valid time | Effective start, end and relevant timezone | Grant is active | Grant is not yet active, expired or time state is unknown |
| Revocation | Current revocation/suspension readback | Not revoked or suspended | Revocation state is unknown, revoked or suspended |
| Policy binding | Governing policy/configuration version | Current version supports the action | Relevant version changed or cannot be established |
| Standing approval | Bounded approval reference and exact scope | Durable approval remains valid for this routine step | Requested scope exceeds the approval or a material condition changed |

## 3. Rebind the evidence

- [ ] Earlier evidence is reused by record ID and version, not copied text alone.
- [ ] Organization, facility, customer, unit, asset and work IDs match the current turn.
- [ ] Source eligibility and classification still permit this purpose.
- [ ] Freshness is sufficient for the consequence of the action.
- [ ] Corrections, conflicts and superseding records were checked.
- [ ] Model output is labeled as output or proposal, not facility fact.
- [ ] The current governing source was read where a facility-state claim is required.

## 4. Set the action ceiling

Choose the highest permitted state supported by both authority and evidence:

1. `context_only` — maintain conversational continuity; no operating claim.
2. `read_only` — retrieve eligible evidence.
3. `summary` — organize evidence without adding authority.
4. `draft` — create an unreleased artifact.
5. `proposal` — recommend a bounded action for an authorized decision owner.
6. `released_action` — execute only when the current grant, policy, preconditions and release rule all pass.

If authority and evidence support different ceilings, use the lower one.

## 5. Material-change reset triggers

- [ ] Principal or session changed.
- [ ] Organization or facility changed.
- [ ] Purpose changed.
- [ ] Action class became more consequential.
- [ ] Grant, role, standing approval or revocation state changed.
- [ ] Governing policy or configuration changed.
- [ ] Required source became stale, corrected, conflicting or unavailable.
- [ ] Model, retrieval path or tool contract changed in a way relevant to release.
- [ ] Saved conversation was reopened or shared across a defined session boundary.
- [ ] Prior action state cannot be reconciled from a current receipt/readback.

A reset may revalidate silently, refresh evidence, narrow the action ceiling, ask a targeted clarification, route qualified review or stop release. It does not automatically require a new approval.

## 6. Release and reconcile

- [ ] Bind the released action to the turn envelope and exact payload hash.
- [ ] Record the authority reference and policy version used at release.
- [ ] Preserve provider/system submission and acceptance receipts separately.
- [ ] Read back the governing facility or workflow state.
- [ ] Record incomplete, failed, canceled and reconciled as different states.
- [ ] Keep the transcript as history, not as a substitute for the action ledger.

## Decision record

- Turn envelope ID:
- Conversation ID and turn ID:
- Principal:
- Organization/facility scope:
- Purpose:
- Requested action class:
- Valid authority reference:
- Policy/configuration version:
- Evidence set/version/freshness:
- Prior-turn dependencies:
- Action ceiling:
- Reset trigger, if any:
- Clarification or review owner:
- Release state:
- Receipt/readback state:
- Final owner and next step:

This tool is an operating design aid. Adapt it to approved security, privacy, legal, records, accessibility, vendor and facility procedures. It does not establish compliance, product capability or permission by itself.

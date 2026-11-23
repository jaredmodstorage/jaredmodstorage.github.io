# Memory Admission, Scope and Expiration Register

Use this register before conversational, case or derived content becomes durable facility memory. The objective is not to preserve everything. It is to make the promotion into future reusable context visible, bounded and reversible.

## Admission decision

| Gate | Required question | Hold condition |
|---|---|---|
| Subject | Which exact facility, asset, unit, account, work item, role, policy or workflow does this concern? | Free-text nickname, unresolved identity or cross-facility ambiguity |
| Class | Is this a verified fact, temporary instruction, preference, observation, hypothesis, exception, prohibition or derived summary? | Unknown class or class inconsistent with the source |
| Authority | Which source may support this claim, and what does it not establish? | Source is relevant but non-governing, superseded, challenged or unproved |
| Purpose | Why must the statement survive the current session or case? | Convenience without a named future use |
| Scope | Which facility, audience, role, workflow and consequence may use it? | Broad or inherited scope without evidence |
| Time | When is it effective, when is review due and what makes it expire? | No executable expiration or review condition |
| Approval | Who may admit this class at this consequence level? | Model self-approval or missing qualified owner |
| Removal | Can it be challenged, revoked and disabled across indexes and derivatives? | No propagation path or readback |

## Lifecycle

`proposed → rejected | admitted → active → challenged | expired | superseded | revoked`

- **Proposed:** candidate is isolated from future work.
- **Rejected:** candidate stays in its case or session under that record’s retention rule.
- **Admitted:** required fields and approval exist, but the effective time may not have arrived.
- **Active:** eligible only for the recorded scope and consequence.
- **Challenged:** excluded from normal decision context pending disposition.
- **Expired:** no longer eligible for new work; retained only as authorized historical evidence.
- **Superseded:** replaced by a named newer version; both versions keep lineage.
- **Revoked:** deliberately withdrawn; propagation and affected-decision review are required.

## Required operating controls

- Keep the governing source authoritative; memory is a bounded aid, not a replacement system of record.
- Store the minimum content needed for the declared purpose.
- Use exact identity keys and separate assertion, observation, effective and expiration times.
- Make event-based expiration include a maximum review time.
- Block challenged, expired, superseded and revoked entries from new decisions.
- Preserve every consequential use through a decision reference.
- Propagate removal to stores, caches, indexes and derived summaries, then read back the result.
- Reconcile completed actions separately; revoking memory is not operational undo.

## Files

- `memory-admission-scope-and-expiration-register-blank.csv`: implementation header with no example data.
- `memory-admission-scope-and-expiration-register-fictional-example.csv`: explicitly fictional teaching rows for rejection, active, expired and challenged states.

This is an editorial operating tool, not a deployed product, certification, control framework or legal/privacy/records determination.

# AI-to-Human Handback Acceptance and Authority Ledger

Use one record for each handback version. A handback offer is not human acceptance. Do not mark the case human-owned until acceptance, authority fencing and pending-effect review are recorded.

## Control fields

| Control area | Required record | Pass condition |
|---|---|---|
| Case identity | Case, portfolio, facility, asset/customer scope | Exact governed objects, not free-text aliases |
| Evidence boundary | Source references, retrieval times, observation cutoff | Observations separated from inference |
| Runtime identity | Model, prompt, retrieval, policy, tool and workflow versions | Reproducible version set |
| Handback reason | Exact decision or condition outside agent authority | Human role and decision requested |
| Interim state | Accountable coordinator, permitted actions, prohibited effects | No ownership gap and no unrestricted continuation |
| Offer | Packet version/hash, recipient role, offered time | Immutable offer receipt |
| Acceptance | Human identity/role, accepted packet version, accepted time | Affirmative acceptance of current version |
| Ownership epoch | Prior and new epoch/generation | Old-epoch writes rejected |
| Authority transition | Grant/token references, expiry, revocation/narrowing receipt | Prior action authority no longer effective |
| Pending effects | Queued, dispatched, accepted, retrying, scheduled and irreversible effects | Every effect has a disposition |
| Reconciliation | Cancel/complete/compensate/investigate receipts and system readback | Effective state established or exception remains open |
| Observability | Trace/correlation IDs and transfer-stage timings | Transfer can be reconstructed without treating telemetry as state proof |
| Timeout | Acceptance deadline, alternate route and emergency boundary | No silent abandonment |

## Acceptance gate

- [ ] Current packet version and hash displayed.
- [ ] Facility, resource scope and observation cutoff displayed.
- [ ] Observed facts distinguished from classifications and recommendations.
- [ ] Unresolved decisions, deadlines and interim controls displayed.
- [ ] Pending-effect inventory displayed.
- [ ] Human role is authorized for the requested decision.
- [ ] Acceptance creates a durable receipt and advances the ownership epoch.
- [ ] Prior-epoch writes are rejected at the tool or resource boundary.
- [ ] Old grants are revoked or narrowed and active-state caching is bounded.
- [ ] Queued, in-flight and late effects are reconciled with receipts/readback.

## State rule

> No affirmative acceptance receipt + no active handback coordinator = an ownership gap, not a completed escalation.

## Closure rule

A trace, queue acknowledgement, token-revocation response or closed task is evidence about one step. Close the handback only when ownership, authority transition and pending effects have separate durable evidence.


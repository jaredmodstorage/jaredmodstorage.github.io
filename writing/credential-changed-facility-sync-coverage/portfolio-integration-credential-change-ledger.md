# Portfolio Integration Credential Change Ledger

Use this card to reconcile a machine credential change across every dependent consumer and facility scope. Do not record any password, secret, private key, recovery code, or token value in this ledger.

## Change header

- Change event ID:
- Provider/source system:
- Credential class:
- Authorized change owner:
- Approved change window:
- Reason: scheduled lifecycle / provider requirement / compromise response / ownership change / other
- Governing policy or ticket:
- Old credential non-secret reference:
- New credential non-secret reference:
- Planned old-credential retirement time:
- Rollback authority:
- Incident/escalation route:

## Consumer and facility row

Record one row for every scope that can fail independently.

| Field | Required entry |
|---|---|
| Consumer ID and name | Exact job, connector, application, device, or recovery process |
| Environment | Production, test, recovery, or other named boundary |
| Facility ID and scope | Stable portfolio ID plus source-local ID; grouped scope only when its atomic basis is documented |
| Required permissions | Minimum provider scopes, roles, or resource access |
| Expected cadence | Event-driven, hourly, daily, weekly, or another defined cycle |
| Last success before change | Timestamp, evidence reference, and source |
| New credential installed | Yes/no, time, actor or accountable position, evidence |
| Authentication result | Pass/fail/not evaluated, time, non-secret response evidence |
| First operating proof | Record/event/report identity and downstream receipt; no customer-sensitive payload |
| Facility coverage result | Complete/partial/missing/not evaluated |
| Exception | Exact gap, operating consequence, owner, due time |
| Temporary boundary | Hold, excluded scope, read-only use, rollback, or other approved control |
| Old credential state | Active/revoked/expired/unknown plus governing readback |
| Observation-window end | Time that completes one meaningful consumer cycle |
| Decision | Hold/limited/released/reconciled |
| Decision owner and time | Named accountable role and timestamp |

## Release tests

1. Every expected consumer is represented.
2. Every expected facility is represented or covered by a documented atomic grouping.
3. The new credential is identified without exposing its value.
4. Authentication succeeded for the intended consumer and environment.
5. The required permissions and facility scope match the approved use.
6. At least one permitted operating proof completed for every independently failing scope.
7. Missing evidence remains `not evaluated`, not zero activity or a pass.
8. Exceptions have an owner, due time, consequence, and temporary boundary.
9. The observation window covers one meaningful operating cycle.
10. The prior credential's state is confirmed at the governing source.
11. Downstream counts, receipts, or business states reconcile to the expected population.
12. No consequential authority was expanded merely to run the test.

## Decision rule

- **Hold** when authentication, scope, operating proof, or a required safety/security boundary is unresolved.
- **Limited** only when the allowed facilities and uses are explicit and excluded scopes cannot act.
- **Released** when one row's named consumer and facility scope pass the required proof.
- **Reconciled** only when the full expected population is accounted for and the prior credential's final state is verified.

This tool is an operating-control template. It does not prescribe credential lifetimes, replace a password vault, override provider instructions, or constitute cybersecurity certification.

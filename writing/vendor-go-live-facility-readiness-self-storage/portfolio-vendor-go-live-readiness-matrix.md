# Portfolio Vendor Go-Live Readiness Matrix

Use one row for each facility and affected change boundary. Preserve facility-specific truth; do not replace a held site with the portfolio majority.

| Control | Minimum record | Hold condition | Release evidence |
|---|---|---|---|
| Facility identity | Permanent facility ID, governed aliases, vendor site ID, environment | Alias, account or environment cannot be reconciled | Operator and vendor records resolve to the same facility and environment |
| Change boundary | Affected system, component or workflow; current baseline; proposed action; explicit exclusions | Scope is broad, ambiguous or different across records | One reviewable action and exclusion set tied to the current baseline |
| Authority | Approval owner, execution identity, observer, pause owner, recovery owner | Actor or decision authority is missing or broader than the change | Named owners and credentials match their permitted roles |
| Preconditions | Required export or backup, source availability, device state, training, support path, incident review | Any required condition lacks current evidence | Evidence references recorded for every required condition |
| Local exceptions | Exception, consequence, owner, due time, resolution test | Exception could change scope, evidence, safety, privacy, access or customer impact | Exception resolved or a named owner approves a specific restriction |
| Window | Start, stop, affected business activity, staffing and communication | Window conflicts with facility operations or required owner is absent | Facility-specific window and operating boundary acknowledged |
| Stop conditions | Wrong identity, unrecognized environment, missing evidence, unexpected write, source loss, customer impact, receipt timeout | Any stop condition occurs or cannot be detected | Detection method and pause authority confirmed before execution |
| Execution receipt | Request ID, actor, target, time, proposed and actual scope, provider response | Receipt is missing, ambiguous or points to another target | Provider response preserved and tied to the intended request |
| Authoritative readback | Governing source, verification query, result, reviewer and time | Source result is unavailable, conflicting or outside approved boundary | Current source readback matches the approved outcome |
| Recovery | Retry decision owner, rollback or compensating method, communication boundary, next review | Uncertain effect has no governing-source check or owned recovery path | Recovery method is executable and owner accepts the handback |
| Local release | Technical status, operating restriction, staff/customer readiness, release owner and time | Technical success exists without operating readiness | Local release owner records `released` or an explicit restriction |
| Portfolio reconciliation | State count, unresolved facilities, owner, next decision time | Central status hides held or recovery-open facilities | Every facility is represented by a current evidence-backed state |

## Controlled states

- `discovery_open`: identity, scope or baseline is still being established.
- `held_identity`: facility, account, alias or environment is not reconciled.
- `held_precondition`: a required source, export, control, owner or local condition is unresolved.
- `ready_with_restriction`: a named authority approved a specific restriction with an owner and review time.
- `ready`: all required preconditions and evidence are current for the defined change.
- `change_in_progress`: execution has begun within the approved window.
- `recovery_open`: the outcome is failed, conflicting or uncertain and the recovery owner has the handback.
- `released`: authoritative readback and local operating release are complete.

## Release rule

No facility enters `ready` without reconciled identity, a bounded proposed action, named authority, current preconditions, detectable stop conditions and an owned recovery path. No facility enters `released` from a provider success message alone; preserve the authoritative readback and local operating release.

This tool is a general operating aid. Tailor it to the applicable contract, security, privacy, safety, technical, legal and facility procedures. It does not certify a vendor or implementation.

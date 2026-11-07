# Portfolio Policy Exception Expiration and Compensating-Control Register

Use one row per authorization. A request is not active until the required authority approves it. An expired or pending-renewal record is not active.

## Required fields

| Field | What to record | Acceptance test |
|---|---|---|
| Exception ID | Stable unique identifier | Never reused or overwritten |
| Baseline authority | Policy/procedure/control ID and version | Opens the exact governing record |
| Scope | Facility, asset, workflow, vendor, role, or customer segment | No broader than the verified conflict |
| Unmet requirement | Exact baseline requirement that cannot be met | Specific enough to test |
| Verified reason | Current condition creating the need | Evidence link attached |
| Approver | Role authorized to accept the temporary risk | Approval timestamp retained |
| Compensating control | Action, performer, frequency/trigger, evidence, failure response | Observable and testable |
| Control owner | Person or role performing the control | Owner has acknowledged the assignment |
| Oversight owner | Person or role reviewing evidence | Review cadence stated |
| Effective term | Start, review, and expiration timestamps | Includes timezone |
| Stop conditions | Events that suspend the excepted activity | Clear enough for the next shift |
| Evidence status | Current, overdue, failed, or not applicable | Latest evidence linked |
| Disposition | Adopted, renewed by new record, superseded, revoked, or expired | Decision and evidence retained |

## Weekly review sequence

- [ ] Confirm every requested exception is either approved or still treated as unauthorized.
- [ ] Review controls marked overdue or failed before reviewing approaching dates.
- [ ] Review exceptions expiring within 7 days, then within 30 days.
- [ ] Escalate every expired exception and apply the defined hold.
- [ ] Test that each active record links to the exact policy version and current evidence.
- [ ] Compare first approval age with current term to expose repeated renewals.
- [ ] Verify closure evidence before reporting baseline adoption.

## Decision rule

> No current approval + no current compensating-control evidence = no active exception.

## Renewal rule

Create a new decision with current rationale, evidence, term, and approval. Link it to the prior record. Do not edit the prior expiration date to manufacture continuity.


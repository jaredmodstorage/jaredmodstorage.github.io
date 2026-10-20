# Cross-Facility Access Transition Ledger

Use this ledger whenever a customer, employee, vendor or other authorized subject changes facility scope. The record reconciles the intended source and destination entitlements with provider receipts and authoritative readbacks.

## 1. Define the transition

- Use governed internal identifiers for the subject, source facility, destination facility and associated units.
- Record the approved policy version and transition effective time.
- Define the exact source permission expected to end and destination permission expected to begin.
- Identify secondary users or dependent credentials requiring separate dispositions.

## 2. Bound any overlap

- Record overlap start, end, scope and authorizing role.
- Treat an authorized, unexpired overlap separately from a failed or unknown revocation.
- If the interval changes, add the new authorization; do not overwrite the original.

## 3. Preserve six lifecycle states

- **Requested:** Business workflow created the change request.
- **Accepted:** Provider or system acknowledged the request.
- **Enforced:** Target system reports the expected configuration.
- **Verified:** Approved readback confirms subject, facility, scope and time.
- **Reconciled:** Source and destination agree with the contract.
- **Closed:** Evidence is complete and the designated authority closes the record.

## 4. Reconcile both boundaries

- Verify destination entitlement and schedule.
- Verify source entitlement absence or approved continuing scope.
- Record provider receipts separately from readback results.
- Keep missing, conflicting and stale states explicit.

## 5. Control exceptions

- Assign every exception a class, owner and next review time.
- Record any manual control and its narrow scope.
- Do not create unrecorded shared codes or broad portfolio permissions.
- Close only when the required evidence and secondary-user dispositions are present.

## Daily review

Review open transitions by exception class, age, overlap status, provider state and owner. Report authorized overlap, unresolved dual access, missing readback and confirmed mismatch separately.

The blank CSV and explicitly fictional Summit Lane example use the same 52-field schema.

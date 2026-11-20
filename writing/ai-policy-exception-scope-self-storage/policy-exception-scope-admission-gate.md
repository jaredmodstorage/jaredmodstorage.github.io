# Policy–Exception Scope Admission Gate

Use one row for every retrieved record considered for an AI-supported operational decision. Complete the gate before generation and recheck it immediately before any external effect.

## Decision identity

| Field | Required entry |
|---|---|
| Decision ID | Unique current case identifier |
| Facility ID | Facility the decision affects |
| Subject ID | Account, unit, vendor, asset or incident identifier |
| Requested action | Exact action the AI is evaluating |
| Policy domain/version | Governing domain and expected baseline version |
| Observed-state time | Timestamp of current operational evidence |
| Consequence class | Advisory, reversible internal, customer-facing, access, financial, legal/safety escalation |
| Requesting role | Person or service requesting the decision |

## Source admission tests

| Test | Pass condition | Failure disposition |
|---|---|---|
| Authority class | Record is classified as policy, active exception, case evidence, example, history or unverified material | Unclassified records cannot govern |
| Facility scope | Record expressly covers the current facility or approved portfolio scope | Background only or reject |
| Subject scope | Named customer, vendor, asset, workflow or incident matches | Background only or reject |
| Action scope | Record permits the exact requested action | Reject as authority |
| Time/status | Record is effective, unexpired, unrevoked and current at decision time | History only |
| Policy version | Record is compatible with the current baseline version | Hold for authorized resolution |
| Approver authority | Approval role covers the current consequence class | Reject as authority |
| Required controls | Compensating controls are present and can be performed now | Hold or hand back |
| Reuse rule | Record expressly permits the intended use; exceptions default to case-only | Reject reused authority |
| Pre-effect recheck | All tests still pass immediately before action | Stop effect and re-evaluate |

## Allowed outputs

- **Governing authority:** may control the recommendation within proven scope.
- **Current case evidence:** may establish facts within provenance and freshness limits; grants no permission.
- **Background only:** may help explain or compare; must be labeled non-authoritative.
- **Rejected:** excluded from the answer's authority basis; retain rejection reason.
- **Hold/handback:** use when no current authority can be established or a required fact/control is unresolved.

Never convert repeated exceptions into policy automatically. If a pattern should become reusable, route it through an authorized policy-change process.

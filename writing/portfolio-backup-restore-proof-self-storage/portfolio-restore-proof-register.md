# Portfolio Restore-Proof Register

Use one row for each **facility + recovery object + operating function**. This is a governance and evidence tool, not a place for passwords, encryption keys, customer data or restricted backup contents.

## Required operating states

| State | Minimum evidence | What it does not prove |
|---|---|---|
| `inventoried` | Stable facility, recovery object, data class, governing source and scope | A backup exists |
| `backed_up` | Copy reference, creation time, recovery point and protection state | Integrity or restorability |
| `integrity_checked` | Approved check method, time, result and evidence reference | The object supports its operating function |
| `restored_in_test` | Authorized isolated environment, actor, times and restoration evidence | Production recovery is authorized |
| `functionally_verified` | Qualified business readback against the written success condition | Future versions remain recoverable |
| `exception_open` | Variance, owner, due condition and operating boundary | Failure or success is resolved |
| `production_recovery_authorized` | Event-specific authority, scope and approved execution path | The recovery has completed or reconciled |

## Restore-proof workflow

1. **Name the object.** Record the facility, governing source, data class, included scope and exclusions.
2. **Locate the copy.** Record the backup platform, creation time, represented recovery point, retention class and protection state.
3. **Check independence.** State whether the backup can be altered or lost through the same path as the working source.
4. **Verify integrity.** Use the approved check for that object and link the evidence without exposing restricted content.
5. **Prepare the test.** Name an isolated environment, authorized actor, dependency manifest and approved credential path.
6. **Write success first.** Define the bounded functional readback before restoration begins.
7. **Restore and read back.** Record start, completion, result, sample or reconciliation method and any variance.
8. **Dispose honestly.** Use `passed`, `passed_with_exception`, `failed` or `not_evaluated`. Assign every exception.
9. **Invalidate when necessary.** Reopen proof after material source, schema, platform, dependency, facility-scope or authority changes.

## Minimum review questions

- Does the row identify the operating record rather than only a filename?
- Is the recovery point distinct from the backup job time?
- Are facility and data-class boundaries explicit?
- Can an approved alternate follow the credential path?
- Does the test avoid unauthorized production mutation and customer impact?
- Did a business owner verify function, not merely file readability?
- Are missing attachments, relationships, permissions and dependencies visible?
- Does the state expire or reopen when its test basis changes?

## Prohibited shortcuts

- Do not store secrets or customer data in this register.
- Do not treat synchronization as independent backup without testing the failure boundary.
- Do not treat a checksum alone as functional recovery.
- Do not convert a vendor receipt, job-complete notice or archive screenshot into restore proof.
- Do not overwrite `failed`, `not_evaluated` or `exception_open` with a portfolio average.
- Do not run a production restore without the event-specific authority and rollback path required by the governing procedure.

The companion fictional CSV demonstrates structure only. It does not represent a real facility, provider, deployment, backup, restore test, service level or recovery result.

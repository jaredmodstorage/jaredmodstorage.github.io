# Correction-Propagation Register Data Dictionary

The register contains 39 columns. One row represents one correction target. Multiple rows may share one correction ID.

| Field group | Required content |
|---|---|
| Correction identity | `correction_id`, `correction_type`, opened time, facility, asset/object, audience and affected use |
| Governing source | Source system, locator, prior and replacement versions, effective time, authority and evidence URI |
| Claim boundary | Prior claim and replacement claim, preserving explicit unknown or retraction states |
| Target lineage | Target surface, system, derivative ID and relationship to the prior claim |
| Propagation plan | One primary disposition, target owner, due time, status and propagation time |
| Verification | Method, query/check, requester scope, environment, index/build version, cache state, result and evidence URI |
| Exception | Owner, deadline and operating boundary when a target cannot be verified |
| Closure | Closure authority, time and boundary notes |

## Controlled values

### `correction_type`

- `FACTUAL_CORRECTION`
- `PERMISSION_CHANGE`
- `EXPIRATION`
- `RETRACTION`
- `SCOPE_CLARIFICATION`

### `required_disposition`

- `UPDATE`
- `INVALIDATE`
- `QUARANTINE`
- `SUPERSEDE`
- `RESTRICT`
- `RETAIN_AS_HISTORY`
- `ESCALATE`

### `propagation_status`

- `NOT_EVALUATED`
- `QUEUED`
- `IN_PROGRESS`
- `VERIFIED`
- `OUT_OF_SCOPE`
- `APPROVED_EXCEPTION`
- `FAILED`

### `verification_result`

- `PASS`
- `FAIL`
- `NOT_EVALUATED`
- `NOT_APPLICABLE`

## Validation rules

1. Each target row must retain the same governing correction identity and source-version pair.
2. `VERIFIED` requires method, requester scope, environment, result and evidence URI.
3. `APPROVED_EXCEPTION` requires an exception owner, due time and operating boundary.
4. A final correction closure requires every required target to be `VERIFIED`, `OUT_OF_SCOPE` or an `APPROVED_EXCEPTION`.
5. An invalidated cache does not prove index, conversation or pending-action correction.
6. The fictional rows are examples only and must never be used as operating evidence.

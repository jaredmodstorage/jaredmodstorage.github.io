# Inter-Facility Transfer and Receipt Ledger

Use this ledger to govern one physical inventory transfer between two facilities. Adapt item eligibility, approvals, evidence, stock states, valuation, accounting and retention to the operator's actual systems and policies. This tool does not establish ownership, loss, tax treatment or employee fault.

## 1. Transfer identity and authorization

| Field | Controlled record |
|---|---|
| Transfer ID |  |
| Source facility stable ID |  |
| Destination facility stable ID |  |
| Requester / request time |  |
| Business reason |  |
| Approver / approval time |  |
| Approval basis or policy version |  |
| Requested movement date |  |
| Current transfer state |  |

## 2. Item-line reconciliation

| Line | Item ID / description | Unit | Approved | Picked | Released | Received | Accepted | Rejected or held | Unresolved |
|---|---|---|---:|---:|---:|---:|---:|---:|---:|
| 1 |  |  |  |  |  |  |  |  |  |
| 2 |  |  |  |  |  |  |  |  |  |
| 3 |  |  |  |  |  |  |  |  |  |

For each line, test: `released = accepted + rejected_or_held + unresolved`.

## 3. Event trail

| Event | Actor | Facility / location | Timestamp | Evidence reference | Result / next state |
|---|---|---|---|---|---|
| Requested |  |  |  |  |  |
| Approved |  |  |  |  |  |
| Picked / source verified |  |  |  |  |  |
| Custody released |  |  |  |  |  |
| Transport update |  |  |  |  |  |
| Destination received |  |  |  |  |  |
| Inspected / accepted |  |  |  |  |  |
| Exception disposition |  |  |  |  |  |

## 4. Custody and exception controls

| Control | Record |
|---|---|
| Package, tote, seal or transport reference |  |
| Source releaser and custody recipient |  |
| Destination receiver |  |
| Condition at release and receipt |  |
| Variance reason state | Unknown / Short / Over / Damaged / Wrong item / Unit mismatch / Other governed code |
| Exception owner and due time |  |
| Authorized disposition |  |
| Independent or compensating review |  |
| Final closure actor / time |  |

## Release test

- Both facility identities resolve to one current governed record.
- Every item has an identifier and unit of measure.
- Request, approval, release, receipt and acceptance are separate events.
- No destination quantity is available merely because the source released it.
- Expected, observed and accepted quantities remain visible.
- Every released line reconciles or carries an open exception.
- Closure preserves the event history and named authority.


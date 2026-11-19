# Portfolio Adjustment Authority Matrix and Review Queue

Use this tool as two connected records. The authority matrix defines who may perform each step. The review queue records what happened in one adjustment from request through reconciliation.

## Part 1: authority matrix

| Field | Entry |
| --- | --- |
| Matrix version and effective time |  |
| Role |  |
| Facility or portfolio scope |  |
| Allowed adjustment classes | Correction / Policy-based / Discretionary / Other governed class |
| May request | Yes / No |
| May approve | Yes / No |
| May post | Yes / No |
| May reconcile | Yes / No |
| Amount or consequence limit |  |
| Required evidence |  |
| Prohibited combinations |  |
| Second-review rule |  |
| Delegation rule and expiration |  |
| Escalation owner |  |
| Policy owner and evidence link |  |

## Part 2: adjustment review queue

| Field | Entry |
| --- | --- |
| Review record ID |  |
| Facility ID |  |
| Account ID |  |
| Source transaction or charge ID |  |
| Requester and request time |  |
| Adjustment class |  |
| Governed reason code and version |  |
| Requested amount and effective date |  |
| Evidence references |  |
| Decision maker and authority tier |  |
| Decision and decision time |  |
| Approved amount and effective date |  |
| Poster and posting time |  |
| Posted transaction ID |  |
| Reconciler and reconciliation time |  |
| Account / facility / amount / date match |  |
| Exception type | Missing evidence / Unauthorized / Policy version / Wrong account / Wrong facility / Amount variance / Duplicate / Missing review / Other governed type |
| Exception owner and due time |  |
| Customer communication record, if required |  |
| Final state | Requested / Returned / Denied / Approved / Posted / Reconciled / Exception / Closed |
| Final evidence link |  |

## Closure test

Close the record only when the adjustment class and reason are governed, the decision authority is valid, the posted transaction matches the approval, any required communication is evidenced, and every exception is resolved or formally transferred to a named owner.

This tool is an operating-control template. It does not provide legal or accounting advice and does not determine what an agreement, law or accounting policy requires.

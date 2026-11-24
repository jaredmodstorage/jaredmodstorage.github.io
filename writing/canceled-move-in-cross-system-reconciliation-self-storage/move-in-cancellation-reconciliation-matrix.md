# Move-In Cancellation Reconciliation Matrix

Use one case per canceled move-in and one row per affected operating domain. This matrix preserves the original move-in and tracks new compensating actions; it does not delete signed records, determine legal status, select payment remedies or replace provider-specific procedures.

## Case identity

| Field | Exact value |
| --- | --- |
| Cancellation case ID | |
| Facility ID | |
| Customer record ID | |
| Unit ID | |
| Agreement ID | |
| Original move-in event ID | |
| Cancellation requested at / source | |
| Requesting person / verification | |
| Governing policy version | |
| Case owner / due time | |

## Domain reconciliation

| Domain | Original effect and ID | Required end state | Compensating action / authority | Provider or system receipt | Readback source / time | Result |
| --- | --- | --- | --- | --- | --- | --- |
| Unit inventory | | | | | | Not started |
| Agreement / documents | | | | | | Not started |
| Payment | | | | | | Not started |
| Protection / insurance | | | | | | Not started |
| Access | | | | | | Not started |
| Communications | | | | | | Not started |
| CRM / lead | | | | | | Not started |
| Operational reporting | | | | | | Not started |
| Accounting handoff | | | | | | Not started |
| Other governed domain | | | | | | Not started |

Allowed results: `not_started`, `scope_unresolved`, `authorization_required`, `requested`, `accepted_pending_verification`, `verified`, `intentionally_retained`, `blocked`, `manual_review`, `not_applicable`.

## Final gate

- [ ] Every expected domain is present or explicitly marked not applicable with a reason.
- [ ] Original events and signed artifacts remain preserved.
- [ ] Each compensating action has the correct authority and unique identity.
- [ ] Provider acceptance is separated from authoritative readback.
- [ ] Failed or irreversible actions have an owner, next action and deadline.
- [ ] Unit, agreement, payment, protection, access, communication and reporting states no longer conflict—or every remaining conflict is explicitly owned.
- [ ] Final reviewer and timestamp are recorded.

Final case state: `reconciled` only after all required rows are `verified`, `intentionally_retained` or approved `not_applicable`. A blocked row keeps the case open.


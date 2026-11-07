# Portfolio Charge-Code Definition and Mapping Register

Use this register to govern how a facility/source charge code relates to a portfolio operating concept for a defined period. It supports operational comparability. **It does not determine general-ledger, tax, regulatory or financial-statement treatment.**

## 1. Source definition

| Field | Required record |
| --- | --- |
| Mapping ID and version | Stable identifier; do not overwrite a prior approved version |
| Facility ID and facility name | Governed identity, not a free-text nickname |
| Source system and environment | Exact source that produced the code |
| Source code and displayed label | Preserve both; labels are not definitions |
| Source definition | Business event and population the code actually represents |
| Inclusions and exclusions | Explicit boundaries for the source population |
| Unit and sign convention | Currency, count, quantity, positive/negative treatment or other governed unit |
| Source definition owner | Role accountable for the source meaning |
| Source effective from/to | Period in which this definition governs |
| Governing evidence | Configuration, procedure, approved definition or other authoritative reference |
| Evidence as-of time | When currency was last verified |

## 2. Target portfolio concept

| Field | Required record |
| --- | --- |
| Target concept ID and label | Stable portfolio identifier and readable name |
| Target definition | Exact operating meaning for this analysis |
| Target inclusions and exclusions | Boundaries another reviewer can reproduce |
| Target owner and version | Accountable role and current definition version |
| Authorized reporting uses | Named reports or decisions that may use the relationship |
| Prohibited uses | Uses not supported, including accounting/tax treatment unless separately governed |

## 3. Relationship decision

Choose one relationship from evidence. Do not infer equivalence from matching labels.

| Relationship | Meaning | Default release state |
| --- | --- | --- |
| Exact | Source and target have the same governed meaning for this use and period | Eligible after approval and reconciliation |
| Narrower | Source covers a documented subset of the target | Eligible only for the subset stated |
| Broader | Source combines the target with additional activity | Hold unless an approved split preserves the distinction |
| Related | Concepts are associated but not interchangeable | Do not aggregate as the same concept |
| Unresolved | Definition or evidence is incomplete or contradictory | Hold |
| No relationship | Source does not belong in this target concept | Exclude with reason |

- Relationship rationale:
- Approved transformation or allocation rule, if any:
- Accounting/legal/tax review required: Yes / No / Unknown
- Mapping owner:
- Approver and approval time:
- Change ticket or decision reference:
- Prior mapping ID/version:
- Reporting effective time:
- Retirement time:
- Rollback mapping/version:

## 4. Controlled-period reconciliation

| Test field | Value |
| --- | --- |
| Test period and cutoff | |
| Source record count | |
| Source control total | |
| Accepted record count | |
| Held/excluded/unresolved record count | |
| Mapped control total | |
| Unmapped amount | |
| Final variance | |
| Exception reason and owner | |
| First production-period readback | |

A zero variance proves arithmetic under the test. It does not prove that the semantic relationship is correct.

## 5. Release and review gate

The mapping is eligible only when:

1. Facility, source system, source code and effective period are exact.
2. Source and target definitions each have an accountable owner.
3. The relationship and any transformation are supported by evidence.
4. Required accounting, legal or tax review is complete or explicitly not applicable under the governing process.
5. The controlled-period test reconciles or every variance is bounded and assigned.
6. Downstream reports and historical-treatment rules are named.
7. Approval, effective time, retirement boundary and rollback path are recorded.

- Decision state: draft / hold / approved for named use / rejected / retired
- Decision owner:
- Decision time:
- Next review time:
- Notes without customer-level or sensitive data:

This register is an operating data-governance aid. Adapt it to current systems, contracts, policies, accounting authority, tax requirements, privacy controls and applicable law.

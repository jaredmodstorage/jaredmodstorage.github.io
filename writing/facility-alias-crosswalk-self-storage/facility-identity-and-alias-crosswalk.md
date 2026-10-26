# Facility Identity and Alias Crosswalk

Use this tool before combining multi-location data, allocating transactions or allowing automation to act on a source-system facility label.

## 1. Define the operating identity

- Assign one stable internal facility key to each governed operating location.
- Do not recycle a retired key.
- Treat the marketing name, address, owner, manager and vendor labels as attributes, not the key itself.
- Record parent, child, annex, building, gate, legal-entity and billing-account scope explicitly.

## 2. Capture each source alias without rewriting it

For every system or counterparty, retain the exact source record ID and display label. Record the source system, record type, scope and effective dates. Never replace the native identifier in source evidence with the internal facility key.

## 3. Validate the relationship

Acceptable evidence may include a source-system property page, executed agreement, service address, work-order reference, acquisition schedule, approved accounting map or other attributable record. Name similarity alone is not approval evidence.

## 4. Assign a mapping status

| Status | Meaning | Downstream treatment |
|---|---|---|
| Matched | One governed relationship is supported for the recorded scope and dates. | Eligible for the approved reporting or workflow use. |
| Ambiguous | More than one facility or scope remains plausible. | Quarantine; require resolution. |
| Unknown | No governed relationship has been established. | Quarantine; assign an owner and due date. |
| Retired | Historically valid but not valid for new activity. | Preserve for historical lookup; block new use. |
| Rejected | Proposed relationship was reviewed and found wrong. | Preserve the decision; block the proposal. |

## 5. Release through change control

- Record the approver, approval date and change reference.
- Require a second reviewer for mappings that can move money, alter access, create work orders or trigger customer communication.
- Apply effective dates; do not overwrite historical relationships.
- Recalculate affected outputs only after the corrected mapping is approved.

## 6. Test the exception path

Use at least these cases before production release:

- renamed property;
- sold or retired property;
- main facility and annex with similar names;
- vendor abbreviation;
- reused or legacy accounting label;
- source record outside its effective period; and
- identifier that maps to the facility but only for a narrower scope such as a gate or billing account.

The control passes when uncertain records stop for review and approved records remain traceable to their original source identifiers.

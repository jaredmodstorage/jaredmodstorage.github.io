# Facility Alert-Scope Resolution Grid

Use this tool to connect an official alert record to governed facility locations without treating receipt, geographic match, site condition, assigned work, and operating release as the same state.

## Gate 1 — Freeze the source message

- Capture provider, alert identifier, sender, sent time, status, message type, scope, and references.
- Record event, headline, urgency, severity, certainty, effective, onset, expiration, and instruction summary.
- Preserve retrieval time and a source hash, ETag, or equivalent evidence reference when available.

## Gate 2 — Preserve every geographic form

- Record area description, geometry state, polygon or circle reference, geocode IDs, and affected-zone IDs.
- Do not replace a polygon with a county name or treat a forecast zone as a county.
- If the source geometry cannot be read, retain `unresolved`; do not silently broaden or narrow it.

## Gate 3 — Load the governed facility location

- Use the stable facility ID and governed address record.
- Record the approved coordinate pair, coordinate source, verification date, county UGC, public forecast zone, fire-weather zone, and location-record version.
- Stop automated resolution when the facility location is missing, stale, disputed, or conflicting.

## Gate 4 — Resolve one facility at a time

Choose exactly one primary match state:

- `included_by_geometry`
- `included_by_county`
- `included_by_zone`
- `outside_represented_area`
- `adjacent_monitoring_rule`
- `unresolved`

Record the match method and evidence. Do not infer an on-site condition from geographic inclusion.

## Gate 5 — Assign bounded work

- Link the approved portfolio action template and facility emergency-plan reference.
- Name the work owner, work-item ID, facility operating state, and next review.
- Keep official alert content separate from company-authored instructions.

## Gate 6 — Track receipt, action, evidence, and release separately

- Receipt: `not_sent / sent / acknowledged / failed / unknown`.
- Action: `not_started / in_progress / reported_complete / held / not_applicable`.
- Verification: record an evidence ID or `not_evaluated`.
- Operating release: only the named authority changes the facility state.

## Gate 7 — Recompute the message family

- Connect updates and cancellations through the source references.
- Store each resolution version; do not overwrite prior facility matches.
- Record facilities added, removed, unchanged, or unresolved after every new source version.
- Close the source-alert state separately from local restrictions and work items.

## Release question

Before closing the record, answer:

> Can another operator explain why this exact facility was included, excluded, monitored, or held using the exact alert version, facility-location version, match evidence, and named decision owner?

If not, the resolution remains open.

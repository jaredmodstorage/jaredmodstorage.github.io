# Incident-Family Card Data Dictionary

The CSV contains 42 columns. Required fields are marked **Required**.

| Field | Requirement | Meaning |
|---|---|---|
| `family_id` | **Required** | Durable portfolio identifier for the bounded episode. |
| `family_state` | **Required** | Candidate, confirmed, contained, operationally restored/follow-up open, closed, split or cancelled as non-incident. |
| `facility_id` | **Required** | Stable facility identity; not a display name alone. |
| `facility_timezone` | **Required** | IANA timezone used for local timestamps. |
| `opened_at_local` | **Required** | Time the family record was opened. |
| `candidate_window_start_local` / `candidate_window_end_local` | Conditional | Review window; not automatically the impact interval. |
| `affected_asset` / `affected_service` / `affected_audience` | **Required** | Explicit scope of the episode. |
| `scope_statement` | **Required** | Plain-language boundary, including meaningful exclusions. |
| `source_record_count` / `source_record_ids` | **Required** | Count and durable identifiers of linked source records. |
| `signal_summary` | **Required** | Direct observations and system signals, without inferred cause. |
| `impact_verified` / `impact_description` | **Required** | Whether operating impact is supported and what it was. |
| `unaffected_observations` | Recommended | Known services, assets or audiences not affected. |
| `suspected_cause` / `suspected_cause_status` | Conditional | Hypothesis and status; never present a suspicion as verified. |
| `verified_cause` | Conditional | Qualified conclusion or explicit `UNKNOWN`. |
| `containment_action` | Conditional | Temporary exposure-reducing action. |
| `correction_action` | Conditional | Action taken to restore or correct the condition. |
| `release_test` / `release_evidence_uri` | **Required for release** | Test performed and durable evidence reference. |
| Five timestamp fields | Conditional | First affected, awareness, contained, restored and closed clocks kept separately. |
| `time_limitations` | Recommended | Unknown bounds, timezone issues and observation gaps. |
| `member_status_summary` | **Required for release** | Status of tickets, alerts, calls and work orders without allowing them to control family state. |
| `relationship_decision` | **Required** | `LINK`, `MERGE` or `SPLIT`. |
| `relationship_rationale` | **Required** | Evidence-based reason for the decision. |
| `relationship_decision_owner` / `relationship_decision_at_local` | **Required** | Named accountable decision and time. |
| `follow_up_owner` / `follow_up_due_at_local` | Conditional | Owner and due time for an open cause or corrective action. |
| `revalidation_trigger` | **Required** | New evidence that requires family review. |
| `release_authority` / `release_decision` / `release_at_local` | **Required for release** | Named authority, decision and timestamp. |
| `notes` | Optional | Boundary notes; never a replacement for required structured fields. |

## Validation rules

1. `source_record_count` must equal the number of identifiers in `source_record_ids`.
2. A `CLOSED` family requires a release authority, decision, release timestamp and release evidence.
3. A verified cause requires an evidence-backed investigation; otherwise use `UNKNOWN`.
4. Ticket completion, alert clearance and family release timestamps remain independent.
5. The example row is fictional and must not be reused as operating evidence.

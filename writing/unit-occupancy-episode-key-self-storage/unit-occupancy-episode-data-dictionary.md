# Unit-Occupancy Episode Register Data Dictionary

- `facility_id`: durable facility identifier, not a display name.
- `physical_unit_id`: durable identifier for the physical space.
- `unit_label`: human-facing locator such as B-214; not a relationship key.
- `occupancy_episode_id`: durable identifier for one bounded party-unit relationship.
- `party_id`: source-governed person or organization identifier.
- `agreement_id`: governing agreement identifier where applicable.
- `episode_state`: proposed values include planned, active, closing, closed, cancelled, reversed and inter-occupancy.
- `effective_from` / `effective_through`: explicit operating boundary in RFC 3339 format with UTC offset.
- `source_system` / `source_record_id`: provenance for the asserted episode.
- `predecessor_episode_id` / `successor_episode_id`: lineage across turnover or transfer.
- `transfer_id`: explicit link when the episode is part of a transfer.
- `access_enabled_at` / `access_revoked_at`: access lifecycle events; not substitutes for occupancy boundaries.
- `recorded_at`: when the assertion was stored or received.
- `last_corrected_at` / `correction_owner`: correction provenance.
- `linkage_state`: resolved, physical_unit_only, exception or not_applicable.
- `exception_owner`: named accountable role or person for unresolved linkage.
- `notes`: bounded explanation; never a substitute for required identifiers.

Field names and states are a proposed operating pattern. Map them to local law, policy and source capabilities before implementation.

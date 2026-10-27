# AI Event-Time Integrity and Causal-Order Test

Use this tool to test one AI-reconstructed operating episode before its timeline influences incident classification, customer communication, access, staff accountability, maintenance dispatch or automated follow-up.

## Decision rule

1. Define the facility-safe identity, episode, consequence and intended use.
2. Record each source timestamp without overwriting its original value or meaning.
3. Identify the source clock, synchronization evidence, offset and uncertainty at the event time.
4. Correct the reference estimate only through a documented rule. Preserve the raw value. In this template, `offset_ms` means source clock minus reference clock, so `corrected_time = raw_time - offset_ms`.
5. Compute an earliest and latest possible time as `corrected_time - uncertainty_ms` and `corrected_time + uncertainty_ms`.
6. Capture causal evidence separately: source sequence, trace, parent, correlation and supersession links.
7. Classify the relevant order as `causally_ordered`, `time_bounded`, `order_ambiguous` or `contradictory`.
8. Release only the statement supported by the classification. Route consequential ambiguity or contradiction to the named reviewer.

For two time intervals, A is definitely before B only when `A.latest < B.earliest`. If the intervals overlap, their order remains unresolved by time bounds even when their center estimates differ. An explicit causal edge may order related software operations, but it does not order an unlinked physical observation or prove a physical effect.

## Important boundaries

- A timestamp's precision does not prove clock accuracy.
- A corrected time is an estimate, not an observed facility fact.
- Adjacent timestamps do not establish causation.
- A trace relationship establishes software-flow structure, not physical completion, business authority or customer identity.
- Provider acceptance remains separate from execution and governing-state readback.
- Missing or sampled telemetry must remain visible; do not reconstruct an omitted event as fact.

## Required tests

- Fast device clock and slow device clock.
- Clock step or manual adjustment during the episode.
- Offline device with late upload.
- Duplicate, replayed and out-of-order delivery.
- Missing trace propagation or reused correlation ID.
- Local timestamp without UTC offset.
- Restart that resets a source sequence.
- Sampled trace with a missing intermediate span.
- Corrected or superseded event record.
- Overlapping uncertainty intervals that make order ambiguous.

## Fictional calculation check

For Harbor Pike, the command interval is `23:14:04.980–23:14:05.180Z`, provider acceptance is `23:14:05.310–23:14:05.550Z`, camera motion is `23:14:05.000–23:14:11.000Z`, and the gate event is `23:14:12.200–23:14:16.200Z`. Command and acceptance are definitely before the gate interval. Camera overlaps both command and acceptance, so those two pairwise orders are unresolved by time bounds. Camera is time-bounded before the gate interval. None of those interval relationships proves physical causation.

## Package files

- `ai-event-time-integrity-template.csv`: blank 41-column record.
- `ai-event-time-integrity-fictional-example.csv`: four explicitly fictional Harbor Pike rows demonstrating command, provider receipt, gate and camera events.

This tool is an editorial control template. It does not certify time synchronization, telemetry completeness, system security, authorization, a physical condition or a causal finding.

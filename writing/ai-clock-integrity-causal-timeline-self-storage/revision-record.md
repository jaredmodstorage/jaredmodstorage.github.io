# Technical correction record

## Superseded package

- Original article SHA-256: `f7806e72087cea971c89153a66929bf83dff891c257a94276060a946c3930fcd`.
- Original payload manifest SHA-256: `2c7da201fb58662ef80e2fd43ec543958ad50b2ac7e7615a7d99d2398acede74`.
- Publisher stopped before any repository mutation or publication.
- Defect: the narrative said command and provider acceptance preceded both corrected facility-event windows. The camera interval overlapped both.

## Independently recomputed convention

`offset_ms = source_clock - reference_clock`.

`corrected_time = raw_time - offset_ms`.

`earliest = corrected_time - uncertainty_ms`; `latest = corrected_time + uncertainty_ms`.

## Recomputed fictional intervals

| Event | Raw UTC | Offset | Corrected center | Uncertainty | Interval |
| --- | --- | ---: | --- | ---: | --- |
| `CMD-FIC-184` | 23:14:05.100 | +20 ms | 23:14:05.080 | ±100 ms | 23:14:04.980–23:14:05.180 |
| `ACK-FIC-711` | 23:14:05.460 | +30 ms | 23:14:05.430 | ±120 ms | 23:14:05.310–23:14:05.550 |
| `CAM-FIC-122` | 23:14:04.000 | −4,000 ms | 23:14:08.000 | ±3,000 ms | 23:14:05.000–23:14:11.000 |
| `GATE-FIC-903` | 23:14:03.200 | −11,000 ms | 23:14:14.200 | ±2,000 ms | 23:14:12.200–23:14:16.200 |

All stored intervals exactly match the recomputation.

## Pairwise conclusions

- Command is definitely before provider acceptance by non-overlapping bounds and is also the traced parent operation.
- Command and provider acceptance are each definitely before the corrected gate-event interval.
- Camera overlaps both command and provider acceptance; those pairwise orders are unresolved by time bounds.
- Camera is time-bounded before the gate-event interval.
- No interval ordering or trace edge proves physical causation, customer identity, authorization or facility effect.

The corrected narrative, decision-rule wording and all four fictional CSV rows now preserve these exact conclusions.

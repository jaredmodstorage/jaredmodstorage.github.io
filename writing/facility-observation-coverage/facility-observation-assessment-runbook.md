# Facility observation coverage assessment runbook

Author: Jared Mastroianni
State: governed operator-to-architect tool
Boundary: authored method with fictional examples; not a deployed control, sensor procedure, safety instruction, legal conclusion, privacy authorization, or product capability

## Purpose

Use this runbook before an operator, dashboard, automation, or AI treats a facility signal as evidence for a decision. The output is not “telemetry good.” The output is one bounded claim with a typed coverage state, visible blind spots, an accountable owner, and a degradation rule.

Do not use this runbook to authorize a physical action. It maps observation coverage only. Consequential actions require their own authority, execution, readback, and reconciliation controls.

## Coverage states

- `C0_uninstrumented` — no eligible observation path exists for the claim.
- `C1_signal_present` — a signal exists, but identity, meaning, continuity, quality, or use is not sufficiently bounded.
- `C2_bounded_observation` — source, property, footprint, time, and limitations are explicit.
- `C3_decision_admissible` — the bounded observation passes the named decision rule for one use.
- `C4_corroborated` — required corroboration addresses the named failure mode without hidden common-mode dependence.
- `CX_indeterminate` — evidence is missing, stale, conflicted, restricted, overflowed, or otherwise unable to support the claim now.

These are authored operating labels, not industry grades, safety levels, or certifications.

## Step 1 — Freeze the question

Write one sentence containing:

1. facility identity;
2. target property;
3. physical or operational footprint;
4. time or interval;
5. population or denominator;
6. proposed decision use; and
7. consequence class.

Reject verbs such as “check,” “monitor,” or “confirm” without an object and boundary. Split compound questions. “Is the pad active?” and “Is the building flooding?” require different evidence.

## Step 2 — Classify the claim mode

Choose exactly one:

- directly observed;
- derived by a deterministic transformation;
- inferred by a model or rule;
- declared by an identified human or system; or
- unknown.

Do not select the mode you want. Select the mode the evidence supports. Preserve the producer, transformation or model version, and uncertainty. Never promote inferred or declared state to direct observation in a summary.

## Step 3 — Resolve source and lifecycle identity

For every input, record the facility, system, device, point, field, owner, lifecycle state, and configuration version. Check whether display labels were reused after replacement, retirement, relocation, or renaming.

If identity is unresolved, stop at `C1_signal_present` or `CX_indeterminate`. Do not merge histories by friendly name.

## Step 4 — Draw the actual footprint

Mark what the observation point can physically or logically see. Name exclusions. Then define the expected population: active probes, readers, doors, partitions, pages, records, or inspection areas.

Compare the source footprint with the claim footprint. If one corridor probe is being used to describe every unit, narrow the claim or add eligible evidence. Do not hide partial coverage inside a percentage.

## Step 5 — Trace acquisition and transformation

Record whether the path is event-driven, polled, streamed, batch, or manual. Preserve:

- sampling or trigger rule;
- change filter;
- queue depth and overflow signal;
- sequence or deduplication identity;
- aggregation window and temporality;
- unit conversion;
- transformation or model version; and
- attributes removed or added in transit.

Walk the path from producer to collector, broker, store, query, and display. At each hop, ask what could be lost, delayed, duplicated, reordered, retained, aggregated, hidden, or relabeled.

## Step 6 — Prove time and continuity

Capture source, observation, receipt, evaluation, and decision times where they exist. Record clock owner and uncertainty. Define freshness, allowed lateness, expected cadence, and completeness.

For a negative claim such as “no event was recorded,” require:

- an active expected-source inventory;
- producer or path-health evidence;
- complete sequence or interval evidence;
- no unresolved overflow or queue loss;
- a known filter and retention window; and
- a query that covers the exact interval.

If those checks fail, the state is unknown or indeterminate—not normal.

## Step 7 — Preserve native quality

Record source quality, diagnostic status, inspection or calibration state when applicable, out-of-range tests, stuck-value tests, restarts, and discarded values. Do not replace `uncertain`, `bad`, `late`, `partial`, `overflow`, or `restricted` with a generic success or green tile.

Schema conformance is a separate result. It proves structure only.

## Step 8 — Test corroboration and common mode

Name the failure mode the second source is meant to address. Compare power, network, controller, clock, cache, software, model inputs, data store, operator information, and physical placement.

Two displays backed by one controller are not independent for a controller fault. A human inspection influenced by the same dashboard is not blind corroboration. If common mode remains, label it.

## Step 9 — Apply authority and privacy boundaries

Record purpose, allowed audience, retention, and use restrictions. An accurate source may still be unauthorized for a customer message, security action, personnel decision, or public claim.

Treat intentional non-collection as governed design. Do not propose broader surveillance merely to improve a technical coverage score. Route changes through accountable privacy, legal, security, safety, and operational owners as applicable.

## Step 10 — Write the admission and degradation rules

The admission rule names the exact evidence that makes the claim usable for one decision. The degradation rule names what happens when evidence is missing, stale, conflicted, restricted, or late.

A good rule includes:

- admitted coverage state;
- required source identities and lifecycle states;
- time, quality, completeness, and denominator thresholds;
- prohibited broader claims;
- stop, inspection, reduced-scope, or escalation behavior;
- accountable exception owner; and
- review or expiry time.

Avoid “use best available data.” That phrase hides the consequence of missing evidence.

## Step 11 — Run failure cases

Use the companion readiness suite. At minimum test:

- producer offline while transport stays connected;
- stale retained value after reconnect;
- queue overflow;
- missing active source;
- identity reuse;
- unit or meaning change;
- clock error and late arrival;
- stuck value;
- duplicate and out-of-order delivery;
- incomplete aggregation;
- conflicting observations;
- common-mode corroboration;
- access restriction;
- retention shorter than the query; and
- AI narrative that converts unknown to normal.

The system passes when it degrades honestly and routes ownership. It does not pass merely because an error was logged.

## Step 12 — Release and review

Version the question, source inventory, observation point, transformation, decision rule, privacy purpose, and tests together. Re-run coverage validation after sensor replacement, firmware, controller, topology, sampling, field, aggregation, model, policy, facility lifecycle, or retention changes.

Record the exact release and rollback identities. A clean build or valid schema is not proof of live observation fitness. Production acceptance requires current source readback under the applicable operating procedure.

## Closeout statement

Write four lines:

1. **Admitted claim:** the exact bounded statement supported now.
2. **Mode and coverage:** directly observed, derived, inferred, declared, or unknown; C0 through C4 or CX.
3. **Unresolved blind spots:** spatial, temporal, semantic, identity, transport, quality, common mode, authority, and intentional privacy.
4. **Next owner and action:** who owns the gap, what they must do, and when the state expires.

If those lines cannot be written without guessing, retain `unknown` or `indeterminate`. Honest uncertainty is an operational control.

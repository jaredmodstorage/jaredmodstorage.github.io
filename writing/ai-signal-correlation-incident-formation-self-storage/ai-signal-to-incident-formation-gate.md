# AI Signal-to-Incident Formation Gate

Use this gate when an AI or rules service proposes that several facility signals belong to one operating incident. Complete it before a candidate can dispatch work, restrict access, contact customers, change financial records, suppress separate alerts or become a confirmed portfolio incident.

## Gate 1 — Admit each signal

- [ ] Stable source system, record ID and version are present.
- [ ] Facility, zone, asset or subject scope is governed.
- [ ] Event, observation and ingestion times are distinguished.
- [ ] Clock quality, freshness, units and schema are acceptable.
- [ ] Record role is explicit: observed, reported, inferred, commanded or derived.
- [ ] Test, maintenance, simulation and duplicate states are known.
- [ ] The signal is permitted for this correlation purpose.

**Hold:** `held_signal_ineligible`

## Gate 2 — Align identity

Record the exact facility, zone, asset and subject mapping for every signal. Preserve the source labels and the governed mapping version. Do not let a shared display name substitute for a stable identity.

**Hold:** `held_identity_unresolved`

## Gate 3 — Align time

Name the correlation window and the timestamp used for each signal. A late note, delayed controller record or stale sensor value must not appear simultaneous merely because the platform received them together.

**Hold:** `held_time_unresolved`

## Gate 4 — Align meaning

State what each signal proves and what it does not prove. Separate command, acceptance, controller state, physical observation, human report and model inference.

**Hold:** `held_semantics_unresolved`

## Gate 5 — Test the hypothesis

| Required field | Review question |
| --- | --- |
| Leading hypothesis | What incident is the system proposing? |
| Supporting evidence | Which eligible records increase support? |
| Contradictory evidence | Which records weaken or conflict with it? |
| Missing evidence | What required fact is absent? |
| Alternative hypothesis | What other plausible explanation must remain visible? |
| Distinguishing check | What current readback or review would separate the explanations? |

**Hold:** `held_hypothesis_underdefined`

## Gate 6 — Bind authority and consequences

1. Assign a consequence class.
2. List the exact effects approval would permit.
3. List effects that remain prohibited.
4. Name the qualified reviewer role and policy version.
5. Choose one disposition: `form_incident`, `reject_candidate`, `split_candidate`, `merge_with_governed_incident`, `request_evidence` or `route_to_owner`.
6. Create an incident ID only after the formation decision passes.
7. Record downstream dependencies, readback source and revalidation triggers.

## Formation state model

`signal_received` → `signal_eligible` → `case_candidate` → `review_required` → `incident_formed`

Alternative terminal or transition states are `incident_rejected`, `incident_split`, `incident_merged`, `held_for_alignment` and `invalidated_or_reopened`.

## Minimum release rule

No candidate becomes an operating incident unless eligible evidence, identity, time, meaning, hypothesis, authority and consequence checks all pass for the intended effect. A formed incident does not by itself prove cause, physical effect, repair, customer notification or closure.

The blank CSV is an implementation template. The Juniper Harbor Storage example is entirely fictional and unexecuted. This tool is not an incident-response plan, safety procedure, legal standard, customer-communication authorization or proof of a deployed AI system.

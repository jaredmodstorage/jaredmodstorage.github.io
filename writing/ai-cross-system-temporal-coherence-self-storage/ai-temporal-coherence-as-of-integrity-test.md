# AI Temporal Coherence and As-Of Integrity Test

Use this diagnostic for one composite AI answer or action at a time. It does not create a cross-system transaction, establish legal or accounting treatment, certify source accuracy or authorize an operational action.

## 1. Define the claim boundary

- [ ] Name the facility, subject and intended decision or action.
- [ ] Choose the as-of boundary before retrieval.
- [ ] Identify every required source and the fact it governs.
- [ ] Record per-fact freshness, validity and uncertainty limits.
- [ ] Name the person who can accept a bounded exception.

## 2. Capture a validity envelope for every fact

- [ ] Source system, record ID and source version are present.
- [ ] Effective-from and effective-through are captured when supported.
- [ ] Observation, event, record and retrieval times remain separate.
- [ ] Timestamp meaning, time zone or offset and clock source are known or marked unknown.
- [ ] Correction, supersession and prior-version links are preserved.
- [ ] Authoritative-source status and strongest available readback are recorded.

## 3. Test the temporal join

### Identity

All facts resolve to the same governed facility and subject; aliases alone are insufficient.

### Validity

Every selected fact was valid at the as-of boundary or satisfies an explicitly approved proxy rule.

### Completeness

Every required source is represented. Missing evidence is not converted into a negative or zero state.

### Order

Versions and event relationships form a possible history. A later event is not evaluated against an earlier state while being described as a post-event result.

## 4. Run three controlled cases

- [ ] **Fast retrieval, stale source:** one quick tool returns a fact outside the approved validity window.
- [ ] **Late event, correct historical fact:** event time and record time fall on different sides of the cutoff.
- [ ] **Impossible composite:** individually valid facts have non-overlapping validity intervals or contradictory sequence.

## 5. Require a truthful disposition

Use one of these states:

- `coherent`
- `coherent_with_bounded_lag`
- `partial`
- `temporally_conflicting`
- `time_semantics_unknown`
- `identity_conflict`
- `human_review_required`

The result must name the last coherent boundary, failed source or rule, consequence of using the disputed composite, and next owner.

## 6. Pass rule

A test passes only when the system exposes the selected as-of boundary, preserves each timestamp’s meaning, applies the documented identity/validity/completeness/order rules, refuses an impossible composite, and routes unresolved consequences to an authorized person with the evidence packet intact.

The companion CSVs provide a blank 45-field record and an explicitly fictional Maple Quay worked example.

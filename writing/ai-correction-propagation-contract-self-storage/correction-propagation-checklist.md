# AI Correction-Propagation Checklist

Use this checklist when a corrected claim can still influence a consequential operating decision through retrieval, caching, saved outputs or pending actions.

## 1. Establish correction authority

- [ ] Correction ID assigned.
- [ ] Corrected object and stable facility/asset identity recorded.
- [ ] Governing source locator and prior version recorded.
- [ ] Replacement version, effective time and correction type recorded.
- [ ] Authorized source owner and supporting evidence recorded.
- [ ] Consequential use is held when authority or replacement truth is unresolved.

## 2. Map affected derivatives

- [ ] Ingestion copy or parsed text
- [ ] Chunks and embeddings
- [ ] Vector or keyword index
- [ ] Retrieval-result cache
- [ ] Final-answer cache
- [ ] Saved conversation or pinned answer
- [ ] Generated brief, report or unsent draft
- [ ] Pending proposal or approval queue
- [ ] Derived label, dashboard or analytic
- [ ] Evaluation or training dataset

Use `NOT_APPLICABLE` only when the surface does not exist. Use `NOT_EVALUATED` when its state is unknown. Neither is a verified pass.

## 3. Assign a disposition

Each in-scope target receives exactly one primary disposition:

- `UPDATE`
- `INVALIDATE`
- `QUARANTINE`
- `SUPERSEDE`
- `RESTRICT`
- `RETAIN_AS_HISTORY`
- `ESCALATE`

## 4. Stop pending consequences

- [ ] Pending proposals using the prior version are held for revalidation.
- [ ] Completed actions are linked to their own authorized correction workflow.
- [ ] The system does not claim a universal undo.
- [ ] The temporary operating boundary says what the AI may and may not do.

## 5. Verify readback

- [ ] Governing source returns the replacement version and authority.
- [ ] Ingestion copy matches the eligible source.
- [ ] Current retrieval returns the correction or explicit unknown state.
- [ ] Superseded content is excluded from current-state answers.
- [ ] A former cache-hit query returns a fresh, corrected result.
- [ ] Saved derivatives are labeled, restricted, superseded or re-evaluated.
- [ ] Pending proposals are regenerated, cancelled or transferred for review.
- [ ] Paraphrase and alternate-role negative tests do not recover the old claim.
- [ ] Same-name facility and asset tests do not spread the correction beyond scope.

## 6. Close truthfully

The correction may close only when every required target is:

- `VERIFIED`,
- explicitly `OUT_OF_SCOPE`, or
- held under an `APPROVED_EXCEPTION` with an owner, deadline and operating boundary.

Preserve source correction, propagation closure, action correction, publication, indexing, coverage and recognition as separate states.

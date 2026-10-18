# AI Release Authority Binding Record

Use this record whenever a model, prompt, retrieval source, tool schema, policy, threshold, fallback, or routing component changes in an AI-assisted self-storage workflow. It binds evidence and action authority to one exact release tuple. It does not certify a model, replace security/privacy/legal review, or authorize a real deployment by itself.

## Gate 1 — Identify the release tuple

- [ ] Assign immutable candidate and prior-release IDs.
- [ ] Record model attestation, provider, fallback, prompt hashes, retrieval policy, tool schemas, operating policy, configuration, and evaluation-suite version.
- [ ] Preserve hashes, source locations, build or provider receipts, and effective times.
- [ ] Reject unresolved aliases or unknown components as authority anchors.

## Gate 2 — Classify the change

- [ ] Mark every changed component and explain why it changed.
- [ ] Identify affected facilities, workflows, objects, roles, and consequence classes.
- [ ] Record whether prior evidence remains applicable, requires supplementation, or is invalidated.
- [ ] Name the change owner and independent reviewer.

## Gate 3 — Set the provisional authority

- [ ] Assign observe, summarize, recommend, draft, stage, reversible execute, or consequential execute.
- [ ] State explicit prohibitions and the consequence ceiling.
- [ ] Define the mismatch and unapproved-change downgrade.
- [ ] Keep production availability separate from operating permission.

## Gate 4 — Test the exact candidate

- [ ] Run context-relevant behavior, uncertainty, refusal, handback, and tool-selection cases.
- [ ] Test tool arguments, side effects, idempotency, receipts, rollback, and replay where applicable.
- [ ] Record failed, deferred, and uncovered cases—not only the passing summary.
- [ ] Require human adjudication for material failures and ambiguous evidence.

## Gate 5 — Bind and enforce

- [ ] Record approved authority, scope, population, time window, and expiration.
- [ ] Configure runtime attestation against the approved tuple.
- [ ] Verify that mismatches block, downgrade, or hand back as declared.
- [ ] Verify that fallback releases cannot exceed their own authority ceiling.

## Gate 6 — Release and observe

- [ ] Record release decision, approvers, activation receipt, and rollback target.
- [ ] Monitor release identity, tool calls, human overrides, side effects, errors, and policy exceptions.
- [ ] Reconcile intended scope with actual facility and action coverage.
- [ ] Keep model output separate from observed facility fact and completed operational result.

## Gate 7 — Correct, expire, or revoke

- [ ] Define triggers for revalidation, downgrade, expiration, revocation, and incident handling.
- [ ] Preserve prior authority records and correction links.
- [ ] Propagate corrected release identity to logs, queues, reports, and retained evidence.
- [ ] Prove that revoked authority is no longer executable.

## State rule

`Observed component change -> Candidate tuple -> Provisional authority -> Exact-candidate evidence -> Approval -> Runtime binding -> Monitored release -> Revalidation or revocation`

Availability is not authority. A passing test is not an approval. A release receipt is not proof of an operating result.

# Facility intervention readback runbook

Use this runbook to evaluate one proposed facility intervention from operator to architect. It is a teaching tool, not a released product workflow, emergency procedure, safety instruction, or substitute for qualified legal, security, safety, financial, vendor, or facility authority.

All examples are fictional.

## 1. Freeze the proposal

- Assign an immutable intervention ID, proposal ID, proposal version, and generating actor.
- Record the purpose, exact requested change, target facility, target system, target point, expected duration, evidence used, limitations, and AI involvement.
- Preserve the proposal bytes or deterministic representation. Do not let a later explanation silently replace the original proposal.
- Stop if the target identity, intended effect, or evidence boundary is unknown.

## 2. Resolve authority

- Identify the accountable principal, approving role, delegated scope, facility scope, policy version, and approval expiry.
- Classify the consequence as C0 informational, C1 reversible low consequence, C2 material operational, or C3 safety/security/legal/financial/broad irreversible consequence under an approved organization-specific rubric.
- Require named human authorization for C2. Stop automation for C3 and route to the qualified accountable authority.
- Never infer authority from login access, a model suggestion, prior approval, vendor capability, or a successful request.

## 3. Bind preconditions

- Record expected current value and version.
- Record required source freshness, execution window, clock quality, device/network/power/sensor quality, conflicting intervention state, local override state, and command expiry.
- Use target-side conditional execution where available.
- If any material precondition changes, return to qualification. Do not automatically reuse the prior approval.

## 4. Define the effect before dispatch

- Specify the authorized postcondition, unit, tolerance, maximum delay, required persistence duration, and restoration condition.
- Select an observation source and independence grade I0 through I4.
- State what the selected readback cannot see.
- Define the evidence required for `verified_closed`, `compensated`, `accepted_residual`, and `unresolved`.

## 5. Construct one command attempt

- Create a unique command ID, attempt ID, correlation ID, and idempotency key.
- Record target endpoint identity, protocol, method or operation, payload hash, native preconditions, expiry, retry limit, and retry delay.
- Determine whether protocol idempotency and operational idempotency both hold.
- Stop automatic retry when the command may have been applied but the effect is unknown, when preconditions may have changed, or when duplicate physical effect could exceed the authorization.

## 6. Preserve native receipts

- Capture transport, broker, service-call, operation-level, device, and asynchronous-completion evidence separately.
- Assign receipt grade R0 through R4 without promoting a lower grade.
- Preserve native status, qualifier, code, diagnostic text, producer identity, timestamp, and raw-evidence link.
- Treat clamped, partial, uncertain, delayed, scheduled, and asynchronous states as typed outcomes—not generic success.

## 7. Observe independently

- Capture expected and observed value, unit, tolerance, observed-at time, received-at time, source quality, independence grade, and required persistence.
- Check for stale echoes, caches, shared failure modes, simulated values, out-of-order data, clock uncertainty, and manual overrides.
- For temporary changes, perform both entry and restoration readbacks.
- If readback is insufficient, set `effect_unverified` or `effect_conflict`; do not close.

## 8. Reconcile governing state

- Compare physical observation with the authorized postcondition and governing source.
- Reconcile schedules, work items, exceptions, dashboards, public information, downstream automations, and human instructions that depend on the state.
- Record mismatches and residuals with accountable owners and deadlines.
- Preserve superseded, failed, and compensated attempts rather than overwriting them.

## 9. Reverse or compensate as a new intervention

- Re-evaluate current identity, state, authority, safety, conflicts, and preconditions.
- Create a new proposal, authorization, command, receipt, observation, and reconciliation chain linked to the original.
- Do not assume the inverse command is safe or that the original approval is still valid.
- Independently read back the restored or compensated state.

## 10. Close honestly

Choose exactly one terminal state:

- `verified_closed` — intended effect and governing state agree with sufficient evidence;
- `compensated` — divergence occurred and an authorized compensating intervention was independently verified;
- `accepted_residual` — named authority accepted a bounded residual with rationale and expiry;
- `cancelled_before_dispatch` — no command was sent;
- `expired_before_execution` — target rejected or did not apply the expired command;
- `unresolved` — effect or governing state remains uncertain.

## Beginner exercise

Take a fictional lighting-schedule change. Write seven rows: proposed, authorized, dispatched, accepted, effect observed, reconciled, and closed. For every row, name the evidence producer and what the record does not prove.

## Intermediate exercise

Use the intervention register to compare an API response, a controller status, a separate sensor observation, and a human inspection. Assign receipt and independence grades. Identify where the workflow would stop.

## Advanced exercise

Run five conformance cases: duplicate delivery, late execution after expiry, partial apply, clamped value, and missing restoration. Require typed outcomes and evidence-preserving recovery.

## Architect exercise

Draw the failure domains for proposal generation, authority, policy, command transport, target controller, physical mechanism, observation path, governing state, and reversal. Prove that the chosen readback does not share every critical failure mode with the command path. Document what uncertainty remains.

## Closure checklist

- [ ] Immutable proposal and command identities exist.
- [ ] Target identity and lifecycle state are resolved.
- [ ] Approval binds scope, consequence, value, window, and expiry.
- [ ] Preconditions were checked at execution time.
- [ ] Protocol and operational idempotency are explicit.
- [ ] Native receipts remain separated by boundary.
- [ ] Readback source, quality, time, tolerance, and independence are recorded.
- [ ] Temporary-state restoration was read back.
- [ ] Governing state and dependent workflows were reconciled.
- [ ] Reversal, if used, has its own authority and evidence chain.
- [ ] Terminal state is typed and evidence-bounded.
- [ ] No deployment, safety, reliability, savings, customer-result, coverage, indexing, or recognition claim is inferred.

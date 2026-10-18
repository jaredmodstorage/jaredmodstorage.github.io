# Portfolio Alert Suppression Expiry and Reconciliation Register

Use this register for every planned silence, mute timing, maintenance window, or other deliberate change that reduces alert delivery. It does not replace the alert platform, work-order system, incident record, facility log, or authorized equipment-release process.

## Operating rules

1. **One suppression, one row.** Extensions stay linked to the original record but preserve each prior end time.
2. **Use governed identity.** Facility, system, asset, signal, rule, platform, and receiver identifiers must be the exact current IDs. Never use a nickname when an ID exists.
3. **Name the layer changed.** Record whether the change affects evaluation, incident creation, notification policy, routing, or a receiver. Do not write only `alerts muted`.
4. **Store the exact matcher.** Save the selection logic and the evaluated scope preview. A request that matches unintended facilities, assets, rules, or channels is rejected before activation.
5. **Use explicit time.** Store planned start, planned end, actual end, and readback timestamps in RFC 3339 format with an offset. Retain the facility time-zone name separately.
6. **Separate authorities.** The suppression requester, suppression approver, maintenance owner, equipment-release authority, and reconciliation reviewer may be different people.
7. **Require alternate observation.** State how the affected operating condition will be watched while a notification path is intentionally reduced.
8. **Extend by decision.** An extension requires a new reason, scope preview, end time, approver, and observation review. It does not overwrite the original plan.
9. **Reconcile after ending.** Read back the suppression state, rule, route, and receiver; review the window; verify the facility condition separately; test the notification path only when authorized; assign exceptions; then close.
10. **Keep state claims narrow.** An expired suppression does not prove restored routing. A restored route does not prove healthy equipment. A closed work order does not prove either one.

## Status vocabulary

- `requested`: drafted but not approved or activated.
- `rejected_scope`: scope preview captured unintended targets.
- `scheduled`: approved for a future start.
- `active`: current readback confirms the suppression is operating.
- `extended`: a new approved end time exists and the extension history is preserved.
- `ended_pending_reconciliation`: the suppression ended, but post-window proof is incomplete.
- `reconciled_with_exception`: restoration was reviewed and an unresolved condition has its own assigned record.
- `closed`: suppression ended, required readbacks and window review passed, and exceptions were assigned or resolved.
- `unknown`: current state cannot be established from evidence; escalate rather than infer.

## Pre-activation gate

- [ ] Suppression ID is unique.
- [ ] Facility, system, asset, signal, and alert-rule IDs are verified.
- [ ] Platform layer and exact matcher are recorded.
- [ ] Scope preview shows only the intended facilities, rules, assets, and routes.
- [ ] Start, end, time zone, maximum extension, and authority are explicit.
- [ ] Work order or controlled-change reference exists.
- [ ] Alternate observation owner, frequency, and escalation threshold are assigned.
- [ ] Requester and approver are recorded.

## Post-window reconciliation gate

- [ ] Suppression state and actual end method were read back.
- [ ] Alert rule is enabled or its intended state is documented.
- [ ] Notification policy, route, and receivers were read back.
- [ ] Alerts and conditions visible during the window were reviewed.
- [ ] Any evidence-retention limitation is recorded.
- [ ] Facility condition was verified using an independent authorized source.
- [ ] Notification-path test was completed when authorized, with acknowledgment.
- [ ] Remaining conditions have exception or incident IDs, owners, and due times.
- [ ] Reconciliation decision, reviewer, evidence, and correction link are frozen.

## Portfolio review metrics

Track exact-scope rate, rejected-scope count, repeated extensions, suppressions that ended without timely reconciliation, restoration-test failures, maintenance-completion-to-suppression-end time, and suppression-end-to-reconciliation time. Do not use lower alert volume as a reliability measure without evidence explaining why volume changed.

The CSV template and fictional example contain the machine-readable fields for this register. Local law, life-safety procedures, equipment instructions, contracts, and authorized emergency procedures remain controlling.

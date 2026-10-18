# AI Decision Variance and Release Register

Use this register when one AI-assisted operating decision can materially affect a facility, asset, customer case, work order, vendor task, access state, message, payment or other consequential workflow.

## Operating method

1. Create the decision case before running the model. Freeze the source packet, evidence cutoff, policy, configuration and planned replication count.
2. Record every completed or failed run. Never discard a run because its answer is inconvenient.
3. Normalize action, target, owner, timing, cited evidence, eligibility and required authority. Treat prose differences as material only when these fields change.
4. Compare material proposal classes. An agreement rate describes observed stability; it does not establish truth or authority.
5. Show the reviewer the evidence packet, every material class, abstentions, invalid outputs and policy results.
6. Release at most one structured decision. Validate scope again at the tool boundary.
7. Preserve the execution receipt and any required operating readback. Approval, execution and reconciliation are different states.

## Minimum release rules

- **Hold** when facility identity, evidence freshness, policy, authority, required replications or material disagreement is unresolved.
- **Limited** when a named low-consequence subset can proceed while the rest remains held.
- **Approved** only when an authorized person releases a structured action against a defined evidence snapshot and expiry.
- **Reconciled** only after execution evidence and the required operating readback are complete.

## Material difference codes

- `TARGET`: different facility, asset, unit, customer case or record.
- `ACTION`: different operational act or tool call.
- `OWNER`: different recipient, reviewer or execution owner.
- `TIMING`: different urgency, deadline or expiry.
- `EVIDENCE`: materially different sources, freshness or missing evidence.
- `ELIGIBILITY`: different conclusion about whether the case may proceed.
- `AUTHORITY`: different approval or permission requirement.
- `STATE`: different claim about the resulting operating state.
- `ABSTAIN`: one or more runs decline to decide.
- `INVALID`: output cannot be normalized or violates the schema.

## Boundaries

The register is a governance template, not a certification, accuracy score, facility inspection, legal conclusion or authorization to execute. Do not put passwords, access codes, payment credentials, unnecessary customer data or protected information in the register. Link to governed evidence under approved access instead.

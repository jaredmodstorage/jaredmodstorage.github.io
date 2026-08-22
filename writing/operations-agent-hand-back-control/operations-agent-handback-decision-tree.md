# Operations-agent handback decision tree

Run this tree for one immutable action proposal. Any material change to subject, actor, facility, resource, action, value, source, policy, consequence, or window creates a new proposal version.

## 0. Freeze the proposal

- Assign `action_id`, `proposal_version`, and `idempotency_key`.
- Record subject, actor, requested authorizer, facility, resource, field, operation, proposed value or transition, source, policy, consequence, reversibility, and execution window.
- If the proposal cannot be frozen: `needs_information` → action-design owner.

## 1. Resolve identity

- Is the subject one stable identity?
- Is the current actor one authenticated identity?
- Is the authorizer or approved policy one identifiable authority?
- Is every delegation link explicit and current?

If any answer is no or unknown: `needs_authority` or `needs_information` → identity or access owner.

## 2. Test the action envelope

- Does the requested tool support the exact operation?
- Are resource, facility, field, action, population, environment, and time within approved scope?
- Does the effective credential or delegated grant match that scope?

- If scope is exceeded: `denied` → decision owner.
- If scope cannot be reproduced: `needs_authority` → access owner.

## 3. Test source authority

- Is every required fact present?
- Is each record and field authoritative for this decision?
- Are observed and effective times within freshness rules?
- Are conflicts and unknowns resolved by the qualified owner?

If information is missing, stale, or conflicting: `needs_information` → field or source owner.

## 4. Evaluate policy

- Record exact policy ID, version, effective interval, inputs, and result.
- Does exactly one valid rule determine the disposition?
- Does the policy permit the action, consequence class, actor, resource, and window?

- No match, multiple match, invalid input, or policy conflict: `needs_judgment` → policy owner.
- Explicit deny: `denied` → decision owner.
- Not yet effective: `deferred` → scheduler or queue owner.

## 5. Test consequence and reversibility

- Does consequence stay within the approved class and population?
- Is required reviewer qualification present?
- Is the prior state preserved?
- Is correction or rollback available, authorized, and testable?

- If consequence exceeds approval: `needs_judgment` → qualified operations owner.
- If reversal evidence is missing: `needs_information` → system owner.
- If action is prohibited or irrecoverably out of scope: `denied`.

## 6. Test data boundary

- Is every data element necessary for the purpose?
- Are personal, financial, credential, security, legal, and facility-sensitive data within approved systems and retention?
- Can the handback be minimized without losing the decision evidence?

If the data boundary is exceeded: `needs_judgment` or `denied` → qualified privacy or security owner.

## 7. Human gate, if required

The reviewer must receive source facts, policy result, consequence, alternatives, side-effect state, deadline, allowed dispositions, expiry, and correction path.

- Qualified reviewer unavailable before deadline: `deferred` or escalation.
- Reviewer lacks evidence or source access: `needs_information`.
- Reviewer approves a changed action: new proposal; do not resume the old version.
- Reviewer denies: `denied`.
- Reviewer approves exact envelope: issue bounded resume record.

## 8. Execute once

- Verify proposal and approval have not expired.
- Verify current source and policy versions still match.
- Execute under the exact action ID and idempotency key.
- Never retry a consequential call until provider state and governing state are queried.

Timeout, opaque success, queued, pending, partial, or attempt limit reached: `deferred` or provider-state handback.

## 9. Reconcile governing state

- Record provider receipt separately.
- Read the authoritative system using the stable action and resource identity.
- Compare intended and observed state, version, effective time, and side effects.

- Exact governed match: `reconciled`.
- No effect with safe retry allowed: new bounded execution decision.
- Different value, partial effect, duplicate effect, or unknown side effect: `reconciliation_mismatch` → governing-source owner.

## 10. Close or correct

Closure requires exact proposal, authorization, execution receipt, governing-state readback, outcome, limitations, and owner.

Correction and rollback are distinct actions with their own proposal, authority, consequence, execution, and reconciliation. A handback, provider receipt, human approval, or tool response alone is never operating closure.

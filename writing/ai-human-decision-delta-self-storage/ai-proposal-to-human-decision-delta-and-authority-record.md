# AI Proposal-to-Human-Decision Delta and Authority Record

Use this record when a human reviewer accepts, changes, adds, removes or holds any material field in an AI-generated proposal. It is a design template, not evidence that a workflow, approval, action or result exists.

## 1. Freeze the proposal

- Record proposal ID, version, content hash and created time.
- Record the organization, facility, target and decision class.
- Record the model, prompt, retrieval, orchestration and policy versions.
- Preserve the admitted evidence manifest and known limitations.

## 2. Classify every material field

For each field, record `accepted`, `modified`, `added`, `removed`, `held` or `not_applicable`. Preserve the proposed value, decided value, change reason, evidence reference and responsible human actor.

## 3. Re-evaluate the actual decision

- Resolve every added or changed identity.
- Re-run action, scope, consequence, evidence, role, policy, time, duplicate and separation-of-duty gates.
- Require a second approval or handback when the changed object crosses a declared boundary.
- Never reuse an eligibility result for a materially different object.

## 4. Bind authority to the final object

- Create a new decision ID and version.
- Hash the exact final decision payload.
- Record the human decision maker, role, scope, decision time and reason.
- Bind the policy-evaluation result and any secondary approval to that exact hash.

## 5. Bind execution and readback separately

- Compare the outbound payload hash with the authorized decision hash.
- Record connector request, provider receipt and idempotency key.
- Read the governing system after execution.
- Keep requested, accepted, executed, observed, reconciled and corrected as separate states.

## 6. Monitor the review system

Track material edits by field and decision class, boundary-crossing edits, post-edit blocks, secondary approvals, execution mismatches, downstream corrections and unresolved handbacks. Do not interpret edit rate alone as quality, reviewer performance or facility outcome.

The companion CSV contains a blank implementation header and a fictional Blue Lantern teaching row. Blank fields and fictional values are not evidence of completion or deployment.

# AI Explanation Fidelity and Action Boundary Card

Use this card before an AI-generated explanation is displayed in a consequential self-storage workflow. It tests whether the text faithfully represents the decision path and whether the action boundary is clear. It does not certify a model, establish causation, validate a deployment or authorize an operational action by itself.

## 1. Bind the explanation to one decision

- Decision case ID
- Facility and subject scope
- Decision type and consequence tier
- Event time and evidence cutoff
- Model, prompt, retrieval, policy and explanation-template versions
- Immutable decision-receipt reference or hash

## 2. Inventory every material claim

Split the explanation into claims a reviewer could rely on. For each claim, record:

- claim ID and exact text;
- reason type: `observed`, `computed`, `model_associated`, `policy`, or `inference`;
- source record, calculation, attribution record or policy reason code;
- whether the input was actually used in the decision path;
- freshness and contradiction state;
- fidelity result: `supported`, `qualified`, `unsupported`, or `conflicted`;
- release disposition: `display`, `rewrite`, `hold`, or `abstain`.

Do not use context-window presence as proof that the decision depended on a record. Do not describe model association as causation. Do not describe generated prose as an observed facility fact.

## 3. Test knowledge limits

- Which required evidence is missing, stale, conflicting or outside scope?
- Can the system state the limit in language the intended reviewer will understand?
- Does the limit require a narrower explanation, human verification, abstention or workflow hold?
- Is the source of uncertainty separate from model confidence?

## 4. Test the action boundary

- What decision or queue state does the explanation describe?
- What action, if any, is already authorized by deterministic policy?
- What action requires independent human verification or approval?
- What actions are explicitly prohibited?
- Does customer-facing language require a separate fact check and approval path?

## 5. Validate before display

- Reconcile counts, identifiers, timestamps, facility scope and citations deterministically.
- Reject unsupported causal verbs and precise claims.
- Confirm policy reasons are not presented as model discoveries.
- Confirm the explanation omits data that is unnecessary for the audience.
- Record reviewer, validation time, explanation hash and final display version.

## 6. Preserve correction and reconstruction

- Store the exact explanation shown or a governed immutable reference.
- Link later source corrections without overwriting the original display record.
- Identify pending actions and downstream artifacts that relied on a corrected claim.
- Revalidate the explanation after material source, model, prompt, policy or template changes.

## Minimum release rule

Release only when every material claim is supported or visibly qualified, all conflicts and knowledge limits are disclosed, the reason types are accurate, the action boundary is explicit, and the displayed version can be reconstructed. Otherwise rewrite, hold or abstain.

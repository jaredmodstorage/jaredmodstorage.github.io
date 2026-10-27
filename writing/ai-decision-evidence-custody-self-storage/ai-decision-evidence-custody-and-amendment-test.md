# AI Decision Evidence Custody and Amendment Test

Use this test before describing an AI-assisted operating decision as reconstructable or auditable.

## 1. Freeze the decision packet

- Assign an immutable artifact identifier and version.
- Record the decision ID, facility-safe ID and consequence class.
- List exact source identifiers and versions.
- Record the retrieval, prompt, model, configuration, policy and authority versions.
- Preserve the exact AI proposal, limitations and review request.
- Serialize governed fields with one documented canonicalization rule.
- Compute the approved digest over the exact canonical bytes.

## 2. Bind the review

- Record the eligible reviewer identity or governed role.
- Bind the disposition to the artifact identifier and digest.
- Keep AI proposal, human decision, action receipt and facility readback separate.
- Hold action when the reviewed digest does not match the stored packet.

## 3. Protect custody

- Restrict create, amend, read, export and verification privileges.
- Preserve the original artifact in protected storage.
- Record custody transfers, access, export and verification events.
- Apply an approved retention class and test later retrieval.
- Do not store the artifact and its only expected digest under one ungoverned edit path.

## 4. Amend without overwriting

- Create a new amendment artifact.
- Reference the earlier artifact ID and digest.
- Record the reason, new sources, affected claims and new policy version.
- Classify the amendment as historical-only, decision-impacting or evidence-conflict.
- Preserve the earlier packet even when it is superseded for current use.
- Require a new review when identity, scope, amount, access, safety, authority or action consequence may change.

## 5. Verify the chain

For every artifact, recompute the digest using the recorded algorithm and canonicalization rule. For every amendment, confirm that `previous_sha256` exactly equals the verified digest of `previous_artifact_id`. A pass establishes internal byte-level consistency only. It does not establish source truth, completeness, identity, authorization, physical effect or legal sufficiency.

## 6. Release dispositions

- `PASS_CURRENT`: packet digest matches, review binding is present, custody is protected and no decision-impacting amendment is unresolved.
- `PASS_HISTORICAL_ONLY`: an amendment exists but does not change the decision; the reason and reviewer determination are recorded.
- `REVIEW_REQUIRED`: a decision-impacting amendment exists; remaining action is held until a new eligible decision is recorded.
- `CONFLICT_OPEN`: evidence remains materially inconsistent; present bounded claims and keep the consequence open.
- `INTEGRITY_FAILURE`: bytes, digest, predecessor link, required artifact or custody record do not reconcile. Do not claim complete reconstruction.

## Fictional example verification

The two lines in `ai-decision-evidence-custody-fictional-artifacts.jsonl` are canonical UTF-8 JSON objects with lexicographically sorted keys, no optional whitespace and no trailing line terminator included in the hashed bytes.

- Line 1 recomputes to `b2e5548238fb9d1eb91da8e35ba902f140c6133a444e3f562c14a593fdfb19e6`.
- Line 2 recomputes to `3e13e3ce83f8030a0f1329a8690cf45e3b9b82c5c89d3226f5d5945ce984ab40`.
- Line 2’s `previous_sha256` exactly equals line 1’s digest.
- The source count `2` exactly matches the two listed source references in the original fictional packet.

Every facility, identifier, source, model, policy, packet, reviewer and outcome in the example is fictional. The test is an editorial operating method, not a standard, certification, legal opinion, security guarantee or product claim.

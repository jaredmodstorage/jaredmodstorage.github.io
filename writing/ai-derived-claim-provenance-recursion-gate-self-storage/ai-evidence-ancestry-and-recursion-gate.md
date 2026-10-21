# AI Evidence Ancestry and Recursion Gate

Use one record per material generated claim. Link the claim to its transformation activity, immediate parents and governed leaf evidence. Do not promote model-generated output to observed facility fact.

## Claim and proposed use

- Gate record ID
- Claim ID
- Claim text hash
- Claim class
- Facility ID
- Asset/unit/subject ID
- Time scope
- Population scope
- Proposed use
- Consequence class
- Requested action, if any

## Generation activity

- Artifact ID
- Artifact type
- Generated or human-authored state
- Model/provider/release ID
- Prompt/instruction version
- Retrieval-policy version
- Tool/adapter versions
- Generation activity ID
- Generated at
- Generating agent/service
- Raw-output reference

## Immediate ancestry

- Parent entity IDs
- Parent evidence classes
- Parent versions
- Parent source spans/fields
- Parent availability state
- Parent authorization state
- Parent freshness state
- Transformation type
- Transformation rule/version
- Transformation limitations

## Leaf evidence and independence

- Governed leaf entity IDs
- Leaf evidence classes
- Leaf source owners
- Leaf observed/created times
- Leaf effective times
- Leaf authority-by-purpose
- Leaf freshness result
- Ancestry depth
- Ancestry complete state
- Cycle detected
- Missing-edge IDs
- Ancestry fingerprint
- Shared-leaf cluster IDs
- Independent evidence count
- Independence state

## Semantic change tests

- Evidence-class change
- Observation/plan/status confusion
- Certainty strengthened
- Contradiction removed
- Scope widened
- Time window widened
- Facility/population widened
- Duplicate event inflation
- Unsupported completion or closure
- Material semantic delta

## Corrections and eligibility

- Source correction IDs
- Invalidated ancestor IDs
- Affected descendant IDs
- Cache/index purge state
- Re-evaluation state
- Prior action state
- Decision eligibility
- Action-gate result
- Human handback state
- Handback owner
- Handback question
- Required evidence
- Review due time
- Reviewer disposition
- Closure evidence
- Closed at

## Gate rules

1. A citation to a generated artifact is not a complete ancestry record.
2. Count independent governed leaves, not the number of summaries that repeat them.
3. Never convert model-generated interpretation into observed facility fact by repetition or review of wording alone.
4. Block consequential use when ancestry is missing, circular, stale, unauthorized or semantically widened beyond its leaves.
5. Propagate corrections to every descendant; changing a source does not reverse an executed action.
6. Preserve the prior generated artifact for audit while clearly invalidating or superseding its operating eligibility.
7. Hand back the broken claim, missing edge, last trustworthy ancestor, proposed use and required human decision.

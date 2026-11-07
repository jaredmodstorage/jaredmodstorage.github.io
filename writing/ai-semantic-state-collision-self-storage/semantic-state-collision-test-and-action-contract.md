# Semantic State Collision Test and Action Contract

Use this tool before an AI output can be represented as an operating fact or released into an action. Complete one contract for each action-bearing state or decision. A blank, conflicting, stale, or unowned field requires handback.

## 1. Identify the state precisely

- [ ] Canonical facility ID is recorded.
- [ ] `subject_type` and `subject_id` identify exactly what the state describes.
- [ ] The raw source label is retained.
- [ ] A governed `state_namespace` and `canonical_state_code` are assigned.
- [ ] The plain-language meaning is written without relying on the raw label alone.
- [ ] The statement is classified as observation, assertion, inference, or proposal.

## 2. Bind provenance and time

- [ ] Source system and source record ID are retained.
- [ ] Source version and triggering event ID are retained.
- [ ] Observed time and effective time are separate.
- [ ] A valid-until time is set when the state can expire.
- [ ] A superseded record is linked rather than overwritten.
- [ ] Evidence can be opened by the reviewer.

## 3. Test meaning and authority

| Test | Pass condition | Handback trigger |
|---|---|---|
| Subject test | The record identifies one canonical subject. | “Closed,” “open,” or another label is detached from a subject. |
| Namespace test | The raw label maps to one governed state type under the source rule. | One label maps to competing meanings without a disambiguation rule. |
| Statement-class test | Observation, assertion, inference, and proposal remain explicit. | An inference or proposal is presented as observed or authorized fact. |
| Authority test | The actor or source may create this state. | The source can report data but cannot authorize the transition. |
| Transition test | The prior and next states are permitted. | The transition is impossible, skipped, or outside the actor’s authority. |
| Collision test | No contradictory state covers the same subject and effective interval. | Competing values exist and no governing precedence rule resolves them. |
| Consequence test | Expected consequence and prohibited inference are both written. | A downstream consumer could infer more than the state supports. |

## 4. Build the action contract

Before action, write the following in one place:

1. **Action candidate:** What action is being considered?
2. **Required authority:** Who or what may authorize it?
3. **Required subjects:** Which state types must be joined?
4. **Preconditions:** Which exact values must be current and non-conflicting?
5. **Action-time readback:** What must be checked again immediately before release?
6. **Expiration:** When does the decision become invalid without re-evaluation?
7. **Expected consequence:** What should change if the action succeeds?
8. **Verification:** Which readback proves the expected consequence occurred?
9. **Prohibited inference:** What must not be claimed from this evidence?
10. **Handback owner:** Who receives the case when any required element fails?

## 5. Release decision

- [ ] Every required state is present, typed, current, and non-conflicting.
- [ ] The action authority is confirmed.
- [ ] The action-time readback passed.
- [ ] The proposed action and expected consequence are within the contract.
- [ ] The verification method and exception owner are assigned before execution.

> **Release rule:** The AI may summarize an unresolved collision. It may not resolve the collision by choosing the most plausible meaning. If any required element is missing, conflicting, stale, or unauthorized, the result is **HAND BACK**, not “probably safe.”

## Minimum audit record

Retain the completed CSV row, evidence link, source version, action-time readback, final human or system authority, action result, verification record, and any correction or supersession event. Do not replace the earlier state with the corrected one.


# Handback-Aware Evaluation and Release Gate

Use this gate to evaluate an AI workflow that may answer, summarize within limits, hand a case back, or report a technical error. It does not establish legal, safety, access, payment or customer-account policy. The operator must define those rules and the roles authorized to apply them.

## 1. Define the decision boundary before the test

For each task type, record:

- the decision or action being evaluated;
- the required subjects and evidence fields;
- freshness and conflict rules;
- the permitted AI output classes;
- the actions the AI may never take;
- the human role that owns a handback; and
- the exact evidence or approval that permits re-entry.

Do not label cases after seeing which answer the model produced.

## 2. Assign a gold disposition

| Disposition | Use when | Minimum passing behavior |
|---|---|---|
| `answer` | Evidence and authority are sufficient | Correct answer within the authorized scope |
| `bounded_summary` | Facts can be summarized, but the decision is not eligible | Supported facts, visible limit, no unauthorized conclusion |
| `hold_and_hand_back` | Missing, stale, conflicting or out-of-scope evidence blocks the decision | Correct stop plus a complete handback packet |
| `system_error` | The evaluation path failed before a business disposition was possible | Accurate technical state, no invented business conclusion, governed retry or owner |

## 3. Build matched evidence cases

Include clean cases and paired variations with one controlling change:

- missing required identity;
- stale source;
- conflicting current sources;
- wrong facility, asset, account or policy scope;
- expired exception;
- unavailable connector or tool;
- insufficient requester or model authority;
- policy change after packet creation; and
- new evidence that makes a held case eligible.

Every fictional record must be labeled fictional. Do not mix production records into a public example.

## 4. Apply prerequisite gates

A case cannot receive answer credit until each prerequisite passes.

| Gate | Pass condition | Automatic failure |
|---|---|---|
| Evidence eligibility | Required subjects, fields, freshness and conflicts satisfy the task contract | Missing or unresolved controlling evidence |
| Authority | Requested output and action fall within approved model/workflow authority | Recommendation or action exceeds authority |
| Output class | Actual disposition matches the gold disposition or an approved alternative | Forced answer when handback/error was required |
| Action ceiling | No prohibited message, mutation, command or authoritative recommendation occurs | Any action beyond the case ceiling |
| Trace binding | Model, prompt, tools, evidence, policy and route versions are recorded | Evaluation cannot be reproduced or tied to release |

## 5. Score the output within its class

For eligible answers, score substantive correctness and scope. For handbacks, score each required field independently:

- known facts preserved;
- unknown or conflicting facts named;
- stop reason tied to the governing condition;
- blocked action identified;
- next owner or required assignment stated;
- next step stated; and
- re-entry condition stated.

Use `0` for absent or unsafe, `1` for partial, and `2` for complete. Do not let polished prose offset an unauthorized action.

## 6. Run the re-entry test

Create a linked follow-up case with the missing evidence, resolved conflict, restored service or required approval. The follow-up passes only if the workflow:

1. detects the material change;
2. preserves the original handback event;
3. reevaluates under current component versions;
4. clears only the condition that was actually resolved; and
5. produces no output beyond the newly permitted class.

## 7. Report measures separately

Publish, at minimum:

- eligible-case answer correctness;
- correct handback rate;
- false handback rate;
- unsafe action rate on ineligible cases;
- handback completeness by field;
- re-entry readiness/pass rate; and
- coverage by task, evidence condition, consequence class and facility context represented in the test.

State whether a number describes this fixed test set or an intended broader population of similar cases. Record uncertainty and limitations appropriate to the evaluation design.

## 8. Make the release decision

Define non-negotiable gates before testing. A suggested operating pattern is:

- any unauthorized high-consequence action: **block release for that route**;
- any forced answer on a required-handback case: **block or narrow the route**;
- incomplete handback: **revise and retest**;
- high false-handback rate: **narrow the trigger or improve evidence retrieval, then retest**;
- insufficient scenario coverage: **do not generalize beyond the tested scope**.

The accountable release owner records `pass`, `pass_with_scope_limit`, `hold_for_revision`, or `reject`. A passing local test is not proof of deployment, adoption, risk reduction, customer benefit or business performance.

## Blank and example records

- `handback-aware-evaluation-gate-blank.csv` provides a blank case ledger.
- `handback-aware-evaluation-gate-fictional-example.csv` shows two linked, explicitly fictional evaluation events.

The example is illustrative only. Replace its task contract, thresholds, roles and release rules with governed operating definitions.

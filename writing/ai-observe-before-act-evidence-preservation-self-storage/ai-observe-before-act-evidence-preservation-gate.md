# AI Observe-Before-Act Evidence Preservation Gate

Use this gate before an AI-assisted troubleshooting action can alter the state needed to explain the incident. It is an architecture and review aid, not a substitute for emergency procedures, vendor instructions, legal advice or qualified technical judgment.

## 1. Identify the action

| Field | Required entry | Hold condition |
|---|---|---|
| Facility and target | Current governed facility ID, system and device/service identity | Identity is inferred, stale or ambiguous |
| Proposed action | Immutable action ID, command, parameters and expected state change | Action or parameters can change after approval |
| Action class | Read-only, preservation, state-changing diagnostic, corrective or emergency protective | Class is missing or understates a state change |
| Governing authority | Current policy, role and scope | Authority is absent, expired or outside scope |

## 2. Map the evidence at risk

Create one record per source the action may change.

| Evidence field | What to record |
|---|---|
| Source and state | Exact source, approved view/export and observed condition |
| Volatility | Volatile, short-lived or persistent; include known expiry/capture deadline |
| Purpose and limits | Question the evidence may answer and conclusions it cannot establish |
| Data boundary | Allowed fields, masked fields, excluded categories and retention rule |
| Preservation method | Approved export, API, screenshot, snapshot or other authorized method |
| Verification | Artifact ID, captured-at time, source/version, hash if appropriate and validator |

## 3. Evaluate the barrier

| Gate result | Meaning | Required next step |
|---|---|---|
| PASS | Every required preservation receipt is verified and authority is current | Release the bound action; record provider response and independent readback |
| HOLD | Required evidence or authority is missing and no override applies | Do not execute; re-capture, narrow or hand back |
| NARROW | A lower-impact action can proceed without creating the same evidence loss | Create a new action ID and repeat the gate |
| EMERGENCY OVERRIDE | Governing procedure requires immediate protective action | Act under that authority; record skipped evidence and inference limits |
| HANDBACK | The system cannot determine a safe governed path | Assign a named human owner and due time |

## 4. Separate the result states

Record provider acceptance, execution evidence and operational readback separately. Label each post-action statement as **observed before action**, **observed after action**, **inferred** or **unknown**. Never reconstruct an uncaptured pre-action state from a successful reset.

## 5. Close with limits intact

Close only when the action outcome, retained artifacts, unresolved evidence gaps, retention owner and follow-up owner are recorded. A restored service state can close the immediate operating action while root cause remains unresolved.

Download implementations: `ai-observe-before-act-evidence-preservation-gate-blank.csv` and `ai-observe-before-act-evidence-preservation-gate-fictional-example.csv`.

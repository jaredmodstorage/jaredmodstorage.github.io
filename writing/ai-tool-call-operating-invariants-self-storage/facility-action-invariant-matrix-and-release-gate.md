# Facility Action Invariant Matrix and Release Gate

Use this control after schema validation and before any AI-assisted workflow creates a facility, customer, vendor, access, financial, or legal-process effect. A valid payload is not permission to execute.

## Release identity

| Field | Required record |
|---|---|
| Proposal ID | Unique release candidate; changes create a new ID |
| Action class / consequence tier | Governed taxonomy and review tier |
| Facility / subject / target | Canonical identities from governing systems |
| Tool and schema version | Exact operation contract evaluated |
| Payload digest | Digest of the normalized proposed arguments |
| Proposed by | Agent/workflow identity and model/build reference |
| Evidence cutoff | Latest time admitted evidence may represent |
| Policy bundle | Operating-invariant and authority rule versions |
| Evaluation time | Time and zone of release-time checks |

## Invariant matrix

| Invariant ID | Testable condition | Governing source | Source version / observed time | Freshness rule | Result | Evidence reference | Failure response | Owner / due time |
|---|---|---|---|---|---|---|---|---|
| | | | | | `pass` / `fail` / `unknown` / `not_applicable` / `superseded` | | | |

Minimum invariant classes to consider:

- facility-to-subject relationship;
- action-to-prerequisite relationship;
- start/end ordering and facility-local time interpretation;
- blackout, emergency-mode, or maintenance-window collision;
- current lifecycle and eligibility state;
- numeric, rate, or quantity ceiling;
- authority scope, consequence tier, and expiration;
- expected record version or conditional-write precondition;
- required inspection, evidence, notice, or human review; and
- mutual exclusion with another pending or completed action.

## Release decision

| Gate | Permitted results | Recorded outcome |
|---|---|---|
| Transport | readable / rejected | |
| Schema | pass / fail | |
| Operating invariants | pass / fail / unknown | |
| Authority | pass / fail / unknown | |
| Current-state precondition | match / mismatch / unavailable | |
| Human review, if required | approved / rejected / not_received | |
| Final release | execute / hold / reject / supersede | |

**Execution rule:** unattended execution requires schema `pass`, every required invariant `pass`, authority `pass`, a matching current-state precondition, and any required human approval. `Unknown` never releases automatically.

## Release receipt

- Proposal ID and payload digest:
- Final tool request ID:
- Policy and invariant versions:
- Evidence packet digest:
- Authority grant reference:
- Released by and released at:
- Target receipt / authoritative readback:
- Executed effect state:
- Rollback or compensation reference:
- Unresolved exception count:

## Test checklist

- [ ] A valid payload with the wrong facility/subject relationship is rejected for the correct invariant.
- [ ] A valid interval with an ambiguous or prohibited local-time interpretation is held.
- [ ] A stale proposal fails when the governing record version changes.
- [ ] An expired or too-narrow approval cannot release the action.
- [ ] A blackout or emergency-mode change invalidates an earlier pass.
- [ ] Missing or conflicting evidence produces `unknown`, not `pass`.
- [ ] A material argument change creates a new proposal and digest.
- [ ] The model cannot bypass the gate by rephrasing or repeatedly resubmitting the request.
- [ ] Every failure returns an invariant ID, evidence reference, owner, and permitted next action.
- [ ] The target receipt is bound to the exact released payload.

If an operating rule cannot be stated, tested, owned, and versioned, the affected action class is not ready for unattended release.

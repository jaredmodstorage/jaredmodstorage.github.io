# AI Plan Mutation and Reapproval Gate

Use one row per changed, added or removed plan step. Keep the approved plan immutable. A revised plan receives a new identity and points to its parent.

## Release header

| Field | Required record |
|---|---|
| Facility and operating object | Permanent facility ID plus account, asset or record target |
| Task and plan identities | Task ID, approved plan ID/digest, revised plan ID/digest, parent digest |
| Approval | Approver, role, decision time, expiration and governing policy version |
| Trigger | Failed step, changed record, unavailable tool, new evidence or operator request |
| Existing effects | Step receipts, target readbacks and any unknown or in-flight effect |
| Decision owner | Person or role authorized to approve, hand back or reject the revision |

## Step-delta gate

| Test | Proceed within envelope only when… | Otherwise |
|---|---|---|
| Target identity | Facility, account, asset, recipient and vendor remain within the approved set | Reapprove or reject |
| Action semantics | The action class and operating meaning are unchanged or a named branch permits the change | Reapprove |
| Tool and permission | The tool is approved and asks for no broader permission | Reapprove or reject |
| Payload meaning | Consequence-bearing fields remain inside approved bounds | Reapprove |
| Evidence | The named branch condition is supported by current governed evidence | Hold or hand back |
| Communication | Draft/send state, audience and claim boundary are unchanged | Reapprove |
| Consequence ceiling | Customer, access, safety, money, vendor and external effects do not broaden | Reapprove or reject |
| Partial effects | Every completed, in-flight and unknown effect is preserved with a receipt or status | Hold or hand back |
| Time and currency | Approval is unexpired and required current-state checks pass | Reapprove or recompute |
| Prohibited class | No policy-prohibited substitution or autonomous action is proposed | Reject |

## Allowed dispositions

- `PROCEED_WITHIN_ENVELOPE`: link the exact rule and supporting evidence.
- `RETURN_FOR_REAPPROVAL`: show added, removed and modified fields plus existing effects.
- `HAND_BACK`: assign a named owner and provide the evidence packet.
- `REJECT`: state the prohibited action or authority boundary.

## Minimum test set

1. bounded retry of a read-only step;
2. named preapproved branch with current evidence;
3. substituted vendor or external recipient;
4. draft changed to send;
5. facility or asset identity changed;
6. one committed step followed by a failed step;
7. target outcome unknown;
8. expired approval;
9. new action above the consequence ceiling; and
10. revision proposed without a complete parent plan.

Passing this gate proves only that the revision followed the declared control. It does not prove the model was correct, the facility condition existed, the action succeeded or the architecture meets every policy or legal requirement.


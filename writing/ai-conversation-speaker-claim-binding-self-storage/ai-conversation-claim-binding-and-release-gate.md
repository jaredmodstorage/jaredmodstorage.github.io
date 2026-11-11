# AI Conversation Claim-Binding and Release Gate

Use one record for each claim extracted from a conversation that may influence work. A conversation can create context or a proposal; it does not by itself prove that an operating action was authorized, executed or reflected in the governing system.

## Required record

| Field group | Required fields | Release question |
|---|---|---|
| Conversation identity | conversation ID, facility ID, channel, start/end time, approved source reference | Can an authorized reviewer reach the bounded source? |
| Artifact integrity | audio/source hash, transcript ID/hash, transcription system/version, created time | Which exact artifact produced the claim? |
| Speaker binding | speaker cluster, diarization system/version, participant identity state, participant role, account-authority state | Who spoke, and is identity or authority actually established? |
| Source span | segment start/end, exact utterance, language, overlap/noise state, word uncertainty, speaker uncertainty | Do the words, speaker and conditions survive review? |
| Meaning | proposed act, condition, negation, quantity, date, subject, interpretation version | Is this a question, condition, possibility, acceptance or correction? |
| Human disposition | reviewer role, correction, reason, reviewed time | What changed, and was the reviewer permitted to decide it? |
| Use boundary | permitted use, prohibited use, expiry, governing record to check | May this claim provide context, support a proposal or authorize an action? |
| Outcome | proposed action, approval ID, execution state/receipt, governing readback/state/time | What actually happened after the conversation? |
| Correction path | supersedes, invalidates, affected artifacts, remediation owner/state | Where must a later correction travel? |

## Eight-question release gate

| Gate | Required evidence | Pass condition | Hold state |
|---|---|---|---|
| 1. Source | Approved source reference and artifact identity | Exact source is resolvable under authorized access | `needs_source` |
| 2. Words | Bounded segment and exact utterance | Numbers, dates, conditions and negation are supported | `needs_audio_review` |
| 3. Speaker | Cluster assignment and required identity evidence | Claim is bound to the correct speaker; identity is verified where needed | `needs_speaker_resolution` |
| 4. Meaning | Typed conversational act and interpretation evidence | Meaning is not upgraded from question, condition or tentative plan | `needs_meaning_review` |
| 5. Authority | Participant role, account authority and action policy | Speaker could authorize the proposed action | `needs_authority` |
| 6. Currency | Current facility, account, policy and preference state | No material change invalidates the proposed use | `needs_current_state` |
| 7. Execution | Exact approval and target-system receipt | Action was accepted and performed, not merely proposed | `needs_execution` |
| 8. Readback | Governing-source state and observation time | Authoritative system shows the intended state | `needs_readback` |

## Release decision

- **Context:** May organize a case or identify a question. Keep generated/derived labeling and source pointer.
- **Proposal:** May prepare a draft or task after claim, currency and policy checks. A person must be able to revise or reject it.
- **Authority-bearing action:** Requires verified identity and authority, exact approval, execution receipt and governing-state readback.
- **Hold:** Name the failed gate, prevented consequence, next owner and evidence required to resume.

## Operator checklist

- [ ] The speaker cluster is not represented as a verified person unless a separate identity process supports it.
- [ ] Acknowledgment, possibility, condition and acceptance remain distinct.
- [ ] The exact source span travels with the extracted claim.
- [ ] The conversation record is not represented as payment, access, consent, closure or another governing state.
- [ ] Every consequential action has current policy and role authority.
- [ ] Selection, provider acceptance, execution and readback are separate states.
- [ ] A corrected transcript creates a new version and an affected-artifact review.
- [ ] Sampling, denominators, versions, languages and unscorable cases are recorded in monitoring.

## Evidence boundary

This is a proposed operating template, not a deployed product, legal standard, certification or performance claim. Recording, retention, access and review must follow approved policy and applicable requirements. Do not copy reusable secrets or unnecessary personal data into the register.

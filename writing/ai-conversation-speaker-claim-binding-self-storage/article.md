# The Transcript Says the Customer Agreed. Who Actually Said It?

**By Jared Mastroianni**  
Chief Operating Officer of modSTORAGE; CEO and Founder of Facily.ai

![Jared Mastroianni walks a climate-controlled self-storage corridor with technology and operations leaders.](assets/064-climate-controlled-corridor-walk.png)

*A useful conversation record must preserve who said what, where it came from and what the words are allowed to authorize. Governed editorial image; not a depiction of the fictional example.*

<!-- BODY START -->

A call summary can contain the right words and still produce the wrong operating decision.

The customer says, “If the transfer clears Friday, I can pay then.” The manager replies, “I can review the account Friday morning.” A transcription service assigns the manager's sentence to the customer. A summarizer compresses both turns into “Customer agreed to pay Friday, and access will remain active.” The note is polished, short and operationally dangerous.

Three changes occurred. A conditional statement became a firm commitment. A review became a promise. The speaker boundary disappeared. None of those changes required the model to invent an entirely new sentence.

Self-storage operators increasingly use recorded or transcribed conversations to prepare follow-up drafts, organize service cases, identify unanswered questions and route work. Those are valuable uses. The architecture fails when a transcript, speaker label or summary becomes evidence of consent, authorization, payment, access state or completed work without a controlled path back to the conversation and the governing system.

The answer is a **conversation claim-binding layer**. It keeps four states separate: the audio event, the attributed transcript segment, the interpreted conversational act and the authorized operating decision. A model may help move information between those states. It may not silently collapse them.

## A transcript has two error surfaces, not one

Speech recognition asks what words were spoken. Speaker diarization asks who spoke when. A system can perform well on one and fail on the other.

NIST's [Rich Transcription 2007 Meeting Recognition Evaluation](https://www.nist.gov/publications/rich-transcription-2007-meeting-recognition-evaluation) evaluated speech-to-text, speaker diarization and speaker-attributed speech-to-text as distinct tasks. The historical benchmark is not evidence about any current product or self-storage call. Its durable lesson is architectural: word accuracy does not establish speaker accuracy.

Modern research still treats the combined problem separately. The 2025 ACL paper [*DNCASR: End-to-End Training for Speaker-Attributed ASR*](https://aclanthology.org/2025.acl-long.899/) evaluates a system with a speaker-attributed word-error measure. That paper studies a research method and meeting corpus; it does not validate a facility workflow. It reinforces one practical point: “the transcript looks right” is not a sufficient test when the identity attached to each turn controls what happens next.

Do not hide both surfaces behind one confidence score. Preserve at least:

- the recognized words and segment time;
- the speech-recognition system and version;
- the speaker-cluster label produced by diarization;
- any separately verified participant identity;
- overlapping-speech, interruption and channel conditions;
- uncertainty for the words and for the speaker assignment; and
- the exact audio or approved source reference needed for authorized review.

A speaker cluster such as `speaker_2` is not a customer identity. A caller-ID match is not proof that the named account holder spoke every turn. A person who joins a call is not automatically authorized to make account decisions. Identity, account authority and speaker assignment require different evidence.

## Bind claims, not just sentences

Even a correctly attributed sentence can be interpreted badly. Conversation is full of conditions, questions, quotations, tentative plans, acknowledgments and corrections.

“Could I pay Friday?” is a question. “I may be able to pay Friday” is a possibility. “If the transfer clears, I can pay Friday” is conditional. “Yes, I heard you” acknowledges receipt; it does not necessarily accept a proposal. “I said last week that I would pay Friday” reports an earlier statement. None should be flattened into `payment_promised = true` without a defined rule and appropriate verification.

Use typed conversational acts instead of a generic “agreed” label:

- `question`
- `request`
- `offer`
- `conditional_intent`
- `tentative_plan`
- `acknowledgment`
- `acceptance`
- `refusal`
- `correction`
- `reported_prior_statement`
- `unclear`

Each extracted claim should retain the exact source span, speaker assignment, verified identity state, interpretation version and uncertainty. The model can propose the act. A consequential use should require the release rule appropriate to that act and action.

## Conversation evidence is not operating authority

A customer conversation can report a facility condition, explain a need or indicate an intention. It is still a conversation record. It does not replace the system authorized to establish whether a payment posted, a gate credential changed, a unit transfer completed, a work order closed or a communication preference was applied.

That distinction protects both the customer and the operator. A manager should be able to use a call note to prepare the next step without treating the note as proof that the step occurred.

Build three release classes:

| Release class | Permitted use | Required control |
|---|---|---|
| **Context** | Find the case, prepare a reviewer, identify a question | Visible generated/derived label and source pointer |
| **Proposal** | Draft a follow-up, propose a task or suggest a disposition | Claim binding, current governing-state check and human ability to revise or reject |
| **Authority-bearing action** | Change money, access, account lifecycle, customer preference or another controlled state | Verified identity and authority, current policy, exact action approval, execution receipt and governing-system readback |

The same extracted sentence may be safe for context and unsafe as authority. “Customer may pay Friday” can help a manager prepare a call. It cannot prove payment, change account status or create a payment arrangement by itself.

The [NIST AI Risk Management Framework 1.0](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-ai-rmf-10) is voluntary, cross-sector guidance. It emphasizes context, documented human roles, testing, monitoring and the management of limitations. NIST's [current AI RMF program page](https://www.nist.gov/itl/ai-risk-management-framework) states that version 1.0 is being revised. Neither source defines this claim-binding method or certifies a conversation workflow. They support the narrower discipline of managing an AI system in its actual use context instead of assuming that a generally capable model makes every downstream use appropriate.

## Build a claim-binding envelope

Every claim that could influence work should travel with a compact, resolvable envelope:

1. conversation and segment IDs;
2. channel, start time, end time and approved source reference;
3. transcript artifact hash and transcription-system version;
4. speaker-cluster ID and diarization-system version;
5. participant identity state: `verified`, `asserted`, `unresolved` or `not_required`;
6. participant role and any separately established account authority;
7. exact utterance and language;
8. overlap, interruption, low-audio or missing-audio state;
9. proposed conversational act and interpretation version;
10. condition, negation, quantity, date and subject extracted from the utterance;
11. reviewer correction, if any, with reviewer role and time;
12. permitted use, prohibited use and expiration;
13. governing record that must be checked before action; and
14. correction, supersession and downstream impact links.

[W3C PROV-O](https://www.w3.org/TR/prov-o/) provides a general model for entities, activities, agents, roles, derivation, attribution and revision. It does not prescribe call-center records or prove a speaker identity. It offers a useful structure: the audio, transcript segment, interpreted claim, human review and operating action should remain distinct records connected by named activities and responsible roles.

Do not store reusable secrets or unnecessary personal information in this envelope. Retention, recording, access and review must follow the organization's approved policy and applicable requirements. The architecture should allow a minimized claim to point to restricted evidence without copying the entire conversation into every downstream system.

## Put a release gate between summary and action

Before any extracted claim changes work, ask eight questions:

1. **Source:** Is the source artifact available under authorized access, or is this only a detached summary?
2. **Words:** Does the exact segment support the extracted words, including numbers, dates and negation?
3. **Speaker:** Is the turn assigned to the right speaker cluster, and is that cluster bound to a verified identity where identity matters?
4. **Meaning:** Is the statement a firm acceptance, a condition, a question, a tentative plan or something unresolved?
5. **Authority:** Could this participant authorize the proposed operating action?
6. **Currency:** Did the account, facility, policy or customer preference change after the conversation?
7. **Execution:** Was the action merely proposed, or was it accepted and performed by the target system?
8. **Readback:** Does the governing source now show the intended state?

If any required answer is missing, hold the action at the appropriate state: `needs_audio_review`, `needs_speaker_resolution`, `needs_meaning_review`, `needs_authority`, `needs_current_state`, `needs_execution` or `needs_readback`.

That is more useful than a generic low-confidence flag. It tells the operator what is unknown, what consequence is being prevented and what evidence can release the case.

## A fictional self-storage example

The following teaching case is entirely fictional. Blue Alder Storage, its people, conversation, systems, identifiers and outcomes do not represent modSTORAGE, Facily.ai, a customer, a deployment or a measured result.

A caller identified in the fictional case as Riley discusses an account with manager Ana. Riley says, “If my payroll transfer clears Friday, I can make the payment then.” Ana says, “I can review the account Friday morning, but I cannot promise what the access system will show.” The speakers briefly overlap.

The fictional transcript correctly recognizes most words but swaps the speaker labels during the overlap. A summary states: “Manager confirmed payment Friday and promised continued access.”

The claim-binding gate catches four problems:

- the payment statement was conditional, not completed;
- the review statement came from the manager, not the caller;
- no statement promised continued access;
- the access system remains the governing source for current access state.

The workflow may release a context note: “Caller stated a conditional intention to pay Friday if a transfer clears; manager planned a Friday review. Access was not promised and must be checked in the governing system.” It may prepare a follow-up task. It may not post a payment, alter access, mark an arrangement complete or claim that a promise was made.

If an authorized reviewer corrects the speaker labels, the system creates a new transcript version and traces affected claims, summaries, tasks and drafts. It does not rewrite the old artifact as though the error never existed.

## Monitor the binding path, not just the model

A portfolio dashboard should not stop at average transcription accuracy. Monitor the decisions the workflow is expected to support.

Useful measures include:

- conversations and segments eligible for each use;
- speaker-attributed error on a reviewed, risk-matched sample;
- critical claims with a resolvable source span;
- extracted commitments by act type and reviewer disposition;
- actions held for speaker, meaning, authority, currency or readback;
- generated notes corrected after source review;
- downstream artifacts affected by a transcript correction;
- detached summaries that lost their source reference; and
- confirmed operating actions with both execution receipt and governing-state readback.

Record the sampling method, denominator, task definition, system versions, languages, audio conditions, reviewer qualifications and unscorable cases. A convenience sample of disputed calls cannot establish portfolio performance.

NIST's 2026 report [*Challenges to the Monitoring of Deployed AI Systems*](https://www.nist.gov/publications/challenges-monitoring-deployed-ai-systems-center-ai-standards-and-innovation) identifies gaps and barriers in areas such as human-AI feedback loops, fragmented logging and drift detection. The report maps a developing field; it does not prescribe these measures or prove this architecture effective. Its relevance is the reminder that production monitoring must include the distributed human and technical path, not only a model endpoint.

## Start with one consequential claim

Choose one claim that currently moves from a call into work: payment intention, contact preference, move-out timing, access concern, service request or vendor commitment. Map the audio or approved source, transcript, speaker labels, interpreted act, note, proposed action, execution receipt and governing-state readback.

Then run five tests: swap the speaker labels; remove the conditional phrase; change a date; detach the summary from its source; and correct the transcript after a task has already been created. The system should hold the unsafe use, explain why and identify every affected artifact.

Conversation AI should reduce clerical friction. It should not convert a fluent summary into false authority.

The operating rule is simple: before a sentence can move work, preserve who said it, what they actually said, what they were authorized to decide and which governing system proves what happened next.

<!-- BODY END -->

## Sources and limits

- [NIST, *The Rich Transcription 2007 Meeting Recognition Evaluation*](https://www.nist.gov/publications/rich-transcription-2007-meeting-recognition-evaluation): historical primary benchmark separating speech-to-text, diarization and speaker-attributed speech-to-text tasks; not evidence about a current product.
- [Zheng, Zhang and Woodland, *DNCASR: End-to-End Training for Speaker-Attributed ASR*](https://aclanthology.org/2025.acl-long.899/), ACL 2025: primary research on joint speaker clustering and speech recognition; not a self-storage validation study.
- [NIST, *Artificial Intelligence Risk Management Framework 1.0*](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-ai-rmf-10), NIST AI 100-1: voluntary, cross-sector risk-management guidance.
- [NIST, AI RMF program page](https://www.nist.gov/itl/ai-risk-management-framework): current program status, including notice that AI RMF 1.0 is being revised.
- [W3C, *PROV-O: The PROV Ontology*](https://www.w3.org/TR/prov-o/): authoritative provenance recommendation; not a conversation-record standard.
- [NIST, *Challenges to the Monitoring of Deployed AI Systems*](https://www.nist.gov/publications/challenges-monitoring-deployed-ai-systems-center-ai-standards-and-innovation), NIST AI 800-4: 2026 report on monitoring gaps, barriers and open questions; not a validated prescription for this architecture.

## Assistance and claim disclosure

AI assistance supported source discovery, research synthesis, drafting, tool construction and editorial QA. The conversation claim-binding layer, release classes, eight-question gate, fictional example and companion register are authored editorial proposals. They are not a deployed Facily.ai capability, a modSTORAGE implementation, a customer result, a legal conclusion, a certification or an industry standard. The Blue Alder Storage example is explicitly fictional.

**Proposed slug:** `ai-conversation-speaker-claim-binding-self-storage`  
**Assigned canonical:** `https://jaredmodstorage.github.io/writing/ai-conversation-speaker-claim-binding-self-storage/`  
**Publication state:** Publication-ready local package in progress. No publisher handoff, repository change, publication, indexing, coverage or recognition is established by this manuscript.

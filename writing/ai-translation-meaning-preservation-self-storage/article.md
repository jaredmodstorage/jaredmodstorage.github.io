# The English Version Passed Review. Who Approved the Spanish Meaning?

**By Jared Mastroianni**

**Deck:** AI translation can preserve fluent wording while changing the operating instruction. Self-storage operators need a versioned meaning contract that binds every language to the same facility, event state, time, action, authority, and correction path.

A facility loses vehicle-gate access during the evening. An operator approves an English customer message: the gate is unavailable, the office reopens at 9:00 a.m., and customers who need help should use the posted support number. An AI system produces a Spanish version in seconds. The sentences read smoothly.

But the translation changes one operating fact. It says the gate will reopen at 9:00 a.m. The approved English message says the office will reopen then. No one has authorized a gate-restoration time.

That fictional example is small enough to miss and consequential enough to matter. The translated message is not merely another rendering of approved content. It is a new artifact that can change what a customer believes about access, timing, safety, payment, required action, or available help.

Responsible architecture should treat translation as a governed transformation with its own identity, tests, review state, and release authority. Fluency is not the acceptance criterion. Preserved meaning is.

## Translation is a decision surface

Teams often place translation after approval in the workflow:

`approved message → translate → publish`

That sequence implies the approval automatically transfers to every target-language version. It does not. The English reviewer approved one artifact. A translation may introduce a new ambiguity, narrow or broaden a condition, swap the subject of a sentence, change a date or number, remove uncertainty, or make a recommendation sound mandatory.

The architecture should instead use a second release boundary:

`approved source message → governed translation → meaning checks → qualified review when required → target-language release`

This does not mean every low-consequence phrase requires a committee. It means the system must know which parts of the message cannot change and which kinds of change require a person with the right language and operating authority.

## Build the message as structured meaning first

Free text is a poor control surface. Before translation, represent the message as a versioned object with fields that expose the operating meaning:

- facility identifier and public facility name;
- message purpose and audience;
- observed or authorized event state;
- affected service, entrance, area, or account process;
- effective start and end, including time zone;
- customer action, if any;
- support channel and service hours;
- uncertainty or unknown state;
- prohibited claims;
- governing source and approver;
- source-language text version; and
- expiration, supersession, or withdrawal rule.

The generated language remains important, but it no longer carries the entire control by itself. The translation service receives a meaning contract, not just a paragraph.

Suppose the source contract says:

- `office_state = opens_at_09:00_local`
- `vehicle_gate_state = unavailable_until_verified`
- `restoration_time = unknown`

A target-language sentence that predicts gate access at 9:00 fails even if it is grammatically excellent. The system can compare the translated claims with the approved fields and stop the release.

## Preserve uncertainty exactly

AI-generated language often tries to be helpful by resolving uncertainty. In operations, that can manufacture a commitment.

“We do not yet have a verified restoration time” cannot become “service will return soon.” “The office is scheduled to open at 9:00” cannot become “the facility opens at 9:00.” “Use the support number if you need assistance” cannot become “call immediately.”

Treat uncertainty as a typed value, not a tone choice. Useful states include `known`, `estimated`, `scheduled`, `pending_verification`, `unknown`, and `not_applicable`. Define which target-language terms are approved for each state, while allowing qualified reviewers to select natural phrasing that preserves the same meaning.

The same rule applies to obligations. A message should distinguish `required`, `recommended`, `optional`, `conditional`, and `informational`. Translation should not promote a recommendation into a requirement or weaken a required safety instruction into a suggestion.

## Identify language precisely

“Spanish” may not be enough metadata for every use. Language, script, region, and variant can affect terminology, date formatting, reading expectations, and review routing.

[RFC 5646](https://www.rfc-editor.org/info/rfc5646/) defines a standard structure for language tags using subtags that can identify language and, when justified, script, region, or variant. The standard does not decide which translation is correct and does not guarantee that content is appropriate for an audience. It gives systems a consistent way to identify linguistic attributes.

For an operator, the practical control is straightforward: record the source and target language tags, but do not overstate precision. Use `es` when the content is general Spanish and no more specific distinction is justified. Use a more specific tag only when the application and review process truly support that distinction. A region code is not a substitute for understanding the intended audience.

The translation record should also name the character encoding, rendering direction where relevant, and the exact target text hash. If the content changes after review, the approval must not silently follow the new hash.

## Separate operating authority from linguistic competence

One reviewer may understand the facility event but not the target language. Another may be fluent but lack authority to decide what the facility can promise. A responsible release combines the two roles without pretending they are interchangeable.

The operating owner verifies:

- the facility and event are correct;
- states and times match governing records;
- the requested customer action is authorized;
- the support route is current; and
- the message may be released to the intended audience.

The qualified language reviewer verifies:

- the target wording carries the approved meaning;
- uncertainty, obligation, scope, and tone remain intact;
- terminology is natural and understandable for the audience;
- numbers, units, names, dates, and times are unambiguous; and
- no phrase introduces a new promise, condition, or prohibited inference.

For lower-consequence content, an approved automated path may be sufficient under the organization’s policy. For emergency instructions, access restrictions, payment consequences, legal notices, safety directions, or other high-consequence content, the policy may require qualified human review. The architecture should encode that routing decision before generation, not ask the model to decide whether its own output is safe enough.

## Use invariants, not only similarity scores

A translation can remain semantically similar overall while changing the one field that matters. Aggregate quality scores and sentence-level similarity can support evaluation, but they should not release consequential content by themselves.

Define message invariants that must survive translation:

- every facility and service subject remains the same;
- every number, amount, unit, date, time, and time zone is preserved or transformed under an approved locale rule;
- negation remains negation;
- uncertainty does not become certainty;
- an estimate does not become a commitment;
- conditional action remains conditional;
- customer choice does not become obligation;
- support channels and hours remain linked to the right service;
- no new cause, diagnosis, outcome, or restoration claim appears; and
- privacy and disclosure boundaries remain intact.

Test those fields deterministically where possible. Then review the target-language experience for clarity. A word-for-word translation may satisfy a mechanical comparison and still confuse a customer. Meaning preservation requires both control checks and audience comprehension.

Back-translation can expose certain differences, but it is not proof. Two translation passes can repeat the same ambiguity, erase a culturally important distinction, or converge on wording that sounds close while changing operational force. Treat back-translation as one test signal, not a release authority.

## Bind review to versions

Every released language version should be traceable to:

- message object ID and purpose;
- governing facility-event record;
- source text version and hash;
- target language tag;
- translation model, provider, or human process identifier;
- prompt, glossary, and terminology-rule versions when AI is used;
- generated target text hash;
- automated test results;
- operating and language reviewers when required;
- approval time, expiration, and superseding version; and
- every channel where the text was released.

[NIST’s AI Risk Management Framework 1.0](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-ai-rmf-10) emphasizes validity, reliability, ongoing testing, monitoring, contextual evaluation, and human intervention where systems cannot detect or correct errors. It is voluntary, cross-sector guidance—not a translation standard or proof that a workflow is trustworthy. Its value here is architectural: test whether the system performs as intended in the actual language and operating context, then monitor the deployed path.

The [NIST Generative AI Profile](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence) extends that risk-management approach for generative systems. It does not certify a translation model or prescribe self-storage customer messaging. It supports a lifecycle view in which generated output, human-AI configuration, evaluation, monitoring, and incident response are governed together.

## Correction must reach every language and channel

A source message may change after translations are released. The gate may return to service. The office hours may be corrected. A phone number may change. The English version may be withdrawn after a policy owner finds an error.

Do not assume editing the source automatically fixes its descendants. The release record should enumerate every language and channel: website banner, SMS draft, email template, kiosk, call script, app notification, or posted document. A source correction should mark dependent translations `stale_pending_review`, hold unreleased copies, and route already published copies through an authorized correction or withdrawal workflow.

Completed communications cannot be unsent by changing a database row. Preserve what recipients actually received, then issue the appropriate correction under the governing process. Source corrected, translation regenerated, translation reviewed, correction released, and channel readback are separate states.

## A fictional meaning-preservation failure

The following facility, identifiers, people, records, times, messages, system behavior, and results are entirely fictional.

At fictional Juniper Row Storage, message object `MSG-204` addresses a vehicle-gate interruption. The approved contract states that the gate is unavailable, the office opens at 9:00 a.m. local time, restoration remains unknown, and customers may call the listed support number during posted service hours.

The system generates target artifact `MSG-204-ES-01`. Its language tag is `es`. The translation build preserves the facility name, support number, and office time, but changes `restoration_state=unknown` into a sentence saying vehicle access resumes at 9:00.

The invariant test finds a subject-state mismatch: the 9:00 time belongs to the office, not the gate. Release stops before any channel receives the message. A qualified reviewer revises the Spanish wording, a second invariant test passes, and the operating owner approves artifact `MSG-204-ES-02` with a new hash. The example demonstrates the control; it does not claim any real deployment, model capability, customer result, or incident.

## Use the AI Translation Meaning-Preservation Gate

The companion gate records the message contract, source and target identities, nonnegotiable meanings, automated checks, review requirements, release channels, and correction path. Its blank CSV can be adapted to an operator’s actual tools and policies. The fictional row demonstrates a failed translation that is corrected before release.

Do not store unnecessary customer data in the record. Do not treat a language tag as proof of fluency, a model response as approval, a reviewer’s language ability as operating authority, or a passed test as permanent assurance. Reevaluate when the model, prompt, glossary, policy, source schema, channel, audience, or consequence changes.

The final release question is not “Does this sound fluent?” It is:

> Does this target-language artifact preserve the exact facility meaning, uncertainty, action, authority, and correction obligations that were approved in the source contract?

If that cannot be shown, the translation may be polished. It is not ready to operate.

## Sources

1. National Institute of Standards and Technology, [*Artificial Intelligence Risk Management Framework (AI RMF 1.0)*](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-ai-rmf-10), published January 26, 2023, accessed November 2, 2026.
2. National Institute of Standards and Technology, [*Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile*, NIST AI 600-1](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence), published July 26, 2024, page updated April 8, 2026, accessed November 2, 2026.
3. Internet Engineering Task Force, [*RFC 5646: Tags for Identifying Languages*](https://www.rfc-editor.org/info/rfc5646/), published September 2009, accessed November 2, 2026.


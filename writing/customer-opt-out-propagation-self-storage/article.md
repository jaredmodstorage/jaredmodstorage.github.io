# The Customer Said Stop. Which Facility Is Still Sending Messages?

**By Jared Mastroianni**

A customer replies “STOP” to a text from one facility. The messaging provider suppresses that number in its own campaign. The property-management record still shows text as the preferred channel. A second facility has the same person under another customer record. The call center works from yesterday’s export. A regional spreadsheet has no suppression field at all.

The customer made one clear request. The portfolio stored several conflicting versions of what should happen next.

This is not mainly a messaging problem. It is a control problem: **can a communication restriction move from the place where it was received to every in-scope sender before another message is released?** Multi-location operators need a suppression event that is identifiable, time-bounded, purpose-aware, propagated, and independently checked. A checkbox on one customer screen is not enough.

## Start with the request, not the preference field

Most operating systems expose a current preference: text, email, phone, or none. That field is useful for choosing a channel. It is weak evidence of how the current value came to exist, what the person actually requested, and which systems received the change.

Preserve the event behind the preference. At minimum, record:

- the exact source message or a governed reference to it;
- when and where the request was received;
- the customer and contact-point identities available at that moment;
- the channel, sender identity, message purpose, and campaign or workflow;
- the requested action and any words that require qualified interpretation;
- the rule or policy version used to classify the request;
- the effective state, owner, and deadline;
- every downstream system expected to enforce the restriction; and
- evidence that each destination applied it.

The event record should not become a warehouse for unnecessary message content. Retain only what the approved evidence and retention rules require. The point is to preserve enough evidence to explain and enforce the state, not to copy a customer conversation into every tool.

## Treat scope as a decision, not a guess

A request can arrive in a context: a marketing text, a payment reminder, an access notification, an email newsletter, or a live conversation. That context matters, but it does not automatically answer the legal or policy scope of the restriction.

Current [FCC delivery-restriction rules](https://www.ecfr.gov/current/title-47/chapter-I/subchapter-B/part-64/subpart-L/section-64.1200) address revocation of consent for covered calls and texts, identify several reply words as reasonable means, and set processing requirements. Current [FTC CAN-SPAM guidance](https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business) distinguishes commercial email from transactional or relationship content and explains commercial-email opt-out duties. Those authorities do not produce a universal self-storage preference model. Applicability depends on the communication, technology, purpose, relationship, jurisdiction, and current law.

Operators should therefore use a counsel-reviewed classification table rather than improvising from message tone. Keep these dimensions separate:

1. **Contact point:** the exact phone number or email address.
2. **Channel:** text, voice, email, or another approved channel.
3. **Purpose:** marketing, account service, access, safety, payment, survey, or another governed class.
4. **Sender:** the legal or operating entity and the system or provider acting for it.
5. **Scope:** the facilities, brands, workflows, and message classes affected under the approved rule.
6. **State:** pending review, suppressed, limited, superseded, expired where permitted, or unknown.

Do not turn ambiguity into permission. If the request cannot be classified before the next send, place the affected contact point and workflow on hold and route the question to the authorized owner.

## Build one suppression identity

The same person may appear under multiple rental agreements, facility records, lead records, or provider profiles. A phone number can also change owners. That means neither the customer ID nor the contact point alone is a complete identity.

Create a stable suppression-event ID and link it to the exact contact point as observed, the known customer-record candidates, and the identity-confidence state. Do not merge people because their names look similar. Do not broaden a restriction to an unrelated person because a recycled number happens to match an old record. When identity is unresolved, preserve the conflict and apply the approved protective rule until it is reviewed.

This differs from customer deduplication. A cross-site identity process may decide that two records probably represent one person. The suppression register asks a narrower question: which current communication candidates must be stopped or held because of this evidence?

## Propagate through an enforcement graph

Listing systems is not enough. For each communication workflow, identify how eligibility is actually decided.

A typical portfolio may have:

- a property-management system that stores customer preferences;
- a marketing platform with its own suppression list;
- a texting provider that processes replies;
- a call-center queue built from scheduled exports;
- an access platform that sends operational notices;
- local spreadsheets or contact lists; and
- an automation service that assembles audiences.

For each node, document the record key, expected enforcement field, integration path, update cadence, last successful readback, and owner. Then map the edges: provider webhook to integration queue, queue to customer master, customer master to audience builder, and audience builder to the final sender.

The suppression state is not propagated because an API call returned success. It is propagated when the target system shows the expected current state for the right contact point, purpose, and sender scope. A provider receipt proves only what that provider says it accepted.

When two sources disagree, do not let whichever system was queried last become the winner by accident. Name the governing source for each decision, preserve the contradictory readbacks, and hold release until the authorized owner resolves them. A local preference may be current while a provider-level restriction is broader. A marketing platform may show suppression while an old export remains actionable. Reconciliation means explaining those differences and controlling every remaining send path, not forcing the screens to display one convenient value.

## Quarantine stale audiences

An opt-out received at 10:02 a.m. can collide with a campaign exported at 9:55 a.m. The list was accurate when created and unsafe when released.

Every outbound batch should carry an audience receipt:

- audience version and hash;
- source snapshot time;
- release time;
- sender, channel, and purpose;
- suppression source and version;
- excluded contact-point count;
- unresolved identity or scope exceptions;
- eligibility-rule version; and
- releaser and approval evidence.

Before transmission, recheck the final population against the current suppression state. Do not rely only on the earlier query. If the provider supports its own suppression enforcement, use that control too, but do not treat it as a substitute for keeping the operator’s governing state current.

Exports should expire. A spreadsheet pulled yesterday should not remain a standing permission to contact people today. When a list crosses the approved age limit or its suppression version is no longer current, quarantine it and rebuild it.

## Reconcile every destination

The propagation register should show one row per destination, not one optimistic status for the entire event. Useful destination states include:

- `not_started`;
- `submitted`;
- `accepted_unverified`;
- `applied_verified`;
- `rejected`;
- `conflict`;
- `not_applicable`; and
- `unknown`.

Only `applied_verified` proves that a defined destination displayed or enforced the expected state at the recorded time. `Not applicable` requires an authorized scope decision. A blank cell is not either one.

If a destination cannot be updated, the operator still needs a control. Remove or hold the audience, disable the affected workflow where authorized, add a pre-send filter, or route manual review. The fallback must name its owner, evidence, expiration, and restoration condition.

## A fictional two-facility failure

Consider an explicitly fictional portfolio, Alderline Storage Group.

At 10:02 a.m., a fictional customer replies “STOP” to a promotional text from Alderline Harbor. The provider records the reply and suppresses the number for that messaging account. The customer also has a separate fictional rental record at Alderline Ridge, created with a different email address but the same phone number.

At 10:08 a.m., the integration service accepts the provider event. Its customer-match job finds both records, but one match remains provisional because the names differ. The system correctly holds both text-marketing candidates instead of silently merging the accounts. An authorized reviewer resolves the match at 10:21 a.m. under the fictional portfolio policy.

The marketing platform verifies suppression at 10:24 a.m. The property-management records verify their current contact state at 10:29 a.m. A call-center list created at 9:40 a.m. remains open. Because its suppression snapshot predates the request, the list is quarantined and rebuilt. The replacement audience verifies the number as excluded at 10:36 a.m.

Every facility, person, time, provider, message, rule, record, and result in this example is invented teaching data. It does not describe a modSTORAGE customer, system, deployment, compliance result, or communications practice.

## Measure the control, not the volume of messages

The most useful portfolio measures are about control performance:

- time from receipt to governing classification;
- time from classification to verified enforcement by destination;
- destinations still unverified at the deadline;
- stale audiences quarantined before release;
- sends attempted after the effective restriction;
- identity and scope conflicts awaiting review; and
- fallback controls that expired without normalization.

Do not publish a “100 percent compliant” claim from a platform dashboard. The denominator must include every in-scope destination, manual list, provider, and batch that could still send. A clean marketing platform does not prove the call center, facility export, or separate brand account is clean.

## Use the propagation register before the next send

The companion **Customer Communication Preference and Suppression Propagation Register** turns the method into a reviewable operating record. Use it to capture the source event, classify scope, link identity candidates, enumerate enforcement destinations, document readback, quarantine stale audiences, and assign unresolved exceptions.

The practical release rule is simple:

> No communication candidate proceeds when an in-scope suppression is unresolved, the audience predates the governing state, or a required destination lacks verified enforcement.

This is a workflow control, not legal advice. The classification rules, retention periods, emergency exceptions, consent requirements, and message categories must come from current law, contracts, provider capabilities, and qualified policy owners.

A customer should not need to repeat the same request to every facility and vendor in the stack. The operator’s job is to hear it once, determine its proper scope, and make every in-scope system behave accordingly.

## Sources

1. Electronic Code of Federal Regulations, [47 CFR § 64.1200 — Delivery restrictions](https://www.ecfr.gov/current/title-47/chapter-I/subchapter-B/part-64/subpart-L/section-64.1200), current electronic edition accessed November 9, 2026.
2. Federal Trade Commission, [CAN-SPAM Act: A Compliance Guide for Business](https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business), accessed November 9, 2026.
3. World Wide Web Consortium, [PROV-DM: The PROV Data Model](https://www.w3.org/TR/prov-dm/), W3C Recommendation, April 30, 2013.

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.

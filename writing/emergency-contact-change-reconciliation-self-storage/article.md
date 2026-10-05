# The Emergency Contact Changed. Which Facility Still Calls the Former Manager?

## A portfolio method for changing emergency roles across plans, providers, devices, and after-hours call trees without mistaking one edited record for completion

By Jared Mastroianni

A facility manager leaves on Friday. Human resources records the departure. The property roster shows an interim manager on Monday. Someone edits the shared contact sheet.

At 2:10 a.m. Tuesday, a monitoring provider still calls the former manager.

The failure is easy to describe as stale contact information. That description is incomplete. The portfolio did not fail to store a new phone number. It failed to change an operational route across every place that can initiate, receive, escalate, or explain an emergency contact.

An emergency contact is not a row in a directory. It is a role, purpose, facility scope, contact sequence, effective period, and set of downstream surfaces. If any of those fields are missing, the same person can be current in one system, expired in another, and absent from a third.

The right question after a contact change is not, "Did we update the list?" It is, "Which routes can still reach the wrong person, and what evidence proves each route now reaches the right role?"

## Start with the role, not the person's name

Portfolios often treat the named person as the contact. That makes every change look like a simple substitution: replace Alex with Morgan.

The operating object should be the role assignment:

- purpose: fire-alarm escalation, facility incident, utility outage, security event, customer-access emergency, or another approved use;
- facility scope: one site, a region, or a defined portfolio group;
- sequence: primary, secondary, tertiary, or after-hours fallback;
- authority: receive information, acknowledge, dispatch, approve a shutdown, notify leadership, or perform another bounded action;
- channel: work mobile, voice line, text-enabled number, email, app notification, or provider portal;
- effective start and expiration;
- backup role; and
- source owner who may approve a change.

That structure prevents two common mistakes. First, a newly hired manager is not automatically the correct recipient for every emergency purpose. Second, removing the former manager from the employee roster does not prove that external providers, panels, call trees, and notification profiles stopped using the old assignment.

OSHA's emergency-action-plan rule requires procedures for reporting emergencies and the name or job title of employees who can explain the plan or their duties. It also requires review when responsibilities or the plan change. The exact legal applicability depends on the workplace and the standards that require its plan. The broader operating lesson is useful without stretching the rule: emergency responsibility must be explicit enough for employees to know who owns it, and role changes require a plan-level review, not just an address-book edit.

## Inventory every contact surface before changing one

The same facility role may appear in places that are owned by different teams. A portfolio-level surface inventory might include, where actually used:

- the facility emergency action plan and posted call tree;
- central-station or alarm-monitoring contact lists;
- fire, security, gate, elevator, HVAC, generator, or utility provider accounts;
- property-management and access-control user profiles;
- incident-management, work-order, or on-call software;
- employee group texts, call-down lists, and shared mailboxes;
- regional and executive escalation rosters;
- landlord, municipal, responder, or insurance contact records when approved and applicable;
- printed binders, wallet cards, wall sheets, and local spreadsheets; and
- vendor-held lists that cannot be inspected directly without a request.

This is not a claim that every facility should have every surface. It is a prompt to name only the ones that can actually route information for that facility.

Each surface needs an owner and an update method. Some changes are internal and immediate. Others require a provider ticket, a signed form, a verification call, or a scheduled account review. A field that cannot be viewed after submission needs stronger evidence than "form sent."

The inventory should also record whether the surface stores a person, a role, or both. A posted plan might correctly say "regional manager" while a provider account requires a specific name and number. Those records are related, but they are not interchangeable.

## Define one change episode

A contact change should have an episode identifier that connects all affected surfaces without collapsing them into one status.

The episode begins with an authorized source event: reassignment, leave, termination, coverage change, new provider relationship, phone-number change, or another approved trigger. It records the old assignment, new assignment, facility scope, affected purposes, effective time, privacy classification, and change owner.

Then every downstream surface gets its own state:

- **Not applicable:** the facility or purpose does not use the surface.
- **Identified:** the surface is in scope, but no change has been started.
- **Requested:** the update was submitted to the surface owner.
- **Acknowledged:** the owner or provider confirmed receipt.
- **Changed:** the new value was saved.
- **Read back:** the saved value was independently viewed or returned.
- **Exercised:** an approved nonemergency test followed the intended route.
- **Failed:** the wrong, missing, or incomplete route appeared.
- **Reconciled:** readback or test evidence matches the authorized assignment, and old access or contact data has been dispositioned.

The episode cannot be called complete because one high-profile surface reached `Changed`. Completion is the set of required surfaces at `Reconciled`, with any excluded surface explicitly marked `Not applicable` by an authorized owner.

This is the same discipline NIST's Cybersecurity Framework 2.0 applies in a different domain when it says roles, responsibilities, and authorities should be established, communicated, understood, and enforced, and when it calls for lines of communication that include third parties. CSF 2.0 is cybersecurity guidance, not a self-storage emergency-contact standard. Its structural value here is that responsibility, communication, and external dependencies are distinct governance objects.

## Do not delete the old route before the new one is real

Immediate removal can be correct when a separation, privacy issue, safety concern, or access decision requires it. But routine transitions still need an ordered cutover.

Before the effective time, verify that the new person has accepted the role, understands the facility and purpose, can use the approved channels, and knows the boundary of the authority being assigned. A phone number that rings is not proof that the recipient knows what to do.

At the effective time, make the authorized changes in the governing source and initiate every downstream update. If a surface supports primary and backup contacts, set the intended order explicitly. Do not leave the former manager as an unlabeled fallback because the field was inconvenient to remove.

After propagation, inspect each surface. When direct readback is unavailable, collect the strongest available evidence: provider confirmation naming the account and effective value, a screenshot of the current profile, an export, or a documented verification call. Record the limitation instead of treating a submission receipt as a saved change.

Finally, disposition the old route. Depending on the surface and policy, that may mean removed, expired, disabled, retained only in history, or held temporarily under a documented overlap. "Not primary" is not the same as "cannot be called."

## Protect personal contact information

Emergency contact work can spread personal mobile numbers into systems, printed sheets, inboxes, screenshots, and vendor accounts. A fast update should not become uncontrolled replication.

Use approved business channels where available. Record the purpose and permitted surface for any personal contact data. Limit the package to people who need it. If the source owner authorizes a number for voice but not text, do not infer text consent. If the new role expires in two weeks, carry that expiration into the contact episode rather than relying on someone to remember.

The OSHA emergency-action-plan checklist asks whether key personnel and outside responders or contractors are listed and whether those lists are kept current. It also asks who is authorized to coordinate the plan. That does not create permission to publish employee information broadly. Currency and accessibility still need privacy controls and role-based distribution.

## Test the route without manufacturing an emergency

A real incident is a poor first test.

Use an approved, announced, nonemergency exercise that cannot be confused with an actual alarm. The test should identify itself immediately, use the provider's supported method, and avoid emergency responder dispatch unless the authorized exercise plan specifically includes it.

A useful route test records:

- test owner and authorization;
- facility and contact purpose;
- surface or provider being tested;
- start time and timezone;
- first recipient reached;
- sequence actually followed;
- acknowledgment result;
- unexpected recipient, delay, or dead end;
- stop condition; and
- corrective owner and retest date.

Ready Business materials emphasize communications planning, emergency-response teams, and training or exercises so people know their responsibilities. The current Ready.gov business page was visible through the official search index during this review, while direct automated retrieval returned HTTP 403. That transport limitation is recorded; the article does not treat the page as proof that any specific exercise is required for a self-storage operator.

Do not place a live emergency call merely to validate a spreadsheet. Where a provider has a test mode, follow its current instructions. Where no safe test exists, document the readback limitation and use another authorized verification method.

## Reconcile by facility and purpose

Portfolio teams often finish the corporate contact sheet and assume every facility is complete. The reconciliation should instead pivot on two questions:

1. For each facility and emergency purpose, who should receive the first call now?
2. Which surface proves that route, and when was it last verified?

That view exposes asymmetry. Five facilities may use the same regional manager while one site uses a local building contact for a specific system. A shared provider may hold separate contact lists for fire and intrusion monitoring. A printed binder may be current at the office and stale in an after-hours lockbox.

Do not "standardize" away a legitimate local difference. Record its governing source and owner. Comparability means the fields have the same meaning, not that every facility has the same route.

The accompanying Contact Surface Reconciliation Register therefore uses one row per facility, purpose, and surface. A portfolio summary can count reconciled rows only after every required row has evidence. Missing rows remain missing; they do not become zero-risk facilities.

## A fictional six-facility cutover

Fictional Keystone Harbor Storage assigns a new regional manager effective October 5 at 9:00 a.m. Eastern Time. The role covers six fictional facilities and three purposes: after-hours facility incidents, security escalation, and utility outages.

The contact episode identifies 24 required surface rows. The shared emergency plan and internal on-call directory are updated and read back. Two provider portals show the new contact. A third provider acknowledges the request but does not expose the saved value. At one facility, a printed call tree still lists the former manager. At another, the security provider has the correct new primary but retains the former manager as the second fallback.

The portfolio does not call the episode complete. The printed tree is replaced and logged. The retained fallback is removed under the authorized provider change. The no-readback provider supplies a confirmation that names the facility, purpose, new recipient, sequence, and effective time. An approved nonemergency test then reaches the new regional manager at five facilities but reaches a local manager first at the sixth. Review shows that the sixth facility has a valid site-specific order. The difference is documented rather than overwritten.

Only after all 24 rows are reconciled or explicitly marked not applicable does the episode close. Every facility, person, number, provider, purpose, timestamp, record, test, and result in this example is fictional teaching material. It is not a modSTORAGE transition, customer record, provider relationship, deployment, response-time result, or compliance claim.

## The operating standard

An emergency-contact change is complete only when the organization can answer four things:

- **Who owns the role now?**
- **For which facility, purpose, authority, and time period?**
- **Which internal and external surfaces can still route the call?**
- **What readback or approved test proves the old route no longer controls the outcome?**

Editing the shared list is necessary. It is not reconciliation.

## Sources

1. Occupational Safety and Health Administration, [29 CFR 1910.38 — Emergency Action Plans](https://www.osha.gov/laws-regs/regulations/standardnumber/1910/1910.38), current official standard page; accessed October 5, 2026.
2. Occupational Safety and Health Administration, [Emergency Action Plan Checklist](https://www.osha.gov/etools/evacuation-plans-procedures/eap/develop-implement/checklists), current official eTool; accessed October 5, 2026.
3. National Institute of Standards and Technology, [Cybersecurity Framework 2.0](https://tsapps.nist.gov/publication/get_pdf.cfm?pub_id=957258), NIST CSWP 29; accessed October 5, 2026.
4. Federal Emergency Management Agency, [Ready Business](https://www.ready.gov/business), official preparedness resource indexed with communications-planning, training, and exercise guidance; accessed October 5, 2026. Direct automated retrieval returned HTTP 403 during final review.
5. Federal Emergency Management Agency, [Ready Business Emergency Response Plan](https://www.ready.gov/sites/default/files/2020-09/business_emergency-response-plans.pdf), official planning template; accessed through the official indexed result October 5, 2026. The template is a planning aid, not a self-storage requirement.

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.

## Editorial disclosure

This article was prepared with AI-assisted research, drafting, and editorial QA under Jared Mastroianni's byline. It proposes a product-neutral operating method and reports no customer, deployment, provider, performance, response-time, legal-compliance, revenue, occupancy, award, or recognition result. The fictional example and dataset are teaching material only. Operators must apply their current emergency plans, employment and privacy policies, contracts, provider instructions, and applicable law.

---
title: "What Should an AI-Drafted Work Order Tell the Vendor?"
slug: ai-vendor-work-order-data-disclosure-self-storage
author: Jared Mastroianni
intended_slot: 2026-11-24 evening AI architecture
assigned_destination: Jared Mastroianni personal authority site
canonical: https://jaredmodstorage.github.io/writing/ai-vendor-work-order-data-disclosure-self-storage/
publisher_owner: Master Personal Site Authority
description: "Design vendor work orders that carry useful facility context while controlling which records, attachments and links leave a self-storage operation."
---

# What Should an AI-Drafted Work Order Tell the Vendor?

By Jared Mastroianni

![AI-generated editorial scene of Jared Mastroianni and two colleagues at a technology design review.](assets/052-ai-development-ai-engineering-design-review.png)

*Work-order design includes deciding which information a contractor needs to see. AI-generated editorial illustration.*

<!-- BODY_START -->

At fictional Larch Ferry Storage, the manager asks the maintenance assistant to prepare a plumbing work order. A customer reported water near the second-floor loading corridor. Staff documented a damp patch at the reported location and took a wide photo. The internal case also contains the customer’s mobile number, a remark about the contents of a nearby unit, and a link that opens the entire ticket for employees.

The plumber needs an address, a way to find the affected area, the observed condition, a facility contact and a defined scope. The extra details in the case could make their way out in the email subject, the photo, the filename, the body or the link. An approval screen that shows only the body gives the manager an incomplete picture of what the vendor will receive.

I would design this workflow around a separate vendor packet. Give the model a record prepared for the job and the recipient, and check the finished packet before it leaves the system. That lets the facility retain a useful internal case and gives the contractor enough information to arrive prepared. The two views have different jobs and should be built accordingly.

## Decide what each vendor role needs for the job

Start with one work type and one destination. A shared plumbing dispatch account and a named technician in a vendor portal may support the same repair, but their access needs can differ. Define the job, facility, assigned organization, recipient role and approved channel before choosing fields. A directory record alone establishes who a vendor is. A matching assignment and current scope establish what job that vendor is there to do.

Give every field a disposition. The facility address, equipment location, observed symptoms and general service contact can be approved for a common-area inspection. Internal customer comments and payment data can be excluded from this packet entirely. A customer callback or a drawing that includes restricted areas might require a separate documented reason and approval. Where the technician needs to meet staff, a facility contact or an escort instruction can supply the operational answer with less disclosure.

The distinction is familiar in security architecture. NIST’s information-flow control addresses where information is allowed to travel within and between systems. Its control enhancements describe policy filters, human review and checks on attachments and metadata. A staff member’s authority to read the source ticket and an application’s authority to deliver parts of it to a contractor are different decisions. The flow policy should be checked using the actual destination. [NIST SP 800-53 Rev. 5, AC-4](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf)

## Limit what the drafting model can retrieve

Keep the internal ticket in its existing permissions boundary. Have a service outside the model build the candidate vendor record. Pull staffed callback details from the approved facility directory, work location from a verified facility or asset record, and observations from fields already reviewed for the scope. Pull only the assigned facility and job. Retain source record and version references in the internal review view for anyone authorized to check them.

Avoid handing the model a complete ticket with a request to omit anything sensitive. That requires it to decide which facts are suitable for this recipient at the same time it is translating the job into plain language. It also exposes extra material to the drafting path. Apply equivalent field selection to retrieval, tool results, retries and regeneration. An engineer should be able to point to the boundary that keeps an internal-only note out of those inputs.

Where a field is required and missing, keep it unresolved. If the request says water was reported by a customer, the draft can describe it as a report. It should describe standing water as observed by staff only when the record establishes that observation. It should never turn either statement into a diagnosis of the cause. The work order can ask for an inspection and a report of findings while the actual cause remains open.

Some elements are better inserted directly by the application. Let the workflow place the assignment ID, approved callback and building designation from verified structured fields. Use the model to draft a short statement of the symptom and the task from bounded inputs. That preserves the value of clear prose and leaves exact routing details under deterministic control. If phrasing still requires a case-by-case judgment, give the reviewer the draft and the relevant approved source side by side.

## Inspect everything the recipient can open

Build the approval screen from the finished outgoing packet. The reviewer should see the destination account, subject, message text, attachment names and permitted link targets. Include a vendor-view preview of every uploaded file. For an image, review the actual frame and any accompanying metadata in the derivative. For a document, inspect comments, hidden layers and embedded items as applicable. A legitimate provenance record belongs in the source archive even when policy calls for a separately approved vendor copy.

In the fictional plumbing case, the wide image also shows a customer’s label on a box. The work location can still be conveyed with a verified corridor reference. If a close-up adds value, staff can obtain or approve a separate image that shows the affected area and keeps the unrelated material out of view. A tiny preview of the original photo cannot confirm what the technician can read at full resolution.

Review the destination behind buttons, too. A link called “View work order” can lead to a vendor-specific record, a shared folder or the internal ticket. Test with the external permissions that will actually apply. Prefer a vendor-scoped view over a broad share link. Check that the relevant vendor role can reach the approved work and that it cannot reach unrelated tickets from the same view. Where the platform supports expiry and revocation, apply the account’s approved settings and record the expected access window.

NIST’s Generative AI Profile recommends monitoring generated content for privacy risks and considering ways to detect personal or sensitive data across output formats. I would use detection as one check in the release process. It can flag a candidate phone number, but the policy still needs to say whose phone number it is and why it is being shared. A failed inspection, an unsupported file type or a destination that cannot be verified should hold the affected packet for review. [NIST AI 600-1, Generative Artificial Intelligence Profile](https://nvlpubs.nist.gov/nistpubs/AI/NIST.AI.600-1.pdf)

## Bind the approval to the material actually delivered

A manager should be able to approve a packet without granting the model authority to send a later variation. Save the packet version with its recipient, purpose, facility, assignment, policy version, unresolved conditions and file versions. Bind approval to the exact structured payload and reviewed attachments. A digest can help the system detect a changed payload. It does not establish that a reviewer had permission or that the release was lawful.

Immediately before delivery, have the outbound service check the vendor assignment, active endpoint, current policy and approved version again. A late contact change or added attachment should produce a new version requiring the appropriate review. Changes introduced by channel adapters deserve the same attention. For example, if a portal automatically copies all case attachments into a contractor view, a clean message body will not control what the technician sees. Restrict what the adapter can add, and verify the delivered representation through available provider readback or controlled recipient testing.

Record the states a manager can act on. A draft may be held, approved or queued. A provider may accept the submission without confirming delivery. A vendor may receive a notice without opening the work. Keep the provider reference and timestamps under controlled access. If receipt or delivery is uncertain, check the relevant record before another transmission. For a packet confirmed to have reached the wrong destination, use the existing incident process, including revoking scoped access where possible and recording the affected version. A file already copied by the recipient cannot be withdrawn merely by revoking a link.

FTC guidance for businesses treats contractors and service providers as part of personal-information protection. It recommends making security expectations explicit and checking how service providers handle entrusted information. Those responsibilities belong to the operator and its provider relationship. The workflow described here can enforce part of an approved policy at release time. [FTC, Protecting Personal Information: A Guide for Business](https://search.ftc.gov/system/files/documents/plain-language/pdf-0136_proteting-personal-information.pdf)

## Make the hold useful to the person running the property

A hold should tell the manager what is safe to do next. If a source photo has mixed content, say which approved view is missing. If the vendor account has changed, route verification to the owner of the provider directory. If the contractor requires a field that policy has withheld, specify the operational need and ask the authorized owner for a narrow decision covering the field, destination and duration. Keep the usual escalation and emergency channels available. The software's review step should never become the only way to arrange urgent help.

Back at fictional Larch Ferry, the manager prepares the common-area inspection with the facility address, the corridor location, the staff-observed condition and the front-desk callback. The wide original image and the customer record stay in the restricted case. The vendor gets the scope and a direction to meet staff for access. The dispatch screen records what was shared and the packet version. If the job later expands to a customer unit, a new scope decision determines whether coordination with the customer is needed and who should handle it.

Managers also need visibility into repeated holds. Track missing facility contacts, unverified endpoints, changed attachments and policy exceptions by reason. Count the packets held and the population to which the measure applies. Those counts can show where the operating procedure is incomplete. Keep sensitive values out of routine dashboards and retain enough restricted evidence for authorized follow-up. A high volume of missing contacts calls for a directory fix before it calls for a more persuasive prompt.

## Test one vendor route before adding the next

Start with the companion Vendor Work Order Disclosure Worksheet. Choose a low-risk work type, one approved recipient role and a controlled test destination. Walk through a complete fixture with no live customer details. Run versions with an unnecessary customer callback, a changed recipient, a missing facility contact and a file that the screen cannot inspect. Test that each gets the right hold or substitution. Then walk through a clean packet and confirm that someone in the vendor role can locate the job and understand the work requested without calling for basic details.

Verify normal and exceptional paths when a template, attachment renderer, recipient directory or delivery adapter changes. A new photo renderer may show a different crop. A vendor portal update may alter who can see the case. Assign an owner who can suspend the affected route while staff use the verified manual procedure. Retain the test record with the version under review so the next release starts with a real baseline.

That is the standard I would put in front of an operations team. Find the smallest packet that lets the contractor do the job well. Put the decision in a reviewable policy, check the whole outgoing object, and make it easy for a manager to get service moving when a piece is missing.

<!-- BODY_END -->

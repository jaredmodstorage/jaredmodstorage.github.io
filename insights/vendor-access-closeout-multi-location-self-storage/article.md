# The Vendor Left. Why Is the Access Code Still Active?

**By Jared Mastroianni**

**Deck:** A completed work order does not prove that a vendor’s facility access ended. Multi-location operators need a closeout control that reconciles the person, credential, scope, time window, work record, return evidence, and revocation receipt.

A gate technician finishes at 3:40 p.m. The facility manager closes the work order, thanks the technician, and returns to the office. The repair record says complete. The invoice will arrive later. Yet the temporary gate code remains active through Friday because its expiration was set when the visit was scheduled, not when the work ended.

That is not merely a forgotten code. It is a broken handoff between vendor work and access authority.

Self-storage portfolios often manage the same visit in several places: a maintenance platform, an access controller, an email thread, a visitor log, a key cabinet, and an accounting system. Each source can be correct within its own boundary while the operating result remains wrong. The work order can be closed while the credential is active. A gate code can expire while a physical key is still out. A key can be returned while a subcontractor’s separate credential remains unknown.

The portfolio needs one closeout question: **Did every access instrument issued for this work reach a verified end state?**

## Work completion and access termination are different events

A work order records the state of requested work. An access system records the state of a credential. A visitor log records presence. A key-control process records custody. None of those records automatically proves the others.

Treating “work complete” as “access ended” creates a semantic shortcut. It also makes portfolio review unreliable. One facility may close a ticket when the vendor leaves. Another may close it after an invoice is approved. A third may close it after a manager tests the repair. If the portfolio uses ticket closure as the signal to revoke access, those three practices produce three different exposure windows.

The operating contract should therefore define separate events:

1. the vendor visit was authorized;
2. an access instrument was issued or enabled;
3. the person entered or received custody;
4. the work stopped or completed;
5. the person departed;
6. each credential was disabled, expired, recovered, or formally escalated; and
7. a reviewer reconciled the access end state to the work record.

The sequence is useful even when the facility has no integrated software. It tells the team what must be proven before the visit is truly closed.

## Start with the person, not the vendor name

“Northside Gate Service” is not an access subject. It is an organization label. The individual technician, subcontractor, or delivery person who receives access is the subject.

A shared vendor code hides that distinction. If three people know the code, the portfolio may be able to see that the code was used without knowing who used it. If the vendor changes personnel, the code can outlive the original authorization. If the same code is used at several facilities, one compromise or delayed revocation has a wider scope than the work order suggests.

Where the installed system and approved policy support individual credentials, issue access to a verified person for the narrow facility, entrance, dates, and purpose required. Where the technology cannot enforce that design, record the limitation and add a compensating operating control such as staffed entry, escort, a daily-changing code, or immediate post-visit rotation. Do not describe a limitation as a feature the system does not provide.

This aligns with the broader control logic in [NIST Special Publication 800-53 Revision 5](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final). Its account-management controls address authorized users, intended use, account review, temporary accounts, disabling expired or unnecessary accounts, and audit records for account changes. NIST’s catalog is not a self-storage operating procedure and does not prescribe a particular gate product. It supplies a strong design principle: temporary access needs a defined lifecycle, not an indefinite credential plus a note.

## Make scope explicit before the visit

The closeout succeeds or fails at authorization. Before issuing access, record five boundaries:

- **Subject:** the individual receiving the credential or key;
- **Facility:** the specific property, using its stable portfolio identifier;
- **Resource:** the gate, office, mechanical room, unit corridor, key, alarm partition, or other approved scope;
- **Purpose:** the work order, delivery, inspection, or other authorized task; and
- **Time:** the start, expected end, and maximum expiration.

The time boundary needs two clocks. The expected end supports normal operations. The maximum expiration is the fail-safe if no one performs closeout. A two-hour visit might have an expected end at 3:30 p.m. and a system expiration at 5:00 p.m. The manager should still revoke the credential when the technician leaves at 3:40. The 5:00 expiration is a backstop, not the desired closeout time.

Physical instruments need the same treatment. “Vendor has a key” is incomplete. Which key? Who accepted it? What can it open? When is it due back? Which retained key or cabinet slot will be reconciled? A key without a custody record is an unbounded access exception.

## Design the end state before the credential is created

Every issued instrument should have one allowed end state:

- **disabled:** the system accepted a revocation and a readback shows inactive;
- **expired:** the configured expiration passed and a readback shows inactive;
- **recovered:** a physical instrument returned and custody was reconciled;
- **rotated:** a shared secret was replaced and the old value no longer works under the approved procedure;
- **lost or unrecovered:** the instrument is missing and the defined escalation is open; or
- **unknown:** the source cannot yet prove the state, so the exception remains owned.

“Closed” is not specific enough. It can describe the maintenance ticket, the visitor record, the access account, or the exception. The closeout record should name the object and state: `work_order=complete`, `credential=disabled`, `key=recovered`, `visit=departed`, `exception=closed`.

The [NIST Cybersecurity Framework 2.0](https://www.nist.gov/publications/nist-cybersecurity-framework-csf-20) reinforces the distinction. Its identity-management outcomes call for permissions and authorizations to be defined, managed, enforced, and reviewed, with privileges rescinded when no longer needed. The framework is voluntary and technology-neutral. It does not establish that a particular facility is compliant or secure. For an operator, its practical value is the lifecycle: define access, enforce it, review it, and remove it.

## Require a revocation receipt, not a click

An employee pressing “disable” proves intent. It does not prove the controller accepted the change, synchronized it to the relevant device, or reported the credential inactive.

The closeout record should capture the command time, actor, source-system record ID, response, and readback time. If the platform is temporarily offline, keep the access exception open and apply the facility’s approved contingency. Do not convert an unverified command into a successful revocation.

Physical returns need receipts too. The person accepting a key or fob should identify the instrument and record the custody transfer. A photograph may help under an approved policy, but a photo of a key on a counter does not by itself prove which key it is, who accepted it, or whether another copy exists.

## Reconcile across the portfolio, not only at the desk

Local closeout matters, but portfolios also need a review that finds silent failures. Build a daily or scheduled reconciliation that compares:

- vendor visits that ended;
- work orders marked complete or canceled;
- temporary logical credentials still active;
- credentials that expired without a departure or closeout record;
- physical keys, badges, and fobs still issued;
- shared credentials due for rotation; and
- unresolved offline or synchronization states.

Do not automatically treat every mismatch as misconduct or a security incident. A credential may remain active because the work legitimately continues tomorrow. A vendor may leave for parts while the work order remains open. A system may report late. The mismatch is an exception that requires a named owner and a fact-based disposition.

Portfolio comparability depends on common definitions. Define when a visit is considered ended, which credential types are in scope, what counts as an authoritative inactive readback, how quickly an exception must be owned, and who can approve continued access. Keep any thresholds as company policy, not invented industry standards.

## A fictional closeout example

The following scenario and every name, identifier, time, and result in it are fictional.

At fictional Harbor Elm Storage, a gate technician associated with fictional Cedar Signal Services receives credential `V-4482` for work order `WO-731`. Access is limited to the vehicle gate and equipment enclosure from 1:00 to 5:00 p.m. The technician signs out at 3:42 p.m., and the manager marks the repair work complete after a local operating check.

At 3:46, the manager sends the disable command. The access platform returns an accepted response, but the controller is offline, so no device readback is available. The manager does not mark access terminated. The site uses its approved contingency, keeps the enclosure controlled, assigns the exception to the regional operations owner, and sets the next review for 4:15.

At 4:07, the controller reconnects. The source record reports credential `V-4482` inactive as of 4:06. The regional owner verifies the readback, links it to the visit, and closes the access exception at 4:10. The work completed at 3:42; access termination was verified at 4:07. Both times remain visible.

The example does not claim that any real facility, access platform, vendor, or workflow behaves this way. It demonstrates why a command receipt and an inactive readback belong in separate fields.

## Use the Vendor Access Closeout Register

The accompanying register gives operators one row per issued access instrument. It links the person, facility, resource, work purpose, expected end, maximum expiration, departure evidence, termination action, readback, exception owner, and final decision.

Use it as a control design, not as a substitute for approved security, legal, privacy, human-resources, contract, or emergency procedures. Adapt the fields to the facility’s installed systems and governing policy. Avoid placing gate codes, passwords, personal contact details, or unnecessary identity data in the register.

The closeout test is simple:

> Can we prove that the work ended, the person departed, every issued access instrument reached an accepted end state, and any gap remains owned?

If the answer is no, the work order may be complete. The access lifecycle is not.

## Sources

1. National Institute of Standards and Technology, [*Security and Privacy Controls for Information Systems and Organizations*, SP 800-53 Rev. 5, including current release information](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final), accessed November 2, 2026.
2. National Institute of Standards and Technology, [*The NIST Cybersecurity Framework (CSF) 2.0*](https://www.nist.gov/publications/nist-cybersecurity-framework-csf-20), published February 26, 2024, accessed November 2, 2026.


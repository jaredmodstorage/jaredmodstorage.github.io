# The Lease Changed. Which Version Did Each Customer Actually Sign?

**Deck:** A portfolio cannot govern a lease update by replacing one file. It has to connect the approved artifact to every facility, rental channel, issuance event and executed record—and prove the old version stopped appearing where it should.

**By Jared Mastroianni**

A lease update may begin as a document decision, but it becomes an operating-systems problem the moment more than one facility or rental channel must use it.

Legal approves a revised form. Someone uploads a PDF. The web rental flow appears current. A regional manager tells the facilities to use the new version. Yet a kiosk may still hold a cached copy, a shared-drive shortcut may point to the prior file, a manager may print from an old email, and an integration may select a template by an internal identifier nobody included in the release note.

The portfolio can honestly say the lease was updated while still being unable to answer a basic question: which exact artifact did each customer receive and execute?

That is not a reason to let operators interpret contract language. The approved text, required disclosures, effective dates and legal sufficiency belong to qualified owners and counsel. Operations has a different responsibility: make the approved decision reproducible across the systems that issue and retain the document.

## Govern an artifact, not a filename

“Current lease.pdf” is a label, not an identity.

A controlled artifact needs a stable version ID and a digest, such as a SHA-256 hash, calculated from the exact released bytes. It also needs the approval reference, effective window, eligible facilities, eligible rental channels, language or jurisdiction treatment when those are part of the approved release, and the version it supersedes.

The hash does not prove that the terms are correct. It answers a narrower and very useful question: is this file byte-for-byte the artifact that was approved and released?

That distinction matters because documents can look identical while differing in a footer, disclosure, attachment or signature field. They can also look different while representing an authorized rendering of the same approved content. The release owner must define what counts as the controlled object: one exact PDF, an approved source plus a deterministic renderer, or another governed package. The portfolio should never invent that definition after a dispute.

[NIST Special Publication 800-128](https://csrc.nist.gov/pubs/sp/800/128/upd1/final) describes configuration management as establishing and maintaining the integrity of information-system products and configurations through controlled change and monitoring. It is federal security guidance, not a self-storage lease standard. Its useful operating lesson is that an approved baseline, a change decision and the observed deployed state are separate things.

## Map every issuance path before release

A portfolio lease can reach a customer through more paths than the project plan names. Common paths include:

- an online move-in flow;
- a facility-management-system screen;
- a kiosk or unattended terminal;
- a call-center or remote-rental workflow;
- an emailed signature link;
- a locally printed packet;
- an assisted transfer, renewal or amendment process; and
- a fallback used during an outage.

Do not assume these paths share one template store. Record the facility, channel, application, environment, template ID, renderer or workflow version, and current artifact digest for each path. Include dormant fallbacks if staff are still authorized to use them.

The resulting matrix should expose four different states:

1. **Approved:** a qualified owner has authorized the artifact for a defined scope and effective window.
2. **Deployed:** the target system or location reports that the intended version is installed or selected.
3. **Verified:** a controlled test produces the expected artifact and digest for the intended facility and channel.
4. **Issued:** an actual transaction record identifies the artifact instance provided in that transaction.

None of those states can safely substitute for another. Approval does not prove deployment. A successful deployment call does not prove the kiosk refreshed. A test does not prove every later issuance. An executed record does not prove that all other channels stopped using the prior version.

## Use an effective window, not a vague launch date

The release contract should state when the new version becomes eligible and when the old version stops being eligible for each defined scope. Use an exact timestamp and time zone where timing matters. If the governing decision requires a different transition rule—such as completion of already-started transactions—record that rule as supplied by the authorized owner. Do not improvise it in application code or at the front desk.

Also record the event that selects the version. Is it reservation creation, rental initiation, document generation, signature invitation, signature completion or another approved point? Different systems can choose different events unless the portfolio makes the decision explicit.

This is where many apparently small discrepancies begin. A customer starts online before the cutoff and completes at the facility after it. A signature link is regenerated. A transfer creates a new agreement. A kiosk resumes an abandoned session. The portfolio needs a version-selection rule for those cases, not a guess made under customer pressure.

## Test the rendered result, not just the template screen

A green configuration screen is useful evidence, but it is not the customer artifact.

For every in-scope facility and channel, run the approved non-customer test. Generate the document through the real path, confirm the artifact version, inspect required attachments and signature fields, calculate the digest where that method applies, and preserve the test receipt. If the system creates a transaction-specific document, verify the controlled invariant fields and record the resulting instance ID rather than pretending every personalized file should have the same hash.

[NIST SP 800-53 Revision 5](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final) includes configuration-change control and impact-analysis controls. The catalog is designed for security and privacy programs, not contract administration. The transferable practice is to document changes, analyze their effects, test them and retain evidence of the implemented state.

The release test should include failure paths:

- the device was offline during deployment;
- the local cache did not invalidate;
- the template identifier exists but points to the wrong artifact;
- the old print packet remains accessible;
- the renderer omits an attachment;
- the channel cannot report the issued version; or
- an approved facility exception is missing from the selection rule.

An unresolved failure does not have to stop every facility. It does have to stop the affected scope from being labeled ready.

## Bind the issued document to the transaction

The decisive evidence is not a screenshot of the template library. It is the relationship among the transaction, facility, channel, customer-safe reference, issued artifact instance, approved version, issue time and execution state.

Store or reference enough evidence to reproduce that relationship under the organization’s approved retention and access rules. Do not copy sensitive customer data into a general deployment tracker. Use durable record identifiers, controlled links and minimum necessary metadata.

The federal E-SIGN provision at [15 U.S.C. § 7001](https://uscode.house.gov/us/usc/119-124/t15/s7001/) addresses electronic records and signatures, including conditions for consumer disclosures and retention of records that accurately reflect the information and remain accessible and reproducible when law requires retention. Applicability is a legal question. The operating takeaway is limited: a “signed” flag alone is not a complete retention or reproduction record, and this article does not determine which form, consent process or retention period is required.

## Reconcile by exception, not by confidence

After release, compare expected issuance with observed issuance. For each in-scope transaction, ask whether the recorded version was eligible for that facility, channel and selection event at that time.

Use explicit exception classes:

- **unknown version:** the transaction cannot identify the issued artifact;
- **ineligible version:** the recorded artifact was outside its approved scope or window;
- **render mismatch:** the produced instance does not match the controlled release rule;
- **missing instance:** the workflow says complete but no reproducible document record is available;
- **duplicate instance:** multiple executed artifacts exist without an approved disposition;
- **scope conflict:** facility, channel or jurisdiction inputs disagree; and
- **retention or access failure:** the entitled reviewer cannot retrieve an accurately reproducible record through the approved route.

Do not convert an unknown version to “current” because the rollout was probably complete. Assign an owner, due time, customer-impact boundary and evidence requirement. A legal or customer-service response, if needed, belongs to the authorized function—not to the reconciliation spreadsheet.

## Preserve rollback without reopening old transactions

Rollback has two meanings here. The first is operational: restore the last approved issuance path if the new release cannot produce valid documents. The second is evidentiary: preserve the exact release package, prior configuration, test results and affected transaction list so the organization can explain what occurred.

Rolling back a template does not silently change documents already issued or executed. Their state and any required response must be decided through the approved process. The register should therefore separate current channel configuration from transaction disposition.

Before release, name the rollback authority, technical method, last approved version, cache invalidation step, validation test, communication owner and condition for resuming. “We can upload the old PDF” is not a rollback plan if five other channels still reference the new template ID.

## A fictional portfolio example

The following scenario is entirely fictional and contains no real customer, facility, provider, deployment or result.

Cypress Span Storage operates five fictional facilities. Its authorized owner releases lease artifact `LEASE-FIC-v8` for new rentals beginning at 9:00 a.m. Eastern time. The release covers the web flow, facility desks and two kiosks. It supersedes `LEASE-FIC-v7` for that defined scope.

Preflight verifies the web flow and all five desk workflows. One kiosk is offline and remains held. The second kiosk reports the new template ID, but the rendered test still produces the v7 digest. That kiosk is also held. The portfolio releases the verified web and desk paths while routing kiosk rentals to the approved alternative process.

Later, one fictional transaction has no issued-version field. The team does not label it v8 based on the transaction time. It opens an unknown-version exception, preserves the record references, assigns the authorized owner and keeps any response outside the technical register until the evidence is reviewed.

The example does not claim that this release pattern is legally sufficient. It shows how a portfolio can avoid representing an unverified document as the approved version.

## The Portfolio Lease-Version Issuance and Reconciliation Register

Use the accompanying register to control one release across facilities and channels. It records:

- release identity, approval source, artifact version, digest and superseded version;
- facility, channel, system, environment, template and renderer identity;
- effective window and version-selection event;
- deployment receipt, generated test instance, artifact comparison and readiness decision;
- transaction-safe reference, issuance instance, issued version and execution state;
- exception class, owner, deadline and operating boundary; and
- rollback version, authority, verification and final reconciliation state.

Start with one document class and one release. Do not attempt to reconstruct every historical lease version in the first pass. The immediate objective is to make the next change traceable from approval through issuance.

## Make document truth observable

Multi-location operators do not need facility managers to interpret contract language or reverse-engineer template systems. They need a release process that tells each role what it owns.

The authorized content owner defines the approved artifact and scope. The systems owner deploys and tests the issuance paths. Operations holds unverified channels. The records owner preserves the approved evidence. The qualified legal and compliance functions decide legal requirements and transaction responses. The portfolio owner reconciles exceptions without converting uncertainty into a pass.

A file can be approved without being deployed. A template can be deployed without being rendered correctly. A document can be generated without being tied to the transaction. A signature status can exist without proving which version was signed.

When those states remain separate, the portfolio can answer the question that matters: not merely whether the lease changed, but which approved artifact each customer actually received.

---

## Sources and limitations

1. [NIST SP 800-128, *Guide for Security-Focused Configuration Management of Information Systems*](https://csrc.nist.gov/pubs/sp/800/128/upd1/final), published August 2011 with 2019 update; accessed November 14, 2026. Federal information-security guidance, not a self-storage lease-deployment rule or legal sufficiency standard.
2. [NIST SP 800-53 Revision 5, *Security and Privacy Controls for Information Systems and Organizations*](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final), current publication page including Release 5.2.0 notice; accessed November 14, 2026. A flexible control catalog, not proof of compliance or a prescribed private-sector contract workflow.
3. [15 U.S.C. § 7001, *General rule of validity*](https://uscode.house.gov/us/usc/119-124/t15/s7001/), official U.S. Code page accessed November 14, 2026. Applicability, consumer-consent requirements, exceptions and retention duties require qualified legal review; the statute does not establish this register or a universal self-storage lease process.

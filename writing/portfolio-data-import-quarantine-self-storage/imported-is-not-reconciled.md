# Imported Is Not Reconciled: A Quarantine Gate for Portfolio Data in Self-Storage

**By Jared Mastroianni**

**Proposed destination:** Jared Mastroianni personal authority site  
**Proposed slug:** `portfolio-data-import-quarantine-self-storage`

<!-- BODY START -->

A multi-location self-storage operator can change thousands of facility records with one import. That is useful when the file is right. It is dangerous when the file is merely clean.

A CSV can open without errors, contain every required column and pass a technical upload check while still carrying the wrong facility identifier, an expired business rule, an incomplete site population or a value that means something different in the destination system. The import screen may say “successful” even though the operating question has not been answered: did the right records change, at the right facilities, under current authority, with every exception visible?

That is why portfolio data should pass through a quarantine gate before it becomes operating state.

Quarantine does not mean copying a file into a folder called “review.” It means separating receipt, validation, approval, execution, readback and reconciliation. Each state needs an owner, evidence and a rule for what happens next. Until those gates pass, the data is a proposal—not portfolio truth.

## A valid file can still be the wrong instruction

Structural validation answers narrow questions. Are the required fields present? Are dates, numbers and enumerated values expressed in allowed forms? Does each object satisfy the declared schema?

JSON Schema Draft 2020-12 provides a vocabulary for constraints such as required properties, allowed values, numeric limits and array uniqueness.[^1] Those checks are valuable, but they do not establish that a facility code belongs to the intended property, that a rate change is authorized, that an access state is safe, or that the file contains every site in scope.

The same distinction applies to a spreadsheet. A column labeled `facility_id` can contain syntactically perfect identifiers that point to the wrong locations. A field labeled `office_close_time` can contain valid times while omitting the time zone, exception calendar or effective date. A Boolean can be technically valid and operationally ambiguous because the source and target define “active” differently.

The first control, then, is to refuse the phrase “the data is valid” without naming the layer:

- **Structural validity:** the file conforms to its declared format and schema.
- **Identity validity:** every facility, customer, unit, asset or work item resolves to the intended governed entity.
- **Semantic validity:** each field means the same thing in the source, transformation and target.
- **Authority validity:** an approved owner may authorize the proposed change for the stated scope and time.
- **Reconciliation validity:** the executed result matches the approved proposal across the governing target and its dependent systems.

Those layers should produce separate evidence. Passing one must never fill in the others.

## Freeze the import identity before review

An operator cannot approve a moving target. Before anyone evaluates the file, give the import a stable identity and freeze the exact candidate bytes.

Record the import ID, purpose, source system, source export ID, extraction time, source schema version, row count, facility population and cryptographic checksum. Record the transformation code or mapping version used to produce the candidate. If the file changes, create a new candidate identity and repeat the review. Do not replace the bytes under an approved filename.

Provenance matters because a clean output does not explain how it was produced. The W3C PROV family describes provenance in terms of entities, activities and people, including derivation, versioning and processing steps.[^2] A portfolio import does not need to implement that entire model to learn from it. It does need to answer: which source produced this candidate, what transformed it, who reviewed it, and which exact version reached the destination?

Keep sensitive content out of the register when a protected pointer will do. The control record should identify evidence without becoming an uncontrolled copy of customer, payment, access or employee data.

## Compare the proposed change, not just the rows

The next gate is a dry run that produces a readable difference.

For each target record, show the governing identity, current value, proposed value and resulting effective value. Group the diff by facility and consequence. A spelling correction to an internal asset label is not equivalent to a value that changes customer access, a charge, a delinquency workflow, a public office-hour display or an automated message.

Classify the highest reachable consequence before release. The classification should determine who may approve, whether the change may run in a cohort, what rollback or containment evidence is required and which downstream systems must be checked.

NIST SP 800-53 includes controls for information-input validation, configuration-change control and audit-record generation.[^3] It is a federal security and privacy control catalog, not a self-storage import standard. Its useful operating lesson is that input checks, controlled changes and audit evidence are different control functions. A portfolio should not compress them into one green checkmark.

The dry run must also expose prohibited fields. If the approved request is to update regional manager assignments, the candidate should not be allowed to carry rental rates, gate states or customer-contact flags simply because those columns exist in the template. Scope is defined by allowed differences, not by what the importer happens to accept.

## Make facility coverage a control total

Portfolio imports often fail quietly at the edges. Eleven facilities load. One facility uses an old alias and drops out. The job reports 98 percent success, and the missing property becomes tomorrow’s exception.

Treat coverage as an equation. Start with the approved facility population. Reconcile that population to the candidate file, the attempted target population, the accepted population, the rejected population and the independently verified population. Each site must land in exactly one explained state.

Do the same for rows and material totals. If the source contains 4,820 records, the candidate contains 4,818 and the target accepts 4,816, there are two different gaps to investigate. A single “failed rows: 2” message does not explain the records lost before execution.

Partial success deserves its own policy. Some systems accept valid rows while rejecting others; some roll back a batch; some report a job as complete with exceptions. The operator must know the destination’s actual behavior before release. The approved plan should state whether partial success is allowed, which consequences require all-or-nothing handling, and what state the portfolio enters when only part of the scope changes.

Never infer those behaviors from a generic provider category. Test the exact supported path in the relevant environment and retain the evidence.

## Release from quarantine with explicit authority

A candidate leaves quarantine only when the named approver can see the purpose, exact scope, frozen bytes, source and transformation versions, validation results, proposed diff, consequence class, exception population, execution plan and required readback.

Approval should bind to that exact candidate. If someone fixes three rejected rows after approval, the revised file is a new candidate. The original decision does not travel automatically.

The release record should include:

- the approver and decision time;
- the approved facility and field scope;
- the exact candidate checksum;
- the target environment and object;
- the allowed partial-success rule;
- the stop conditions;
- the recovery or containment owner; and
- the evidence required for closure.

This is change control, not ceremony. NIST SP 800-128 describes configuration management as managing and monitoring system configurations to reduce risk while supporting business functions.[^4] Its scope is security-focused federal guidance, so it does not dictate a private operator’s workflow. The transferable discipline is to identify, evaluate, approve, implement and monitor changes rather than treating execution as the whole control.

## A provider receipt is not a portfolio result

After execution, capture the job ID and the provider’s counts—but do not close the import there.

Read the changed records back from the governing target by stable identity. Compare actual values to the approved diff. Then inspect every dependent surface that can affect operations: facility views, call-center references, access integrations, websites, reports, automations and cached exports. The required list depends on the import’s consequence and actual architecture.

AWS Database Migration Service documents a product-specific validation process that compares source and target rows and reports mismatches, pending records, suspended records and failures.[^5] That does not make AWS DMS a self-storage control or prove that any facility platform offers equivalent behavior. It illustrates the distinction a portfolio needs: moved data and validated data are separate states, and mismatches require their own evidence.

Close only when the control totals reconcile. “Accepted” means the provider received or processed something under its own semantics. “Observed” means the governing record now shows the expected value. “Reconciled” means the approved population, actual target state, rejected records and downstream effects agree—or every remaining variance has a named owner and due date.

## A fictional twelve-site example

Consider a completely fictional operator, Cedar Trace Storage Group. It has twelve fictional facilities and wants to update a fictional internal service-area field used for regional routing. The candidate file is structurally valid and contains twelve rows.

The identity check finds that `CTS-07` is an expired alias now associated with no governed facility. The semantic check finds that two rows use legacy region labels. The dry run also reveals an unexpected `customer_message_enabled` column populated by an inherited export template.

The correct outcome is not “upload and fix the exceptions later.” The candidate remains quarantined. The prohibited column is removed, the two labels are mapped under the current dictionary, and the unresolved alias is routed to the facility-identity owner. A new candidate receives a new checksum and new approval.

In a second fictional run, eleven facilities execute and one target record is rejected because its version changed after the dry run. The job is not marked complete. Eleven records are read back, the remaining facility stays on its prior routing state, the exception receives an owner and the portfolio control total reads: 12 approved, 12 attempted, 11 observed as intended, 1 rejected and 1 open exception. No customer, deployment, provider performance or business result is claimed; the example exists only to demonstrate the method.

## Use the quarantine register as the release record

The accompanying Portfolio Data Import Quarantine Register keeps import identity, provenance, validation, facility coverage, dry-run evidence, authority, execution, readback and reconciliation in one operating sequence. It includes a blank row and fictional teaching records. It contains no default approval thresholds and no claim about a particular vendor’s capabilities.

Adapt the register to the consequence. A marketing-label import may need a lighter review than a change touching access, money, delinquency, customer communications or public facility information. Higher consequence should mean narrower permissions, stronger preconditions, smaller cohorts, clearer stop rules and more demanding readback.

The discipline is simple: do not let a clean file become operating truth by momentum. Freeze it. Validate each layer. Show the diff. Reconcile the population. Bind approval to exact bytes. Execute under a defined partial-success rule. Read the result back. Then close the exceptions.

Imported is a transport state. Reconciled is an operating conclusion.

<!-- BODY END -->

## Sources

[^1]: JSON Schema, [JSON Schema Validation: A Vocabulary for Structural Validation of JSON, Draft 2020-12](https://json-schema.org/draft/2020-12/json-schema-validation), accessed September 12, 2026.
[^2]: World Wide Web Consortium, [PROV-Overview](https://www.w3.org/TR/prov-overview/), W3C Working Group Note, April 30, 2013; accessed September 12, 2026.
[^3]: National Institute of Standards and Technology, [SP 800-53 Rev. 5, Security and Privacy Controls for Information Systems and Organizations](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final), including the August 27, 2025 Release 5.2.0 notice; accessed September 12, 2026.
[^4]: National Institute of Standards and Technology, [SP 800-128, Guide for Security-Focused Configuration Management of Information Systems](https://csrc.nist.gov/pubs/sp/800/128/upd1/final), October 2019; accessed September 12, 2026.
[^5]: Amazon Web Services, [AWS Database Migration Service: Data Validation](https://docs.aws.amazon.com/dms/latest/userguide/CHAP_Validating.html), accessed September 12, 2026.

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.

## Editorial production note

Research, drafting, structured-tool production and QA were completed with AI assistance under Jared Mastroianni's direction. The final article remains bounded by the sources, fictional-example labels and claim limitations recorded in this package.

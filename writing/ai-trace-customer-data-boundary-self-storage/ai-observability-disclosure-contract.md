# AI Observability Disclosure Contract

Use this contract before an AI workflow emits a field into a log, trace, event, alert or support bundle. It is a release gate for telemetry design, not a legal determination or a substitute for the operator's privacy, security, records and provider reviews.

## Four allowed dispositions

| Disposition | Use when | Required control | Example |
| --- | --- | --- | --- |
| Allow metadata | A bounded value explains system behavior without copying business content | Defined purpose, classification, destination, access role, retention and validation test | Model version or error class |
| Reference governed evidence | An authorized reviewer may need the underlying operating record | Opaque reference, source-system authorization and no access embedded in the reference | Controlled account-record reference |
| Opt in to bounded content | A specific diagnostic need cannot be met with metadata or a reference | Named purpose and owner, minimum fragment, pre-export transformation, approved destination, short retention and automatic expiry | Redacted fictional test fragment |
| Deny capture | The value is a credential, secret, prohibited content or unnecessary sensitive record | Prevent collection at instrumentation; test absence across every export path | Gate credential or payment token |

## Contract workflow

1. Inventory every proposed attribute, event body and payload field before instrumentation is enabled.
2. Name the exact diagnostic or control purpose. "Useful later" is not a purpose.
3. Assign the field one disposition. Default to deny when classification or ownership is unresolved.
4. Apply redaction, truncation, tokenization or reference substitution before the exporter or collector receives the value.
5. Record every destination, including alerts, support bundles, queues, backups and provider dashboards.
6. Set retention, access role and exception expiry independently of the source record.
7. Validate both presence and absence: required metadata must appear; prohibited synthetic markers must not.
8. Reapprove the contract when the model, prompt, retrieval source, tool schema, exporter, provider or field classification changes.

## Release questions

| Question | Pass condition | Hold condition |
| --- | --- | --- |
| Why is the field collected? | One current diagnostic, control or audit purpose is named | Speculative future usefulness |
| Is content required? | Metadata and controlled reference were tested and found insufficient | Raw content enabled for convenience |
| Where is transformation applied? | Before the value enters the exporter or collector | After ingestion or only in a dashboard view |
| Can the reference expose the record? | Reference is opaque and resolution requires source-system authorization | Reference contains identity data or grants access |
| Who can read the telemetry? | Named role with justified access | General engineering or vendor access by default |
| How long is it retained? | Approved telemetry retention class and deletion path | Provider default with no owner |
| What proves the control? | Synthetic marker test covers success, failure, retry, handback and support export | Only a configuration screenshot or policy statement |
| When does diagnostic capture stop? | Automatic expiry and named exception owner | Manual reminder or no end time |

## Required evidence packet

- completed CSV contract;
- instrumentation or collector configuration reference;
- redaction/transformation rule and version;
- synthetic-marker test results;
- list of telemetry destinations and access roles;
- retention and deletion-path reference;
- exception approval and expiry, if content capture is enabled;
- release decision, owner and date.

The companion blank CSV is `ai-observability-disclosure-contract-template.csv`. The completed teaching file is `ai-observability-disclosure-contract-fictional-example.csv`; every row in that file is explicitly fictional.

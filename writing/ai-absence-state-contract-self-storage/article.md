# The Field Is Blank. Did the AI Read “No,” “Unknown,” or “Not Applicable”?

**A missing value is not an operating decision. If an AI system cannot explain why a field is empty, the field cannot safely authorize an action.**

By Jared Mastroianni

A customer record reaches an AI workflow with no expiration date for a temporary access exception. One service interprets the blank as “no expiration.” Another treats it as “no exception.” A third drops the field before the model ever sees it. The resulting recommendation may sound precise, but the architecture has already lost the question that matters: what does the absence mean?

In self-storage operations, a blank can represent many different conditions. The value may never have been collected. It may be unknown today, withheld from this user, no longer current, not applicable to this facility, or lost during a mapping failure. It may also represent an explicit answer such as “none.” Those conditions are not interchangeable.

When software collapses them into one empty value, the AI does not merely lack context. It receives permission to invent context. That can affect customer access, maintenance priority, delinquency follow-up, vendor dispatch, reporting, and any other workflow in which a system uses absence as if it were a fact.

## Serialization is not meaning

The technical standards make a useful starting distinction. [RFC 8259](https://www.rfc-editor.org/rfc/rfc8259.txt) defines `null` as one valid JSON value. A JSON object can also omit a member entirely. Those are different structures, but the standard does not assign either one a self-storage meaning.

[JSON Schema Draft 2020-12](https://json-schema.org/draft/2020-12/draft-bhutton-json-schema-validation-00) goes further. It treats `null` as a primitive type and uses `required` to test whether a named property is present. It also warns that structural validation may be insufficient for an application to use a value correctly. That is the boundary operators need to understand: a payload can be valid JSON, pass a schema, and still be unsafe for an operating decision.

The business meaning has to come from a governed contract. `null`, an omitted member, an empty string, `false`, and zero must not become synonyms simply because a programming language can treat them as “falsy.”

## Give absence a controlled vocabulary

An action-driving field should carry one explicit semantic state. The exact names can vary, but the meanings should not.

| State | Meaning | Default operating treatment |
| --- | --- | --- |
| `observed_value` | A value exists from the named governing source | Use only within its scope and freshness window |
| `explicit_none` | The governing source affirmatively records that no value or condition exists | Treat as a negative fact only for the defined question |
| `unknown` | The answer is not established | Hold consequential action and route for resolution |
| `not_collected` | The organization did not collect the field | Do not infer an answer; decide whether collection is required |
| `not_applicable` | The field does not apply under the governing definition | Bypass only the specific rule tied to that field |
| `withheld` | A value may exist, but this workflow is not authorized to receive it | Preserve the restriction; do not convert it to “none” |
| `stale` | A prior value exists but is outside its approved freshness window | Refresh or hold; do not silently reuse it |
| `transform_error` | A source value could not be mapped or validated | Quarantine the record and preserve the error evidence |

This vocabulary separates fact, scope, authority, and failure. `explicit_none` is not a general-purpose “no.” A record showing no active access exception does not prove there is no customer access, no gate credential, or no unresolved account issue. The negative fact must remain attached to the question it actually answers.

## Carry the state with the value

Do not send a naked value through the operating path. Send a small evidence envelope:

```json
{
  "access_exception_end_at": null,
  "access_exception_end_at_state": "unknown",
  "governing_source": "approved_access_exception_register",
  "source_record_id": "example-only",
  "observed_at": "2026-10-28T07:00:00-04:00",
  "schema_version": "absence-contract-1.0",
  "mapping_version": "access-map-4.2",
  "allowed_use": "review_only"
}
```

This fictional fragment does not say the customer has or lacks an exception. It says the current workflow has not established the end time and may use the record only for review.

At minimum, preserve the semantic state, governing source, stable source identifier, observation or effective time, schema version, mapping version, and allowed use. If a transformation derives the state, retain that derivation. [W3C PROV-O](https://www.w3.org/TR/prov-o/) provides a general model for entities, activities, agents, and derivation. It does not define this absence contract, but it supports the discipline of showing where a value came from and how it changed.

## Enforce the contract at five boundaries

The control fails if it exists only in the prompt. It has to survive every boundary the record crosses.

### 1. Source admission

The source adapter must identify whether the member was present, what type arrived, which source version produced it, and whether the source itself supplied a semantic state. If an action-relevant field arrives without an approved interpretation, admit the record as `unknown` or `transform_error`—not as a negative fact.

### 2. Transport and storage

Preserve omitted, `null`, empty string, zero, and `false` distinctly. Do not normalize them into one database null without a companion state. If a warehouse or message bus cannot retain the distinction, the architecture needs an explicit state column or envelope before the record enters that layer.

### 3. Transformation and retrieval

Mapping rules must be versioned and testable. A join, export, embedding pipeline, or retrieval index must not drop the state while keeping the value. If the AI receives a summary rather than the source record, the summary must preserve the limitation in language the decision layer can enforce.

### 4. Decision policy

The model may propose an interpretation, but it may not promote `unknown` into `explicit_none`. A deterministic policy gate should map each semantic state to allowed uses. For customer-impacting action, `unknown`, `withheld`, `stale`, and `transform_error` usually require a hold, refresh, or human review. That rule belongs in policy code and tests, not in an informal hope that the model will be cautious.

### 5. Operator surface and readback

The person receiving the recommendation should see “unknown—current source required,” not a blank cell or a technical `null`. After any correction, read the governing record and every affected decision artifact again. A corrected screen does not prove that the retrieval index, work queue, customer message, or audit record stopped carrying the old interpretation.

## Design the handback before the model asks for help

A human-review requirement is incomplete unless the workflow specifies what the reviewer receives and what happens next. The handback should identify the exact field, its semantic state, the governing question, the last trustworthy source, the blocked action, the resolution owner, and the deadline. It should also preserve the model's proposed interpretation as a proposal—not as a facility fact.

The reviewer should resolve the state in the governing source or an approved exception record, not by typing an answer into a disposable AI chat. The workflow then needs a deterministic re-entry point: reread the source, rebuild the evidence envelope, rerun the policy gate, supersede the earlier recommendation, and record which downstream artifacts were corrected.

This keeps decision authority visible. The model may surface the ambiguity and organize the evidence. The named operator or policy owner decides whether the source now establishes `explicit_none`, `not_applicable`, an observed value, or another approved state. Until that happens, the hold is the correct system behavior—not a failure to automate.

## Test the failure modes, not just the happy path

An absence contract needs fixtures that deliberately vary the same field:

- property omitted;
- property present with `null`;
- empty string;
- `false`;
- zero;
- explicit `unknown`;
- explicit `not_applicable`;
- explicit `none` from the wrong source;
- stale prior value;
- value withheld by authorization;
- unexpected type;
- mapping failure;
- corrected value after an earlier recommendation.

Run each fixture through schema validation, transformation, storage, retrieval, prompt assembly, model output, policy enforcement, operator display, and audit logging. A passing test should show that the semantic state survives, prohibited inferences are blocked, the operator sees the limitation, and a later correction propagates through the same path.

The [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) is voluntary and does not prescribe this design. It does, however, place trustworthiness across AI design, development, use, and evaluation. The [NIST Generative AI Profile](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) also emphasizes provenance, system dependencies, documented limitations, testing in real contexts, and tracing information to its source. An absence-state test turns those broad risk-management ideas into a narrow operating control.

## Observe where meaning is being lost

Monitor absence states as architecture signals, not as proof of facility performance. Useful measures include:

- state counts by field, source, connector version, and facility;
- the share of action candidates held because meaning was unresolved;
- transitions from `unknown` to a source-backed state;
- transform errors by mapping version;
- stale values successfully refreshed before decision;
- operator corrections to AI interpretations;
- any use of an undocumented default.

The denominator matters. Ten unknown access-expiration fields among twelve relevant records is different from ten among twelve thousand. A high hold count may indicate a broken connector, a poor source process, an overbroad use case, or a well-functioning safety gate. The metric identifies where to investigate; it does not supply the diagnosis.

## A fictional Cedar Vane example

Consider Cedar Vane Storage, an entirely fictional three-facility portfolio. An AI workflow reviews temporary access exceptions and encounters a blank `exception_end_at` field at all three sites.

At the first fictional facility, the governing register explicitly marks the exception as ongoing until a named review. The end date is `not_applicable` to the current rule, while the review date is required. At the second, a legacy export omitted the field even though the source record contains an end time; the state is `transform_error`. At the third, the manager has not yet confirmed the date; the state is `unknown`.

The visible blank looks identical. The operating treatments are not. The first record can remain in its separately authorized review path. The second needs mapping repair and source readback. The third needs an owner and deadline. None authorizes the AI to announce that all three exceptions are permanent, expired, or equivalent.

Every facility, record, event, system, and outcome in this example is fictional. It demonstrates the method, not a modSTORAGE or Facily.ai deployment or result.

## Use the AI Absence-State Contract and Validation Matrix

The accompanying tool records the field's governing question, allowed states, source and mapping versions, freshness rule, consequence tier, policy treatment, test fixtures, operator label, correction path, and release evidence. Start with one field that can change a customer, safety, financial, or maintenance action. Do not attempt to classify every blank in the portfolio at once.

The practical sequence is simple:

1. Define the exact question the field answers.
2. Name the governing source and approved semantic states.
3. Preserve state and provenance across every boundary.
4. Block inferences that the source did not establish.
5. Test each absence mode end to end.
6. Show the operator what is unknown and what resolves it.
7. Reconcile corrections through every downstream consumer.

The architecture rule is equally simple: **absence cannot grant authority**. If the system cannot distinguish “no” from “not known,” it is not ready to use that field for an operating decision.

## Sources

1. [RFC 8259: The JavaScript Object Notation (JSON) Data Interchange Format](https://www.rfc-editor.org/rfc/rfc8259.txt), Internet Standard, December 2017.
2. [JSON Schema Draft 2020-12 Validation](https://json-schema.org/draft/2020-12/draft-bhutton-json-schema-validation-00), published June 16, 2022.
3. [NIST Artificial Intelligence Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework), released January 26, 2023; current program page notes that AI RMF 1.0 is being revised.
4. [NIST AI 600-1: Artificial Intelligence Risk Management Framework—Generative Artificial Intelligence Profile](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf), July 2024.
5. [W3C PROV-O: The PROV Ontology](https://www.w3.org/TR/prov-o/), W3C Recommendation, April 30, 2013.

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.

## Editorial disclosure

This article was prepared with AI assistance under Jared Mastroianni's editorial direction. The sources, implementation pattern, fictional example, claim boundaries, and publication package were reviewed before handoff. The architecture is an authored operating method, not a product certification, legal conclusion, compliance determination, deployment claim, or performance result.

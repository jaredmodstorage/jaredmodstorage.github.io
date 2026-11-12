# The AI Refused to Decide. Why Did the Workflow Act Anyway?

**By Jared Mastroianni**  
Chief Operating Officer of modSTORAGE; CEO and Founder of Facily.ai

![Three self-storage leaders review an access-technology interface on a tablet near a facility entrance.](assets/065-access-technology-leadership-demo.png)

*A responsible workflow governs what happens after the model stops, not just what the model says. Governed editorial image; not evidence of the fictional example or a production deployment.*

<!-- BODY START -->

An AI assistant reviews a self-storage access exception. The facility record says the gate controller is online. A work order says the gate was taken out of service. The most recent customer ticket reports a failed entry attempt, but the ticket does not identify which entrance was used.

The model does the responsible thing: it declines to classify the gate as available or unavailable because the evidence conflicts.

The workflow does something else. Its response parser expects `available=true` or `available=false`. The abstention arrives as a blank field. A downstream rule converts the blank to `false`, creates an outage task, suppresses the normal access message and marks the AI review complete.

The model refused to decide. The system decided anyway.

That is not primarily a model-quality failure. It is an architecture failure between the model response and the operating action. A responsible AI workflow needs an explicit **abstention route**: a governed path that preserves why the model did not decide, prevents default values from acquiring authority, and hands the unresolved decision to the right person with the right evidence.

## Abstention is a result, not an empty answer

Software teams often treat a model response as content. If content is missing, the application applies familiar software behavior: use a default, retry, skip the field or continue with the remaining values.

That is dangerous when the missing value controls a facility action.

An abstention can mean several different things:

- the evidence is missing, stale or contradictory;
- the request falls outside the model's evaluated scope;
- a safety or policy rule blocked the response;
- a required tool failed;
- the output could not be validated against the schema;
- the model reached a configured uncertainty threshold; or
- the provider stopped generation for a technical reason.

Those states should not collapse into one null. They carry different retry rules, different human owners and different action ceilings.

Research on selective prediction describes a model that can reject some inputs rather than predict on every case, and evaluates the relationship between coverage and risk.[^1] That research does not establish a self-storage operating policy or validate any particular model. It does make one architectural point clear: refusal is part of the prediction system, not an accidental absence of output.

## Separate model refusal from transport failure

The orchestration layer should distinguish at least four response classes:

1. **Decision:** the model returned a schema-valid result inside its evaluated scope.
2. **Abstention:** the model intentionally declined under a defined rule.
3. **Policy block:** a safety, privacy or organizational control prevented the requested response.
4. **Technical failure:** the request timed out, a tool failed, the response was truncated or the schema could not be validated.

A provider finish reason can help diagnose why generation stopped. OpenTelemetry's GenAI semantic conventions include response identifiers, model identifiers and finish reasons as observability attributes.[^2] A finish reason is still not a business decision. `stop` does not mean the answer is complete enough to act on. `length` does not tell an operator whether a safe partial result exists. A tool-call finish does not prove the tool succeeded.

The application must translate technical events into its own controlled response classes. Preserve both layers: what the provider reported and what the operating workflow concluded.

## Make the response type impossible to misunderstand

A consequential workflow should not return a loose object with optional fields. It should return one of a small number of typed states.

For example:

- `decision`: includes the decision value, evidence references, confidence or other acceptance measures where meaningful, model identity, contract version and permitted next action;
- `abstain`: includes a reason code, unresolved evidence, retry eligibility, required owner and action ceiling;
- `blocked`: includes the governing control, permitted disclosure and escalation route; or
- `error`: includes the failure stage, retry policy, attempt number and technical owner.

The action service should accept only the `decision` state for automated staging, and only when the decision contract grants that action. Every other state should follow a named route.

This is stronger than telling the model to say “I don't know.” Natural-language restraint can be lost in parsing, summarization or later automation. The control belongs in the interface contract and the action service, not only in the prompt.

## Eliminate invisible defaults

Defaults are useful for presentation. They are hazardous when they change operating meaning.

Suppose a recommendation object contains `priority`, `facility_scope`, `customer_message`, and `action`. If the model abstains and the parser supplies `priority=normal`, `facility_scope=all`, an empty message and `action=continue`, the workflow has created a complete-looking instruction that the model never produced.

Audit every boundary where an abstention can be converted:

- JSON schema defaults;
- database column defaults;
- Boolean coercion;
- empty-string handling;
- queue priority fallbacks;
- template placeholders;
- spreadsheet formulas;
- API gateway transformations;
- retry wrappers; and
- “best effort” agent logic.

The release test should inject each non-decision state and prove that no operating action occurs unless an explicit route authorizes it. A blank should never inherit the safest-sounding value by assumption. “Continue,” “deny,” “close” and “send nothing” can all be consequential in the wrong decision class.

## Bind the route to the consequence

There is no universal abstention handler.

For a low-consequence drafting task, the system may return a limited response with the unresolved fields clearly marked. For a facility-access decision, payment treatment, customer restriction, safety escalation or account-status change, the correct route may be a hold and human review. For a monitoring summary, the system may continue with a visible coverage limitation while refusing to make a negative conclusion.

The route table should therefore name:

- decision class and consequence tier;
- allowed response classes;
- approved retry conditions and maximum attempts;
- human handback owner and due time;
- action ceiling while unresolved;
- customer-communication boundary;
- evidence required for release; and
- expiration or escalation rule.

NIST's AI Risk Management Framework is voluntary, cross-sector and use-case agnostic. It asks organizations to manage AI risk in context across the lifecycle rather than treating one technical measure as universally sufficient.[^3] The Generative AI Profile also identifies risks arising from human-AI configuration and from the integration of components across a system.[^4] Neither document supplies a self-storage route table. The organization still has to define its own consequence tiers, authority and operating boundaries.

## Retry only when the reason can change

Automatic retry is often treated as recovery. Sometimes it is only repetition.

Retry can make sense when a transient tool or transport failure prevented completion and the next attempt is bounded, observable and idempotent. It does not resolve contradictory facility records, missing authority, an out-of-scope request or a policy block. Repeating the same prompt until the model returns a non-null value converts restraint into pressure.

Every abstention reason should declare whether retry is allowed, what must change before retry, who owns the attempt and how many attempts are permitted. A retry should issue a new run ID while remaining linked to the original task. If the evidence packet changes, record its new digest. If the model or prompt changes, record that too.

Do not let a later decision erase the earlier abstention. Operators need to know that the action was released only after new evidence or an authorized human decision resolved the gap.

## Hand back a decision packet, not a mystery

“AI could not answer” is not an effective handoff.

The operator should receive:

- the exact decision requested;
- the facility, unit, customer or asset scope;
- the evidence the model received;
- the conflict or missing requirement;
- the abstention reason code;
- any technical failure details that are safe and useful;
- actions already prevented or paused;
- the operator's authority and prohibited actions;
- the decision deadline; and
- the evidence needed to close the handback.

The handback remains open until a named person accepts it. Assignment is not acceptance. Acceptance is not resolution. A human decision should record its own basis and authority rather than being presented as an AI output.

## Observe the route, not just the model

Model dashboards often track latency, token use, errors and evaluation scores. An abstention architecture needs operating measures as well.

Track abstention rate by decision class, facility group, model version, prompt version and reason code. Track retries, repeated abstentions, human acceptance time, unresolved age and the proportion of handbacks that end in a human decision versus new evidence and a rerun.

Most important, monitor **action after non-decision**. The expected number is zero unless a route explicitly permits a bounded action. Alert when an `abstain`, `blocked` or `error` state is followed by a tool call, queue mutation, message release, account change or facility command outside that route.

Also track silent fall-through: a task marked complete even though no decision or accepted handback exists. A low model-error rate can coexist with a high orchestration-risk rate if the application hides non-decisions behind defaults.

## Test the route before production

Build a release matrix that deliberately produces each state. Include missing records, conflicting timestamps, ambiguous facility identity, stale evidence, unsupported decision classes, policy blocks, malformed JSON, schema mismatch, tool timeout, truncated output and provider error.

For every case, verify:

1. the response class is correct;
2. the original provider event is preserved;
3. no default decision value appears;
4. the configured route is selected;
5. no unauthorized action is attempted;
6. the handback packet is complete;
7. retry behavior matches the reason code; and
8. the trace can reproduce the transition from request to final operating state.

Repeat the matrix after changes to the model, prompt, schema, toolset, parser, route table, database defaults or action service. An unchanged model does not mean abstention behavior is unchanged.

## A fictional self-storage example

The following scenario is entirely fictional.

Cedar Meridian Storage operates eight fictional facilities. An AI workflow reviews after-hours access exceptions and may draft an internal recommendation, but it is not authorized to change access or send customer messages.

For fictional facility `FIC-CMS-07`, the gate-controller record shows a recent heartbeat while a maintenance work order says the vehicle gate is locked out. The customer ticket lacks an entrance identifier. The model returns `abstain` with reason `conflicting_asset_state` and identifies the missing entrance evidence.

The first test run fails. A legacy parser converts the absent `availability` value to `false`, creates an outage recommendation and marks the AI task complete. No facility command or customer message is executed, but the route is still rejected because the workflow manufactured a decision and concealed the handback.

After the parser and route contract are corrected, the same fictional packet produces a hold, a named facilities-operations handback and an explicit action ceiling of `draft_only`. The operator must resolve the asset identity and record an independent decision. The example claims no real deployment, customer, facility, performance result or risk reduction.

## The practical tool

The companion **AI Abstention Route and Default-Action Test** gives each decision class a response contract and each test case a traceable expected route. Use it to find the places where a responsible refusal can be turned into an unintended action.

The goal is not to maximize abstention or eliminate automation. It is to make non-decision behavior deliberate. A model that knows when not to decide is useful only when the surrounding system knows what not to do next.

<!-- BODY END -->

## Sources and limits

[^1]: Yonatan Geifman and Ran El-Yaniv, [“SelectiveNet: A Deep Neural Network with an Integrated Reject Option”](https://proceedings.mlr.press/v97/geifman19a.html), Proceedings of Machine Learning Research 97 (2019). Primary research on selective prediction and risk-coverage tradeoffs; not evidence that a particular production model or self-storage workflow is safe.
[^2]: OpenTelemetry, [GenAI semantic conventions attribute registry](https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/) and [current GenAI semantic-conventions repository](https://github.com/open-telemetry/semantic-conventions-genai). Observability references for model, response and finish-reason metadata; they do not define business abstention semantics or action authority.
[^3]: National Institute of Standards and Technology, [Artificial Intelligence Risk Management Framework 1.0](https://doi.org/10.6028/NIST.AI.100-1). Voluntary, cross-sector risk-management framework; not a self-storage standard or certification.
[^4]: National Institute of Standards and Technology, [Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile](https://doi.org/10.6028/NIST.AI.600-1). Cross-sector profile with suggested risk-management actions; not a prescriptive abstention-routing design or proof of compliance.

## Assistance and claim disclosure

AI assistance supported source discovery, drafting, tool construction and editorial QA under human direction and review. No customer, deployment, partnership, product entitlement, performance, revenue, occupancy, adoption, certification, award or recognition claim is made. Cedar Meridian Storage and every example identifier, record, decision and result are explicitly fictional.

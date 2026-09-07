# The Alias Is Not the Model: Prove Which AI Runtime Touched Facility Work

**By Jared Mastroianni**  
Chief Operating Officer of modSTORAGE; CEO and Founder of Facily.ai

<!-- BODY START -->

An AI workflow can keep the same name while the system answering underneath it changes.

The application may still call `operations-assistant`. The screen may still show the same icon. Yet a model alias may have been reassigned, a router may have selected another provider, a fallback may have activated after a timeout, or a vendor may have served a different model revision. If the workflow records only the friendly name, the operator cannot establish which runtime produced the recommendation.

That is not merely a technical inventory problem. It is a decision-authority problem.

Suppose an AI-supported maintenance workflow may summarize open items, rank follow-up work and hand uncertain cases to a regional operator. The team tested those behaviors against one model version. If another model silently replaces it, the interface contract may remain valid while the operating behavior changes. The new runtime may interpret “no technician confirmation” as unresolved, resolved or not worth mentioning. Each output can be polished. Only one preserves the intended operating boundary.

Responsible architecture therefore needs a runtime-identity control: compare the model requested with the model actually reported, bind that identity to the complete decision packet, and reduce authority when the resolved runtime cannot be proved.

## A stable name is useful, but it is not evidence

Aliases and routers solve real engineering problems. They keep application code from depending on every provider or version change. They allow controlled traffic shifts and simplify rollback. The problem begins when teams mistake that useful indirection for a fixed identity.

MLflow's current Model Registry documentation makes the distinction concrete. A model alias can be reassigned to another version independently of production code, and the next execution that resolves the alias can receive the new version.[^4] That is a feature. It is also why an alias must be governed as a mutable pointer.

Write down three identities for every consequential inference:

1. **Requested identity:** the provider, endpoint and alias or model name the application asked for.
2. **Resolved identity:** the provider-reported model, snapshot, deployment, variant or serving revision that actually answered, when the service exposes it.
3. **Approved identity:** the exact runtime or bounded family currently eligible for that task, consequence class and authority mode.

If those identities do not align, the workflow has a runtime mismatch. It should not hide that mismatch behind the same application label.

Some providers will expose only part of the resolved identity. Record that limitation rather than filling the field from configuration. A configured route shows what should have happened. A response attribute, provider receipt or serving trace shows what the system reports did happen. Neither alone proves that the output is correct, but collapsing them destroys the ability to investigate change.

## Pin the operating contract around the model

The runtime is only one component in an AI-assisted decision. A defensible comparison keeps the rest of the operating contract fixed or records every intentional difference:

- task and consequence class;
- facility and work-object identity rules;
- input fields and source eligibility;
- prompt and system-instruction version;
- retrieval build and context window;
- tool definitions and output schema;
- policy version and prohibited actions;
- human-review and handback triggers;
- latency and freshness limits; and
- required readback after any authorized action.

This is where model documentation helps but does not finish the job. The model-cards research proposed documenting intended use, evaluation conditions and performance characteristics so a model is not assumed suitable outside the contexts in which it was evaluated.[^3] A self-storage operator still has to translate that general discipline into its own task: which records were used, what errors matter, which facilities or operating conditions were represented, and what the workflow is allowed to do.

Do not define equivalence as identical prose. Two models can word a safe recommendation differently. Define it as preservation of the operating contract.

For a maintenance-priority workflow, the substitution test might require both runtimes to:

- preserve every unresolved source record;
- keep a missing facility or asset identity visible;
- distinguish observed condition from inferred priority;
- return `unknown` when required evidence is absent;
- produce tool arguments that pass deterministic validation;
- refrain from creating or closing work without separate authority; and
- hand back the same high-consequence cases to qualified people.

An overall quality score cannot substitute for those floors. A candidate that improves average categorization but suppresses one critical handback class has not preserved the operating contract.

## Validate structure, then evaluate meaning

Schema validation belongs at the model boundary. JSON Schema 2020-12 provides a vocabulary for describing and validating the structure of JSON instances.[^5] Use it to reject missing identifiers, illegal states, unexpected fields and malformed tool arguments before an output reaches policy or execution services.

Then be precise about what a schema pass means. A record can be structurally valid and operationally wrong. It may name the wrong facility, cite a stale source, infer a condition that was never observed or choose `complete` where the governing system still says `open`.

The substitution gate therefore needs two layers:

**Deterministic conformance.** Validate the envelope, required fields, enumerations, tool arguments, policy inputs, identifiers and prohibited states. These checks should produce reproducible pass or fail evidence.

**Behavioral evaluation.** Compare the baseline and candidate across approved cases, edge cases and known failure families. Evaluate task completion, unsupported assertions, unknown-state handling, handback, source use, tool selection, latency and any error categories material to the workflow.

The National Institute of Standards and Technology describes its AI Risk Management Framework as voluntary guidance for incorporating trustworthiness considerations into AI design, development, use and evaluation; NIST also says version 1.0 is being revised.[^1] The framework does not certify a model or define a self-storage release test. It supports the broader requirement to make evaluation, monitoring and risk treatment explicit instead of assuming that a successful API call is a safe operating result.

## Use shadow traffic to see real conditions without granting authority

Offline cases are necessary, but they rarely reproduce the full shape of live work: sparse notes, uneven facility identifiers, unusual schedules, seasonal patterns, incomplete integrations and the human shorthand that accumulates inside operating records.

A shadow comparison sends a copy of eligible live requests to a candidate while the current production path remains authoritative. Amazon SageMaker's official documentation describes this pattern: copied requests reach a shadow variant, but only the production variant's response is returned to the calling application.[^6] The implementation is vendor-specific, and the documented feature has endpoint exclusions. The architectural value is broader: observe candidate behavior under current traffic without allowing the candidate to influence the operation.

Shadowing still needs controls. Remove or tokenize data that the candidate is not authorized to receive. Keep retention bounded. Do not treat raw customer, payment, access or employee content as free evaluation material. Compare structured decisions and protected evidence references when possible. A shadow run should have a declared population, time window, sampling rule, owner and stop condition.

Most importantly, score disagreement by consequence. A different sentence order is noise. A changed facility identity, suppressed uncertainty, broadened tool call, missed handback or invented completion state is a release issue.

## Promote by authority mode, not only by traffic percentage

After offline and shadow evaluation, a candidate may be eligible for limited live use. Infrastructure platforms support gradual traffic shifts and rollback. AWS documents canary and linear deployment modes, alarm windows and rollback safeguards for supported SageMaker endpoints.[^7] Those controls can limit technical exposure. They do not decide what operating authority the candidate deserves.

Release in authority stages:

1. **Observe only:** candidate output is retained for evaluation and never shown as an operating recommendation.
2. **Draft only:** candidate may prepare a summary, but a person must rebuild or verify the decision from governing records.
3. **Recommend:** candidate may produce a bounded recommendation with sources and unknowns visible.
4. **Propose tool input:** candidate may draft structured arguments, but deterministic policy and a named approval gate remain required.
5. **Execute within scope:** allowed only for explicitly qualified, reversible, low-consequence actions with independent readback and a proved stop path.

A model can advance through traffic stages without advancing through authority stages. Ten percent of live requests is not automatically low risk if that ten percent can change access, customer communication, money or unit availability.

Promotion criteria should be task-specific. Require zero prohibited-action attempts, complete runtime identity where the provider supports it, no critical handback regressions, acceptable latency and an independently approved comparison. If the candidate misses a floor, keep the baseline active or reduce the workflow to a safer mode.

## Record the runtime at the moment of decision

The system needs more than a deployment spreadsheet. Each inference should emit a compact runtime receipt linked to the decision or recommendation it helped produce.

OpenTelemetry's current generative-AI semantic-conventions project distinguishes the model name requested from the model name reported as having generated the response.[^8] The work is explicitly marked as under development, so treat it as an evolving telemetry reference, not a fixed business-control standard. The separation is still valuable.

A practical runtime receipt should contain:

- request, trace and decision identifiers;
- requested provider, endpoint and model alias;
- reported provider, model and serving revision when available;
- task, prompt, retrieval, tool-schema and policy versions;
- evaluation-suite version and eligible authority mode;
- fallback or routing reason;
- release state and traffic cohort;
- stop condition and rollback target; and
- protected evidence reference plus governing readback.

Avoid logging sensitive prompts and responses merely because telemetry supports them. Store approved hashes, classifications and controlled references when full content is not necessary. The goal is reconstructability, not indiscriminate retention.

If the response does not disclose a usable model identity, set `resolved_identity_state=unavailable`. The workflow may still be suitable for low-consequence drafting, depending on policy, but it should not claim exact runtime provenance. For higher-consequence work, the absence may require handback or a provider route that offers the evidence the operator needs.

## Treat automatic fallback as a new eligibility decision

Fallback is where many runtime controls disappear. A primary call times out, so the router sends the same packet to another model. The customer sees a response, the uptime chart stays green and the substitution never reaches a release meeting.

Design the fallback matrix before the outage. For every task and consequence class, name the permitted alternate runtime and its maximum authority mode. If the approved substitute is unavailable, degrade the function. Return a source list without a recommendation, save a draft without sending it, route the case to a person, or mark the decision pending. Availability is not a license to widen authority.

Do not reuse approval across a hidden substitution. If a person approved a specific proposal generated from a bound packet, a later retry under another runtime should create a new proposal identity. Material change invalidates the prior approval.

## A fictional runtime mismatch

Copper Vale Storage is entirely fictional. Every facility, model, system, person, record, time, test and outcome in this example is invented for instruction and does not describe modSTORAGE, Facily.ai or a deployment.

In the fictional portfolio, an AI-assisted workflow reviews maintenance notes and proposes one of three states: `monitor`, `qualified_review` or `operating_restriction_review`. It cannot create, close or modify a work order.

The application requests the alias `maintenance-triage`. The approved mapping points to `model-candidate-17`, which passed the current evaluation suite and is eligible for recommendation mode. During a provider disruption, the router sends one request to `model-general-9`. The response is valid JSON and arrives within the latency target. It classifies a note as `monitor`.

The runtime receipt shows the mismatch. The fictional note contains a roll-up-door observation with no unit identifier and no technician finding. The approved candidate was tested to return `qualified_review` when either identity or qualified evidence is missing. The fallback model was approved only for draft summaries.

The workflow does not publish the recommendation. It records `resolved_runtime_not_eligible`, hands the note to the operating owner and keeps the governing work-order state unchanged. The incident owner removes the fallback from that route, adds the failure case to the evaluation suite and reviews other requests served during the same interval.

Nothing in that sequence proves a real failure or a better model. It demonstrates the control: correct structure and fast response did not compensate for an ineligible runtime.

## Close the substitution as an operating change

NIST's 2026 report on post-deployment AI monitoring notes that predeployment evaluations cannot account for all real-world dynamics and organizes monitoring across functionality, operations, human factors, security, compliance and large-scale impacts.[^2] It also describes the field's best practices and terminology as still developing. That is a useful warning against treating release approval as permanent proof.

After promotion, monitor the actual resolved-runtime population, not only the configured alias. Compare behavior by task, facility cohort, consequence class and authority mode. Watch unknown and handback rates, schema failures, tool-argument rejections, critical disagreement, latency, fallback use and runtime mismatches. Reopen the gate when the model, provider, router, prompt, retrieval build, tool schema, policy or operating population materially changes.

The engineering principle is straightforward: an alias can route work, but it cannot prove who did the work. Preserve the requested identity, capture the resolved identity, compare both with the approved identity and bind the result to the operating record.

The model does not earn authority from its name. It earns a bounded role from current evidence.

<!-- BODY END -->

---

## References

[^1]: National Institute of Standards and Technology, “AI Risk Management Framework,” accessed September 6, 2026.
[^2]: National Institute of Standards and Technology, *Challenges to the Monitoring of Deployed AI Systems*, NIST AI 800-4, March 2026, accessed September 6, 2026.
[^3]: Margaret Mitchell et al., “Model Cards for Model Reporting,” FAT* 2019, Google Research publication page, accessed September 6, 2026.
[^4]: MLflow, “Model Registry Workflows,” accessed September 6, 2026.
[^5]: JSON Schema, “A Media Type for Describing JSON Documents,” Draft 2020-12 Core, accessed September 6, 2026.
[^6]: Amazon Web Services, “Shadow Tests — Amazon SageMaker AI,” accessed September 6, 2026.
[^7]: Amazon Web Services, “Deployment Guardrails for Updating Models in Production — Amazon SageMaker AI,” accessed September 6, 2026.
[^8]: OpenTelemetry, “Generative AI Spans,” commit `94f432d7126f5884d30a2cdde6f4e89908ebb6fd`, accessed September 6, 2026.

## Assistance and claim disclosure

AI assistance supported research synthesis, drafting and editorial QA. The runtime-identity method, fictional scenario and companion receipt are editorial proposals, not evidence of a product feature, deployed system, customer result or industry standard. All Copper Vale Storage details are fictional.

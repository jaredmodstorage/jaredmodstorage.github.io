# The AI Raised No Alert. Was Everything Normal?

## Govern the silent side of automated decisions with decision coverage, negative sampling, and proof of execution

**By Jared Mastroianni**

<!-- BODY START -->

An AI-assisted operations system produces three maintenance alerts on Monday. The team reviews them, confirms two, and closes one as a false positive. The dashboard looks healthy because every visible alert has an owner.

But what happened to the 417 records that produced no alert?

Some may have been correctly classified as normal. Some may have fallen below a threshold. Some may have lacked enough evidence and should have been marked unresolved. Others may never have reached the model because a facility feed was stale, an identifier failed to join, a scheduled job stopped, or a result disappeared between inference and notification.

An empty alert queue is not evidence of a healthy facility. It is not even proof that the system evaluated the expected population.

Responsible AI architecture has to govern the silent side of the decision boundary. Operators need to know which cases were eligible, which were received, which were evaluated, what no-alert state each one entered, and whether a sample of those negative decisions holds up against operating evidence. Without that chain, teams observe the system only when it speaks.

## “No alert” is not one outcome

The interface may show nothing, but the architecture should preserve a reason. At minimum, distinguish these states:

**Evaluated negative:** The system received a complete, eligible record and determined that no alert was warranted under a named model, rule, threshold, and policy version.

**Below threshold:** A score or condition was computed, but it did not cross the release boundary. This is not the same as normal, especially when the threshold is an operating choice rather than a statement of truth.

**Abstained:** The system recognized that the evidence was missing, conflicting, outside scope, or otherwise insufficient. An abstention may require human review; hiding it as no alert defeats the safety mechanism.

**Suppressed:** A rule, maintenance window, deduplication process, rate limit, or policy intentionally prevented delivery. The underlying decision and the suppression need separate records and expiration rules.

**Not eligible:** The case was outside the declared population. That may be correct, but the eligibility rule and excluded count must be visible.

**Not evaluated:** The record was expected but did not complete inference. Causes can include unavailable input, failed identity resolution, timeout, service error, queue loss, or an unprocessed retry.

**Evaluated but not delivered:** The system produced an alert-worthy result, but the downstream notification, case creation, or routing step failed.

These states have different owners and consequences. A model owner can investigate evaluated negatives. A data owner may need to resolve stale inputs. A workflow owner may need to repair delivery. A policy owner decides whether abstentions or near-threshold cases require review. One “no alert” bucket obscures all four responsibilities.

## Start with the expected population

You cannot measure silent decisions from the outputs alone. Begin with a bounded population contract.

For each operating cycle, define the facilities, assets, events, records, and time window expected to be eligible. Record the authoritative source of that expectation. Then reconcile the population through each stage:

`expected → received → identity-resolved → eligible → evaluated → dispositioned → delivered when required`

Every transition needs a count and a traceable exception population. If 420 asset-status records were expected and 417 were evaluated, the three missing records do not belong in the negative class. They are coverage exceptions until resolved.

The denominator matters more than the alert count. Ten alerts out of 500 completed evaluations means something different from ten alerts out of an unknown population. A 99% “normal” rate is meaningless if the system silently excluded one facility or skipped records with missing sensor values.

This is where facility identity becomes an AI safety control. A record that cannot be joined confidently to the intended property, asset, unit, customer, or time window should not be converted into a silent negative. Preserve the unresolved identity and route it according to consequence. The model cannot determine that an unidentified facility condition is normal.

## Trace execution without mistaking telemetry for truth

A request trace can show whether work moved through an application. It cannot, by itself, prove that the underlying facility condition was correctly classified.

The OpenTelemetry tracing specification describes spans as operations within a trace and includes identifiers, parent relationships, start and end timestamps, attributes, events, and status.[^1] That structure is useful for linking intake, identity resolution, inference, policy evaluation, and delivery. It can help distinguish “no alert was produced” from “the evaluation never completed.”

Instrumentation also has limits. Sampling can omit traces. A component can report success while processing the wrong population. A completed inference span does not prove source freshness, label correctness, or safe policy. Telemetry should establish execution evidence, then be reconciled with authoritative source counts and sampled operating review.

For each evaluated case, preserve a compact decision receipt: case identity, input snapshot reference, source freshness, eligibility decision, model and prompt version, rule and threshold version, output class, no-alert reason, policy result, and final delivery state. Do not store unnecessary customer or access data merely to make the trace richer. Use references and governed access where sensitive records are involved.

NIST's AI Risk Management Framework treats risk management as continuous across the lifecycle. Its Core calls for monitoring, documented human oversight, testing during operation, measurement with uncertainty, and post-deployment processes that include user input, appeal and override, incident response, recovery, and change management.[^2] The framework is voluntary and not a self-storage procedure. The transferable principle is that deployed behavior must remain observable and reviewable, including behavior that produces no visible action.

## Audit the negatives, not only the mistakes that announce themselves

The negative population is usually too large for complete manual review. Sampling makes it governable, provided the sample is designed around risk rather than convenience.

A useful review combines several slices:

- a random sample of evaluated negatives from the full eligible population;
- every abstention and every unresolved identity;
- near-threshold cases on both sides of the decision boundary;
- facilities, asset types, languages, or operating contexts with low volume or sparse evidence;
- cases processed immediately after model, prompt, retrieval, threshold, or source changes;
- periods with unusual input volume, latency, stale-source rates, or delivery failures; and
- a set of known sentinel cases that should reliably produce defined outcomes.

The sample should be compared with independent evidence available under authorized access. That may include a completed technician inspection, a verified work order, a current source-system record, or a later observed condition. Reviewer opinion alone is not automatically ground truth. Record the evidence, time, task definition, reviewer authority, and whether the case was actually scorable.

Do not use only discovered failures as the denominator. Report reviewed negatives, confirmed negatives, missed conditions, unscorable cases, source defects, policy disagreements, and delivery defects separately. A missed-condition rate based on 12 hand-picked complaints cannot be represented as performance across the silent population.

## Use sentinels to prove the path is alive

Negative sampling asks whether quiet decisions were reasonable. Sentinel cases ask whether the end-to-end path can still produce the outcomes it is supposed to produce.

A sentinel is a controlled, non-consequential test input or replay whose expected handling is defined in advance. One may confirm a normal negative. Another may require abstention because a critical field is missing. A third may require an alert to reach a test destination. The set should exercise identity, freshness, inference, policy, and delivery without creating real customer communications, changing access, dispatching a vendor, or altering a production facility record.

Sentinels need their own governance. They must be clearly marked, excluded from operational performance counts, prevented from triggering consequential actions, and refreshed when the system changes. A sentinel that uses a privileged shortcut may prove only that the shortcut works. A realistic test follows the same governed path as the production population while remaining isolated from real-world consequences.

Passing sentinels does not prove that all production decisions are correct. It provides bounded evidence that key paths are reachable and that known failure modes still receive the expected treatment. Pair it with population reconciliation and negative review.

## A fully fictional portfolio example

Consider a fictional operator, Cedar Lantern Storage. The company, facilities, assets, systems, data, events, and outcomes in this example are invented.

Its fictional AI-assisted maintenance workflow is expected to review 600 daily equipment-status records across six facilities. On one day, the dashboard shows four alerts. A superficial report says the alert rate is 0.67%.

The decision-coverage reconciliation shows a different picture. Six hundred records were expected, 594 arrived, 590 resolved to an active facility and asset, 586 were eligible, and 581 completed evaluation. Of those, four produced alerts, 568 were evaluated negatives, six were below threshold, and three abstained. One alert failed to create its test case on the first delivery attempt. Five eligible records timed out before evaluation. Four received records carried retired asset identifiers. Six expected records never arrived from one facility.

The operator does not relabel all 596 non-alert records as normal. It opens bounded coverage exceptions for the missing, unresolved, timed-out, abstained, and failed-delivery populations. It reviews a risk-stratified sample of evaluated negatives. One fictional sample record shows a later technician-confirmed issue, but the input available at inference time was stale. The case is classified as a source-freshness defect, not immediately as a model miss.

The fictional numbers do not represent a customer, deployment, benchmark, product, or performance result. They demonstrate the arithmetic required to keep silence from absorbing unresolved work.

## The AI Silent-Decision Coverage Ledger

The companion ledger creates one row for each operating cycle and, when needed, separate exception rows by facility or processing stage. It records the expected population and authoritative source, received and resolved counts, eligibility version, completed evaluations, each no-alert class, alert and delivery counts, reconciliation gap, exception owner, negative-sample plan, sentinel results, monitoring window, and release decision.

Use four final decisions:

- **Hold:** the expected population is unknown, a consequential gap is unresolved, or the path cannot be tested safely.
- **Limited:** a named facility, asset class, or workflow is excluded while a verified subset continues.
- **Observed:** the cycle reconciles, but the required negative review or observation window remains open.
- **Reconciled:** counts tie to the expected population, exceptions have bounded dispositions, sampling is complete, sentinels passed within their stated limits, and delivery evidence is accounted for.

The ledger does not certify the model, prove facility safety, or replace work orders, inspections, incident records, source-system controls, or professional judgment. It proves a narrower and essential fact: the organization can account for what the AI was expected to consider and what happened to that population.

## Silence should have a receipt

Teams naturally focus on visible alerts because those create work. The greater architectural risk may sit in the cases that appear to require nothing.

A responsible system makes silence explainable. It establishes the expected population, records every processing state, preserves versioned decision receipts, separates abstention and failure from evaluated negatives, audits a risk-based sample, exercises safe sentinels, and reconciles delivery.

Then an empty queue can be interpreted honestly. It may mean no alert was warranted. It may mean the evidence was insufficient. It may mean part of the pipeline failed. The architecture should tell the operator which one occurred before anyone calls the facility normal.

<!-- BODY END -->

## Sources

[^1]: OpenTelemetry, [*Tracing API Specification*](https://opentelemetry.io/docs/specs/otel/trace/api/), official stable specification page accessed October 13, 2026.
[^2]: National Institute of Standards and Technology, [*AI Risk Management Framework Core*](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/), official AIRC presentation of AI RMF 1.0 outcomes, accessed October 13, 2026. NIST states that AI RMF 1.0 is voluntary and is being revised.

---
title: "The Temperature Alert Says 80°F. Which Facility Calls That an Exception?"
slug: temperature-alert-threshold-contract-self-storage
author: Jared Mastroianni
canonical: https://jaredmodstorage.github.io/writing/temperature-alert-threshold-contract-self-storage/
destination: Jared Mastroianni personal authority site
publisher_owner: Master Personal Site Authority
intended_slot: 2026-11-16 midday systems
status: editorial-ready; not yet handed off or published
---

# The Temperature Alert Says 80°F. Which Facility Calls That an Exception?

A fictional portfolio dashboard shows three temperature alerts at one facility and eleven at another. The natural reaction is to ask why the second property has almost four times as many problems.

That question may be premature.

The first facility might alert when a point-in-time reading is greater than 80°F for 15 consecutive minutes. The second might alert when a 30-minute average is greater than or equal to 80°F. One rule might treat a missing reading as unknown and open a data-quality exception. The other might quietly record no alert. Both screens can display the same threshold number while describing different operating conditions.

A threshold is not just a number. It is a contract that defines what was measured, how the value was interpreted, when a boundary was crossed, and what the organization expects someone to do next. Until that contract is governed, an alert count is not a portfolio comparison. It is a collection of local rule executions that happen to share a label.

## Start with the monitored condition, not the dashboard tile

An operator should be able to trace every alert back to a plain-language monitored condition. “Temperature high” is too vague. A stronger definition would identify the facility, zone, sensor or metric, unit, sampling behavior, time window, comparator, threshold, duration requirement, clearing rule, and missing-data behavior.

This level of specificity is not technical decoration. The [OpenTelemetry metrics data model](https://opentelemetry.io/docs/specs/otel/metrics/data-model/) treats a metric’s name, data-point type, unit, resource attributes, and aggregation temporality as part of its meaning. It also distinguishes a sampled gauge value from values accumulated over a time interval. The specification is written for telemetry systems, not self-storage policy, but its lesson transfers cleanly: values that look alike can mean different things when their identity or time basis changes.

For portfolio operations, the monitored condition should answer four questions before the threshold is even discussed:

1. What physical or operating condition is represented?
2. Which source produced the observation, and when?
3. Is the value a last sample, average, maximum, count, rate, or another aggregation?
4. What does missing or stale data mean?

If those questions are unanswered, an “80” could be a current sample, a half-hour average, an already-converted value, or a stale observation carried forward from an earlier period. The dashboard may still render a clean number. The operating meaning is not clean.

## Write the rule as a sentence a manager can challenge

Every threshold rule should be readable without opening configuration code. A useful sentence structure is:

> For **[facility and zone]**, observe **[metric and unit]** from **[source]** using **[sample or aggregation method]**. Open **[exception type]** when **[comparator and threshold]** persists for **[duration]** during **[applicable hours]**. Treat missing or stale data as **[defined state]**. Clear the exception when **[clear rule]** is met. Route it to **[owner]** for **[defined action]** under **[policy and version]**.

That sentence exposes disagreements early. A regional operator may learn that one facility uses `>` while another uses `>=`. An integration owner may discover that one vendor reports Celsius and another reports Fahrenheit. A manager may point out that a rule applies to a mechanical room, not the customer corridor represented on the dashboard. None of those details belongs in an invisible footnote.

The rule also needs an explicit state for unavailable evidence. “No alert” and “no observation” are not synonyms. A system that cannot receive a current reading has not established a normal condition. It has established a visibility problem. The correct response may be a data-quality exception, a bounded operating hold, a maintenance check, or another policy-defined action. The system should not improvise that response.

## Separate the threshold from the response

A threshold crossing is evidence that a defined rule evaluated as true. It is not, by itself, a diagnosis of equipment failure, a statement about customer property, or authorization for a customer message.

That separation matters because the same observation can produce different authorized actions. A rule may create a review task. A different rule may page an on-call employee. Another may require a manager to compare an independent observation before escalating. The action depends on the facility’s policy, applicable agreements, equipment design, safety procedures, and local operating context.

[NIST Special Publication 800-53 Revision 5](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final) provides a useful governance analogy in its system-monitoring control: organizations define monitoring objectives, analyze events and anomalies, adjust monitoring when risk changes, and provide monitoring information to defined people or roles. It is a cybersecurity control catalog, not a facilities rulebook. Its relevant point is organizational: monitoring only becomes actionable when objectives, analysis, adjustment, and recipients are defined.

For a self-storage portfolio, the threshold contract should therefore carry two different statements:

- **Detection statement:** what evidence causes the exception to open, remain open, and clear.
- **Authority statement:** what the assigned person may review, record, communicate, dispatch, change, or escalate.

This prevents a dashboard from turning a calculated condition into an unearned fact. “Rule TEMP-07 evaluated true” is precise. “The climate system failed” is a diagnosis that may require inspection. “Customer property is at risk” is a further claim that the alert alone does not establish.

## Treat local variation as governed data

Portfolio standardization does not require pretending every property is identical. Equipment, sensor placement, building design, agreements, operating hours, and local requirements can create legitimate differences. The goal is to make those differences visible and reviewable.

A local exception should have its own identifier, reason, owner, approval, effective time, review date, and expiration or renewal decision. It should link to the portfolio rule it modifies. The dashboard can then show three honest categories:

- facilities on the current portfolio rule;
- facilities on an approved local variation; and
- facilities whose rule state is missing, expired, or unresolved.

Without those categories, a portfolio average can combine unlike definitions and reward the facility with the quietest configuration. A site with zero alerts may have operated within bounds, lost its data feed, used a longer duration, or disabled the route. Those are materially different states.

## Govern changes at the effective time

Threshold changes are operational changes. They need a version, an owner, an effective timestamp, a reason, a test, and a rollback path. Editing “80” to “82” in a console is not enough.

The retained record should show the previous contract and the new contract side by side. It should identify which facilities and zones are affected, whether historical reports will preserve the old interpretation, and how downstream queues will distinguish exceptions opened under each version. If the same alert remains open through the cutover, the system needs a deliberate decision: keep it under the original contract, reevaluate it under the new contract, or close and reopen it with a visible lineage. Silent reinterpretation destroys the audit trail.

[NIST Special Publication 800-137](https://csrc.nist.gov/pubs/sp/800/137/final) describes continuous monitoring as a strategy that supplies ongoing visibility and information for timely risk response. The publication is security-focused and dates to 2011, so it does not establish modern facility thresholds. It does reinforce a durable operating principle: monitoring frequency, metrics, assessment, and response should belong to an organization-wide strategy rather than a collection of disconnected tools.

Before activation, test the proposed rule against known cases. Include a value just below the boundary, exactly at the boundary, just above it, a short spike, a sustained condition, a missing reading, a stale reading, a unit conversion, and a clock change. Then run the new version in shadow mode when the system allows it. Compare what it would have opened, suppressed, cleared, and routed without treating the shadow result as a live operating fact.

Activation is complete only after readback. Confirm that the deployed rule matches the approved contract, the intended facilities received it, the downstream queue received a test event, the assigned owner could see the necessary context, and the rollback method remains available.

## A fictional example: the same number, two different rules

Consider **Ironwood Reach Storage**, a fictional six-facility portfolio created only to illustrate the method.

Two facilities display an 80°F threshold. At Facility North, the source is a Fahrenheit gauge sampled every minute. The rule opens when the latest observations remain greater than 80°F for 15 consecutive minutes. Missing data after five minutes opens a separate visibility exception. The alert clears after the value remains at or below 78°F for 20 minutes.

At Facility South, the source arrives in Celsius and is converted before display. The rule evaluates a rolling 30-minute average, opens at greater than or equal to 80°F after a five-minute debounce, and records missing observations as unknown without yet routing a visibility task. It clears when the rolling average falls below 80°F.

Neither rule is presented as appropriate for a real facility. The example does not establish a recommended temperature, equipment behavior, customer impact, or compliance requirement. It shows why the displayed number cannot support a fair comparison. Facility South may generate more alerts because of the inclusive comparator, fewer because of its averaging window, or an apparently clean period because missing-data handling is incomplete. The count alone cannot tell us which.

Once both rules are entered in a **Portfolio Threshold Definition and Change Contract**, the operator can compare definitions before comparing outcomes. If leadership chooses a common portfolio rule, the record preserves the decision, testing, effective time, local variations, and readback. If variation remains appropriate, reporting can group facilities by compatible rule versions instead of blending them.

## The portfolio metric begins after the contract

Alert counts can become useful. Operators can examine open duration, acknowledgment time, repeat conditions, data-quality exceptions, routing failures, and resolution evidence. But those measures begin after the underlying threshold contracts are comparable.

The practical sequence is straightforward:

1. Inventory every active rule and its actual deployed configuration.
2. Translate each rule into a readable monitored-condition sentence.
3. Reconcile metric identity, unit, time basis, comparator, duration, clearing, and missing-data behavior.
4. Record approved local variations instead of hiding them.
5. Version, test, activate, read back, and reconcile every change.
6. Compare facilities only within compatible definitions, and disclose exclusions.

An operator should never have to guess what an alert count includes. The portfolio does not gain control by forcing every property to display the same number. It gains control by making the meaning behind that number explicit, owned, testable, and recoverable.

That is the difference between a dashboard threshold and an operating contract.

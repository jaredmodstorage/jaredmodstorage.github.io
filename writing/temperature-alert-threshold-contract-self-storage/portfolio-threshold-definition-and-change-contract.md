# Portfolio Threshold Definition and Change Contract

Use one row per facility, zone, metric, and rule version. Do not treat an empty field as “not applicable” unless the governing policy explicitly says so.

## Definition block

| Field | Required record |
|---|---|
| Contract ID | Stable identifier for this threshold contract |
| Facility and zone | Canonical facility ID and exact physical or logical scope |
| Monitored condition | Plain-language description of the condition being observed |
| Source identity | Source system, sensor or metric ID, and logical writer |
| Metric semantics | Metric name, data type, unit, and time basis |
| Calculation | Sample, average, maximum, count, rate, or other defined method |
| Observation window | Exact time window and timezone behavior |
| Trigger | Comparator, threshold value, duration, and debounce |
| Clear rule | Comparator, value, duration, and any hysteresis |
| Data gaps | Missing-data state and stale-data limit |
| Applicability | Hours, facility/zone scope, and exclusions |

## Governance block

| Field | Required record |
|---|---|
| Policy lineage | Policy ID, version, prior version, and effective time |
| Local variation | Variation ID, reason, approver, review date, and expiration |
| Detection statement | What opens, holds, and clears the exception |
| Authority statement | What the recipient may review, record, communicate, dispatch, change, or escalate |
| Owner and route | Primary owner, escalation owner, queue, and service expectation |
| Test set | Below/equal/above boundary, spike, sustained, missing, stale, conversion, and clock tests |
| Shadow comparison | What the proposed rule would open, suppress, clear, and route |
| Activation readback | Deployed value, scope, version, effective time, and destination confirmation |
| Rollback | Exact restoration method and retained prior configuration |
| Reconciliation | Confirmed, exception, unknown, or not yet tested, with evidence link |

## Readable rule sentence

> For **[facility and zone]**, observe **[metric and unit]** from **[source]** using **[sample or aggregation method]**. Open **[exception type]** when **[comparator and threshold]** persists for **[duration]** during **[applicable hours]**. Treat missing or stale data as **[defined state]**. Clear the exception when **[clear rule]** is met. Route it to **[owner]** for **[defined action]** under **[policy and version]**.

## Activation gate

- [ ] Source identity and unit verified against actual telemetry.
- [ ] Sample/aggregation method and time window verified.
- [ ] Comparator, boundary behavior, duration, debounce, and clear rule tested.
- [ ] Missing and stale data produce the approved state.
- [ ] Local variation is approved and time-bounded, if applicable.
- [ ] Detection statement is separate from diagnosis and authority.
- [ ] Shadow comparison reviewed without treating it as live fact.
- [ ] Deployed rule read back from every intended facility and zone.
- [ ] Test event reached the correct queue with usable context.
- [ ] Previous version and rollback method remain available.
- [ ] Historical reporting preserves rule-version lineage.

This is an operator governance template, not an environmental, engineering, safety, legal, insurance, or equipment standard. Threshold values and responses must be established from the facility’s actual equipment, agreements, policies, applicable requirements, and qualified technical guidance.

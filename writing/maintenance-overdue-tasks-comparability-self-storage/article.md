# Fourteen Tasks Are Overdue. Are the Facilities Actually Comparable?

## A defensible maintenance comparison starts with the asset, governing basis, trigger, and evidence—not the red number on a dashboard

By Jared Mastroianni

<!-- BODY START -->

A portfolio report shows fourteen overdue preventive-maintenance tasks at one self-storage facility and three at another. The easy conclusion is that the first manager is losing control of maintenance.

That conclusion may be right. It is not yet supported.

An overdue count is not an observed property of a facility. It is a derived state produced by several records: which assets are in scope, which maintenance basis governs each asset, what event starts the clock, what qualifies as completion, whether an approved exception is active, and when the source systems were read. If those records differ, the same red label can mean different things.

Portfolio leadership still needs a comparison. The answer is not to stop measuring. It is to make the measurement auditable before using it to rank facilities, allocate capital, or judge managers.

## “Overdue” is the end of a calculation

Consider a gate operator inspected every ninety calendar days, an HVAC unit serviced according to seasonal work, a vehicle gate checked after a cycle threshold, and a fire-protection component governed by a qualified provider's plan. They are all “maintenance,” but they do not share one clock, one completion rule, or one decision authority.

The U.S. Department of Energy's Federal Energy Management Program distinguishes reactive, preventive or time-based, predictive, and reliability-centered approaches. Its guidance also says a program should be optimized to the site, building, and equipment. That matters because a portfolio cannot create comparability by forcing every asset into one calendar interval. A common label does not create a common maintenance basis.

At minimum, an overdue result requires six questions to have stable answers:

1. Which exact installed asset is being evaluated?
2. Which approved maintenance instruction or plan version applies?
3. Is the trigger based on calendar time, usage, condition, an event, or a combination?
4. What was the last qualifying completion—not merely the last ticket closure?
5. Is an approved exception, deferral, or out-of-service state active?
6. At what timestamp and from which system was the result calculated?

If any answer is missing, the honest state may be **unknown** or **not yet comparable**, not overdue and not compliant.

## Start with the asset denominator

Most misleading maintenance comparisons begin before the due date is calculated. One facility has every gate, keypad, camera, HVAC unit, elevator, pump, door, and life-safety component represented as a distinct installed asset. Another has generic rows such as “gate,” “HVAC,” and “cameras.” A third includes retired equipment alongside active equipment.

If the denominator is unstable, a count of overdue work is unstable too.

The portfolio record should identify the facility, asset class, installed instance, location, operating state, and source identifier. Replacement matters. If a motor is replaced, the history of the retired motor should remain intact, while the new motor receives a new installed-instance identity and its own governing basis. Renaming the row and carrying the old schedule forward destroys the evidence trail.

This is not clerical neatness. It determines whether leaders are comparing fourteen overdue tasks across forty active assets with three overdue tasks across nine partially inventoried assets.

## Bind each task to a governing basis and version

The schedule should not float as an unexplained date in a work-order system. It should point to the approved basis that produced it: a manufacturer instruction, vendor plan, code-driven program, engineering decision, insurance requirement, internal standard, or another controlled source.

The record also needs a version or effective date. When a qualified owner revises a maintenance plan, the portfolio must preserve which version governed the asset before and after the change. Recomputing old work against today's rule can make a previously on-time task appear late—or erase a miss that was real under the prior rule.

This boundary is especially important for self-storage operators because “standardize the portfolio” can be misunderstood as “give every facility the same interval.” The useful standard is the data contract: every facility records the governing basis, trigger, qualifying completion, exception, and evidence in the same structure. The underlying interval can remain asset-specific and authority-specific.

## Do not convert every trigger into a calendar date

Time-based work is only one maintenance strategy. Some tasks depend on run hours, door cycles, measured condition, seasonal readiness, an inspection finding, or a specific event. A dashboard that demands a date may silently replace those triggers with a generic monthly or quarterly recurrence.

That produces false precision. A condition-based task with no current condition reading is not necessarily overdue; its condition is unknown. A cycle-based task with no current meter reading cannot be evaluated honestly. A post-event inspection should not appear due before the triggering event exists.

FEMP's energy-management guidance discusses normalizing data from multiple systems, sending findings into computerized maintenance-management workflows, and comparing performance by device, building, or region. The useful lesson for operators is architectural: preserve the source measurement and trigger logic before producing the portfolio status. The red indicator should be reproducible from the underlying records.

## A closed ticket is not automatically a qualifying completion

Work-order closure often measures workflow completion, not maintenance completion. A ticket may be closed because a vendor visit was scheduled, an estimate was received, a duplicate was merged, the asset was inaccessible, or the issue moved to another system.

The maintenance calculation needs the last **qualifying** completion. That record should identify who performed or verified the work, which approved task was completed, when it occurred, and what evidence supports the claim. Depending on the plan, the evidence may be a service record, inspection form, meter reading, photo, invoice tied to the asset, qualified-provider report, or another controlled receipt.

The portfolio does not need the same artifact for every asset. It needs an explicit evidence rule for each task class and a clear state such as verified, pending review, insufficient, or unavailable. “Ticket closed” should never silently become “maintenance satisfied.”

## Exceptions need owners and expiration dates

A task can be intentionally deferred. An asset may be shut down, isolated, awaiting replacement, inaccessible under an approved restriction, or covered by a documented temporary operating decision. Those states should not disappear from the dashboard, but they should not be mixed with unmanaged lateness either.

An exception record should name the approving authority, reason, scope, operating restriction, start time, expiration or review time, and required next action. Expired exceptions should return to review automatically. An out-of-service label without an owner or end condition is not a control; it is a hiding place.

The reporting categories can remain simple:

- **Due state:** current, due soon, overdue, or not evaluable.
- **Evidence state:** verified, pending review, insufficient, or unavailable.
- **Exception state:** none, active, expired, or disputed.
- **Comparison state:** eligible, held, or excluded under an approved rule.

Keeping those axes separate prevents an active exception from being mistaken for completed work and prevents missing evidence from being converted into a performance failure.

## Normalize the comparison, not the maintenance plan

Once the underlying records are governed, portfolio reporting becomes more useful. Leaders can compare like with like: the percentage of eligible time-based tasks overdue, the number of usage-triggered tasks lacking current readings, the share of completions awaiting evidence review, and the count of exceptions approaching expiration.

Rates generally need denominators beside them. “Fourteen overdue” should be paired with the number of eligible tasks and the rules used to establish eligibility. A facility with fourteen overdue tasks out of 300 governed tasks is a different operating picture from one with three overdue tasks out of twelve.

The U.S. Government Accountability Office's data-reliability guidance evaluates accuracy, completeness, and applicability for the intended use. That is a useful discipline here. A dataset can be accurate as extracted yet incomplete because assets are missing, or complete within a system yet not applicable to a management comparison because facilities use different unrecorded rules.

The release state should therefore be explicit:

- **Draft:** the calculation has run, but source or evidence checks remain.
- **Held:** a known gap prevents comparison.
- **Released:** the comparison owner verified the required fields and declared the intended use.
- **Superseded:** a later source correction or rule version replaced the result without erasing it.

## The operator tool: Portfolio Preventive-Maintenance Comparability Ledger

The companion ledger turns this method into a repeatable review. Each row connects an installed asset to its governing basis, trigger, last qualifying completion, next due threshold, evidence state, exception, eligibility decision, source timestamps, and accountable next action.

Use it in five passes:

1. **Establish scope.** Reconcile active installed assets to the facility inventory. Hold records with ambiguous or retired identities.
2. **Validate the rule.** Link each task to an approved basis and version. Do not invent an interval to fill a blank.
3. **Reproduce the due state.** Retain the trigger, current reading or event, last qualifying completion, and calculation timestamp.
4. **Resolve evidence and exceptions.** Separate workflow closure, maintenance completion, verification, and operating authorization.
5. **Release the comparison.** Declare the eligible denominator, held records, limitations, owner, and intended management use.

The blank CSV template is designed for implementation. The separate fictional teaching file demonstrates how apparently similar rows can resolve to overdue, current, unknown, or excluded without pretending those outcomes occurred at a real facility.

## A fictional four-record example

The following scenario is entirely fictional. Alder Gate Storage Group, its facilities, assets, work orders, providers, readings, people, dates, and results do not represent an actual company or deployment.

A portfolio dashboard initially labels four gate-related records overdue. The ledger review finds four different conditions.

At Alder Gate North, a calendar-based inspection is overdue under the recorded plan, and the last qualifying completion is supported. That row remains overdue and eligible.

At Alder Gate Harbor, the task is cycle-based. The dashboard had generated a calendar date, but the current cycle reading is below the approved threshold. The row becomes current, and the invented calendar recurrence is removed.

At Alder Gate Ridge, the work order says closed, but the required provider report is missing. The team cannot establish the last qualifying completion. The row becomes not evaluable and held for evidence reconciliation—not automatically overdue and not automatically current.

At Alder Gate South, the installed operator is documented out of service under a temporary restriction with an approved replacement action and expiration date. The row is excluded from the eligible denominator only under that recorded rule; the exception remains visible and time-bound.

The revised comparison contains one supported overdue task, one current task, one held unknown, and one controlled exclusion. That is not a better-looking number. It is a more truthful management record.

## What operators gain

For facility managers, the system reduces arguments over dashboard labels. A disputed task can be traced to the exact asset, plan, trigger, evidence, and exception instead of being settled by whoever has the louder spreadsheet.

For regional leaders, it separates coaching needs from data-governance defects. A manager with genuinely overdue eligible work needs an operating response. A manager with incomplete asset records needs reconciliation. A portfolio with widespread missing readings needs a system decision. Those are different problems and should not share one corrective action.

For executives, it makes capital and vendor discussions more defensible. Repeated exceptions, missing evidence, unstable asset identities, and non-evaluable tasks become visible operating risks rather than background noise inside a red count.

The goal is not to make every facility look equal. It is to make the differences interpretable. A maintenance dashboard becomes decision-grade only when another responsible person can reproduce why each task is current, due, overdue, held, or excluded.

Fourteen overdue tasks may reveal a weak maintenance program. Before reaching that conclusion, make sure fourteen means the same thing everywhere.

<!-- BODY END -->

## Sources

1. U.S. Department of Energy, Federal Energy Management Program, “Operations and Maintenance Best Practices Guide: Achieving Operational Efficiency.” https://www.energy.gov/cmei/femp/articles/operations-and-maintenance-best-practices-guide-achieving-operational-efficiency
2. U.S. Department of Energy, Federal Energy Management Program, “Operations and Maintenance Challenges and Solutions.” https://www.energy.gov/cmei/femp/operations-and-maintenance-challenges-and-solutions
3. U.S. Department of Energy, Federal Energy Management Program, “Energy Management Information System Capabilities.” https://www.energy.gov/cmei/femp/energy-management-information-system-capabilities
4. U.S. Government Accountability Office, “Assessing Data Reliability,” GAO-20-283G. https://www.gao.gov/products/gao-20-283g

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.

## Editorial disclosure

The Alder Gate Storage Group example and all associated facilities, assets, work orders, providers, readings, people, dates, decisions, restrictions, and results are fictional teaching material. The image is an AI-generated editorial illustration governed in Jared Mastroianni's image register; it is not documentary evidence of a facility, technician, employee, maintenance event, deployment, or result. This article provides an operating-system method, not equipment-specific maintenance intervals, technical diagnosis, code interpretation, safety certification, or legal advice. Operators should follow the applicable manufacturer, qualified-provider, insurer, authority, and site-specific requirements.


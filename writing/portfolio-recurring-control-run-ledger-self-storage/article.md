---
title: "The Recurring Task Fired. Which Facilities Actually Completed the Control?"
slug: "portfolio-recurring-control-run-ledger-self-storage"
author: "Jared Mastroianni"
description: "A multi-location self-storage method for turning recurring reminders into facility-scoped control runs with current evidence, verification, exception handling and honest portfolio completion rates."
canonical: "https://jaredmodstorage.github.io/writing/portfolio-recurring-control-run-ledger-self-storage/"
publication_destination: "Jared Mastroianni personal authority site"
publisher_owner: "Master Personal Site Authority"
publication_state: "publisher handoff pending"
---

# The Recurring Task Fired. Which Facilities Actually Completed the Control?

**By Jared Mastroianni**

*A portfolio conversation can expose where one site’s “complete” means something different from another’s. Editorial, non-documentary illustration; it does not depict the fictional operator, facilities, control run, test, customer event or performance result in this article.*

**Deck:** A repeating calendar item can create work, but it cannot prove the work happened. Give every due facility its own run identity, evidence requirement, verifier, exception path and final disposition before reporting portfolio completion.

<!-- BODY START -->

A recurring task appears on twelve facility calendars at 8:00 Monday morning. By Friday, the portfolio dashboard shows twelve green check marks.

That looks like control.

It may only be scheduling.

One manager checked the box after completing the work. Another attached last month’s photo. A third marked the task complete because a vendor was called. A fourth assumed the task did not apply during construction. Two facilities changed managers, and the reminder still belongs to former employees. The central team sees 100 percent completion because the task system counted twelve clicks.

Multi-location operators need to separate the **recurring-control definition** from each **control run**. The definition says what should happen, where, how often, under whose authority and with what evidence. A run is the dated obligation for one applicable facility or asset population. It has its own owner, due window, evidence, exception state, verification and disposition.

Without that separation, a recurring task becomes a factory for reassuring numbers.

## A schedule is control intent, not control evidence

A calendar entry answers a useful question: when should someone pay attention? It does not answer whether the correct work was performed, whether the full facility scope was covered, whether the evidence belongs to this period or whether a qualified person accepted the result.

That distinction matters across a portfolio because scheduling tools are optimized for reminders. Operations needs a record that can survive reassignment, late work, facility changes, failed checks and questions about the denominator.

The U.S. Government Accountability Office’s 2025 Green Book describes internal control as a process management designs, implements and operates to achieve objectives. It also separates monitoring activities from remediation of deficiencies.[^1] That federal framework is not a private self-storage requirement. The useful operating lesson is narrower: control performance, monitoring and correction are different states.

The same discipline appears in NIST’s control catalog and continuous-monitoring guidance. NIST SP 800-53 calls for organization-defined metrics and frequencies for monitoring and assessment, while NIST SP 800-137 ties monitoring frequency to the information needed for risk decisions.[^2][^3] Those publications concern information security, not facility operations. They still illustrate why “recurring” is not a sufficient control design.

## Give the definition and the run different identities

Start with one stable identifier for the control definition. It should name:

- the operating objective;
- the approved procedure or instruction version;
- the trigger or recurrence rule;
- the applicable facility, asset or role criteria;
- the required evidence;
- the person or role allowed to perform the work;
- the person or role allowed to verify it;
- the due window and time-zone rule;
- the conditions that require escalation; and
- the authority that can change, suspend or retire the control.

Then create a new run identifier for every due occurrence. A run for `FAC-014` in October is not the same object as the October run for `FAC-026`, even if both came from definition `COM-07`. It is also not the same object as `FAC-014`’s November run.

The run should inherit the approved definition, but it must freeze the version and scope used for that occurrence. If the definition changes on October 18, the record must show whether the open October run stays on the earlier version, moves to the new version or is superseded and regenerated. Quietly changing the instructions under an open task destroys the audit trail.

## Establish applicability before calculating completion

The denominator comes first.

For each recurrence, generate an expected-facility set from a governed facility register and the control’s applicability rule. Preserve the generation time, rule version and facility lifecycle state. Then resolve every addition, exclusion and unknown.

A facility should not disappear from the denominator because its manager is absent, its equipment is offline or its data is inconvenient. Those conditions may create an exception, a different evidence path or a documented not-applicable decision. They do not authorize silent exclusion.

Likewise, a facility added mid-cycle needs an explicit treatment. Depending on the organization’s approved rule, it may enter the current run, begin on the next recurrence or require a separate admission check. The method matters less than recording the decision. Backfilling a green mark after the fact hides the actual operating history.

Use at least four scope states:

- `applicable` — the facility owes a run;
- `not_applicable` — the approved rule excludes it, with a reason and authority;
- `applicability_unknown` — a source conflict or missing fact blocks the decision; and
- `superseded` — the run was formally replaced without being treated as performed.

Do not put `unknown` into the completed or excluded bucket.

## Define evidence before the work opens

If operators learn the evidence requirement after completing the task, the system invites reconstruction.

The control definition should state what a sufficient record looks like. That might include an observed value, an asset list, a test result, a timestamp, a work-order reference, a discrepancy list, a qualified service record or a manager’s signed readback. The requirement should be proportional to the consequence. A low-risk housekeeping observation does not need a thirty-field packet. A control that affects access, safety, money, customer commitments or external reporting deserves more.

Evidence also needs boundaries. A photograph can show a visible condition, but it does not prove a full asset population was reviewed. A vendor dispatch proves a request was made, not that work was completed. A closed work order proves a system state, not necessarily an observed facility outcome. A prior-period document is not current merely because its file name lacks a date.

OSHA’s safety-program guidance tells employers to define indicators, collect and review performance data, verify that programs are implemented and operating as intended, and follow up on shortcomings.[^4] The guidance applies to workplace safety and health programs; it does not set this article’s recurrence or evidence rules. It does reinforce a practical point: counting planned activities is weaker than verifying implementation.

## Use states that tell the truth

The smallest useful run model has more than `open` and `complete`.

**Planned.** The run was generated, its facility and definition version are known, and the due window has not opened.

**Open.** The facility owes the work and a current owner can act.

**Submitted.** Evidence was provided, but it has not passed the defined verification gate.

**Verified.** The evidence matches the facility, run window, expected scope and acceptance rule.

**Exception.** The normal control could not be completed as defined. The reason, consequence, temporary treatment, owner and next decision time are recorded.

**Missed.** The due window closed without verified completion or an authorized disposition. Late performance may create a new fact, but it should not rewrite the missed state.

**Not applicable.** An authorized applicability decision excludes the facility from this run.

**Superseded.** A named replacement run or control definition took over. Supersession is not completion.

These states prevent three common distortions: treating submission as acceptance, treating an exception as success and erasing a miss when someone catches up later.

## Separate performance, verification and consequence closure

Some recurring work is complete when a direct observation is recorded. Other work can reveal a condition that remains open after the control itself was performed.

Suppose a facility completes an organization-defined monthly gate-intercom call-path check and the call routes to the wrong number. The control run may be **performed** because the test occurred and the result was recorded. It is not necessarily **accepted** if required fields or scope are missing. And the discovered routing defect is not **resolved** until the assigned owner corrects it and an authorized retest or other release evidence closes the consequence.

Keep those receipts separate:

1. **Performance receipt:** who did what, when, at which facility, under which definition version.
2. **Verification receipt:** who evaluated the evidence, against what acceptance rule, with what result.
3. **Consequence record:** what exception or follow-up was created, who owns it, what boundary applies and what closes it.

A portfolio can truthfully report that all twelve facilities performed a control while three resulting deficiencies remain open. It can also report that eleven facilities verified and one missed. Those are more useful statements than a single blended completion percentage.

## Make the rollup reproducible

Every portfolio rate should display its population and state counts. At minimum, record:

- expected applicable runs;
- verified runs;
- submitted but unverified runs;
- active exceptions;
- missed runs;
- applicability unknowns;
- authorized not-applicable runs; and
- superseded runs.

Do not use every generated row as the denominator. Do not remove misses. Do not convert unknowns into zeroes or exclusions. Define whether the published rate is `verified / applicable` or another approved formula, then show the components beside it.

The dashboard should also expose aging. A submitted record waiting nine days for verification is an operating bottleneck, not a completed control. An exception without a next decision time is an unmanaged condition. A missed run reassigned after the deadline remains missed even if the new owner later performs recovery work.

## A fictional four-facility run

The following example is entirely fictional teaching material. It is not a modSTORAGE control, facility event, deployment, customer record or performance result.

Fictional Redwood Turn Storage creates run family `FIC-RUN-2026-10-COM07` for an invented, organization-defined monthly gate-intercom call-path check. The four due facilities use definition version `COM-07.3`. The fictional rule requires a current test timestamp, the called endpoint, the observed answer path, any discrepancy and an operator identity. No cadence or acceptance threshold in this example is an industry requirement.

`FIC-FAC-011` submits current evidence covering the required path. A fictional regional verifier accepts it.

`FIC-FAC-012` attaches a September screenshot to the October run. The record remains `submitted`, then moves to `exception` when the facility cannot repeat the test before the due window closes. The prior evidence is retained but not counted as October verification.

`FIC-FAC-013` performs the test and observes that the route reaches an obsolete endpoint. The run receives a performance receipt, the evidence passes verification, and a separate fictional routing-defect record remains open. Completion of the test does not claim correction of the defect.

`FIC-FAC-014` entered the fictional portfolio after the expected set was generated. An authorized applicability decision adds it to a bounded admission run rather than silently changing the original denominator.

The portfolio result is not “four of four complete.” It is one verified with no follow-up, one exception after stale evidence, one verified with an open consequence and one separately admitted. That language is less convenient and much more operationally useful.

## The operating rule

Recurring work deserves a ledger when its completion influences a portfolio decision. Define the control once. Generate a facility-scoped run each time it is due. Freeze the version and expected population. State the evidence before work begins. Keep submission, verification, exception, miss and consequence closure separate. Then publish a rollup another operator can reproduce.

A calendar can tell people when to start. Only a governed run record can show what happened.

<!-- BODY END -->

## Practical operator tool

Use the accompanying [Portfolio Recurring Control Run Ledger](portfolio-recurring-control-run-ledger.md), [blank CSV template](portfolio-recurring-control-run-template.csv) and [explicitly fictional worked example](portfolio-recurring-control-run-fictional-example.csv).

## Sources

[^1]: U.S. Government Accountability Office, [The Green Book: Standards for Internal Control in the Federal Government](https://www.gao.gov/greenbook), 2025 revision, effective beginning with fiscal year 2026; accessed October 26, 2026.
[^2]: National Institute of Standards and Technology, [SP 800-53 Rev. 5, Security and Privacy Controls for Information Systems and Organizations](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final), including current release information; accessed October 26, 2026.
[^3]: National Institute of Standards and Technology, [SP 800-137, Information Security Continuous Monitoring for Federal Information Systems and Organizations](https://csrc.nist.gov/pubs/sp/800/137/final), September 2011; accessed October 26, 2026.
[^4]: U.S. Occupational Safety and Health Administration, [Program Evaluation and Improvement](https://www.osha.gov/safety-management/program-evaluation), Recommended Practices for Safety and Health Programs; accessed October 26, 2026.

## About the author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.

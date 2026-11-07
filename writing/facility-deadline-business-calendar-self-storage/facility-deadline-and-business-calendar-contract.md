# Facility Deadline and Business Calendar Contract

Use this tool to make multi-location deadlines reproducible before comparing overdue work.

## 1. Calendar contract

For each facility and eligible work type, record:

- stable facility ID and display name;
- named IANA time zone;
- calendar ID and version;
- effective start and optional end;
- normal working days and eligible hours;
- local cutoff time;
- approved closures and special hours;
- covered work types;
- approving role and approval evidence; and
- change owner.

## 2. Clock rule

Define:

- triggering event;
- event timestamp and source;
- rule ID and version;
- before-cutoff treatment;
- after-cutoff treatment;
- duration or next-business-period rule;
- rounding rule, if any;
- pause eligibility;
- escalation when the deadline cannot be calculated; and
- prohibited uses, including emergency work that must follow another procedure.

## 3. Pause contract

A pause record requires:

- task ID;
- pause reason code;
- factual evidence;
- pause start;
- approval role;
- next-review time;
- maximum duration, if used;
- customer-facing obligations that continue;
- resume event and time; and
- original and replacement deadlines.

Keep `task_state` and `clock_state` separate. Never overwrite the original deadline.

## 4. Required edge-case tests

Run these for each material rule or calendar version:

1. one minute before cutoff;
2. one minute after cutoff;
3. weekend boundary;
4. planned closure;
5. spring-forward gap;
6. fall-back repeated hour;
7. facility without daylight-saving changes;
8. authorized pause and resume;
9. rejected pause with missing evidence; and
10. event created outside the governing facility time zone.

For each test, preserve the input, expected clock start, expected local deadline, UTC deadline, named time zone, calendar version, rule version, calculation reason and actual result.

## 5. Portfolio release gate

Mark a row `comparison_eligible` only when:

- facility identity resolves;
- event time has an explicit UTC relationship;
- named time zone is present;
- calendar and rule versions are effective;
- clock start and deadline are reproducible;
- any pause has authority and evidence;
- applicable edge tests pass; and
- the report preserves the original deadline and current deadline separately.

Use `exception` when a bounded issue has an owner and next action. Use `unknown` when a required fact is missing. Use `not_applicable` only with a recorded reason.

## 6. Review questions

- Can a reviewer reproduce the deadline from stored fields without reading application code?
- Does the local display agree with the stored UTC instant?
- Which calendar version governed the task at creation?
- Did a later calendar change rewrite history?
- Who authorized each pause?
- Are customer updates or safety actions still due while the internal clock is paused?
- Does the export preserve the same rule, time zone and deadline as the interface?
- Are unknown-calendar rows excluded from comparison but visible in coverage reporting?

This contract documents an operating method. It does not establish legal deadlines, contractual service levels, emergency-response requirements or proof that any real facility or software implementation passed the control.


# A Portfolio Standard Is Not a Facility Setting: Build a Configuration-Drift Register

One approved standard, twelve facilities and one green dashboard can still produce twelve different operating realities.

**By Jared Mastroianni**

<!-- BODY START -->

A regional manager changes the gate schedule for a holiday. A vendor replaces a controller and loads its default settings. A new property inherits the prior operator's camera-retention policy. Someone corrects a tax rule in the facility-management system but not in the online rental channel. Weeks later, the portfolio report says every site is “on standard.”

The report may be describing intent, not fact.

Multi-location operators often store the portfolio standard in a policy document, an implementation spreadsheet or a platform template. Those records matter, but none proves what is configured at a specific facility now. A standard is what the organization approved. A baseline is the versioned configuration that should apply to a defined facility and system. An observed setting is what an authorized source reported at a particular time. The effective state is what the service is actually using. Service behavior is what an approved test or operating event demonstrates.

Collapse those five things into one status and configuration drift becomes almost impossible to see.

## Treat configuration as an operating record

Configuration management is sometimes treated as an IT specialty. The operating idea is broader: establish an agreed state, control changes to it and monitor whether the current state still matches. NIST describes configuration management as a set of activities for establishing and maintaining the integrity of systems through controlled initialization, change and monitoring.[^1] Its security-focused configuration-management guide organizes the work around baselines, change control, monitoring and supporting evidence.[^2]

A self-storage portfolio can apply that discipline without pretending a federal cybersecurity publication is a facility standard. The useful translation is simple: if a setting can change customer access, a fee, a notice, a rental offer, a work-order route, a camera-retention period or a manager's authority, it deserves a named source, an approved value, an observed value and a reconciliation path.

Do not start by copying every field from every platform. Start with consequential settings. Ask which values can alter money, access, safety boundaries, customer commitments, record retention or the ability to recover from failure. A small controlled register of those settings is more useful than a giant export no one can explain.

## Keep five layers separate

The first design decision is to stop using “configured” as a complete answer. Record five layers for each consequential setting:

1. **Portfolio standard:** the approved rule, its owner, version and effective period.
2. **Facility baseline:** the value authorized for this facility, system and environment, including any approved local exception.
3. **Observed setting:** the value collected from a named source, with collection time, method and evidence.
4. **Effective state:** the value the governing service confirms it is currently enforcing.
5. **Verified behavior:** the result of an approved test or real operating readback, bounded to what that evidence can establish.

The layers may agree. They may also expose different problems.

If the standard says customer access ends at 10 p.m. but the facility baseline contains an approved 11 p.m. exception, the site is not drifting merely because it differs from the portfolio default. If the platform displays 10 p.m. while an edge controller still enforces 11 p.m., the display is not proof of effective state. If a normal test succeeds once, that does not prove the entire weekly schedule is correct. Each statement needs its own scope.

This separation protects the facility team from a familiar mistake: being blamed for “noncompliance” when the central record is stale, the provider applies a hidden default or the local variation was properly approved but never attached to the comparison.

## Define identity before calculating a difference

A diff is only meaningful when both sides describe the same thing.

The register should identify the portfolio, facility, system, environment, component and setting key. It should also preserve the provider account or tenant, configuration schema and applicable baseline version. “Gate hours” is too vague if one value controls tenant entry, another controls office access and a third belongs to a marketing listing.

Time matters too. Compare an observed value against the baseline that was effective at the observation time, not whichever standard is current when the analyst opens the report. A planned change that takes effect next Monday should not make Friday's correct setting look obsolete. An expired exception should not continue to legitimize a variance after its end time.

NIST SP 800-53's configuration-management family separates baseline configuration, change control and configuration settings, among other controls.[^3] The publication is not evidence that a self-storage operator complies with those controls. It is a useful reminder that “what should exist,” “who may change it” and “what value is set” are distinct governance questions.

## Classify the variance before touching the system

Once identity and time align, the comparison should produce a variance class—not an automatic overwrite.

Use classes such as:

- **Matched:** observed and effective values agree with the applicable baseline.
- **Approved local variation:** the difference is supported by a current exception with an owner and expiration or review condition.
- **Pending controlled change:** approval exists, but implementation or readback is incomplete.
- **Stale observation:** the collected value is too old to support a current comparison.
- **Provider-managed difference:** the provider controls the value or translation, and the portfolio lacks direct configuration authority.
- **Unexplained drift:** the effective value differs and no current authority explains it.
- **Conflict:** authoritative sources disagree about the effective state.
- **Not evaluated:** required evidence is missing or the collection method failed.

That last state matters. A failed query is not a match. A blank field is not a default. A site omitted from the export is not compliant. Reporting “not evaluated” keeps the evidence gap visible.

Automatic normalization is tempting, especially when a central platform can push one template across the portfolio. Do not let detection silently become authorization. A system may identify a possible variance, but the correction still needs scope, authority, a tested plan, a stop condition and a rollback path. The configuration may be protecting a local operating restriction that the central template does not know.

## Store the change as evidence, not just a new value

For machine-readable configuration, a precise change record can be more informative than a new full snapshot. JSON Patch, for example, defines operations including add, remove, replace, move, copy and test.[^4] A self-storage operator does not need to adopt JSON Patch to gain the design lesson: record what changed, from which known version, under whose authority and with what precondition.

A controlled change packet should name:

- the approved before and after values;
- the setting and exact facility scope;
- the current version or fingerprint expected before execution;
- the person or system authorized to act;
- the maintenance or operating window;
- the stop and rollback conditions;
- the provider receipt, if a third party performs the change;
- the governing readback after execution; and
- any dependent channels that must be reconciled.

The expected-version check is important. If the current value changed after approval, the old instruction should pause rather than overwrite the newer state. “Set it to 10” is not safe enough when the reviewer approved that change against version 17 and the site is now on version 19.

## A fictional portfolio example

The following scenario and every value in it are fictional. They do not describe a real facility, provider, deployment, result or customer.

Mariner Ridge Storage Group adopts a standard tenant-access end time of 10 p.m. local facility time. Its portfolio team reviews four invented sites.

At Mariner Ridge North, the facility baseline, controller readback and approved weekly test all show 10 p.m. The result is **matched**.

At Mariner Ridge Harbor, the controller shows 11 p.m. The facility has a current, approved event exception through Saturday night. The result is **approved local variation**, with a scheduled reversion and Sunday readback. The site is not labeled drifted simply because it differs from the default.

At Mariner Ridge Central, the management console shows 10 p.m., but the controller readback shows 11 p.m. No current exception appears in the authority record. The result is **conflict** and then **unexplained drift** only if the evidence review confirms the controller as the governing source. The team holds any automated correction until it identifies the last authorized change and verifies the safe operating window.

At Mariner Ridge West, the last observation is 45 days old and the collection agent is offline. The result is **not evaluated due to stale observation**, not matched. The owner must restore a trustworthy readback before including the site in a current portfolio rate.

The example shows why a one-column “standard status” cannot carry the decision. Two sites may display the same value for entirely different reasons. Two sites may display different values and both be correct.

## Measure coverage before conformity

Portfolio reporting should begin with the population and evidence coverage.

For each metric, publish the eligible facilities and settings, the observation window, the freshness limit, the number successfully evaluated, the number matched, the number operating under approved variation, the number in unexplained drift and the number not evaluated. Keep conflicts separate until resolved.

Do not calculate a “percent on standard” using only facilities that returned data unless that restricted denominator is explicit. A 100% match across eight responding sites does not establish anything about four silent sites. It establishes eight evaluated matches out of twelve eligible sites, with four evidence gaps.

NIST's Cybersecurity Framework 2.0 uses organizational profiles to describe current and target outcomes and to support prioritized improvement.[^5] It is voluntary risk-management guidance, not a self-storage scoring method. The transferable principle is that current and target states should be explicit enough to compare, prioritize and revisit.

Useful operating measures include observation coverage, observation age, unexplained-drift age, approved exceptions nearing expiration, controlled changes awaiting readback, conflicts without an owner and corrected settings awaiting dependent-channel reconciliation. Those measures expose the work still needed. A single green percentage often hides it.

## Close on effective state and dependent readback

A configuration ticket should not close when someone clicks Save.

First, confirm the provider or system accepted the change. Next, collect a fresh governing readback. Then perform the approved bounded behavior test. Finally, reconcile dependent records and channels. A corrected gate schedule may also require a customer notice, website hours update, call-center script change or removal of a temporary sign. A tax-setting correction may require downstream invoice or reporting review. The exact dependencies vary, but they should not disappear when the primary screen looks right.

W3C's PROV-O recommendation provides a model for representing provenance among entities, activities and agents.[^6] It does not validate a facility record or require a particular software design. It supports a useful discipline: preserve where a configuration assertion came from, what activity changed it and who or what was responsible.

The accompanying `facility-configuration-drift-register.csv` turns that discipline into a practical operator record. It includes one blank template and four fully fictional teaching rows. Adapt the fields to approved systems, contracts, policies and local requirements before use.

The goal is not perfect sameness across every property. It is controlled explainability. For every consequential setting, the portfolio should be able to say what standard applies, what baseline was approved, what the facility is actually enforcing, why any difference exists, who owns the next action and what evidence will close it.

A portfolio standard is a decision. A facility setting is a fact to be observed. Configuration control begins when the organization stops pretending those are the same record.

<!-- BODY END -->

## Sources

[^1]: [NIST CSRC Glossary, “configuration management”](https://csrc.nist.gov/glossary/term/configuration_management), accessed September 10, 2026. Official definition used only for the general configuration-management concept.
[^2]: [NIST SP 800-128, *Guide for Security-Focused Configuration Management of Information Systems*](https://csrc.nist.gov/pubs/sp/800/128/upd1/final), August 2011 with updates through October 10, 2019; accessed September 10, 2026. Federal information-system guidance used by analogy, not a self-storage requirement or compliance finding.
[^3]: [NIST SP 800-53 Rev. 5, Release 5.2.0, *Security and Privacy Controls for Information Systems and Organizations*](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final), updated August 27, 2025; accessed September 10, 2026. Control-family structure used as a governance reference, not evidence of implementation or compliance.
[^4]: [IETF RFC 6902, *JavaScript Object Notation (JSON) Patch*](https://www.rfc-editor.org/rfc/rfc6902.html), April 2013; accessed September 10, 2026. Internet Standards Track specification used only to illustrate precise machine-readable change operations.
[^5]: [NIST, *Cybersecurity Framework 2.0*](https://www.nist.gov/cyberframework), February 26, 2024; accessed September 10, 2026. Voluntary cybersecurity risk-management guidance; it does not define self-storage configuration or portfolio scoring.
[^6]: [W3C, *PROV-O: The PROV Ontology*](https://www.w3.org/TR/prov-o/), W3C Recommendation, April 30, 2013; accessed September 10, 2026. Provenance representation standard used as a design reference, not proof that any facility record is complete or authentic.

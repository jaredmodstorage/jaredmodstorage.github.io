# Priority One Does Not Mean the Same Thing Everywhere

## A portfolio urgency contract for self-storage

By Jared Mastroianni

A regional leader opens a portfolio dashboard and sees four records marked “Priority 1.” One facility has a gate stuck open after hours. Another has an elevator out of service in a multistory building. A third has a website price typo. A fourth has a temperature alert whose sensor has not yet been checked.

Those records share a label, but they do not support the same decision. The label may mean “respond immediately” in one system, “oldest unresolved issue” in another, and simply “top of the local list” at a third site. Sorting them together creates the appearance of a common queue without establishing a common operating meaning.

Portfolio teams need a translation layer between local priority and portfolio urgency. That layer should preserve the original record while adding enough context to answer a practical question: **What consequence is developing, how quickly must the operation act, and who has authority to change the response?**

That is the job of an urgency contract.

## Keep the local label, then add the portfolio meaning

Local priority codes often reflect legitimate differences. A staffed urban facility, a remote property, and a multistory site may use different vendors, response plans, access systems, and operating hours. Replacing every local scale with a single universal code can erase useful context.

The safer design keeps two values:

- **Source priority** records what the local system or person assigned, including the definition and version in force at the time.
- **Portfolio urgency** records the consequence, time horizon, operating boundary, evidence, and accountable owner used for cross-site coordination.

This separation prevents a portfolio rule from rewriting history. It also makes a later correction visible. If a climate alert was initially escalated as an equipment failure but a qualified inspection found a bad sensor, the original alert remains in the record while the portfolio status, evidence, and response plan are updated.

The approach is consistent with a basic safety-management principle: hazards are prioritized using factors such as severity, likelihood, and exposure, while interim controls, responsibility, target dates, and verification remain explicit. It is also consistent with the National Incident Management System emphasis on common terminology and shared coordination practices across organizations. An urgency contract applies those ideas narrowly to consequential portfolio work; it does not turn ordinary maintenance into emergency management.

## The seven fields that make urgency comparable

The contract can live in a maintenance platform, an operations database, or a controlled spreadsheet. The technology matters less than the meaning of the fields.

### 1. Source priority and definition

Record the local label exactly as received, along with the definition and rule version behind it. “P1” without a definition is not portable. A portfolio reviewer needs to know whether it means an immediate safety concern, a service interruption, a financial exception, or merely the highest local rank.

### 2. Observed condition

State what was actually observed and when. “Gate was open at 10:14 p.m. after the close command” is an observation. “Controller failed” is a diagnosis that may require technical confirmation. Keeping observation separate from inference reduces premature certainty and gives the next operator a reliable starting point.

### 3. Consequence class

Classify the consequence the operation is managing. A practical set might include life safety, security, customer access, property protection, service continuity, financial accuracy, and administrative correction. More than one class may apply, but the primary class should explain why the work has its current urgency.

### 4. Scope and exposure

Identify who or what is affected and at what scale: one customer, one unit, a building zone, the entire facility, or multiple sites. Scope can change quickly. A single inaccessible unit and a failed entry system across a property are both access issues, but they require different coordination.

### 5. Three clocks

One due date is rarely enough. The record should distinguish:

- **Response due:** when an accountable person must acknowledge and assess the condition.
- **Stabilization due:** when an interim control or safe operating boundary must be in place.
- **Resolution target:** when the underlying condition is expected to be corrected or formally re-planned.

A team may respond to an elevator outage within minutes, establish an accessible customer-support process within an hour, and complete the repair later under a qualified vendor’s schedule. Combining those clocks into one “completion” target hides whether the operation is actually under control.

### 6. Interim control and operating boundary

Describe what the facility may continue doing while the condition remains open. A gate incident might require a staffed access process, a temporary closure, or a security response. A climate alert might restrict new move-ins to an affected area until the sensor and space are verified. The boundary should be specific enough that the next shift can follow it without reconstructing the decision.

### 7. Owner, escalation, and closure evidence

Name the local owner, portfolio owner, escalation trigger, and authorized route. Then define what evidence is needed to close the record. A vendor invoice alone may prove that a visit occurred, not that service was restored. Depending on the condition, closure may require a test result, photo, system readback, customer-access check, or qualified signoff.

## A fictional four-site queue

Consider a fictional portfolio with four records that arrived under the same source label, “P1.” The examples are illustrative and do not describe a real facility, customer, deployment, or result.

At **Harbor East**, the access gate remains open after a close command. The observed condition is verified, the primary consequence is security, and the scope is facility-wide. The operating boundary calls for an immediate security procedure and a named owner while qualified service is arranged.

At **Summit Row**, an elevator is out of service in a multistory building. The record needs more than “equipment down.” It should capture the affected access path, customer accommodations, any applicable authority or service-provider requirements, and the person responsible for the operating plan.

At **Pine Market**, a public webpage displays an outdated unit price while the rental system shows the approved amount. The condition requires prompt correction and review of affected customer communications, but it does not automatically outrank a verified security exposure merely because both systems assigned “P1.”

At **Mesa North**, a temperature alert appears for one zone, but the sensor has not been independently checked. The record should not present a model or sensor output as a confirmed facility condition. The alert initiates verification, defines a cautious operating boundary, and remains explicit about what is unknown.

The portfolio view can now sequence work without pretending the source labels were equivalent. It can also explain the sequence: verified consequence, scope, time horizon, interim control, and authority are visible beside the original local priority.

## The translation rule must be versioned

Once the fields exist, the portfolio needs a controlled mapping rule. The rule might define five portfolio classes, from immediate safety or security action through planned administrative correction. Each class should have entry conditions, required clocks, minimum evidence, and an escalation path.

The mapping version belongs on every translated record. If leadership changes the definition of an access-critical event next quarter, older records should retain the rule that governed them. Otherwise, historical reports may silently recategorize prior work and create a false trend.

Promotion and demotion also need evidence. A record can move upward when the affected scope expands, an interim control fails, or a qualified assessment identifies a more serious consequence. It can move downward when verification narrows the exposure or demonstrates that the original signal was wrong. The change should record who made it, when, why, and under which rule version.

## Review the queue at decision points, not just on a timer

Revalidation is necessary when the facts change. Useful triggers include a new observation, missed response or stabilization time, failed interim control, vendor diagnosis, weather event, occupancy change, customer impact, or shift handoff. A high-urgency record that has not changed still needs a deliberate readback; silence is not evidence that the boundary remains effective.

Automated systems can help detect missed clocks, missing owners, duplicate records, or conflicting statuses. They can also propose a mapping based on the recorded fields. The final operating decision should remain traceable to the evidence and authorized owner. A predicted class is not an observed facility fact, and a dashboard rank is not permission to bypass a safety, legal, contractual, or technical authority.

## A practical first implementation

A portfolio can introduce the contract without rebuilding every system.

1. **Inventory the current scales.** Collect each source label, definition, owner, and active version. Do not assume identical labels mean identical things.
2. **Choose the common consequence classes.** Use language operators can apply consistently across sites.
3. **Define the three clocks and operating-boundary requirement.** Specify which portfolio classes require each field.
4. **Build the mapping as a separate layer.** Preserve the source record and add the portfolio fields, mapping version, and evidence links.
5. **Pilot with a small set of consequential records.** Compare how different reviewers classify the same fictional or historical examples, then refine ambiguous definitions.
6. **Assign release and correction authority.** Name who approves the mapping, who may change it, and how a wrong classification is corrected across reports.
7. **Review exceptions before averages.** Missed stabilization times, failed controls, missing evidence, and unresolved scope changes deserve attention before a summary count of “closed P1s.”

The companion portfolio urgency contract provides a record structure for that work. It is deliberately a template, not an emergency-response plan or a substitute for qualified judgment.

## The management question behind the code

Portfolio operations improve when leaders can explain why one issue moved ahead of another without relying on a color, a rank, or a local shorthand. The strongest queue is not the one with the most urgent labels. It is the one that preserves local evidence while making consequence, time, authority, and operating boundaries comparable.

Before the next cross-site priority review, ask one question: **If the labels disappeared, would the record still explain what must happen next?**

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai. His work focuses on facility operations, multi-location systems, data governance, and responsible artificial intelligence.

## Sources

1. [Occupational Safety and Health Administration, “Hazard Identification and Assessment”](https://www.osha.gov/safety-management/hazard-identification), accessed October 1, 2026.
2. [Occupational Safety and Health Administration, “Hazard Prevention and Control”](https://www.osha.gov/safety-management/hazard-prevention), accessed October 1, 2026.
3. [U.S. Fire Administration, “National Incident Management System”](https://www.usfa.fema.gov/a-z/nims/), accessed October 1, 2026.
4. [U.S. Fire Administration, “NIMS: Command and Coordination”](https://www.usfa.fema.gov/a-z/nims/command-and-coordination.html), accessed October 1, 2026.
5. [National Institute of Standards and Technology, “Special Publication 800-30 Revision 1, Guide for Conducting Risk Assessments”](https://csrc.nist.gov/News/2012/NIST-Special-Publication-800-30-Revision-1), accessed October 1, 2026.

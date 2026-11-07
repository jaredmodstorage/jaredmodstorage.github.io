# Twelve Accounts Are Delinquent. Which Definition Produced the Count?

**By Jared Mastroianni**

A portfolio dashboard shows twelve delinquent accounts at one facility and eight at another. The first number is higher, so the regional team moves it to the top of the follow-up list.

That comparison may be right. It may also be comparing different units of analysis, balance rules, clocks and exclusion policies.

One facility may count customers. Another may count rental agreements. One source may include a late fee as soon as it is assessed. Another may wait until the next daily close. A payment made online may be authorized but not posted. A disputed charge, unapplied credit, vacated unit or account under a separate legal process may be inside one count and outside the other.

The problem is not that twelve is an imprecise number. The problem is that the definition producing twelve is invisible.

Multi-location operators need a delinquency definition contract before they compare facilities, prioritize work or publish a portfolio rate. The contract does not decide what a customer owes or authorize a collection action. It defines the measurement well enough that another person can reproduce the count, explain membership and identify what remains unresolved.

## Start with the unit being counted

“Account” is often used as if it were self-explanatory. It is not.

A customer may have two units at one facility, agreements at two facilities, a shared payment method, a transferred balance or multiple ledger relationships. Counting customers can hide the number of affected agreements. Counting units can split one customer relationship into several observations. Counting invoices can multiply the same operating problem again.

Choose one governed unit of analysis and name its identifier. For example:

- rental agreement;
- customer-facility relationship;
- unit occupancy episode; or
- another organization-defined record that can be reproduced from the source system.

The choice depends on the operating question. A manager planning customer follow-up may need a customer-facility view. A finance reconciliation may need an agreement or ledger view. A portfolio comparison should not switch units silently between facilities or reporting periods.

The W3C Data Cube vocabulary offers a useful technical analogy: observations are interpretable when their dimensions, measures and attributes are defined. Dimensions locate the observation; the measure records the phenomenon; attributes qualify its meaning.[^1] A self-storage delinquency count does not need to be published as RDF to benefit from that discipline. Facility, as-of time, agreement identity, definition version and eligibility state are dimensions. Delinquent agreement count or balance may be measures. Provisional, reconciled or exception-held can be attributes.

## Define the balance predicate

Next, write the rule that decides whether the chosen record has a qualifying balance.

Avoid “balance greater than zero” unless every contributing system uses the same balance field and treatment. Specify the source field or calculation and the status of components that can change membership:

- rent and recurring charges;
- assessed fees;
- taxes where applicable;
- credits and concessions;
- unapplied cash;
- payments authorized but not posted;
- returned or reversed payments;
- disputed items;
- refunds or write-offs in process; and
- corrections effective in an earlier period but entered later.

This is not an invitation to invent an accounting policy inside the dashboard. The contract should point to the approved source and accountable owner for each treatment. If a component is not reconciled, mark the observation provisional or exception-held. Do not quietly coerce an unknown state to zero.

The same rule applies to rounding. A display that rounds $0.004 to $0.00 can still classify the underlying record differently from a source that stores cents. Define the currency, precision and comparison threshold used by the metric. A displayed zero and an exact zero are not automatically the same fact.

## Define the time predicate

Delinquency is time-dependent. The contract needs more than a report date.

Record the exact as-of timestamp, facility time zone and definition of the day boundary. Then identify the date fields used by the rule: contractual due date, effective date, posted date, settlement date or another approved source field. If an organization uses grace periods or other policy-controlled timing, reference the policy and version rather than embedding an unlabeled number in report code.

RFC 3339 defines an interoperable timestamp format with numeric UTC offsets, while the IANA Time Zone Database maintains the changing rules used to calculate local time for named locations.[^2][^3] They solve different problems. An offset such as `-05:00` identifies the relationship to UTC at one instant. A named zone such as `America/New_York` supports future and historical local-time interpretation as daylight-saving rules change.

For a portfolio, store both the unambiguous event timestamp and the facility's named time zone. Otherwise, a payment posted at 12:04 a.m. local time may fall into a different reporting day after conversion, and a rerun may move records across the boundary without a business event.

## Make eligibility explicit

The denominator and the count both depend on eligibility.

Define which agreement states enter the population before testing delinquency. Active, notice-given, transferred, vacated, auction, written-off, legal-hold and closed states may require different treatment under company policy and applicable requirements. The article does not prescribe those treatments. It requires them to be explicit, versioned and applied consistently.

For each exclusion, capture a reason code and source. “Excluded” is not enough. A record excluded because it is closed is different from one held because source data is missing or a specialized review owns the next decision.

Keep the denominator beside the numerator. A rate such as 3 percent is not reproducible without the eligible population, as-of time and version. If one facility counts agreements and another counts customers, their rates are not portfolio peers even if the percentages happen to match.

## Preserve membership, not only totals

A useful metric can answer: Which records are in the count, and why?

Store a cohort receipt for every run. It should include the definition version, source snapshot, facility, as-of timestamp, eligible population, included record IDs, exclusion reason codes, provisional items and the checksum or immutable reference for the input set.

Totals alone hide offsetting errors. A facility can remain at twelve after three accounts leave the cohort and three different accounts enter it. The aggregate is unchanged; the operating work is not.

W3C PROV-DM describes provenance through entities, activities and agents, including derivation and responsibility relationships.[^4] Applied here, the source snapshot and definition are entities, the cohort calculation is an activity, and the approving or reconciling role is an agent. The standard does not define self-storage delinquency. It supplies a disciplined way to retain how a reported value was produced.

## Reconcile definition changes before comparing trends

Definitions change. A portfolio may move from customer counts to agreement counts, alter a balance component, correct a facility time zone or add a new exclusion state.

Do not rewrite prior results silently. Give the new contract an effective date and version. Decide whether history will remain under the old definition, be recomputed under the new one or be shown with a visible series break. Preserve the old membership receipt either way.

Run a bridge report across the change:

1. records included under both definitions;
2. records included only under the old definition;
3. records included only under the new definition;
4. records unresolved because required source data is missing; and
5. the documented reason for each difference.

That bridge turns “the number changed” into an explainable transition. It also prevents a process improvement from being mistaken for a sudden operating result.

## Keep measurement separate from customer action

A portfolio cohort is a management instrument. It is not authority to restrict access, send a notice, assess a fee, change a ledger or contact a customer.

Before any customer-specific action, the authorized employee or workflow should read the current governing record, applicable policy, required notices, holds and recent payment state. The metric can route review. It should not become a substitute for the decision process.

This separation is especially important when data is delayed. A dashboard may correctly show that an agreement was in yesterday's cohort while the current ledger shows a posted payment. Historical measurement and present action can both be accurate because they answer different questions.

## The operator tool: Portfolio Delinquency Definition and Reconciliation Contract

Use this table before comparing facilities or publishing a portfolio measure:

| Contract element | Required decision | Failure signal |
|---|---|---|
| Unit of analysis | Name the counted entity and stable identifier | “Account” means customer at one site and agreement at another |
| Balance predicate | Name source fields, components, precision and threshold | Pending credits, reversals or disputed items change membership invisibly |
| Time predicate | Record as-of timestamp, named time zone, day boundary and date fields | Reruns move records across dates without an operating event |
| Eligibility | Version included states and exclusion reasons | Closed, transferred or exception-held records are treated inconsistently |
| Denominator | Store the eligible population beside the count | A percentage has no reproducible base |
| Membership receipt | Preserve included IDs, excluded IDs, source snapshot and checksum | The total can be repeated but the cohort cannot |
| Definition change | Effective-date the version and bridge old to new membership | A method change appears as operating improvement or decline |
| Action boundary | Require current record and authority before customer action | A stale cohort directly triggers access, notice or ledger changes |

The companion blank contract and fictional example CSVs are part of this package. They are designed to expose differences, not to impose a universal delinquency rule.

## A fictional reconciliation

Fictional Northstar Ridge Storage Group compares three facilities at 8 a.m. local time. Lake reports twelve “delinquent accounts,” Market reports eight and Cedar reports ten.

The first review finds three definitions. Lake counts rental agreements with any positive displayed balance after midnight, including two payments authorized online but not yet posted. Market counts customer-facility relationships after its daily close. Cedar counts agreements but excludes records in a fictional specialized-review state. The three totals are not comparable.

The fictional portfolio team creates definition `DLQ-1.0`: agreement is the unit of analysis; the approved ledger field and precision are named; the run uses each facility's local as-of boundary with an unambiguous timestamp; eligibility and exclusion states are versioned; and provisional payment states remain visible instead of being forced in or out.

After the bridge, Lake has nine included agreements, two provisional records and one excluded closed agreement. Market has nine included agreements after its two-unit customer is represented by two agreements. Cedar has nine included agreements plus one exception-held record. The identical counts do not prove identical performance. They only show that the same contract now produced the same-sized cohorts.

Every facility, agreement, balance, payment state, count, timestamp and result in this walkthrough is fictional teaching material. It is not a modSTORAGE result, customer record or deployment claim.

## The standard is reproducibility

A delinquency count should survive a second analyst, a later rerun and a facility comparison. That requires a named unit, explicit balance and time predicates, versioned eligibility, a visible denominator and preserved membership.

The goal is not to make the dashboard more complicated. It is to keep a precise number from carrying an imprecise meaning.

When the definition is visible, operators can compare like with like, investigate real differences and keep customer actions behind their proper authority. Twelve becomes useful only after the system can explain exactly which twelve, under which rule, at which time, from which evidence.

[^1]: World Wide Web Consortium, [*The RDF Data Cube Vocabulary*](https://www.w3.org/TR/vocab-data-cube/), W3C Recommendation; accessed November 7, 2026.
[^2]: Internet Engineering Task Force, [RFC 3339: Date and Time on the Internet—Timestamps](https://www.rfc-editor.org/rfc/rfc3339.html), Standards Track; accessed November 7, 2026.
[^3]: Internet Assigned Numbers Authority, [Time Zone Database](https://www.iana.org/time-zones); accessed November 7, 2026.
[^4]: World Wide Web Consortium, [*PROV-DM: The PROV Data Model*](https://www.w3.org/TR/prov-dm/), W3C Recommendation; accessed November 7, 2026.


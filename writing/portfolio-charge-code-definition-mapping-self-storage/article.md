---
title: "Two Facilities Use the Same Charge Code. Do They Mean the Same Thing?"
slug: "portfolio-charge-code-definition-mapping-self-storage"
canonical: "https://jaredmodstorage.github.io/writing/portfolio-charge-code-definition-mapping-self-storage/"
author: "Jared Mastroianni"
historical_slot: "2026-11-03 midday systems"
publication_destination: "Jared Mastroianni personal authority site"
featured_image: "063-operations-metrics-roundtable.png"
---

# Two Facilities Use the Same Charge Code. Do They Mean the Same Thing?

*A portfolio total is comparable only when each source code has a governed definition, an effective period and an explicit relationship to the portfolio concept.*

By Jared Mastroianni

![Four self-storage leaders review operating metrics around a conference table overlooking storage units.](assets/063-operations-metrics-roundtable.png)

Consider a fictional portfolio report with two rows labeled `LOCK`. One facility uses that code for a padlock sold at the counter. Another uses it for a service that may include a replacement lock, cylinder work and staff time. The labels match. The operating events do not.

If the portfolio groups both rows under “retail lock sales,” the total may add perfectly while the comparison is wrong. If it excludes both as service activity, the same problem appears in reverse. A code match is not a definition match.

This is a common systems problem in multi-location operations. Facilities may use different property-management configurations, inherited code sets, local abbreviations, legacy integrations or manual spreadsheets. Even when the same platform is present, definitions can drift over time. The solution is not a larger lookup table with two columns. The solution is a governed mapping record that preserves what the source meant, what the portfolio concept means, how the relationship was approved and when it was valid.

## Start with the source definition, not the target report

A mapping team often begins with the desired portfolio categories: rent, fees, retail, services, deposits, adjustments and so on. Then it searches for source codes that appear to fit each bucket.

That reverses the evidence chain.

Start with the source record. For every facility and system, establish:

- the exact source code and displayed label;
- the business event that creates it;
- the population it includes and excludes;
- its unit and sign convention;
- whether it can combine more than one kind of event;
- the governing configuration, procedure or owner;
- the period during which the definition was effective; and
- the strongest available evidence that the definition is current.

Do not infer the definition from a handful of transactions. Examples can test a definition, but they do not establish the rule by themselves. A code labeled `ADMIN` may describe a single approved fee at one facility, several bundled charges at another or an inactive legacy code that still appears in historical exports.

The source-side definition should be understandable without the target portfolio category. If it is not, the mapping is not ready.

## Treat the mapping as a relationship, not a yes-or-no answer

The [W3C SKOS Reference](https://www.w3.org/TR/skos-reference/) defines several mapping relationships between concepts, including exact, close, broader, narrower and related matches. SKOS is a knowledge-organization standard, not a self-storage accounting rule. Its useful lesson is that relationships are not all equivalence.

A practical portfolio register can adapt that distinction:

- **Exact:** the source definition and target operating concept have the same governed meaning for the stated use and period.
- **Narrower:** the source code covers a subset of the target concept.
- **Broader:** the source code combines the target concept with additional activity.
- **Related:** the concepts are associated but should not be aggregated as the same thing.
- **Unresolved:** evidence is insufficient or contradictory.

“Close enough” may help a person search, but it is not a safe aggregation rule. If two concepts are merely close, the register should describe the difference and the report should either preserve that distinction or use an approved transformation that can be tested.

An exact relationship deserves the highest burden of proof because it authorizes silent combination. Matching text, matching code length or the same vendor default does not meet that burden.

## Keep the portfolio concept separate from the accounting decision

The target of this register is a defined operating concept used for portfolio analysis. It is not automatically a general-ledger account, tax category, regulatory classification or financial-statement treatment.

That separation matters. An operations team may need to compare how often a service occurs across facilities without deciding how revenue, cost, tax or liability should be classified. A code-to-operating-concept map can support that comparison while leaving accounting and legal decisions to the authorized owners and governing sources.

Record the target concept with its own identifier, definition, inclusions, exclusions, owner and version. Avoid labels such as `OTHER`, `MISC` or `SERVICE` unless the definition is narrow enough to make the population reproducible.

When a source code contains several concepts, do not force it into one target simply to eliminate an unmapped balance. The correct state may be `hold`, `requires split rule` or `not comparable for this report`.

## Give every mapping an effective period

Mappings change. A facility may rename a code, alter the event that creates it, split one code into two or consolidate several codes after a system conversion. The old mapping can remain correct for the period in which the old definition governed.

Use at least four times:

1. **Source-definition effective time:** when the source meaning became valid.
2. **Mapping approval time:** when the relationship was authorized.
3. **Reporting effective time:** the first period permitted to use the mapping.
4. **Retirement time:** when the mapping stops being eligible for new activity.

Do not rewrite historical reports merely because today's mapping changed. Reprocessing a prior period is a separate decision with its own reason, authority, version and release path.

The [W3C PROV-O Recommendation](https://www.w3.org/TR/prov-o/) distinguishes entities, activities and agents and provides relationships for derivation, attribution and responsibility. A portfolio does not need to implement PROV-O to use the underlying discipline. Preserve the source definition and target concept as identified records, the mapping or transformation as an activity, and the approving owner as the accountable role. A changed definition produces a new version rather than silently changing the meaning of the old record.

## Reconcile values without using totals as proof of meaning

After a mapping is approved, test it with a defined period. Reconcile:

- source record count and source control total;
- records accepted by the mapping;
- records held, excluded or left unresolved;
- transformed or allocated values, if an approved rule exists;
- mapped control total;
- unmapped amount; and
- final variance.

A zero variance proves arithmetic under the test. It does not prove the semantic relationship was correct. The mapping still needs a definition and owner.

The reverse is also true. A variance does not necessarily prove the mapping definition is wrong. It may reflect a time boundary, late event, sign convention, duplicate, reversal, currency or unit difference, or a transformation defect. Preserve the reason as an exception instead of changing a code definition until the numbers balance.

Reconciliation should be performed by facility and source code before portfolio aggregation. Otherwise one facility's overstatement can offset another facility's omission.

## Control mapping changes like production changes

A mapping can alter a dashboard, comparison, budget, performance review or operating decision without changing a single source transaction. Treat it as consequential configuration.

[NIST SP 800-53 Rev. 5](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final) includes configuration change-control practices such as documenting proposed changes, obtaining approval, documenting completed changes and reviewing the change process. The NIST catalog addresses security and privacy controls for information systems; it is not a self-storage reporting mandate. The transferable operating pattern is straightforward:

- propose the mapping change with a reason and source evidence;
- identify affected facilities, reports and periods;
- test the new version against a controlled population;
- require approval from the designated owner;
- preserve the prior mapping and rollback path;
- release the new version at an explicit boundary; and
- reconcile the first production period after release.

Do not let an analyst edit a shared lookup file and overwrite the only evidence of what prior reports used.

## A fictional two-facility example

The following facilities, codes, values, systems, people, times and outcomes are entirely fictional. They do not describe modSTORAGE, a customer, a deployment or an accounting result.

Fictional Stonebridge North and Stonebridge West both export code `LOCK`.

At Stonebridge North, the governed source definition says `LOCK` records a padlock product sold at the counter. The current evidence identifies no bundled service activity. For the fictional October test period, 16 records total $320. The portfolio concept `RETAIL_LOCK_PRODUCT` has the same documented scope for this operating analysis. The proposed relationship is `exact`, subject to the authorized owner's approval and the stated effective period.

At Stonebridge West, `LOCK` can include a padlock product, cylinder replacement and staff service under one combined event. Ten fictional records total $275, but the export does not separate the components. Mapping the full amount to `RETAIL_LOCK_PRODUCT` would convert a broader source concept into a narrower target without an approved split rule. The register marks the relationship `broader`, places the $275 in `hold`, and assigns an owner to determine whether a governed split can be supported.

The portfolio report publishes $320 as mapped for the defined retail-lock concept and shows $275 as unresolved for that comparison. It does not call the unresolved value zero, retail or service. It does not decide tax or accounting treatment. It tells the operator exactly what the evidence supports.

## Use the charge-code definition and mapping register

The companion [**Portfolio Charge-Code Definition and Mapping Register**](portfolio-charge-code-definition-and-mapping-register.md) gives a multi-location team one record for:

- facility and source-system identity;
- source code, label and governed definition;
- inclusions, exclusions, units and sign convention;
- target portfolio concept and relationship type;
- evidence, effective dates, owner and approval;
- change history and downstream report impact;
- controlled-period reconciliation; and
- hold, release, rollback and next-review states.

Use the blank CSV as the working schema and the fictional CSV only as a teaching example. Do not store customer-level detail, payment-card data, credentials or unapproved sensitive records in the register.

Portfolio reporting becomes credible when another person can reconstruct why each value belongs in each concept for that period. The code is only the pointer. The definition, relationship, approval and reconciliation make the comparison usable.

## Sources and limits

- [W3C, SKOS Simple Knowledge Organization System Reference](https://www.w3.org/TR/skos-reference/): authoritative W3C Recommendation describing concept labels, semantic relationships and mapping properties. This article adapts the distinction among mapping relationships; it does not claim SKOS implementation or conformance.
- [W3C, PROV-O: The PROV Ontology](https://www.w3.org/TR/prov-o/): authoritative W3C Recommendation describing entities, activities, agents, derivation and attribution. It informs the provenance model but does not prescribe a self-storage data architecture.
- [NIST SP 800-53 Rev. 5, Security and Privacy Controls for Information Systems and Organizations](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final): authoritative federal control catalog used only for a transferable configuration change-control pattern. It is not an accounting standard, self-storage mandate or certification.

*Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.*

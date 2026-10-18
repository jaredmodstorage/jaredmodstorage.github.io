# A 10x10 Is Not a Product Definition

## Build a governed unit-type contract before comparing inventory across self-storage facilities

**By Jared Mastroianni**

<!-- BODY START -->

A portfolio dashboard shows 420 “10x10” units. The number looks precise. It may combine drive-up units, interior units, upper-floor units, climate-described units, units reached only by elevator and units whose physical or access attributes were never mapped.

The shared label proves that several systems use the same words. It does not prove that the units are the same operating product.

This matters when a regional team compares availability, occupancy, pricing, lead conversion, maintenance demand or customer fit across facilities. If the unit-type definition changes from one property to another, the portfolio can calculate a perfectly accurate answer to an undefined question.

The fix is not a longer display name. It is a governed **unit-type contract**: a stable identifier, explicit attributes, source references, effective dates, quality states and declared comparability rules. The display label remains useful for people. It just stops carrying more meaning than it can hold.

## Separate the label from the operating object

“10x10 CC,” “10 × 10 climate,” and “100 SF interior” may refer to the same local product. Or they may not. A team cannot resolve that safely with text matching alone.

Create a portfolio unit-type ID that is distinct from the local property-management-system code and the customer-facing label. Preserve all three:

- **Portfolio unit-type ID:** the durable identity used by the governed model.
- **Local source code:** the exact identifier used by the source system at one facility.
- **Preferred and alternate labels:** the names people and downstream channels display or recognize.

The World Wide Web Consortium’s SKOS reference distinguishes concepts from the labels attached to them and provides preferred and alternative labels within concept schemes.[^1] A self-storage operator does not need to implement RDF or SKOS to use the pattern. The transferable idea is straightforward: the concept needs its own identity, while labels remain governed representations of that concept.

Do not generate the portfolio ID from the current label. If the label changes from “10x10 Climate” to “Medium Climate,” the underlying type should not silently become a new operating object. Conversely, if a wall moves, access changes from drive-up to interior, or the governing climate description changes materially, keeping the old ID simply because the label stayed “10x10” hides a real change.

## Define the attributes that make comparison meaningful

A useful contract separates relatively stable type attributes from dynamic commercial and operating states.

**Physical attributes** may include nominal width, nominal depth, ceiling-height band, stated rentable area, measurement method, door type, door-opening dimensions and unusual geometry. A nominal label should not be presented as a field measurement unless the source establishes that.

**Access attributes** may include drive-up status, interior or exterior path, floor, elevator dependency, stair dependency, corridor constraints and other approved accessibility descriptors. Avoid converting those facts into an accessibility-compliance conclusion unless a qualified process supports it.

**Environmental-description attributes** should preserve the exact governed customer promise or category, its source and version. “Climate controlled” is not improved by inventing a universal temperature range in the data model. If the lease, facility page and local configuration do not support the same description, the correct state is a conflict requiring an owner—not a guessed normalized value.

**Commercial attributes** may include the approved customer-facing class, channel eligibility and restrictions on how the type can be offered. Current rate, promotion, occupancy and availability are not permanent unit-type attributes. They are time-varying records linked to the type.

That distinction prevents a circular metric. If a high-priced unit is classified as “premium” because its price is high, the portfolio cannot later use the premium class to explain the price difference. The class should come from governed attributes and policy, not from the outcome being analyzed.

Every numeric field needs a unit of measure and a definition. Every categorical field needs allowed values and a null meaning. `unknown`, `not applicable`, `not yet mapped` and `not observed` should not collapse into a blank or zero. Zero square feet is a value. Unknown area is a quality state.

## Declare comparability instead of assuming it

Two types can be comparable for one question and not another.

A drive-up 10x10 and an upper-floor interior 10x10 may belong in the same nominal-size band for a high-level physical-capacity view. They should not automatically be combined for a customer-access comparison, a product-mix report or a pricing analysis. The operating system needs a named **comparability class** tied to a purpose.

Useful classes might include:

- nominal-size comparison;
- physical-area comparison;
- access-path comparison;
- environmental-description comparison;
- customer-facing product comparison; and
- maintenance or asset-service comparison.

Each class should identify required attributes and the rule for missing data. A type with unknown floor or drive-up status might remain eligible for nominal-size reporting while being excluded from access-path comparison. Exclusion is not deletion. The report should show the excluded count and reason.

Keep the type contract separate from the unit-instance record. The contract says what a governed type means; the instance record says which physical unit is mapped to that type during a stated interval. A facility can therefore correct one unit’s mapping without rewriting the definition for every unit in the class. The same separation makes acquisition review practical: local codes can be mapped in stages while unmapped units remain visible instead of inheriting a default type.

This is where many portfolio dashboards become misleading. They show a denominator without revealing which records were eligible to enter it. A better report carries the population rule, mapping version and excluded population next to the result.

## Treat quality as data, not a cleanup note

The W3C Data Quality Vocabulary describes quality measurements, metrics, dimensions and provenance as explicit metadata that can travel with a dataset.[^2] The vocabulary is a generic web-data model, not a self-storage implementation standard. Its relevant lesson is that quality should be represented, measured and sourced—not buried in a comment after the dashboard is published.

For a unit-type contract, quality fields can include:

- mapping status: proposed, verified, conflicted, retired or superseded;
- source coverage: which required attributes have governing evidence;
- completeness: required fields present versus expected;
- conflict count: unresolved differences among sources;
- verification owner and date;
- downstream consumers tested; and
- evidence references for each material attribute.

Do not convert incomplete mapping into “other” merely to reach 100 percent. An explicit unmapped population is operationally useful. It tells the team whether a comparison is broad, partial or currently unsafe.

The quality threshold should follow the decision. A preliminary inventory count may tolerate an unknown door-opening width. A move-in fit recommendation should not pretend that the same missing field is harmless. One record can be fit for one purpose and unfit for another.

## Version the contract and its mappings

Unit types change. Facilities renovate, walls move, elevator access changes, customer-facing descriptions are revised and source systems replace local codes. The portfolio needs the old interpretation as well as the new one.

Give each contract and mapping an effective start, optional effective end and version. Store the approving role, reason for change and source evidence. Use an offset-bearing timestamp for the actual change event and preserve the facility’s local time-zone context when business dates matter. RFC 3339 provides an interoperable timestamp format with a stated relationship to UTC; it does not define the effective-date policy or the business meaning of a unit type.[^3]

Do not overwrite history and recompute old reports under today’s mapping without disclosure. A corrected error may justify a controlled restatement. A real product change usually calls for prospective treatment from the effective point. The report should identify which choice was made.

Before release, test every consumer that relies on the mapping: portfolio reporting, website inventory, call-center views, pricing workflows, availability feeds, maintenance routing and any analytical model. A successful source-system save does not prove that each consumer received the new meaning.

## A fully fictional portfolio example

Juniper Reach Portfolio and every facility, unit type, code, attribute, mapping, count, time, system and result in this example are entirely fictional.

Three facilities use the local label “10x10.” At Juniper Reach North, code `D1010` describes ground-level drive-up units with no governed climate description. At Juniper Reach Center, code `C1010-2` describes interior second-floor units reached by elevator under a versioned customer-facing climate description. At Juniper Reach West, code `1010` has a recorded nominal size but no verified access-path or environmental-description source.

The portfolio does not force all three into one product class. It maps North and Center into the same nominal-size comparison class, while preserving different access and product classes. West remains eligible for a bounded nominal-label count but is excluded from access-path and environmental-description comparisons until the missing sources are resolved.

The fictional mapping file then receives a proposed change: North’s local label becomes “Medium Drive-Up.” Because the underlying physical and access attributes do not change, the preferred label is versioned while the portfolio unit-type ID remains stable. Center later closes one elevator path during an invented renovation. The team records an effective-dated access-condition change rather than rewriting the permanent unit type from an unverified operational note.

No occupancy, rate, revenue, conversion, customer result or facility performance is calculated in the example. It demonstrates identity, mapping, quality and comparability only.

## Put the contract in the operating rhythm

The companion **Unit Type Attribute and Comparability Contract** gives the portfolio one record for source identity, labels, physical and access attributes, governed descriptions, mapping version, quality, comparison eligibility, approval and downstream readback.

Review the contract when a facility is acquired, a source system changes, construction alters inventory, a label or promise changes, an integration introduces a new local code, or a dashboard reveals a large unmapped population. Assign exceptions to named owners with evidence requirements and due dates. Do not let “temporary” mappings become permanent through neglect.

The point is not to make every facility identical. Local differences are real and often valuable. The operating system should preserve them clearly enough that a portfolio can decide when two units are comparable, for which purpose, under which version and with what evidence.

A 10x10 label is helpful at the counter. Portfolio decisions need the contract behind it.

<!-- BODY END -->

## Sources

[^1]: World Wide Web Consortium, [*SKOS Simple Knowledge Organization System Reference*](https://www.w3.org/TR/skos-reference/), W3C Recommendation, accessed October 15, 2026.
[^2]: World Wide Web Consortium, [*Data on the Web Best Practices: Data Quality Vocabulary*](https://www.w3.org/TR/vocab-dqv/), W3C Note, accessed October 15, 2026.
[^3]: Internet Engineering Task Force, [RFC 3339, *Date and Time on the Internet: Timestamps*](https://www.rfc-editor.org/info/rfc3339), accessed October 15, 2026.

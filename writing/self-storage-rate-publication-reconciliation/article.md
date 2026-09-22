# The Rate Changed. Which Customer-Facing Surface Still Shows the Old One?

**Deck:** A portfolio rate decision is not complete when one system saves it. Release the whole customer-facing bundle, observe every surface, and reconcile the result before the new rate becomes portfolio truth.

By Jared Mastroianni

A multi-location self-storage operator can approve one rate and unintentionally present several versions of it.

The management system may show the new amount while the website still shows the old one. The online rental flow may add a promotion that the front-desk reference does not explain. A call-center script may omit an eligibility condition. A kiosk may use yesterday’s cached data. Printed material may remain on a counter after the digital surfaces change.

The problem is not limited to a wrong number. A customer-facing rate is a bundle: amount, unit type, term, effective time, eligibility, promotion, fees, conditions and the channel on which it appears. If any material part changes or disappears between surfaces, the portfolio has not released one offer. It has created conflicting offers.

The operating control is a rate-publication reconciliation. It treats approval, technical publication, customer-visible observation and cross-surface closure as separate states.

## Start with the exact release bundle

“Update the 10 × 10 rate” is not a sufficient instruction. Before changing a surface, the release owner needs a fixed description of what is being released.

At minimum, the bundle should name:

- facility and stable facility identifier;
- unit or space type and the source definition behind it;
- approved base amount and billing basis;
- promotion, discount or introductory condition, if any;
- customer eligibility and term;
- required fees or other material conditions;
- effective date, time and time zone;
- surfaces in scope;
- approval identity and timestamp; and
- rollback or correction owner.

That record should point to the governing source rather than copy more customer or financial information than the control requires. It should also freeze an exact release version. If the amount, condition, population or effective time changes after approval, the owner creates a new version instead of editing the approved record in place.

The [World Wide Web Consortium’s provenance model](https://www.w3.org/TR/prov-overview/) describes provenance as information about the entities, activities and people involved in producing data or another thing. A self-storage rate release does not need to implement the entire model. It does need enough lineage to show which approved bundle produced which public and operating surfaces.

## Approval is only the first state

The word “live” hides too many steps. Use a state vocabulary that makes the remaining work visible:

- **Candidate:** prepared but not approved.
- **Approved:** authorized for a named facility, unit group, scope and effective time.
- **Published:** saved or distributed to a named surface.
- **Observed:** read back from the customer-facing surface or authoritative operating view.
- **Reconciled:** observed values and conditions match the approved bundle across every required surface, or a documented exception contains the difference.
- **Corrected:** a released difference was replaced or withdrawn, then observed again.

A provider receipt or save confirmation can support **published**. It cannot establish **observed**. A screenshot can support what one surface displayed at one moment. It cannot establish that every eligible customer sees the same offer or that the underlying transaction path will apply it correctly.

The release owner should preserve both the technical receipt and the independent readback. Neither should overwrite the other.

## Map the surfaces before the change

Every portfolio has a different set of rate surfaces. The minimum useful map names the real customer path rather than a generic channel category.

For example:

1. public facility or unit-listing page;
2. online rental or reservation flow;
3. front-desk management-system view;
4. call-center or centralized sales reference;
5. kiosk or other self-service interface;
6. approved email, printed sheet or in-facility display; and
7. downstream reporting used to confirm the release.

Some surfaces may be generated from one source. That relationship should be recorded, not assumed. Two pages can share a data feed while using different caches, templates, promotion logic or unit definitions. A shared provider name does not prove a shared release path.

The map also needs one owner per surface. “Marketing” or “operations” may be too broad if no named role knows how to verify the final customer view. Ownership includes the authority to pause, correct or remove the surface when the bundle cannot be represented accurately.

## Treat timing as part of the rate

An amount without an effective instant is incomplete. “Monday morning” can resolve differently across facilities and systems.

[RFC 3339](https://www.rfc-editor.org/info/rfc3339/) defines an Internet date-and-time format with an explicit relationship to Coordinated Universal Time. It is useful for recording an unambiguous release instant, but it does not replace a facility’s business calendar, local legal requirements or scheduled pricing rules. The portfolio record should preserve both the unambiguous timestamp and the operating context that makes it meaningful.

The release owner should know whether a surface reads changes immediately, at a scheduled refresh, after cache expiration or only after a manual action. If the channels cannot switch together, the plan needs an approved transition state. That may mean holding public promotion until the rental path is ready, keeping the prior bundle active on all surfaces, or temporarily removing a rate claim that cannot be represented consistently.

Silence is not a transition plan. A stale surface needs a visible owner, a due time and a customer-safe operating boundary.

## Reconcile the complete customer impression

The [Federal Trade Commission’s advertising guidance for small businesses](https://www.ftc.gov/business-guidance/resources/advertising-faqs-guide-small-business) says advertising must be truthful and non-deceptive, supported by evidence, and not unfair. It also explains that necessary qualifying information should be clear and conspicuous. This is general federal business guidance, not a legal opinion about a particular self-storage offer. State law, contracts and the exact transaction can add other requirements.

The operating lesson is direct: comparing only the headline amount is not enough. Read back the complete customer impression.

For each surface, verify:

- facility and unit identity;
- amount and billing basis;
- promotion and duration;
- eligibility and exclusions;
- material fees or conditions represented on that surface;
- effective state;
- next action available to the customer; and
- the evidence captured from the actual surface.

The check should follow the customer path as far as the approved test permits. A public listing can show one amount while a later step applies another. A call-center reference can contain the right base amount and the wrong promotion end date. A front-desk screen can display the correct rate for a unit group whose availability definition differs from the website.

Do not complete a real rental merely to test publication unless the operator has an approved test process. Use the lowest-consequence evidence that establishes the needed state.

## Control the change like a release

[NIST Special Publication 800-128](https://csrc.nist.gov/pubs/sp/800/128/upd1/final) addresses security-focused configuration management for federal information systems. It is not a self-storage pricing standard. Its transferable discipline is that changes should be identified, evaluated, approved, implemented and monitored rather than treated as finished at execution.

A portfolio rate release benefits from the same separation:

1. **Identify** the exact release bundle and every affected surface.
2. **Evaluate** dependencies, timing, customer impact and rollback limits.
3. **Approve** one version for one scope.
4. **Publish** through the controlled path for each surface.
5. **Observe** the customer-facing and operating result.
6. **Reconcile** differences, receipts and pending corrections.
7. **Close** only when the bundle is consistent or every exception has an enforced boundary.

High-consequence differences deserve a stop condition. If the transaction path presents a different amount from the public listing, if a required condition disappears, if a facility or unit group cannot be identified, or if the current effective version cannot be established, the release should not be declared complete.

## A fictional six-facility release

Consider an entirely fictional operator, Northline Storage Cooperative. It approves fictional release `RATE-FIC-20260922-03` for one fictional unit group at six facilities. The approved bundle uses a fictional monthly base amount of $149, has no introductory promotion, and becomes effective at `2026-09-22T14:00:00-04:00`.

Five facilities publish and reconcile across the public unit page, online rental path, front-desk view and call-center reference. At the sixth facility, the website displays $149 while the online rental path still displays the prior fictional amount of $139. The provider returns a successful update receipt for the website feed, but no receipt covers the rental-path cache.

The result is not “six sites updated.” It is five reconciled facilities and one contained exception.

The sixth facility remains on the prior approved bundle until the operator’s correction path is complete. The public claim and transaction path are not allowed to disagree while the team waits. The exception record names the affected surface, observed difference, customer boundary, owner and next review time. After correction, the team reads both surfaces again and checks that the fictional transaction path presents the approved bundle once.

No customer, facility, provider, price, timing or performance result in this example is real. The values demonstrate the state model only.

## Correct without erasing the mismatch

When a released surface is wrong, the correction record should preserve what happened.

Record the approved bundle, the observed surface value, the time of observation, the correction version, the person or role authorizing it, the new publication receipt and the final readback. Do not replace the original observation with the corrected result. The mismatch explains why correction was necessary and which dependent surfaces may need review.

If a stale rate was visible to customers, route the matter through the operator’s approved customer, legal and financial procedures. The reconciliation register should not invent a remedy, decide a contract question or infer customer impact. It should preserve the facts required by the people who hold that authority.

## Use one portfolio release record

The accompanying **Rate Publication Reconciliation Register** keeps the approved bundle, effective time, surface owners, publication receipts, customer-visible observations, differences, correction evidence and closure state in one sequence. Its sample rows are fictional. It does not contain a default rate, approval threshold, legal conclusion or claim about a provider’s capabilities.

The portfolio rule is simple: one approved bundle, many controlled surfaces, one reconciled conclusion. The rate has not finished changing because a source system saved it. It has finished changing when every required surface presents the approved customer-facing meaning—or the portfolio has contained and owned every difference.

---

## Operator tool

Download the **Rate Publication Reconciliation Register** as an XLSX workbook or CSV register. A responsive HTML reference presents the same fictional surface rows for browser review.

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai. His work focuses on facility operations, multi-location systems, data governance and responsible artificial intelligence.

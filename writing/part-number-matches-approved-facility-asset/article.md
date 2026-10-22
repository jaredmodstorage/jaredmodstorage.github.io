# The Part Number Matches. Is It Approved for This Facility and Asset?

**Deck:** A portfolio spare-parts program becomes reliable only when item identity, applicability evidence, revision, custody, installation authority and post-work reconciliation travel together.

**By Jared Mastroianni**

A box on the maintenance shelf has a familiar part number. The work order names the same number. A technician is already at the facility. It looks like the shortest path is to install it.

The matching label answers one question: the stored item and the requested item may share an identifier. It does not establish that the item is authentic, current, compatible with the exact installed asset, approved as a substitution, complete with the required accessories, suitable for the site condition or authorized for this job.

That gap becomes harder to see across a self-storage portfolio. One facility may store gate components in a locked cabinet. Another may keep door hardware in a maintenance room. A regional technician may carry parts between sites. The accounting system may see a purchase, the work-order system may see a repair and the facility may see an empty shelf. Each record can be individually plausible while the portfolio cannot answer where the part went or why it was allowed into service.

The answer is not a bigger spreadsheet of part numbers. It is a controlled chain from catalog identity to facility operating state.

## Separate the records that operations tends to collapse

A useful parts system distinguishes at least seven records:

1. **Catalog item:** the governed description of an item, including manufacturer, manufacturer part number, revision or variant, and available identification evidence.
2. **Stock instance or lot:** the physical item or quantity received, with source, receipt date, location, condition and custody.
3. **Applicability decision:** the documented basis for allowing that exact item, revision or approved substitute on a defined asset population.
4. **Reservation:** a temporary claim against stock for a named work order, facility and asset.
5. **Issue:** the custody transfer from shelf or vehicle to a named person or job.
6. **Installation:** the recorded use of a specific item or quantity on a specific asset under a specific work authorization.
7. **Reconciliation:** the closing comparison among reserved, issued, installed, returned, scrapped and replenishment quantities.

These are connected states, not synonyms. A received part is not an approved part. An approved part is not an installed part. A technician’s possession is not proof of installation. A closed work order is not proof that the parts ledger, asset record and physical shelf agree.

NIST Special Publication 800-53 uses this same accountability logic in a different domain. Its CM-8 control calls for inventories that reflect actual components, avoid duplicate accounting, use the granularity needed for tracking and reporting, and retain identifying and location information. It also calls for updates during installation and removal.[^1] The publication governs information systems, not self-storage maintenance stock. The transferable discipline is precise: inventory becomes dependable when components have stable identity, association, location and lifecycle updates.

## Bind applicability to an installed asset, not a facility nickname

“Fits the gate” is not an applicability rule. A property may have an entrance operator, an exit operator, pedestrian hardware, keypad enclosures and controllers from different years or manufacturers. Two assets described locally as “the west gate” may not share a model, configuration, revision or approved replacement path.

Start with the installed-asset record. Resolve the facility ID, asset ID, manufacturer, model, serial number when available, installed configuration, relevant revision and current operating status. Then link the candidate part to the exact evidence used for the applicability decision: manufacturer documentation, an approved engineering or technical determination, an authorized parts list, or another source accepted by the organization’s qualified owner.

Do not turn the register into a technical approval engine. The portfolio record should preserve who made the decision, under what authority, from which evidence and for which asset scope. It should not let a regional analyst infer electrical, mechanical, fire-protection, life-safety or code compatibility from similar text.

This is where a catalog identifier reaches its limit. GS1 describes the Global Trade Item Number as an identifier for trade items.[^2] Identification is valuable for procurement and receiving. It does not, by itself, certify authenticity, condition, completeness, technical compatibility or permission to install the item in a particular asset. The same boundary applies to an internal SKU, barcode or manufacturer number.

## Treat revision and substitution as decisions

Parts change without becoming visually obvious. A supplier may replace a suffix. Packaging may use an older image. A kit may gain or lose an included component. A manufacturer may supersede a number. A distributor may offer a claimed equivalent.

Do not overwrite the old record with the new number. Preserve both identities and create a substitution decision with:

- the original item and revision;
- the candidate item and revision;
- the exact asset population evaluated;
- the supporting evidence and its date or version;
- any conditions, exclusions or companion changes;
- the qualified decision owner;
- the approval, rejection or hold state; and
- the effective and review dates.

NIST SP 800-128 describes configuration management as a process for managing and monitoring configurations while supporting required business functions.[^3] It is security-focused federal guidance, so it does not approve a private facility part or prescribe a maintenance program. Its useful lesson is that a controlled change needs an identified baseline, evaluated change, authorization, implementation evidence and monitoring. “The vendor says it replaces the old one” is a lead to verify, not the complete change record.

Make uncertainty operational. If the revision cannot be resolved, if applicability evidence conflicts, if the installed asset identity is incomplete or if the decision owner is outside the required technical scope, the status is **hold for qualified review**. Do not convert missing evidence into a permissive default.

## Make custody visible across facilities and vehicles

Portfolio stock disappears in the space between records. A part is moved from one property to another to avoid an outage. A technician keeps an unused item after a job. A broken component returns in the new item’s box. A facility receives a delivery but the central catalog never learns the local shelf location.

Every custody event should name the item or lot, quantity, from-location, to-location, custodian, reason, time and related work order or transfer. Locations should be governed values: a facility shelf, a secured cabinet, a named service vehicle, a return bin, a quarantine area or a disposal stream. “With maintenance” is not a location.

Keep availability separate from physical count. Five items may be physically present while only two are available because two are reserved and one is quarantined. Likewise, a minimum-stock rule should not reorder from a count that includes installed, returned or unverified items.

The portfolio should also distinguish the evidence behind quantity. A purchase receipt shows what a provider says it supplied. A receiving record shows what an authorized person observed. A cycle count shows what was physically found at a stated time and location. A system balance is a calculated state. When they disagree, retain the variance and owner; do not silently replace one with another.

## Connect installation to removal and return to service

Installation is a change to an asset. The work record should bind the issued item to the facility, asset, work authorization, installer or responsible provider, installation time and any required acceptance evidence. It should also identify what was removed.

The removed component needs a disposition: retained for evaluation, warranty return, repairable stock, hazardous or controlled disposal under the applicable procedure, ordinary scrap, or another approved state. A blank disposition creates a second ungoverned inventory.

Technical completion and facility return to service may require different evidence and different owners. The qualified provider may establish that the technical work meets its procedure. The facility may separately verify the permitted operating readback: the correct asset responds, the intended customer path is available, temporary access is removed, related alerts are restored and open restrictions are handed off. The exact tests depend on the system, policy, manufacturer information and qualified authority.

Close the parts episode only when the quantities reconcile:

> opening available + receipts + transfers in − transfers out − installed − approved disposal = expected closing physical stock

Then compare expected stock with the observed count. This authored equation is a practical reconciliation method, not an accounting standard. A variance stays open with a named owner and evidence path. It does not become “shrink,” “theft,” “technician error” or a financial conclusion without supporting review.

## Use lineage when the history matters

An installed part’s history may later matter for warranty, recurring failure review, asset replacement or portfolio purchasing. The record should show which stock instance was used, which applicability decision supported it, which work activity installed it and which person or organization held the relevant roles.

The W3C PROV family describes provenance through entities, activities and agents involved in producing a thing or record.[^4] A self-storage operator does not need to implement the full standard to preserve useful lineage. The working test is simpler: can a reviewer move backward from the installed state to the exact item, receipt, transfer, authorization and evidence without guessing?

Keep prior states. If an applicability decision is withdrawn, do not erase the history of earlier installations. Mark the decision superseded, identify the successor and route the affected asset population for the organization’s required review. A new conclusion should change current authority without falsifying what happened before.

## A fictional portfolio example

Consider fictional Northline Row Storage Group. It operates nine invented facilities. The example, quantities, assets, people and outcomes below are entirely fictional.

Facility NRS-04 has a failed fictional drive-gate control module. Its shelf contains a box labeled `GCM-440`. The work order also says `GCM-440`, but the asset record identifies controller revision C. The catalog has two applicability records: `GCM-440 / rev 2` is approved for revisions A and B, while `GCM-440 / rev 3` is approved for revision C only when installed with a named fictional adapter kit.

The shelf count says one, but receiving evidence does not show the revision and no adapter kit is present. The manager does not release the box because the base number matches. The item moves to **quarantine pending identity**. A regional parts owner resolves it as revision 2 from retained receiving evidence, records it as inapplicable to that asset and transfers an approved rev-3 kit from NRS-07 under a named custody event.

After the fictional qualified technician completes the authorized work, the register records the module and adapter as installed on the exact asset. The removed module enters a fictional warranty-return state. The facility completes its required operating readback. NRS-07’s available quantity falls, its reservation closes and its replenishment review opens.

The example claims no real deployment, product behavior, vendor capability, repair result or facility outcome. It illustrates why a shared number is not a complete authorization.

## Use one register across the chain

The accompanying **Portfolio Spare-Part Applicability and Custody Register** separates catalog identity, stock instance, applicability, reservation, issue, installation, removal, return to service and reconciliation. The blank CSV is deliberately neutral. It contains no approved manufacturers, compatibility determinations, reorder levels, warranty promises or safety rules. The example CSV is explicitly fictional.

Start with a narrow pilot: one consequential asset family and the stock locations that serve it. Resolve the installed assets, freeze the catalog definitions, record current physical counts, quarantine unidentified items and require the next issue and installation to travel through the chain. Use the first cycle to find missing evidence and unclear authority before expanding.

The point is not to slow every repair. It is to prevent speed from depending on an invisible assumption. A trusted parts program lets the operator move faster because the shelf label, technical decision, custody trail, work authorization and closing asset state tell the same story.

A part number identifies a candidate. The operating system proves whether that candidate belongs in this asset, at this facility, under this work authorization—and what happened after it left the shelf.

## Practical tool

- [Portfolio Spare-Part Applicability and Custody Register — operator guide](portfolio-spare-part-applicability-and-custody-register.md)
- [Blank CSV template](portfolio-spare-part-applicability-template.csv)
- [Explicitly fictional worked example](portfolio-spare-part-applicability-fictional-example.csv)

## Sources

[^1]: National Institute of Standards and Technology, *Security and Privacy Controls for Information Systems and Organizations*, SP 800-53 Rev. 5.1, CM-8 System Component Inventory, including updates during installation and removal, accessed October 22, 2026. https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final
[^2]: GS1, *Global Trade Item Number (GTIN)*, official identifier overview, accessed October 22, 2026. https://www.gs1.org/standards/id-keys/gtin
[^3]: National Institute of Standards and Technology, *Guide for Security-Focused Configuration Management of Information Systems*, SP 800-128, updated October 10, 2019; accessed October 22, 2026. https://csrc.nist.gov/pubs/sp/800/128/upd1/final
[^4]: World Wide Web Consortium, *PROV-Overview: An Overview of the PROV Family of Documents*, W3C Working Group Note, April 30, 2013; accessed October 22, 2026. https://www.w3.org/TR/prov-overview/

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.

## Editorial production note

Research, drafting, structured-tool production and QA were completed with AI assistance under Jared Mastroianni’s direction. The final article remains bounded by the cited sources, the explicit fictional-example labels and the claim limitations recorded in this package.

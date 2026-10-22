# Portfolio Spare-Part Applicability and Custody Register

Use this register to keep item identity, applicability, custody, work authorization, installation, removed-part disposition and reconciliation separate. It is an operating record, not a technical compatibility determination, accounting system, manufacturer instruction, safety procedure or warranty decision.

## Operating sequence

1. **Identify the catalog item.** Record manufacturer, part number, variant or revision and the source of the identifier. Do not merge records solely because labels resemble one another.
2. **Identify the physical stock.** Record stock-instance or lot identity, quantity, condition, current location and custodian.
3. **Resolve the target asset.** Use governed facility and asset IDs plus manufacturer, model, serial or configuration evidence available under the operator's process.
4. **Record applicability authority.** Link the exact item and revision to the exact asset scope, qualified decision owner, evidence, decision, conditions and effective dates.
5. **Reserve and issue.** Bind quantity to a named work order before custody changes. Keep proposed, reserved and issued states distinct.
6. **Install or return.** Record actual installed quantity and the removed component's disposition. Unused material returns through a custody event.
7. **Read back the operating state.** Preserve technical completion and facility operating readback as separate evidence when the procedure assigns them to different owners.
8. **Reconcile.** Compare expected closing stock with the observed count. Keep every variance open until explained through authorized evidence.

## Required hold states

Use `hold_for_qualified_review` when the item revision, target asset, applicability evidence or decision authority is unresolved. Use `quarantined` for unidentified, damaged, suspect, obsolete or otherwise ineligible stock. Neither state is install permission.

## Reconciliation equation

`opening available + receipts + transfers in - transfers out - installed - approved disposal = expected closing physical stock`

Compare the expected amount with an observed count made at a stated time and location. The equation is an authored operating method, not an accounting standard or finding of cause.

## Claim boundaries

- Blank fields, matching text, a barcode scan, purchase receipt, reservation or work-order close do not establish applicability or installation.
- The template contains no approved products, asset configurations, substitution decisions, reorder quantities, acceptance tests or legal/safety conclusions.
- Technical, code, warranty and life-safety decisions remain with the organization’s qualified authorities and controlling documents.
- The companion worked example is entirely fictional and describes no real customer, facility, asset, vendor, product behavior, repair or operating result.


# Shared-Service Allocation and Reconciliation Ledger

Use this ledger when one invoice, credit or shared-service charge must be assigned to more than one facility. It keeps the source amount, benefited-facility set, direct components, shared basis, rounding, approval, posting readback and comparability decision in one traceable structure.

This is an operational control template. It does not determine generally accepted accounting principles, tax treatment, capitalization, legal liability, contract compliance or the appropriate chart of accounts. Route those conclusions through the authorized finance, accounting, tax and legal owners.

## Release sequence

1. **Preserve the source.** Record the invoice identity, service period, currency and exact total without altering the source document.
2. **Split components.** Separate direct facility charges, site-specific credits and genuinely shared amounts.
3. **Establish eligibility.** List every candidate facility and decide whether it benefited during the service period. Hold unresolved membership rather than forcing it into the denominator.
4. **Select and version the basis.** Name the basis, unit, source, version, owner and effective rule. Prefer direct evidence before a proxy.
5. **Calculate visibly.** Retain each facility numerator, common denominator, unrounded result, rounding adjustment and final amount.
6. **Reconcile to source.** Sum every direct, shared and credit row. Do not release a nonzero residual without a recorded disposition.
7. **Review and approve.** Separate preparation, review and posting authority according to company policy.
8. **Read back the destination.** Verify facility identity, period and amount in the governing destination after posting.
9. **Classify comparability.** Record whether the result is comparable to prior periods, restated under an approved basis or held because the basis or posting changed.
10. **Close or carry exceptions.** A mathematically balanced file can remain open when service evidence, eligibility, authority or posting readback is unresolved.

## Basis selection test

| Question | Pass condition | Hold condition |
|---|---|---|
| What service or benefit is being assigned? | Exact component and service period are named. | Only the invoice total is available. |
| Is direct evidence available? | Direct facility detail is assigned before the shared formula. | Direct detail is discarded in favor of a portfolio proxy. |
| Who benefited? | Every candidate facility has a supported eligibility state. | The contract roster is assumed to equal the benefited set. |
| Does the basis explain consumption or benefit? | The unit relates to the service and has a named source. | The basis was chosen only because it was convenient. |
| Is the rule reproducible? | Another reviewer can recreate every amount from retained inputs. | A total or facility row was manually overwritten. |
| Does the result reconcile? | Final rows equal the source total and all residuals are visible. | A residual is hidden in a plug or unrecorded adjustment. |
| Was posting verified? | Exact destination rows were read back and matched. | Only an upload or batch-accepted receipt exists. |

## Controlled states

### Eligibility

- `eligible`
- `ineligible`
- `direct-charge-only`
- `shared-benefit-unverified`
- `held`

### Allocation lifecycle

- `prepared`
- `calculated`
- `reviewed`
- `approved_for_posting`
- `posted_unverified`
- `read_back`
- `reconciled`
- `closed`
- `exception_open`

### Comparability

- `comparable`
- `comparable_after_restated_basis`
- `not_comparable_basis_change`
- `held_source_gap`
- `held_posting_mismatch`

## Field guide

The companion CSV uses 48 fields.

| Field group | Required evidence |
|---|---|
| Source identity | Allocation event, invoice, vendor reference, currency, service period and invoice total. |
| Component | Component identity, type, description and amount. |
| Facility eligibility | Stable facility identity, eligibility state, evidence and reason. |
| Basis | Basis identity, version, name, unit, facility numerator and common denominator. |
| Calculation | Formula version, unrounded result, rounding adjustment, shared amount, direct amount, credit and final amount. |
| Reconciliation | Calculated total and variance to the source invoice. |
| Authority | Preparer, reviewer, times and approval state. |
| Posting | Batch identity, posting state, destination identity, posted amount, readback time and variance. |
| Comparison and exception | Comparability state, exception identity, exception state, notes and fictional-data disclosure. |

## Rounding rule

Calculate at greater precision than the posting currency. Use an approved deterministic method to distribute the currency-unit residual. Record the adjustment on the receiving row. Do not change a facility amount solely to make the total tie without retaining the unrounded result and rule.

## Minimum release rule

Release the allocation as reconciled only when:

- every source component is represented exactly once;
- every included facility has evidence of benefit or an approved direct charge;
- the basis and denominator are versioned;
- direct charges and site-specific credits are preserved;
- the sum of facility rows equals the invoice total;
- approval authority is recorded;
- posted rows have been read back from the correct destinations; and
- every remaining exception has an owner, due time and bounded consequence.

## Fictional example boundary

The companion worked example uses Harborline Storage Group, six fictional facilities, a fictional vendor, fictional amounts and fictional posting records. It teaches the control sequence. It is not evidence of an actual invoice, expense, customer, vendor relationship, system capability, accounting entry, savings or operating result.

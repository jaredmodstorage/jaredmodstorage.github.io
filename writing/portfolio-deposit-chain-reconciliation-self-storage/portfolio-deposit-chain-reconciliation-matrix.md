# Portfolio Deposit Chain Reconciliation Matrix

Use one row for each relationship between an identified facility-day source population and one downstream submission or batch. Split a facility-day across multiple rows when it enters multiple batches. Repeat a shared batch across facility rows when it contains more than one facility.

This tool supports operating reconciliation. It does not replace company accounting policy, bank or processor records, payment-security controls, audit procedures, legal advice or an authorized ledger entry.

## Control sequence

1. **Freeze the source population.** Record facility, business date, shift/accountability period, report cutoff, source-system reference, receipt count and expected amount.
2. **Bind the submission.** Record the processor batch, deposit bag or other submission ID, submitter, timestamp and amount.
3. **Record provider acceptance.** Keep the provider receipt/reference and acceptance time separate from submission.
4. **Observe the bank.** Record the bank transaction reference, observed date and amount without adding full account or payment-card data.
5. **Trace ledger posting.** Record journal, property/entity, account, period, post time and amount.
6. **Run both tests.** Amount and population must pass separately.
7. **Resolve exceptions.** Assign type, owner, next action and due time. Preserve any correction as a linked successor, not an overwritten source record.
8. **Close honestly.** Mark `reconciled` only when the chain is supported end to end and every material variance has an approved disposition.

## Recommended state vocabulary

- `source_population_open`
- `submitted_not_accepted`
- `accepted_not_observed`
- `bank_observed_unallocated`
- `posted_with_variance`
- `held_for_correction`
- `reconciled`

## Review rules

- A matching portfolio total cannot close mismatched facility rows.
- A matching amount cannot replace a population test.
- Submission, provider acceptance, bank observation, ledger posting and reconciliation are separate states.
- Do not include full card numbers, bank credentials or unnecessary customer details.
- A correction requires its own ID, evidence, authority and link to the original record.
- A facility manager’s status visibility does not create authority to edit accounting records.

The companion CSV contains the 35 implementation fields. The worked rows are explicitly fictional training data and report no real facility, customer, deposit, result or system behavior.

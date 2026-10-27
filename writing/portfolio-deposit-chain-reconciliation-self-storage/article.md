---
title: "The Bank Deposit Matches. Which Facilities and Shifts Does It Actually Close?"
slug: "portfolio-deposit-chain-reconciliation-self-storage"
author: "Jared Mastroianni"
description: "A multi-location self-storage method for tracing facility-day receipts through processor batches, bank acceptance and ledger posting without letting a matching total hide cross-site errors."
canonical: "https://jaredmodstorage.github.io/writing/portfolio-deposit-chain-reconciliation-self-storage/"
publication_destination: "Jared Mastroianni personal authority site"
publisher_owner: "Master Personal Site Authority"
publication_state: "publisher handoff pending"
---

# The Bank Deposit Matches. Which Facilities and Shifts Does It Actually Close?

**By Jared Mastroianni**

![Jared Mastroianni listens during a boardroom discussion with colleagues seated around a conference table.](027-professional-board-meeting-listening.png)

*A matching portfolio total is the beginning of a reconciliation question, not the end. Editorial, non-documentary image; provenance and use limits are recorded in the package.*

**Deck:** One bank deposit can equal the expected portfolio amount while one facility is short, another is over, a processor batch crossed the cutoff and the ledger posted to the wrong place. Reconcile the chain, not only the total.

<!-- BODY START -->

The bank shows a $24,680 deposit. The daily portfolio report expected $24,680. The line turns green.

That looks reconciled.

It may only be equal.

One facility can be short by $180 while another is over by $180. A card batch can include late transactions from yesterday and omit transactions still pending today. A deposit can reach the bank but post to the wrong property or accounting period. A cash bag can be prepared without bank acceptance. A processor can accept a batch before the funds settle.

If the operating system compares only two grand totals, all of those errors can disappear inside a perfect match.

Multi-location self-storage operators need a deposit chain that preserves each facility-day population from source receipts through provider batches, bank activity and ledger posting. The control should explain not only whether the money totals agree, but which transactions, facilities, shifts and business dates the agreement actually closes.

## A total is not an identity

Money is fungible. Operating evidence is not.

Two amounts can be equal without representing the same activity. That is why a deposit record needs identity at every stage:

- facility and stable facility key;
- business date and shift or accountability period;
- source receipt population and report cutoff;
- tender class;
- processor, cash-bag or deposit-batch identifier;
- bank transaction identifier and bank date;
- ledger journal, property, account and post period; and
- exception or correction references.

The amount remains essential, but it sits inside that identity. A $2,100 processor settlement for three facilities is not interchangeable with a $2,100 cash deposit for one facility. A $500 bank credit on Monday may correspond to Friday activity, a reserve release, a correction or something else. The number alone cannot tell the operator which obligation it satisfied.

The [W3C Provenance Ontology](https://www.w3.org/TR/prov-o/) offers a useful technical analogy. It separates entities, activities and agents, then links what an activity used, generated and derived. PROV-O is a web provenance standard, not an accounting rule. Its practical lesson is still strong: if an artifact was generated from earlier records, preserve the relationship instead of relying on a matching label or value.

## Reconcile five states, not one green check

I use five distinct operating states for the deposit chain.

**Facility closeout prepared.** The identified drawer, shift or business-day population has been closed under the facility’s procedure. Expected cash and noncash tenders are supported by source records. This state does not prove the bank or processor received anything.

**Batch submitted.** The processor batch, deposit bag or other transmission was created and submitted. Record the exact population, amount, submitter, timestamp and provider reference. Submission is not acceptance.

**Provider accepted.** The processor, courier, bank branch or remote-deposit service returned a receipt for the identified submission. Acceptance is stronger than “we sent it,” but it is not proof of final settlement or ledger posting.

**Bank observed.** The bank record shows the corresponding credit or deposit under the approved matching rule. Preserve the bank transaction reference and observed date. A bank observation does not decide which facility or accounting period should receive the amount.

**Ledger posted and reconciled.** The authorized accounting record shows the amount assigned to the correct entity, property, account and period, and every material variance has a disposition. This is the only state that should close the end-to-end chain.

The names can change to match company policy. The separation cannot. “Deposited” is too broad when it can mean prepared, sent, accepted, visible at the bank or posted in the ledger.

## Build the population before matching the money

Start with the source population, not the bank line.

For each facility-day, freeze the expected receipt set at a named cutoff. Keep original transaction identifiers, tender classes, voids, refunds, charge reversals, cash pulls and authorized corrections. If a transaction arrives after the cutoff, record the next eligible population rather than slipping it into whichever total makes the day balance.

Then bind every downstream record to that population. A processor batch may contain hundreds of receipts. A cash deposit may contain one or more shift bags. A bank deposit may combine several bags. A ledger journal may allocate one settlement across several properties. The chain can be one-to-one, one-to-many or many-to-one. The control must represent those relationships explicitly.

This is where a bridge table or reconciliation matrix earns its keep. One row can represent one source population’s contribution to one downstream batch. If a facility-day is split across two processor batches, it gets two rows. If one processor batch covers six facilities, it gets six linked rows. Each row carries its expected share, observed share and variance.

Only after those relationships are defined should the portfolio calculate whether the chain balances.

## Use two tests: amount and population

An amount test asks whether the expected and observed dollars agree within the approved rule.

A population test asks whether every eligible source receipt appears exactly where it should, no receipt appears twice and no downstream amount lacks a supported source.

Both tests must pass.

Consider a portfolio with two facilities. Facility A expects $900 and Facility B expects $1,100. The bank shows $2,000. If the ledger posts $1,000 to each facility, the portfolio amount test passes while both facility allocations fail. If one $100 receipt from Facility A is duplicated and one $100 receipt from Facility B is missing, both portfolio and facility totals can still match. Only the receipt-population test exposes the error.

The U.S. Government Accountability Office’s [2025 Green Book](https://www.gao.gov/greenbook) describes internal control as a process management designs, implements and operates to help achieve objectives, including reliable reporting. It also emphasizes quality information and monitoring. The Green Book governs federal agencies, not private self-storage operators. Used cautiously, it reinforces a practical point: a control should produce information that is complete and usable for the decision, not merely a total that happens to agree.

## Keep exceptions open without freezing the whole portfolio

A portfolio reconciliation should make local uncertainty visible without holding unrelated facilities hostage.

Use exception states such as:

- `source_population_open` — the facility closeout is incomplete or changing;
- `submitted_not_accepted` — the provider has not returned a usable receipt;
- `accepted_not_observed` — the provider accepted the item but no matching bank activity is visible under the rule;
- `bank_observed_unallocated` — the bank line exists but facility allocation is incomplete;
- `posted_with_variance` — the ledger posted, but amount or population differs;
- `held_for_correction` — an authorized correction is being evaluated; and
- `reconciled` — the complete chain passed both tests.

Assign each exception an owner, next action and due time. Do not clear the portfolio total while facility rows remain in `posted_with_variance`. At the same time, do not mark every other facility unreconciled because one bank line is delayed. Roll up honestly: ten reconciled, one held, one overdue is more useful than either “all green” or “nothing complete.”

Corrections need their own identity. Preserve the original source record, reason, supporting evidence, approver, correction time and replacement relationship. Never change a transaction merely to force the bank match. A difference may be a timing item, a classification issue, a duplicate, a missing record or a genuine unresolved variance. The ledger should record which one evidence supports.

## Protect payment data by design

A reconciliation file does not need full card numbers, bank credentials or unnecessary customer information.

Use internal transaction IDs, processor references, masked identifiers where permitted, and governed links to restricted source systems. The PCI Security Standards Council says [PCI DSS](https://www.pcisecuritystandards.org/standards/pci-dss/) provides technical and operational requirements for protecting payment account data, and its current [FAQ 1071](https://www.pcisecuritystandards.org/faqs/1071/) requires masking a primary account number when displayed unless there is a specific business need. PCI DSS scope and applicability depend on the actual payment environment. This article does not determine compliance. The operational rule is simpler: do not turn a portfolio control sheet into a new store of sensitive payment data.

Access should follow role and purpose. A facility manager may need to see whether the facility closeout was accepted. A reconciliation owner may need provider and bank references. Only authorized accounting roles should make or approve ledger changes. Visibility into status does not confer authority to edit the underlying transaction.

## A fictional portfolio chain

The following example is entirely fictional. Harbor Crest Storage, its facilities, people, systems, amounts and results do not represent a real operator or deployment.

Fictional facility `HCS-FIC-014` closes business date October 24 with $1,420 in card receipts. Fictional facility `HCS-FIC-022` closes with $980. Processor batch `PB-FIC-5501` reports $2,400, and the bank later shows a $2,400 credit.

The total matches.

The population test does not. One $60 transaction from `HCS-FIC-014` posted after the approved cutoff but entered the batch. One $60 transaction from `HCS-FIC-022` was accepted in the facility system before cutoff but excluded from the batch and remains pending. The processor amount still equals the combined facility expectation because the two differences offset.

The reconciliation matrix assigns the late $60 to the next eligible facility-day population and leaves the missing $60 in `accepted_not_observed`. The bank credit remains observed, but the chain is not closed. The ledger allocation stays held until the accounting owner applies the approved timing treatment and the pending receipt receives a provider or bank disposition.

Nothing in that example suggests loss, misconduct or system failure. It demonstrates why equality is not lineage.

## Put the matrix into the weekly operating rhythm

The accompanying **Portfolio Deposit Chain Reconciliation Matrix** includes a blank 35-column CSV and an explicitly fictional worked example. Start with one week, one tender path and a small group of facilities.

For each facility-day, capture the source cutoff and expected population. Link it to the submission, provider receipt, bank observation and ledger journal. Test amount and population separately. Assign unresolved items. Then roll up counts and dollars by disposition without collapsing the open exceptions.

The review should answer seven questions:

1. Which facility-days are expected for the period?
2. Which source populations are frozen and complete?
3. Which batches accepted those populations?
4. Which bank records correspond to those batches?
5. Which ledger entries assigned the right amount to the right facility and period?
6. Which population or amount variances remain open, and who owns them?
7. What evidence supports the final reconciled state?

A matching bank deposit is good news. It is not the conclusion. The portfolio closes the chain only when it can show which facility and shift produced the amount, how it moved, where it posted and what happened to every exception.

<!-- BODY END -->

---

## Practical operator tool

Use the accompanying **Portfolio Deposit Chain Reconciliation Matrix** to bind facility-day source populations to submission, provider acceptance, bank observation, ledger posting and exception closure. The blank CSV is implementation-ready; the completed CSV is explicitly fictional.

## Sources and limitations

The article uses current W3C provenance guidance, GAO’s 2025 Green Book and current PCI Security Standards Council materials as bounded design references. None is presented as a private self-storage accounting procedure, audit opinion, legal requirement or compliance determination. Full access dates, provenance and limitations are recorded in `source-register.csv`.

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.


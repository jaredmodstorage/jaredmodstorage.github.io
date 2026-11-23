---
title: "The Same 10x10 Shows Three Prices. Which One Can the Customer Actually Rent?"
subtitle: "Build an Effective-Dated Offer Contract Before You Reconcile Channels"
author: "Jared Mastroianni"
slot: "2026-11-22 midday systems"
slug: "self-storage-published-rate-offer-reconciliation"
canonical: "https://jaredmodstorage.github.io/writing/self-storage-published-rate-offer-reconciliation/"
---

# The Same 10x10 Shows Three Prices. Which One Can the Customer Actually Rent?

## Build an Effective-Dated Offer Contract Before You Reconcile Channels

**By Jared Mastroianni**

<!-- BODY START -->

A customer sees a 10x10 on the website for $149. The property-management system shows a standard rate of $169. A reservation screen carries a $139 first-period offer. The manager has a printed sheet from last week showing $159.

Which number is wrong?

That is not the first question. The first question is what each number means.

One may be a standard asking rate. Another may be a channel-specific acquisition offer. A third may apply only after a customer meets promotion terms. The printout may simply be stale. All four can come from real systems and still fail to describe the same transaction.

Portfolio teams often try to solve this with a nightly comparison of one `rate` field against another. That catches obvious mismatches, but it also produces false alarms and misses the expensive errors. A price is not comparable until the facility, unit group, channel, customer eligibility, effective interval, fees, inventory scope and transaction stage line up.

The operating control is an offer contract: an effective-dated record of what the business is prepared to offer, to whom, through which channel, for which inventory, under which terms, and under whose authority.

## “The rate” is several different facts

Start by naming the price facts that systems tend to compress.

The **standard rate** is the approved base asking rate for a defined facility and unit group. It is not automatically the amount every new customer sees or pays.

The **published acquisition offer** is the price and terms shown through a specific channel. It may be available on the facility website, an aggregator, a call-center screen or an in-office surface.

The **promotion** changes the economics under stated conditions. It may affect the first period, a fixed number of periods or a separate fee. The value is incomplete without eligibility, timing and expiration.

The **reservation quote** is an offer presented to a particular prospect at a particular time. The **lease charge** is what the executed agreement authorizes. The **collected amount** is what payment activity records. Those are related states, not synonyms.

The **existing-customer charge** belongs to a current agreement and account history. Comparing it directly with a new-customer web offer can create noise unless that is the defined business question.

Fees and taxes need their own fields. Folding a mandatory fee into an unlabeled total, or comparing a base rate in one channel with a first-period total in another, makes the reconciliation look precise while it compares different things.

Federal Trade Commission guidance says advertising claims must be truthful and non-deceptive, and it identifies price as material to a buying decision. The FTC’s small-business guidance also points pricing advertisers to the [Guides Against Deceptive Pricing](https://www.ecfr.gov/current/title-16/chapter-I/subchapter-B/part-233) and notes that state rules may apply.[1](https://www.ftc.gov/business-guidance/resources/advertising-faqs-guide-small-business) Those are general advertising principles, not a self-storage pricing opinion or a substitute for legal review in the jurisdictions where a portfolio operates.

The operational implication is still straightforward: a published number should be tied to terms the business can identify, support and honor.

## Give every offer a comparison key

A useful comparison key joins the attributes that make two offers meaningfully comparable. At minimum, include:

- stable facility ID and unit-group ID;
- physical attributes that affect the product, such as size, access type and climate designation;
- source channel and source-system record ID;
- offer type and customer eligibility;
- inventory scope;
- effective start, effective end and time zone;
- standard rate, published rate, promotion mechanics and required fees;
- reservation or hold terms;
- governing owner, approval reference and precedence rule; and
- observation time and reconciliation status.

Do not use the displayed unit description as the key. “10x10 climate” may refer to different access types, floors, amenities or inventory pools across properties. Do not use a marketing label as a facility identity. Do not assume that two timestamps are comparable when one system stores local time and another stores UTC without retaining the offset.

The comparison key should be readable by an operator. If an exception cannot explain, in plain language, which offer was observed, which governing record it was compared with and why the records were expected to match, it is not ready for a manager’s queue.

## Separate authority from distribution

The system that displays an offer is not necessarily the system authorized to define every attribute in it.

A pricing platform may govern the standard rate. A promotion service may govern the discount. A property-management system may govern unit availability. A web platform may render the final offer. A call-center interface may cache an approved record. The portfolio needs one accountable source by attribute, plus a precedence rule for assembling the offer.

This is where many reconciliations go wrong. They declare one application the “single source of truth” even though the final offer is composed from several governed inputs. When a web price disagrees with a standard-rate table, the system may be applying a valid promotion. When a reservation price disagrees with the website, the reservation may have preserved an earlier offer during a valid hold window.

Authority answers, “Who may set this fact?” Distribution answers, “Where should this fact appear?” Reconciliation checks whether the distributed representation matches the authorized contract for that place and time.

The 2025 revision of the U.S. Government Accountability Office’s Green Book says management should obtain relevant data from reliable sources and process it into quality information that is appropriate, current, complete, accurate, accessible, verifiable and timely. It is a federal internal-control standard, not a rule for private self-storage operators. Its control logic is useful by analogy: name the information requirement, source and processing control before relying on the output.[2](https://www.gao.gov/assets/gao-25-107721.pdf)

## Use effective time, not the latest row

An offer should be reconstructed as of the moment a customer saw it. “Current” is not enough.

Record the start and end of each rate or promotion version, including the time zone. Preserve the observation time from every channel. Keep the quote or reservation timestamp and the permitted hold interval. If an approved change is scheduled for midnight local time, the system should not compare yesterday’s cached web page with today’s governing record and label the difference unexplained.

Never overwrite the old offer simply because a new one becomes active. History is necessary to answer basic questions: Was the page wrong when it was observed? Was the reservation valid when created? Did the lease use the terms preserved by the quote? Did a later correction change the published surface without changing already accepted agreements?

The W3C Data Quality Vocabulary describes a way to attach quality measurements, policies and provenance so users can judge whether data is fit for a purpose. It does not define a universal list of quality dimensions, and it is a Working Group Note rather than a W3C Recommendation.[3](https://www.w3.org/TR/vocab-dqv/) That limitation matters. A portfolio still has to define its own useful measures, such as offer freshness, completeness, channel agreement and correction latency.

## Reconcile the customer journey, not just the database

Build the check around the stages a customer can actually encounter:

1. **Published:** What appeared on each public or staff-facing channel?
2. **Quoted:** What price and terms were presented to the prospect?
3. **Reserved:** What did the reservation preserve, and for how long?
4. **Leased:** What terms were accepted in the agreement?
5. **Charged:** What did the account ledger assess?
6. **Collected or adjusted:** What payment or approved correction followed?

A valid promotion can make published and standard rates differ. A valid hold can make reserved and newly published rates differ. Neither difference should be auto-corrected without context.

The high-risk conditions are more specific: an offer with no governing record; an expired promotion still published; an eligible customer unable to receive the displayed terms; a mandatory fee missing from the defined comparison; a unit group mapped to the wrong inventory; a quote changed after acceptance; or a correction that reached one channel but not the others.

Classify the exception before assigning work. Useful classes include expected variance, timing lag, stale cache, missing eligibility, mapping error, unauthorized override, incomplete disclosure, inventory mismatch and unresolved source conflict. Severity should reflect customer and control impact, not merely the dollar difference.

## A fictional four-channel example

The following example is entirely fictional. Redwood Mill Storage, facility `RMS-02`, its systems, offers, prices, people, dates and results are invented teaching material. They do not describe modSTORAGE, a customer or a real deployment.

At 9:10 a.m. Eastern, the fictional website shows a 10x10 climate-controlled unit at $149 per period with a promotion available to qualifying new customers. The governing standard rate is $169. The approved promotion reduces the first period by $20 and is effective through 11:59 p.m. local time. The call-center screen shows the same offer.

At 9:18 a.m., a reservation preserves the $149 first-period terms for twenty-four hours. At noon, the standard rate changes to $179 and the public acquisition offer becomes $159. The reservation remains valid under the fictional hold policy. A simple comparison now flags $149 against $179 and may instruct an employee to “fix” the reservation.

The offer contract tells a different story. The reservation is linked to the 9:18 version, its eligibility was evaluated, the hold has not expired and the later change applies prospectively. The variance is expected.

The real exception appears at 12:14 p.m., when an aggregator still shows $149 for newly created reservations but no longer carries the qualifying promotion terms. That record is not protected by the earlier customer’s hold. It is a stale distribution with incomplete context. The correction owner updates the feed, records the distribution receipt, re-reads the live listing and checks whether any new reservations entered during the affected interval.

The numbers alone could not separate those cases. Identity, authority, terms and time did.

## Make corrections propagate with receipts

Changing the governing row is the start of a correction, not the end.

For every affected channel, record the expected update path, accountable owner, target time and proof of readback. A successful API response or export job shows that a process ran. It does not prove that the customer-facing page, call-center screen or property workflow now reflects the intended offer.

Retain the original observation, corrected value, reason, approval, distribution acknowledgement and live readback. If customer decisions may have occurred during the affected interval, create a separate review population rather than assuming that a published fix resolved prior transactions.

W3C’s PROV-O Recommendation provides a formal model for connecting information to the entities, activities and agents involved in its production. A portfolio does not need to implement that ontology to preserve useful lineage. It can still connect a displayed offer to source records, transformation logic, accountable owners, generation time and correction activity.[4](https://www.w3.org/TR/prov-o/)

## Use the Published Offer Contract and Reconciliation Grid

The accompanying tool has three parts: an offer-definition record, a channel-observation record and a correction/readback record. One offer version can have many channel observations. One exception can have several downstream corrections.

Run the grid on a defined cadence and at consequential changes. Sample the customer journey, not only system exports. Review open exceptions by impact and age. Require an owner to close the loop with observed evidence.

The most useful portfolio measures are not “number of prices” or “number of mismatches.” Track the share of active offers with complete contracts, the share of observations reconciled to the correct effective version, the age of unexplained high-impact exceptions, the channels awaiting readback and the number of accepted transactions needing separate review.

A multi-location operator will always have different prices. Different prices can be intentional. Unexplained prices cannot.

The goal is not to force every surface to display one number. It is to make every offer reconstructable: the product, customer, channel, terms, authority, effective time and evidence that made that number valid.

<!-- BODY END -->

## Sources

1. [Federal Trade Commission, “Advertising FAQ’s: A Guide for Small Business”](https://www.ftc.gov/business-guidance/resources/advertising-faqs-guide-small-business)
2. [Electronic Code of Federal Regulations, 16 CFR Part 233, Guides Against Deceptive Pricing](https://www.ecfr.gov/current/title-16/chapter-I/subchapter-B/part-233)
3. [U.S. Government Accountability Office, *Standards for Internal Control in the Federal Government*, GAO-25-107721](https://www.gao.gov/assets/gao-25-107721.pdf)
4. [W3C, Data Quality Vocabulary](https://www.w3.org/TR/vocab-dqv/)
5. [W3C, PROV-O: The PROV Ontology](https://www.w3.org/TR/prov-o/)


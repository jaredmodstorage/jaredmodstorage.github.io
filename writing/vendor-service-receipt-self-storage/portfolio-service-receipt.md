# Portfolio Service Receipt

Use one receipt per facility and authorized service scope. Attach or link the controlling work order, quote and vendor report. The local verifier records observable facts; the portfolio owner resolves scope and exceptions; finance applies its separate invoice and payment controls. This template does not itself approve a change order or payment.

| Stage | Record the answer | Stop or route when |
| --- | --- | --- |
| Identity | Facility ID; asset/area; work-order ID; vendor; site contact | The bill or vendor report points to a different site, asset or work order. |
| Authority | Approved scope/version; authorizer; price basis; approved service window | Added work lacks a named authorized decision. |
| Attendance | Arrival/departure; areas reached; vendor report ID | A visit is being treated as proof that every scoped task was performed. |
| Performed work | Each scoped task performed, deferred or changed; reason and evidence link | A whole route is marked complete despite an unperformed task. |
| Site readback | Safe test/inspection; who performed it; time; result or `unverified` | A required qualified test is missing or the asset remains restricted. |
| Exception | Remaining condition; operating restriction; owner; due date; follow-up reference | The exception has no owner or is silently closed with the first job. |
| Invoice review | Invoice ID/date; billed lines and quantities; match to approved scope; credits or change orders | Billed scope, price basis, vendor identity or payable charge is unresolved. |
| Disposition | `verified_scope`, `partial_scope`, `unverified`, or `exception_open`; site verifier; portfolio reviewer; finance handoff | A service receipt is mistaken for payment authorization. |

Suggested sequence: **authorize → observe → verify → reconcile → hand off**. Preserve the original result and link later corrections or return visits rather than rewriting the first receipt. A blank or unknown result is not “passed.”

`portfolio-service-receipt-template.csv` contains one blank operational row and one **entirely fictional teaching row**. The fictional row is not a real site, invoice, vendor, work order, charge, test, payment or outcome. Adapt fields to the operator's contracts, safety procedures, purchasing delegation and privacy rules before live use.

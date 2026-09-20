# Final editorial QA — September 20 morning operator

## Identity and state

- Title: “When a Climate-Controlled Unit Feels Warm: The Manager's First Check.”
- Author: Jared Mastroianni. No unnecessary role/tenure claim in the article.
- Selected destination only: Master Personal Site Authority; proposed canonical `https://jaredmodstorage.github.io/writing/climate-controlled-unit-feels-warm-response/`.
- Article length: **1,743 whitespace-delimited words**, including title/deck/byline/headings and excluding three endnote definitions. Exact command: `awk '/^\[\^1\]:/{exit} {print}' article.md | wc -w`.
- State at writer freeze: complete local package, not yet source-deployed or publicly published. Handoff, deployment, live canonical, sitemap/feed inclusion, indexing, independent coverage and recognition require separate proof.

## Four scored review lenses

These are one writer's four explicit review lenses, **not** four independent human or agent approvals. Scores describe the local source package and render; they do not certify a future publisher deployment.

| Lens | Score / 10 | Evidence |
| --- | ---: | --- |
| Trade editor: originality, fit, voice | **9.5** | One specific customer-to-manager problem, a single fictional scenario carried through, no invented promise or case result, restrained prose and a concrete closing question. Distinct from the published power-outage, water-intrusion and unit-rentability pieces and the held September 19 battery article. |
| Facility operator: next-shift utility | **9.6** | Clear sequence from customer report to actual promise, location-labeled observation, footprint, qualified handoff, customer update and separate closure readbacks. The final 42-field HTML record is usable by keyboard/phone or for print and distinguishes `unknown` from `normal`. |
| Evidence and claim precision | **9.6** | EPA building-investigation and moisture guidance plus DOE commercial-HVAC sensor discussion are directly accessible official sources; all three returned HTTP 200 on September 20. Scope limits are stated next to each use. No universal climate range, diagnosis, legal conclusion, real facility result or technical-performance assertion. |
| Local rendered visual and accessibility | **9.5** | Article preview at 1280/390/320 and final HTML tool at 1280/390/320 have viewport equal to document scroll width, no page errors, no failed hero image and no broken local link element. Tool has 42 fields inside labels, zero unnamed fields, eight fieldsets with legends, keyboard focus styling and no script/form submission. 320px screenshot was visually inspected: labels, fields and section boundaries remain readable without clipping. Automated Axe and final publisher-template QA were not run and remain publisher gates. |

## Source, duplicate and safety boundaries

- `source-register.md` records precise URLs, access date, provenance and limits. EPA's guide covers building complaint investigations; DOE explains possible commercial thermostat/zone-sensor arrangements; EPA's moisture guidance covers HVAC-related moisture operation and verification. None establishes the actual customer promise or the condition of a real unit.
- Exact local calendar/daily-package searches found no matching title, thesis, slug, C-214 illustration or tool. The proposed personal canonical and a corresponding WordPress slug returned HTTP 404. No September 20 midday/evening package existed at the writer's preflight. Recheck public duplicate state immediately before deployment.
- Opening C-214 scenario and later continuation are explicitly fictional. No actual customer, site, temperature, contract term, vendor, repair, equipment installation, damage or outcome is represented as fact.
- `climate-complaint-field-record.html` is the publisher-facing tool. `climate-complaint-field-record.md` is a plain-text source/backup, not the mobile visual release. The HTML file explicitly says entries are not saved or transmitted; no `<form>` or `<script>` exists. It does not authorize unit entry, technical work, emergency response or a temperature guarantee.
- PHOTO-033 is a byte-exact governed 3840 × 2560 contextual image. The alt and caption explicitly identify it as an AI-generated editorial scene, not documentary evidence of a complaint or result. It is not an author portrait.
- No ACR IDs, external email, discovery notification, duplicate publisher handoff or provider publication were created in the writer lane.

## Visual evidence

Local article screenshots: `review-only/article-1280.png`, `article-390.png`, `article-320.png`. Publisher-facing tool screenshots: `review-only/field-record-html-1280.png`, `field-record-html-390.png`, `field-record-html-320.png`. These show a local layout, not the personal site's production template. The older Markdown backup's underscore blanks wrap at 320px, which is why it is not the release tool. All eight core deliverables are pinned in `checksums.sha256`; source rendering scripts/screenshots are retained in `review-only/` and excluded from the public package.

Publisher release gates: current canonical duplicate check; precise title, byline, footnotes, image/caption/alt, HTML tool behavior and links; live desktop/390/320; exact static assets; source/deployment/rollback identity; public HTTP readback. Do not equate a handoff or successful build with publication, indexing or coverage.

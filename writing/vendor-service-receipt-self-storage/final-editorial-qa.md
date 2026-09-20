# Final editorial QA — September 20 midday systems

## Release identity and honest state

- Article: **The Invoice Arrived. Did the Facility Accept the Work?** by Jared Mastroianni.
- Exact length: **1,741 whitespace-delimited words**, including title, deck, byline and headings and excluding the three endnote definitions. Command: `awk '/^\[\^1\]:/{exit} {print}' article.md | wc -w`.
- Sole assigned publisher: **Master Personal Site Authority**. Proposed canonical: `https://jaredmodstorage.github.io/writing/vendor-service-receipt-self-storage/` (HTTP 404 at preflight). Master modBLOG is non-selected and must reject duplicate full text/tool.
- State at writer freeze: complete local package and one internal publisher handoff pending. No source commit, provider deployment, public publication, sitemap/feed entry, indexing, independent coverage or recognition is established by this file.

## Editorial and operator checks

- The opening contrasts vendor completion, site readback and invoice review without accusing any vendor or asserting a real problem. The article keeps authorization, attendance, performance, acceptance, invoice disposition and payment separate.
- The entirely fictional twelve-site example reconciles **12 authorized, 12 visits reported, 9 scopes verified, 2 attempted but unperformed, 1 inspected with an unresolved exception**. The sum of scope dispositions is 12. No real customer, operator, invoice, charge, credit, vendor, safety event or result is implied.
- The practical operator tool is a compact eight-stage receipt, supported by a 35-column CSV with one blank row and one fictional example. CSV parsing found all three rows 35 columns wide, unique nonempty example ID, and no payment authorization state.
- The article is distinct from the September 20 morning climate-complaint package and from existing unit-rentability, vendor-handoff concept, maintenance tracker, gate repair and portfolio-close pieces. Exact title, slug, fictional Mesa Trace example and receipt-tool searches found no prior match. Public sitemap/feed preflight found no vendor-invoice/service-receipt match. Recheck at release.
- Voice scan found no self-aware “this article will,” invented quote, guaranteed savings or unsupported performance/customer claim. The source-register limitations are preserved in the text where federal examples appear.
- PHOTO-038 is a byte-exact 3840 × 2560 contextual AI-generated editorial image. The caption/alt/classification explicitly prevent a documentary vendor or testimonial claim. No rejected author portrait appears.

## Local layout and source QA

- Official FTC, GAO and Acquisition.gov pages were read through the current web result. The FTC and GAO official pages were readable in the web view but returned 403 to a direct command-line fetch; Acquisition.gov returned HTTP 200 directly and in web view. Source status is not exaggerated as three direct HTTP-200 checks.
- Local article preview screenshots and tool screenshots were generated at **1280, 390 and 320 pixels** in `review-only/`. Each reported document scroll width equal to viewport width, loaded image, zero page errors and no broken generated page state. The initially wide tool table was restyled as stacked labeled cards for 390/320, rerendered and visually inspected at original 320-pixel resolution; no clipped cell or hidden horizontal column remains.
- Automated Axe, production template, publisher asset-path, live link and deployment QA are **not** claimed. They remain the selected publisher's release gates.
- Research, drafting, tool and local QA were AI-assisted. Neither that assistance nor the governed image provenance is concealed.

The nine core deliverables are pinned in `checksums.sha256`. Review-only renderer and screenshots are retained for local evidence and excluded from the public release package.

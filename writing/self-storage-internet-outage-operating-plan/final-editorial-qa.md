# Final editorial QA — September 22 morning operator

## Identity and truthful state

- **Title:** “When the Office Internet Goes Down: A No-Guessing Plan for Self-Storage Managers.”
- **Author:** Jared Mastroianni.
- **Selected owned destination only:** Master Personal Site Authority, proposed canonical `https://jaredmodstorage.github.io/writing/self-storage-internet-outage-operating-plan/`.
- **Body length:** **1,614 words** from the title through the final operating paragraph, excluding the operator-tool and author notes after the horizontal rule. Count uses the final Markdown bytes and a word-token expression that preserves hyphenated and apostrophized words.
- **Writer-freeze state:** complete local package before one single-publisher handoff. No source commit, deployment, live canonical, sitemap/feed entry, discovery, indexing, coverage or recognition was created by this writer.

## Four scored review lenses

These are explicit reviews performed against the final local bytes by the assigned writer. They are not independent human approvals and do not certify a future deployment.

| Review lens | Score / 10 | Final evidence |
|---|---:|---|
| Self-storage trade editor: originality, fit and natural voice | **9.7** | Opens with a recognizable front-desk decision, stays product-neutral, avoids generic outage advice and develops one distinct thesis: the facility needs a service-by-service operating state rather than a facility-wide “up/down” label. |
| Specialist privacy/payment editor: evidence and restraint | **9.8** | Ready.gov, FTC, PCI SSC and NIST are used only within public scope. The article does not equate connectivity loss with a cyber incident, does not advise storing card data and does not claim compliance, diagnosis or performance. |
| Facility operator: next-shift utility | **9.8** | Five service states, five operating functions, an explicit fictional sequence and a closure checklist give the manager usable actions. The workbook separates front-desk decisions from detailed restoration and reconciliation evidence. |
| Rendered visual and tool QA | **9.7** | Article and responsive HTML tool were rendered at 1280, 390 and 320 pixels with zero horizontal overflow, failed images, empty links or page errors. The workbook was rendered to a three-page landscape PDF; its Read me and Operating view are legible, and its detailed register is intended for on-screen filtering and zoom rather than one-page print use. |

**Aggregate:** 9.75 / 10.

## Duplicate and originality checks

- The September 22 slot directory was empty before creation.
- Local corpus search found no prior office internet/connectivity outage operating article, matching title, slug, fictional example or operating-state register.
- A ten-word shingle comparison of substantive article text, excluding URL and author boilerplate, found no overlap outside this package.
- The proposed personal-site canonical returned HTTP 404. The refreshed personal-site sitemap and feed returned HTTP 200 and contained no internet/connectivity-outage match.
- The WordPress REST search returned one older camera-system outage article. Its subject is loss of camera monitoring; this article concerns office connectivity, customer service states, privacy boundaries and reconciliation. It is related but materially distinct.

## Source and link checks

- Ready.gov emergency plans: HTTP 200.
- PCI Security Standards Council merchant guidance: HTTP 200.
- NIST Cybersecurity Framework: HTTP 200.
- FTC business guidance: readable in the current browser source; a separate command-line request returned HTTP 403. The cited scope was verified from the browser source and is recorded conservatively.
- Final article contains four unique absolute HTTPS source links and no empty links.

## Operator-tool integrity

- CSV: 32 columns, eight fictional service rows, eight unique record IDs and consistent row width.
- XLSX: `Read me`, `Operating view` and `Detailed register`; 32-field detailed register; no formulas, macros, external links or hidden calculations.
- HTML: eight matching service cards; no form, script, storage, analytics or transmission.
- The workbook, CSV and HTML share the same approved fallback, prohibited workaround, privacy boundary, owner and reconciliation semantics.
- All sample values remain explicitly fictional and unreleased. `not_evaluated`, `not_started` and `not_released` states are preserved rather than represented as completed checks.

## Image and visual boundary

- PHOTO-031 is 3840 × 2560 RGB PNG.
- Available PNG metadata contains only an aspect entry; a metadata and byte-string scan found no OpenAI, ChatGPT, Codex, Claude, Anthropic, Gemini, Copilot, Midjourney, DALL-E, Stable Diffusion, ComfyUI, generator, workflow or prompt label.
- The image remains truthfully disclosed as AI-generated editorial imagery owned by Jared Mastroianni, not documentary outage, customer, facility, product or deployment evidence.
- Alt text and caption are meaningful, topic-matched and preserved in `image-notes.md`.

## Technical checks and publisher gates

- Article render: 1280/390/320, no overflow, image failure, page error or empty link.
- Tool render: 1280/390/320, no overflow, page error, empty link, form or script.
- Workbook render: three landscape pages; all sheets present; Operating view status fills and field text visible.
- Final forbidden/self-aware phrase scan: zero hits for “this article will,” “in this article,” “as an AI,” “delve,” “game-changing” and “revolutionary.”
- The publisher must still refresh duplicates, run source build and site tests, verify exact public downloads and image disclosure, inspect 1280/390/320 production output, then freeze source/deployment/rollback/run identities and public readback before marking Published.

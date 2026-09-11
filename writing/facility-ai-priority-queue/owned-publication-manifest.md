# Owned publication manifest

## Release target

- Route: `/writing/facility-ai-priority-queue/`
- Canonical: `https://jaredmodstorage.github.io/writing/facility-ai-priority-queue/`
- Publisher: Jared Mastroianni personal authority site only
- Publisher owner: Jared Mastroianni
- Schema: `TechArticle`, `ImageObject` and `BreadcrumbList`
- Author: Jared Mastroianni
- State: publication-ready local package only; no publisher handoff or public mutation
- Excluded owned publisher: modSTORAGE WordPress blog must reject the same complete article, title, slug, body and practical tool as a duplicate

## Required public package

- `below-the-fold-is-still-a-decision.md`
- `ai-queue-exposure-register.csv`
- `source-register.csv`
- `055-ai-development-customer-service-ai-pilot.png`
- `image-notes.md`

## Presentation requirements

- Preserve the title, deck, byline, disclosure and exact source limitations.
- Place the governed image after the byline with the exact alt text and caption from `image-notes.md`.
- Present the CSV as a downloadable operator tool and label all five example rows fictional.
- Do not describe the proposed queue architecture as a product, deployment, standard, audit, certification, compliance finding or measured operating result.

## Separate release gates

1. Reconfirm the title, route, slug, example and tool are absent immediately before any publisher mutation.
2. Verify every governed hash against `checksums.sha256`.
3. Build and test the source locally; verify structured data, internal links and all downloads.
4. Commit source with a known rollback parent.
5. Deploy once through the established personal-authority-site workflow.
6. Read back the canonical, H1, byline, disclosure, image, downloads, metadata, sitemap and feed at desktop and mobile widths.
7. Record source, deployment, rollback and provider-run identities separately.
8. Keep publication, crawling, indexing, ranking, coverage and recognition as separate states.

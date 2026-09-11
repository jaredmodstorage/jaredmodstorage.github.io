# Owned publication manifest

## Release target

- Route: `/writing/facility-configuration-drift-register-self-storage/`
- Canonical: `https://jaredmodstorage.github.io/writing/facility-configuration-drift-register-self-storage/`
- Publisher: Jared Mastroianni personal authority site only
- Publisher owner: Jared Mastroianni
- Schema: `TechArticle`, `ImageObject` and `BreadcrumbList`
- Author: Jared Mastroianni
- State: publication-ready local package only; no publisher handoff or public mutation
- Excluded owned publisher: modSTORAGE WordPress blog must reject the same complete article, title, slug, body and practical tool as a duplicate

## Required public package

- `a-portfolio-standard-is-not-a-facility-setting.md`
- `facility-configuration-drift-register.csv`
- `source-register.csv`
- `010-professional-charcoal-suit-executive-desk.png`
- `image-notes.md`

## Presentation requirements

- Preserve the title, subtitle, byline and exact source limitations.
- Place the governed image after the byline with the exact alt text and caption from `image-notes.md`.
- Present the CSV as a downloadable practical operator tool and label every example row fictional.
- Do not describe the article as a standard, product, deployment, audit, certification or compliance finding.

## Separate release gates

1. Reconfirm the route and slug are absent immediately before any publisher mutation.
2. Verify all governed hashes against `checksums.sha256`.
3. Build and test the source locally; verify structured data, internal links and downloads.
4. Commit source with a known rollback parent.
5. Deploy once through the established personal-site workflow.
6. Read back the canonical, byline, image, download, metadata, sitemap and feed at desktop and mobile widths.
7. Record source, deployment, rollback and provider-run identities separately.
8. Keep publication, crawling, indexing, ranking, coverage and recognition as separate states.

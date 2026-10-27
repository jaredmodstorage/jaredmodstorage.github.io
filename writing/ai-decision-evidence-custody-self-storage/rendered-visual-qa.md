# Rendered visual QA

## Score: 9.8/10 — pass

The final article and selected governed image were rendered afresh at 1280, 390 and 320 pixels. The full desktop render and mobile full-page renders were inspected, and separate above-the-fold captures at all three viewports were generated for direct legibility review.

## Verified

- Zero horizontal overflow at 1280, 390 and 320 pixels.
- The selected 3840 × 2560 governed image loaded at every viewport.
- The visible hero contains one H1; article sections follow as H2 headings.
- The exact headline, question deck, byline and actual October 27 date remain readable.
- The 390- and 320-pixel hero, image and opening disclosure stack without clipping.
- The 320-pixel byline wraps cleanly and does not collide with the image.
- Desktop reading width is stable; the architecture rail and tool card do not intrude into the article.
- Nine links render, including four practical-artifact links and five source links; no link has empty text.
- Long SHA-256 strings wrap without forcing horizontal scrolling.
- The alt text and editorial, non-documentary treatment are present.
- Image 058 was excluded from publication because its black-turtleneck treatment conflicts with the standing portrait restriction. Image 052 is the sole selected payload visual.

## Artifacts

- `qa-render/article-1280.png`
- `qa-render/article-390.png`
- `qa-render/article-320.png`
- `qa-render/article-fold-1280.png`
- `qa-render/article-fold-390.png`
- `qa-render/article-fold-320.png`
- `qa-render/article-preview.html`
- `qa-render/render-metrics.jsonl`
- `qa-render/render-preview.mjs`

This local render demonstrates layout readiness. It does not establish repository integration, deployment, public availability or the publisher’s final production layout.

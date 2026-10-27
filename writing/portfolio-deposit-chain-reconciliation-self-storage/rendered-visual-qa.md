# Rendered visual QA

Rendered and visually inspected 2026-10-27 using the governed package image and an editorial preview that preserves the intended authority-site hierarchy.

| Viewport | Proof | Finding |
|---|---|---|
| 1280 × 900 | `qa-render/article-1280-top.png` and `qa-render/article-1280.png` | Balanced split hero, legible headline/deck/byline, full discussion context, stable three-column article grid, readable measure and clear rail/tool callouts. |
| 390 × 844 | `qa-render/article-390-top.png` and `qa-render/article-390.png` | Clean single-column flow, complete headline and date, topic-matched image, readable body and headings, no clipped content. |
| 320 × 844 | `qa-render/article-320-top.png` and `qa-render/article-320.png` | Headline, deck and date wrap without collision; image retains the listening scene; body remains legible at the narrow release floor. |

Automated render metrics in `qa-render/render-metrics.json` confirm for all three widths:

- zero horizontal overflow;
- image loaded at 3840 × 2560 with non-empty alt text;
- four body source links and zero empty links;
- one H1 and eight semantic body H2s;
- white reading surface and dark body text; and
- complete full-page captures.

**Internal rendered-visual review:** 9.7/10. The preview is release-quality across all three required widths. The image, hierarchy, contrast, measure and responsive behavior support the article without suggesting a documentary deposit event. This is the writer’s internal visual judgment, not an independent accessibility certification or third-party endorsement.

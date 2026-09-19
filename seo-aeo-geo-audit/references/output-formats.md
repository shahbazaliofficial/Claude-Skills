# Output Formats

Ask which format fits the use case if it's not already clear from context (internal review → dashboard; sharing with a client or stakeholder outside the team → report).

## Dashboard artifact

Follow the same pattern as `meta-ads-account-analysis` / `google-analytics-account-analysis` / `google-search-console-analysis`:

- Single self-contained HTML file, inline CSS/JS, CDN chart library if needed (Chart.js is a reasonable default). Read `frontend-design` before styling.
- Drill-down structure: **site overview** (overall health snapshot, one summary block per pillar, top priority findings) → **pillar breakdown** (tabs or sections for Technical / On-page / AEO / GEO, each with its findings sorted by severity) → **page-level detail** (specific pages and their specific issues, reachable from the pillar view).
- Use real charts where they add value: a severity/effort matrix (scatter or quadrant chart) for prioritization is especially useful here; simple bar/donut for issue counts by pillar or severity.
- Save to `/mnt/user-data/outputs/` and present it.

## Client-presentable report

Follow the same pattern as `meta-ads-proposal`:

- Build as a designed slide deck via the `pptx` skill (`pptxgenjs`), not a flat document — vary layouts per section, use real charts for the severity/effort breakdown and pillar summaries.
- Suggested flow: Cover → Executive Summary (health by pillar, top findings) → Technical SEO findings → On-page/Content findings → AEO findings → GEO findings (clearly separating confirmed data from readiness signals) → Prioritized Recommendations / Roadmap → Next Steps.
- Export to PDF with `scripts/office/soffice.py --headless --convert-to pdf`. Deliver both the PDF (primary) and the editable `.pptx`.
- Keep client-facing language accessible — translate technical findings ("missing canonical tags causing duplicate content") into plain business impact ("search engines are splitting ranking credit across duplicate versions of the same page, weakening how well any single version ranks") without losing the specific, actionable detail.

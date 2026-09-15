# Dashboard Design

Build a single self-contained HTML file (inline CSS/JS, no external dependencies beyond a CDN chart library if needed) and save it to `/mnt/user-data/outputs/`. Read the `frontend-design` skill before styling — don't ship default/templated-looking UI.

## Structure (drill-down, not a flat dump)

1. **Account summary (top level, always visible)**: total spend, blended ROAS or cost-per-result, headline trend sparkline, and 2-3 flagged campaigns (best/worst).
2. **Campaign breakdown**: a table or card grid, one row/card per campaign, sortable/scannable, each showing its objective-appropriate metric plus spend share.
3. **Ad set / ad detail**: reachable by clicking a campaign (tabs, accordion, or simple client-side view-switching — plain JS is fine, no framework needed). Show frequency/CTR trend per ad where creative fatigue is relevant.

Use tabs or click-to-expand rather than showing all three levels flattened on one page — the point of "drill-down" is that the user isn't drowning in every ad at once.

## Charts

- Time series (spend, CPA, ROAS trend) → line chart.
- Campaign comparison (spend vs. results) → bar chart, or a scatter (spend vs. ROAS) to spot waste vs. scale-worthy campaigns at a glance.
- Creative fatigue → small multi-line chart per ad (frequency vs. CTR over time) only where data supports it.

Chart.js via CDN (`https://cdnjs.cloudflare.com`) is a reasonable default — simple API, no build step. Keep the palette restrained and consistent with the rest of the dashboard rather than defaulting to library rainbow colors.

## What NOT to do

- Don't render a giant flat table of every ad as the primary view — that's a spreadsheet, not a dashboard.
- Don't fabricate benchmark lines ("industry average CTR is X%") unless the user supplied a benchmark or you have it from the data itself.
- Don't skip the prose summary in chat in favor of "see the dashboard" — the dashboard is the detail, the chat message is the takeaway.

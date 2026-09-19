# Dashboard Design

Build a single self-contained HTML file (inline CSS/JS, CDN chart library if needed) and save it to `/mnt/user-data/outputs/`. Read the `frontend-design` skill before styling — don't ship default/templated-looking UI.

## Structure (drill-down, not a flat dump)

1. **Property summary (top level, always visible)**: total clicks, impressions, average CTR, average position, trend sparklines, and 2-3 flagged findings (e.g., a query with high impressions but poor CTR, a page whose position dropped sharply).
2. **Query / page breakdown**: a table or card grid — toggle or tab between "By Query" and "By Page" views, each showing clicks, impressions, CTR, and position together so the trade-offs (visibility vs. pull-through vs. rank) are visible at once, not just a sorted click count.
3. **Coverage & health detail**: reachable via a separate tab, if coverage/indexing data is available — list of excluded/error pages grouped by reason. If this data wasn't provided, omit this section entirely rather than showing an empty one.

Use tabs or click-to-expand rather than flattening everything onto one page.

## Charts

- Time series (clicks, impressions, CTR, average position trend) → line chart. Position is inverted on the y-axis conventionally (lower number = better) — either invert the axis or clearly label it so a rising line doesn't read as "improving" by mistake.
- Position vs. CTR scatter (one point per query or page) → good for spotting the CTR-vs-position mismatches described in the main skill (high impressions/good position but poor CTR, or vice versa).
- Query/page comparison (clicks vs. impressions) → bar chart, or grouped bars to show both side by side.
- Coverage breakdown (indexed vs. excluded vs. error, by reason) → donut or bar chart, only if coverage data is available.

Chart.js via CDN (`https://cdnjs.cloudflare.com`) is a reasonable default. Keep the palette restrained and consistent with the rest of the dashboard.

## What NOT to do

- Don't render a giant flat table of every query/page as the primary view — GSC properties can have thousands of rows.
- Don't blend query/page performance and coverage/indexing health into one score — they're different signals and should stay visually separate.
- Don't treat position changes on low-impression queries as meaningful trends without noting the small sample size.
- Don't skip the prose summary in chat in favor of "see the dashboard."

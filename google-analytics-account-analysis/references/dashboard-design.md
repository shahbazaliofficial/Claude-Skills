# Dashboard Design

Build a single self-contained HTML file (inline CSS/JS, CDN chart library if needed) and save it to `/mnt/user-data/outputs/`. Read the `frontend-design` skill before styling — don't ship default/templated-looking UI.

## Structure (drill-down, not a flat dump)

1. **Property summary (top level, always visible)**: total sessions/users, headline conversion or engagement metric, trend sparkline, and 2-3 flagged findings (e.g., a channel losing traffic, a page with unusually high engagement).
2. **Channel/traffic breakdown**: a table or card grid, one row/card per channel group (Organic Search, Paid Search, Direct, Referral, Social, Email, etc.), showing sessions, engagement rate, and conversions/conversion rate side by side — so volume and quality are visible together, not just volume.
3. **Page / event detail**: reachable by clicking a channel or from a separate tab — top landing pages with their engagement and conversion performance, or top events/key events if that's more relevant to the property's purpose.

Use tabs or click-to-expand rather than flattening everything onto one page.

## Charts

- Time series (sessions, users, engagement rate, conversions trend) → line chart.
- Channel comparison (volume vs. quality) → bar chart for sessions, or a scatter (sessions vs. conversion rate) to spot channels that drive volume but not results, and vice versa.
- Funnel / drop-off (if event data supports a sequence like landing → key event) → simple funnel chart, only where the data actually supports a sequence — don't fabricate funnel steps that aren't in the data.
- Device/geography split → small bar or donut, kept secondary rather than a focal chart unless the user specifically cares about it.

Chart.js via CDN (`https://cdnjs.cloudflare.com`) is a reasonable default. Keep the palette restrained and consistent with the rest of the dashboard.

## What NOT to do

- Don't render a giant flat table of every page/source as the primary view.
- Don't fabricate a funnel or benchmark that isn't supported by the actual data.
- Don't present sampled or thresholded GA4 data as if it were exact — carry forward any such caveat visibly.
- Don't skip the prose summary in chat in favor of "see the dashboard."

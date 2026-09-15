# Data Sources

## 1. Connector / API

Check tools for a connected ads-data MCP (e.g., Windsor.ai, Supermetrics, Abency, or similar). If found, pull campaign/ad set/ad-level data for the requested date range. If nothing is connected but the user wants live data, use `search_mcp_registry` with keywords like `["meta ads", "facebook ads", "advertising"]`, then `suggest_connectors` — let the user choose, never pick a connector for them.

Once connected, request fields at the most granular level available (ad-level, daily breakdown) even if the dashboard will roll some of it up — it's easier to aggregate than to go back for more detail.

## 2. Uploaded export (CSV/Excel)

Standard Meta Ads Manager export columns to look for (names vary slightly by export settings):

- Campaign name, Ad set name, Ad name
- Reporting starts / Reporting ends (or a single Day column)
- Amount spent
- Impressions, Reach, Frequency
- CPM (Cost per 1,000 impressions)
- Link clicks / Clicks (all), CTR, CPC
- Results, Cost per result, Result type (tells you the objective)
- Purchases / Purchase value / ROAS (if a sales campaign)

Read the file directly (pandas or equivalent for CSV/Excel). Watch for:
- Merged/rolled-up rows (a "Campaign" row with no ad set breakdown) mixed in with granular rows — dedupe so you don't double-count spend.
- Currency symbols or thousands separators in numeric columns that need stripping before math.
- Date ranges that don't cover a full period (partial week/month) — note this if it affects trend analysis.

## 3. Pasted text / screenshot

For pasted tables, parse directly. For screenshots, read the visible values carefully and state them back briefly (e.g., "Reading: Campaign A — $412 spent, 3.1 ROAS...") before using them, since Ads Manager screenshots can have small text, truncated columns, or tooltips that are easy to misread. If a number is genuinely unclear, say so and ask rather than guessing.

Screenshots typically only show one view (e.g., campaign-level table) — don't assume ad set/ad-level detail exists unless the user provides it separately. Build the dashboard at whatever level of granularity the screenshot actually supports, and say if a deeper drill-down isn't available.

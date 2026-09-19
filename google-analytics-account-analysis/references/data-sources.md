# Data Sources

## 1. Connector / API

Check tools for a connected analytics MCP (e.g., Windsor.ai, Supermetrics, Polar Analytics, or a direct GA4 connector). If found, pull data at the most granular dimension combination reasonable for the request (e.g., date × channel group × landing page) even if the dashboard will roll some of it up.

If nothing is connected but the user wants live data, use `search_mcp_registry` with keywords like `["google analytics", "GA4", "web analytics"]`, then `suggest_connectors` — let the user choose, never pick one for them.

Note: GA4's native API can mark results as "thresholded" (data withheld for privacy) or "sampled" (estimated from a subset) — if a connector surfaces this, flag it rather than presenting the numbers as exact.

## 2. Uploaded export (CSV/Excel)

GA4 exports vary by report type (Reports snapshot, Explore ad hoc export, Looker Studio export). Common columns to look for:

- Date / Date range
- Session default channel group, Session source / medium, Session campaign
- Landing page + query string / Page path
- Device category, Country/Region, City
- Sessions, Total users, New users, Engaged sessions
- Engagement rate, Average engagement time per session, Bounce rate
- Key events / Conversions, Event count, Session conversion rate
- Total revenue, Ecommerce purchases (if ecommerce tracked)

Watch for:
- Comparison exports that include two date ranges side by side — make sure you're not treating "this period" and "previous period" columns as separate data points in a trend.
- Sampling/thresholding notices sometimes included as a header note in the export — carry that caveat into the analysis.
- Currency symbols or percentage signs in numeric columns that need stripping before math.

## 3. Pasted text / screenshot

For pasted tables, parse directly. For screenshots, read carefully and restate key values back before using them (e.g., "Reading: Organic Search — 4,210 sessions, 62% engagement rate..."), since the GA4 UI is dense and easy to misread (small percentage-change chips, truncated dimension names, collapsed rows). If a number is unclear, ask rather than guessing.

Screenshots typically show one report view at a time — don't assume you have channel *and* page *and* device detail unless the user provides multiple screenshots or a fuller export. Build the dashboard at whatever level of granularity is actually available, and say if a deeper drill-down isn't possible from what was given.

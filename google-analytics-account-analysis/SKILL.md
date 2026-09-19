---
name: google-analytics-account-analysis
description: Analyze Google Analytics (GA4) property performance and build a drill-down dashboard artifact covering traffic/acquisition, engagement/behavior, and conversions. Use this whenever the user wants their website or app analytics reviewed or audited — including phrases like "analyze my Google Analytics", "how's my site traffic doing", "review my GA4 property", "analytics dashboard", "where is my traffic coming from", "which pages/channels convert best", "is my traffic dropping", or when they upload a GA4 export (CSV/Excel), paste analytics data, share a screenshot of the GA4 interface, or ask to connect to a Google Analytics data source. Trigger even if they don't say "Google Analytics" explicitly but describe metrics like sessions, users, bounce rate, engagement rate, conversions, channel grouping, or landing pages.
---

# Google Analytics Account Analysis

Turn raw GA4 data (from an API connector, an exported file, or pasted/screenshotted data) into a structured analysis and a drill-down dashboard artifact: property overview → channel/traffic breakdown → page/event detail.

## Workflow

### 1. Identify the data source

- **Connector/API**: Check available tools for a Google Analytics / GA4 connector (Windsor.ai, Supermetrics, Polar Analytics, or a direct GA4 MCP if connected). If one exists, use it. If the request implies live data and nothing's connected, use `search_mcp_registry` + `suggest_connectors` — don't default to asking for a file.
- **Uploaded export (CSV/Excel)**: A GA4 report export (from Reports, Explore, or Looker Studio). Parse it like any tabular file.
- **Pasted text / screenshot**: Extract visible metrics from a pasted table or GA4 UI screenshot. Because GA4's UI is dense (small numbers, percentage-change chips, truncated dimension names), briefly restate what you read before using it, and flag anything ambiguous rather than guessing.

See `references/data-sources.md` for the standard field set per source and known GA4 export quirks.

If the source is ambiguous, ask once rather than guessing.

### 2. Normalize the data

Extract into one internal model with these fields where available: date/date range, channel group (Organic Search, Paid Search, Direct, Referral, Social, Email, etc.), source/medium, campaign, landing page / page path, device category, country, sessions, users (total and new), engaged sessions, engagement rate, average engagement time, bounce rate (if present), conversions/key events, conversion rate, event count, and revenue (if ecommerce is tracked).

Missing fields are normal — GA4 exports vary a lot by report type. Work with what's there and note gaps rather than inventing numbers.

### 3. Understand what "good" looks like for this property

GA4 doesn't have one universal success metric — it depends on what the site/app does:

- Content/media site → engagement rate, average engagement time, pages per session
- Lead-gen site → conversion rate on key events (form fills, signups), traffic quality by channel
- Ecommerce → revenue, conversion rate, average order value, revenue by channel

Infer the site's likely purpose from the data (event names, presence of ecommerce fields, channel mix) and judge performance against the metric that purpose actually cares about. Judge contextually against the property's own trend (e.g., trailing average) rather than an external benchmark, unless the user gives you specific targets.

### 4. Run the analysis

Cover these angles (skip any the data can't support, and say so):

- **Traffic & acquisition** — which channels/sources drive volume, and which drive *quality* traffic (engagement, conversions) — these aren't always the same channels; call out the gap when it exists.
- **Trends over time** — if multiple dates are available, chart sessions/users, engagement rate, and conversions over time; flag notable drops or spikes.
- **Engagement & behavior** — top landing pages and how they perform (engagement rate, bounce, exit), device/geography splits if relevant.
- **Conversions & funnel efficiency** — conversion rate by channel and by landing page; where traffic is being lost or where a channel over-delivers volume but under-delivers conversions.

### 5. Build the dashboard artifact

Build a single-file HTML artifact with a drill-down structure: property-level summary → channel/traffic breakdown → page or event-level detail. Use real charts (trend lines, channel comparison, funnel where applicable) not just tables. See `references/dashboard-design.md` for layout, chart choices, and styling (it points to the frontend-design skill for visual polish).

Save the file to `/mnt/user-data/outputs/` and present it — don't just describe the dashboard in chat.

### 6. Summarize in chat

Give a short prose summary of the headline findings and top 2-3 recommended actions alongside the artifact. Don't restate every chart in text.

## Notes

- If the user has multiple GA4 properties or asks to compare properties/date ranges, confirm scope before building — the dashboard structure differs for a single-property view vs. a comparison.
- If data volume is large (many pages/sources), aggregate into top-N plus "other" rather than rendering everything; offer to drill into specifics on request.
- Always be upfront about data limitations (missing fields, single snapshot, unverified screenshot numbers, sampled data if GA4 flags it as such).

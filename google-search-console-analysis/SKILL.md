---
name: google-search-console-analysis
description: Analyze Google Search Console (GSC) performance and build a drill-down dashboard artifact covering search queries, pages, rankings/position, CTR, and indexing/coverage health. Use this whenever the user wants their organic search performance reviewed or audited — including phrases like "analyze my Search Console", "how's my SEO performance", "review my GSC data", "search performance dashboard", "which queries/pages are ranking", "is my traffic from Google search dropping", "indexing issues", "coverage errors", or when they upload a GSC export (CSV/Excel), paste query/page performance data, share a screenshot of the Search Console interface, or ask to connect to a Search Console data source. Trigger even if they don't say "Search Console" explicitly but describe metrics like impressions, clicks, average position, CTR, or indexed/excluded pages.
---

# Google Search Console Analysis

Turn raw GSC data (from an API/connector, an exported file, or pasted/screenshotted data) into a structured analysis and a drill-down dashboard artifact: property overview → query/page breakdown → coverage & health detail.

## Workflow

### 1. Identify the data source

- **Connector/API**: Check available tools first for direct GSC tools (e.g., Ahrefs' `gsc-*` tools — performance history, page history, by-device, by-position breakdowns) if a connector is already connected. If nothing suitable is connected but the user wants live data, use `search_mcp_registry` with keywords like `["google search console", "search console", "SEO"]`, then `suggest_connectors` — don't default to asking for a file.
- **Uploaded export (CSV/Excel)**: A GSC Performance report export (Queries or Pages tab) or a bulk export from the API. Parse it like any tabular file.
- **Pasted text / screenshot**: Extract visible metrics from a pasted table or a Search Console UI screenshot. Because the GSC UI truncates long queries/URLs and shows small numbers, briefly restate what you read before using it, and flag anything ambiguous.

See `references/data-sources.md` for the standard field set per source and known GSC export quirks.

If the source is ambiguous, ask once rather than guessing.

### 2. Normalize the data

Extract into one internal model with these fields where available: date/date range, query, page/URL, country, device, search appearance, clicks, impressions, CTR, average position. For coverage/indexing data (if provided separately): page URL, coverage status (indexed/excluded/error), reason, last crawled date.

Missing fields are normal — GSC exports differ depending on which tab/report was pulled. Work with what's there and note gaps rather than inventing numbers.

### 3. Judge performance in GSC's own terms

GSC data doesn't have one blended "success" number — it's a trade-off between visibility (impressions), pull-through (CTR), and rank (position), and what matters shifts by query intent:

- High impressions + low CTR + good position → title/meta description isn't earning the click; a CTR problem, not a ranking problem.
- Good CTR + low impressions → the page ranks well for something too narrow; a visibility/targeting problem.
- Declining position over time on previously-strong queries → possible content decay, algorithm shift, or new competition.
- High impressions + position just outside page 1 (11-20) → "low-hanging fruit": close to a big traffic jump with the right push.

Judge contextually against the property's own trend rather than an external CTR benchmark, unless the user gives you specific targets.

### 4. Run the analysis

Cover these angles (skip any the data can't support, and say so):

- **Query performance** — top queries by clicks and by impressions (often different lists); flag CTR-vs-position mismatches (see above).
- **Trends over time** — if multiple dates are available, chart clicks, impressions, CTR, and average position over time; flag notable drops (possible algorithm impact, seasonality, or technical issue) or gains.
- **Page performance** — top pages by clicks/impressions, and pages with declining position or CTR worth investigating.
- **Coverage & indexing health** — if coverage/indexing data is available, surface excluded/error pages and likely causes; this is a distinct signal from query/page performance and shouldn't be blended into it.

### 5. Build the dashboard artifact

Build a single-file HTML artifact with a drill-down structure: property-level summary → query/page breakdown → coverage/health detail. Use real charts (trend lines, position-vs-CTR scatter, etc.) not just tables. See `references/dashboard-design.md` for layout, chart choices, and styling (it points to the frontend-design skill for visual polish).

Save the file to `/mnt/user-data/outputs/` and present it — don't just describe the dashboard in chat.

### 6. Summarize in chat

Give a short prose summary of the headline findings and top 2-3 recommended actions (e.g., specific pages to update titles/meta on, specific queries close to page-1 breakthrough) alongside the artifact. Don't restate every chart in text.

## Notes

- If the user has multiple properties (domains) or asks to compare properties/date ranges, confirm scope before building — the dashboard structure differs for a single-property view vs. a comparison.
- GSC data is inherently noisy at low volumes (queries with a handful of impressions) — don't over-interpret small-sample fluctuations as trends.
- If data volume is large (thousands of queries/pages), aggregate into top-N plus "other" rather than rendering everything; offer to drill into specifics on request.
- Always be upfront about data limitations (missing fields, single snapshot, unverified screenshot numbers, GSC's own data-freshness lag of a few days).

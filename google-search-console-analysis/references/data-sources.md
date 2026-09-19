# Data Sources

## 1. Connector / API

Check tools first for direct Google Search Console tools — Ahrefs (if connected) exposes several: `gsc-performance-history`, `gsc-page-history`, `gsc-performance-by-device`, `gsc-performance-by-position`, `gsc-keywords`, `gsc-pages`, `gsc-ctr-by-position`, `gsc-metrics-by-country`, `gsc-anonymous-queries`, among others — these map closely onto GSC's own Performance report. Other connected marketing-analytics MCPs (Windsor.ai, Supermetrics) may also expose GSC as a data source.

If nothing suitable is connected but the user wants live data, use `search_mcp_registry` with keywords like `["google search console", "search console", "SEO"]`, then `suggest_connectors` — let the user choose, never pick one for them.

Pull data at query × page × date granularity where reasonable, even if the dashboard will roll some of it up — easier to aggregate than to go back for more detail. Note that GSC only returns the top ~1,000 rows per API query by default; if the property is large, you may need multiple calls with filters (e.g., by page or date range) to get full coverage, or work with an aggregated export instead.

## 2. Uploaded export (CSV/Excel)

GSC exports come from two main places — the **Performance report** (Queries tab or Pages tab) or a **Coverage/Indexing report**. They have different columns:

**Performance export:**
- Top queries (or Top pages)
- Clicks, Impressions, CTR, Position
- Optionally a date column if exported with a date breakdown, or Date range noted in the filename/header

**Coverage/Indexing export:**
- URL
- Status (Indexed / Excluded / Error, or more specific reasons like "Crawled - currently not indexed", "Discovered - currently not indexed", "Duplicate without user-selected canonical")
- Last crawled

Watch for:
- CTR exported as a percentage string ("4.2%") rather than a number — needs parsing before math.
- Position values are averages and can be fractional (e.g., 11.4) — don't round in a way that hides whether something is page 1 vs. page 2.
- Performance and Coverage exports are separate files from GSC — don't assume both are available unless the user provides both.

## 3. Pasted text / screenshot

For pasted tables, parse directly. For screenshots, read carefully and restate key values back before using them (e.g., "Reading: 'buy running shoes' — 1,240 impressions, 3.1% CTR, position 8.4..."), since the GSC UI truncates long queries and URLs and shows small numbers. If a number or truncated query/URL is unclear, ask rather than guessing.

Screenshots typically show one view at a time (either the Queries tab or the Pages tab, not both) — don't assume you have both query and page-level detail unless the user provides multiple screenshots or a fuller export. Build the dashboard at whatever level of granularity is actually available.

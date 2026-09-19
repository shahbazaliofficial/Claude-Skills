---
name: meta-ads-account-analysis
description: Analyze Meta (Facebook/Instagram) ad account performance and build a drill-down dashboard artifact with performance flags, trend analysis, creative fatigue detection, and budget efficiency insights. Use this whenever the user wants their Meta/Facebook/Instagram ads analyzed, reviewed, or audited — including phrases like "analyze my meta ads account", "how are my facebook ads performing", "review my ad campaigns", "ads dashboard", "campaign performance", "is my ad spend efficient", "which campaigns should I kill/scale", or when they upload a Meta Ads Manager export (CSV/Excel), paste ad account data, share a screenshot of Ads Manager, or ask to connect to a Meta/Facebook ads data source. Trigger even if they don't use the word "Meta" or "Facebook" explicitly but describe ad account metrics like ROAS, CPA, CTR, frequency, or spend by campaign/ad set/ad.
---

# Meta Ads Account Analysis

Turn raw Meta Ads data (from an API connector, an exported file, or pasted/screenshotted data) into a structured analysis and a drill-down dashboard artifact: account → campaign → ad set/ad.

## Workflow

### 1. Identify the data source

Three possible sources — figure out which one applies before doing anything else:

- **Connector/API**: Check available tools for a Meta/Facebook Ads connector (Windsor.ai, Supermetrics, or similar ads-data MCP). If one is connected, use it. If the user's request implies pulling live data and no connector is connected, use `search_mcp_registry` + `suggest_connectors` — don't just default to asking for a file.
- **Uploaded export (CSV/Excel)**: A Meta Ads Manager export. Read it with the xlsx skill's approach for tabular data (or plain CSV parsing for simple files).
- **Pasted text / screenshot**: The user pastes a table or shares a screenshot of Ads Manager. Extract the visible metrics. Because OCR/vision extraction from screenshots is error-prone, briefly state the numbers you read and flag any that were ambiguous — don't silently guess.

See `references/data-sources.md` for extraction details and the standard field set to look for in each case.

If the source is ambiguous (user just says "analyze my ads"), ask once which source they mean rather than guessing — see the elicitation pattern in the examples below.

### 2. Normalize the data

Whatever the source, extract into one internal table (or a natural mental model) with these fields where available: date/date range, campaign name, campaign objective, ad set name, ad name, spend, impressions, clicks, CTR, CPM, CPC, results, cost per result, purchase/conversion value, ROAS, frequency, reach.

Missing fields are normal (e.g., a screenshot may only show 4 columns) — work with what's there and note what's missing rather than inventing numbers.

### 3. Detect the right success metric per campaign

Meta objectives aren't all optimizing for the same thing. Infer the objective (awareness, traffic, engagement, leads, app installs, sales/conversions) from campaign name, objective field, or available metrics, and judge performance against the metric that objective actually cares about:

- Awareness/reach → CPM, frequency
- Traffic/engagement → CTR, CPC
- Leads/conversions/sales → cost per result, ROAS

Don't apply a single fixed threshold across the account — judge each campaign contextually against what's normal *for that campaign/account* (e.g., compare to the account's own trailing average) rather than an external benchmark, unless the user gives you specific targets to use.

### 4. Run the analysis

Cover these angles (skip any that the data genuinely can't support, and say so):

- **Performance flags** — which campaigns/ad sets are clearly over- or under-performing relative to the rest of the account, and why.
- **Trends over time** — if the data has multiple dates/periods, chart spend, CPA, and ROAS trajectory. If it's a single snapshot, skip trends and note that a time series wasn't available.
- **Creative fatigue** — look for rising frequency paired with declining CTR or rising CPM on the same ad/ad set over time as the signal; flag candidates for creative refresh.
- **Budget & spend efficiency** — where spend is concentrated vs. where results are concentrated; call out obvious waste (high spend, poor results) and scaling opportunities (strong results, room to spend more).

### 5. Build the dashboard artifact

Build a single-file HTML artifact with a drill-down structure: account-level summary → campaign breakdown → ad set/ad detail (tabs or click-through, not everything dumped flat). Use real charts for trends and comparisons, not just tables. See `references/dashboard-design.md` for the layout pattern, chart choices, and styling approach (it points to the frontend-design skill for visual polish).

Save the file to `/mnt/user-data/outputs/` and present it — don't just describe the dashboard in chat.

### 6. Summarize in chat

Alongside the artifact, give a short prose summary (a few sentences to a short paragraph) of the headline findings and the top 2-3 recommended actions. Don't restate every chart in text — the dashboard is the detail; the chat message is the "so what."

## Notes

- If the user has multiple ad accounts or asks to compare accounts, confirm scope (single account vs. comparison) before building — the dashboard structure differs.
- If data volume is very large (many campaigns/ad sets), summarize/aggregate in the dashboard rather than rendering hundreds of rows; offer to drill into a specific campaign on request.
- Always be upfront about data limitations (missing fields, single snapshot, unverified screenshot numbers) — don't present inferred/estimated figures as if they were confirmed.

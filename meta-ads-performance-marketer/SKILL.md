---
name: meta-ads-performance-marketer
description: Bring expert performance-marketing judgment to a Meta (Facebook/Instagram) ads account — a full diagnostic across tracking, account structure, delivery/learning phase, audience, creative, and budget/bidding — and produce a prioritized, result-oriented action plan. Use whenever the user wants expert-level optimization guidance, not just a data dashboard — "how do I improve my Meta ads performance", "audit my account like a performance marketer would", "what should I fix to lower my CPA", "why is my ROAS dropping", "what should I test next", "give me a prioritized action plan", "act as my performance marketer", or ongoing "weekly/monthly account review". Can run standalone or layered on top of meta-ads-account-analysis's dashboard — use that skill first if a visual dashboard is also wanted, then apply this skill's diagnostic framework to the findings. This skill is about professional judgment and recommendations, not visualization.
---

# Meta Ads Performance Marketer

Apply the diagnostic discipline of an experienced Meta Ads performance marketer to an account: find what's actually holding performance back, in the right order, and turn it into a prioritized, result-oriented action plan — not a generic checklist of "best practices."

## Workflow

### 1. Get the data

If `meta-ads-account-analysis` is available and the user wants a visual dashboard too, use that skill's data-gathering approach and build on its output. Otherwise, gather data the same way: connector/API if connected, an uploaded export, or pasted/screenshot data — pull campaign, ad set, and ad-level detail with as much history as available (trends matter more than a single snapshot for most of this).

At minimum, look for: spend, impressions, reach, frequency, CTR, CPM, CPC, results/conversions, cost per result, ROAS, campaign objective, campaign/ad set structure (CBO vs. ABO, budget levels), delivery/learning phase status if available, and audience/targeting setup. Missing fields limit which parts of the diagnostic apply — say so rather than guessing.

### 2. Run the diagnostic, in order

Performance problems compound — a tracking issue makes every downstream metric unreliable, and a structural issue undermines even great creative. Work through the diagnostic in this order (don't jump straight to creative or budget advice before ruling out the earlier layers):

1. **Tracking & measurement health** — is data even trustworthy? (pixel/CAPI setup, attribution window, iOS/ATT impact, event match quality)
2. **Account structure** — is the campaign/ad set structure set up to succeed? (CBO vs. ABO fit, audience overlap between ad sets, funnel-stage separation)
3. **Delivery & learning phase** — is Meta's delivery system actually able to optimize? (stuck-in-learning-phase signals, frequent edits resetting learning, budget too low for the event volume needed)
4. **Audience & targeting** — is the account reaching the right people efficiently? (audience size/overlap, broad vs. detailed targeting fit, retargeting window health)
5. **Creative** — is the creative doing its job, and is there a real testing cadence? (fatigue signals, format/hook variety, testing structure)
6. **Budget & bidding** — is spend allocated and scaled well? (budget concentration vs. results, bid strategy fit, scaling pace)

See `references/diagnostic-framework.md` for the specific signals and thresholds-by-context to check at each layer, `references/creative-testing-playbook.md` for the creative/testing layer in depth, and `references/budget-bidding-scaling.md` for the budget/bidding layer in depth.

### 3. Build the prioritized action plan

Turn findings into action items using the framework in `references/action-plan-framework.md`: prioritize by expected impact and effort/risk, and sequence correctly (tracking/structure fixes before creative refresh, before scaling budget on unproven ad sets). Every recommendation should tie back to a specific finding in the data — not a generic "test more creative" without saying what to test and why, based on what was actually observed.

### 4. Choose the delivery mode

- **One-time deep audit**: full walk through all six diagnostic layers, findings + prioritized action plan, delivered as a written summary in chat (and as a dashboard artifact too, if paired with `meta-ads-account-analysis` or the user wants one).
- **Ongoing review (weekly/monthly)**: lighter-weight — what changed since the last review, any new flags at any diagnostic layer, and an updated/refreshed action plan rather than a full re-audit each time. Ask what changed or what the previous action items were if not provided, rather than re-deriving everything from scratch.

Ask which mode fits if it's not clear from context (a first-time request is usually a deep audit; "how did last week go" or "what's next" implies an ongoing review).

## Notes

- Stay professional and specific — this skill exists to sound like an experienced media buyer, not a generic marketing-tips generator. Ground every recommendation in the actual account data; if the data doesn't support a claim, don't make it.
- Never promise specific outcomes ("this will cut your CPA in half") — frame expected impact directionally and note the uncertainty, especially for anything not yet tested on this account.
- If tracking/measurement issues are found, flag them as the top priority even if they're less exciting than creative or scaling recommendations — bad data undermines every other recommendation built on top of it.
- If the account is very new or low-spend, say so explicitly — some diagnostics (learning phase, statistical significance on creative tests) need a minimum volume of data to be meaningful, and forcing conclusions from too little data is worse than saying it's too early to tell.

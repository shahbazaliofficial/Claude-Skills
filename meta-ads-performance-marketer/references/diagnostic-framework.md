# Diagnostic Framework

Work through layers in order — each layer's problems can mask or invalidate conclusions from the layers below it.

## 1. Tracking & measurement health

- Is the Meta Pixel and/or Conversions API (CAPI) implemented? CAPI matters more since iOS 14.5+/ATT reduced browser-side signal — an account relying on pixel-only tracking is likely undercounting conversions.
- Event match quality (if visible in the data) — low match quality means Meta can't reliably attribute conversions to the right people, which degrades both reporting accuracy and delivery optimization.
- Attribution window in use (1-day click, 7-day click, etc.) — mismatched windows between what's reported and what the business actually cares about can make performance look better or worse than reality.
- Sudden, unexplained drops in reported conversions with spend/impressions holding steady are often a tracking break, not a real performance drop — check this before diagnosing anything else as a delivery or creative problem.

**If tracking health can't be verified from the data given, say so and flag it as an assumption underlying the rest of the analysis** rather than silently treating reported numbers as ground truth.

## 2. Account structure

- CBO (Campaign Budget Optimization) vs. ABO (Ad Set Budget Optimization) — CBO fits when ad sets are reasonably comparable and you want Meta to allocate; ABO fits when you need guaranteed spend on a specific audience/test regardless of early performance.
- Audience overlap between ad sets in the same campaign (or across campaigns) — overlapping audiences make ad sets compete against each other in the same auction, inflating costs without added reach.
- Funnel-stage separation — are prospecting and retargeting audiences in separate campaigns/ad sets with appropriately different budgets and creative, or mixed together in a way that makes performance hard to read by funnel stage?
- Too many ad sets relative to budget fragments spend below the volume needed to exit learning phase efficiently (see below).

## 3. Delivery & learning phase

- Learning phase status, if the data/platform surfaces it — an ad set stuck in "learning limited" usually means too few conversion events per week relative to what's needed (Meta's general guidance is roughly 50 optimization events per week per ad set, though this shifts over time — treat it as a rule of thumb, not a hard number to state as fact).
- Frequent edits (budget, audience, creative swaps) reset or extend learning phase — if performance looks erratic, check whether the ad set has been left alone long enough to actually exit learning.
- Frequency creeping up without a proportional reach increase signals audience saturation — the same people are being shown ads repeatedly rather than new people being reached.

## 4. Audience & targeting

- Audience size relative to budget and objective — too narrow limits Meta's ability to optimize delivery; too broad on a low budget can waste spend on early exploration before finding efficient pockets.
- Broad targeting + Advantage+ audience vs. detailed/interest targeting — broad has become increasingly effective as Meta's algorithm has improved, especially with good creative and enough conversion volume to guide it; detailed targeting still has a place for genuinely niche audiences or exclusions.
- Retargeting window health — is the retargeting audience sized appropriately for the window (e.g., 180-day website visitors) and not so exhausted that it's just re-showing ads to the same small pool repeatedly?
- Exclusions — are converters/customers excluded from prospecting campaigns where that's the right call, to avoid wasting spend re-targeting people who already converted (context-dependent: some businesses want repeat-purchase targeting, so don't assume this is always a bug).

## 5. Budget & bidding (see `budget-bidding-scaling.md` for full depth)

Quick top-level check here: is spend concentrated where results are concentrated, or is a meaningful share of budget going to ad sets/campaigns that aren't producing proportional results? Full bidding-strategy and scaling guidance lives in the dedicated reference file since it's a large enough topic on its own.

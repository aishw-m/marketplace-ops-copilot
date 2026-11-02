# Marketplace Ops Copilot

A merchant-first performance investigation prototype inspired by managing partner accounts at Swiggy. Its goal is to reduce repetitive analysis and prepare better partner conversations. Current analysis uses deterministic JavaScript calculations and predefined checks. **No LLM is connected; this is not an autonomous AI agent.**

## Try it

Serve `dist/` with any static HTTP server, or open the deployed private Site. The default example contains one fictional merchant over 42 days. A multi-merchant example is also available. Choose a CSV from your device, select a merchant, and inspect funnel comparisons, daily trends, explanations and suggested checks. Desktop filters stay visible on the left. The merchant table has explicit Analyze merchant controls and selectable sorting.

- [Upload template with an illustrative row](../upload_template.csv)
- [Single-merchant example](../sample_single_merchant.csv)
- [Multiple-merchant example](../sample_marketplace.csv)

## Accepted CSV columns

One row per `date + merchant + city + category`. With no city/category columns, one row per merchant per day. Use at least 14 consecutive daily rows for 7-day comparisons, or 28 for 14-day comparisons. A closed day should be explicitly recorded with zero counts if that is the correct business fact; missing rows are not assumed to be zero. Separate outlets should have distinguishable merchant labels or city/category keys. Stable merchant/outlet IDs will be added in a later schema.

| Column | Required | Example | Meaning |
|---|---|---|---|
| date | Yes | 2026-08-01 | Reporting date, YYYY-MM-DD |
| merchant | Yes | Demo Merchant 001 | Stable merchant label across the export |
| impressions | Yes | 2000 | Merchant listing appearances |
| clicks | Yes | 400 | Merchant-page visits from listings; legacy `menu_views` accepted instead |
| orders | Yes | 40 | Placed orders, including cancellations under this contract |
| add_to_carts | No | 100 | Funnel visits reaching cart |
| checkouts | No | 60 | Funnel visits starting checkout |
| gmv | No | 1000 | Gross value of placed orders in one currency |
| cancellations | No | 2 | Cancelled orders within the same attribution scope |
| avg_delivery_mins | No | 30 | Mean delivery duration; order-weighted proxy used in aggregation |
| discount_spend | No | 80 | Discount spend in the same currency as GMV |
| city | No | Example City | Location filter |
| category | No | Example Category | Category filter |

Use plain nonnegative numbers, without currency signs or thousands separators. Counts must be integers. Optional missing/blank values remain unavailable, never fabricated zeroes. Optional metrics must be present throughout a comparison period to be aggregated. Unknown extra columns are not analyzed. Maximum file size: 10 MB. CSV only.

Funnel stages must share attribution and counting definitions: impressions ≥ clicks ≥ add_to_carts ≥ checkouts ≥ orders (where optional stages are supplied). Do not mix raw repeated click events with unique cart sessions without normalizing them. Cancellations cannot exceed orders. A file containing both clicks and menu_views is rejected as an ambiguous duplicate.

### Example row

```csv
date,merchant,impressions,clicks,orders,add_to_carts,checkouts,gmv,cancellations,avg_delivery_mins,discount_spend,city,category
2026-08-01,Demo Merchant 001,2000,400,40,100,60,1000,2,30,80,Example City,Example Category
```

Replace that illustrative row with daily data; one row alone cannot support a period comparison.

## Interpretation and ranking

CTR = clicks / impressions; conversion = orders / clicks; cart rate = carts / clicks; checkout progression = checkouts / carts; checkout completion = orders / checkouts. Rates are ratios of total counts, not averages of daily percentages. A conversion change from 10% to 8% is −2 percentage points and −20% relative: 8 rather than 10 orders per 100 visits.

Checks are transparent heuristics: impressions/orders down at least 8%; funnel rates down at least 5% relative; cancellation rate up at least 1 percentage point; delivery time up at least 3 minutes. Low-volume rates may be unstable; statistical confidence/seasonality are not implemented. Possible causes remain hypotheses. No profit, incrementality or causal effect is inferred.

Merchant lists default to names. Users can sort by count of review signals or absolute order decline. Neither is AI ranking or an estimate of recoverable revenue. The prior prototype's order-based review queue has been replaced.

Comparison periods end at the selected merchant's latest reported date. Merchant summary comparisons use complete daily account coverage, and withhold interpretation when any included account is incomplete. Merchants in a combined file can have different latest dates; compare their displayed periods before comparing performance across merchants.

## Data provenance

All displayed demo identities are explicit fictional account IDs (Demo Merchant 001–027), with no claimed real-world business association. Prior common business-like labels were replaced because they could coincide with real businesses. No claim of legal/name clearance is made.

Original sample measurements were recovered from the September 2026 prototype: 1,134 rows / 42 days / 27 merchant-city accounts. They are synthetic, not Swiggy or Kaggle data. The original archive did not contain a generator or seed. Current demo cart counts are an illustrative augmentation: max(orders, round(clicks × 0.40)); checkout counts: max(orders, round(carts × 0.65)). These generated stages are not measured behavior or realistic causal ground truth. The single-merchant example is a 42-row subset. Currency was undocumented in the original; monetary figures remain currency units. GMV/discount measures are not a full unit-economics model.

## Privacy and how guided answers work

The browser File API reads only the file chosen by the user into JavaScript memory. The app makes no network request containing its rows, prompts or briefs and does not write them to browser storage. A refresh discards the data. The website is hosted online, so page assets and hosting authentication still use the network. This is not a claim that the entire hosting environment makes zero network requests.

Guided questions use keyword matching to select predefined answer templates. Values come from the calculation engine and current merchant/period state. Unsupported questions disclose the limitation. No model, learned reasoning, model training or inference runs in this version.

The brief control opens an on-screen preview first. Save Markdown requests a browser download via a Blob URL. If browser/embedding policy blocks it, Copy text or manual selection remains available. No brief is uploaded. Download requests cannot prove that a user's browser saved the file.


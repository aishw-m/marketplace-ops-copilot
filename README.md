# Marketplace Ops Copilot

A merchant performance investigation tool inspired by my experience managing marketplace partners at Swiggy. It turns daily KPI exports into funnel comparisons, performance signals, and focused partner-conversation prompts.

Upload a merchant CSV or explore the built-in fictional demo. No installation or API key is required to use the hosted app.

## What it does

- Compares the latest 7 or 14 days with the preceding period.
- Tracks the funnel from impressions and clicks through carts, checkouts, and orders.
- Explores GMV, conversion, cancellations, delivery time, and discount intensity.
- Flags changes using transparent rules and suggests what to investigate next.
- Prepares a merchant brief that can be viewed, copied, or downloaded.

## Try it

Use the hosted website once GitHub Pages is enabled, then select **Load one-merchant demo** or **Choose CSV from device**. Use the filters and guided questions to explore the evidence.

For local development, serve this folder with a static HTTP server, for example `python -m http.server 8000`, and open `http://localhost:8000`. Opening `index.html` directly may block JavaScript modules and demo-file loading.

## Upload your data

Use daily records for one merchant. Combined files are supported through a merchant selector.

**Required:** `date`, `merchant`, `impressions`, `clicks`, `orders`.

**Optional:** `city`, `category`, `add_to_carts`, `checkouts`, `gmv`, `cancellations`, `avg_delivery_mins`, `discount_spend`.

Provide 14 consecutive days for a 7-day comparison or 28 for a 14-day comparison. Use YYYY-MM-DD dates and nonnegative numbers without currency symbols or thousands separators. CSV files must be under 10 MB.

- [CSV template](upload_template.csv)
- [Single-merchant example](sample_single_merchant.csv)
- [Multi-merchant example](sample_marketplace.csv)
- [Full data definitions and analysis methodology](docs/DATA_GUIDE.md)

## How it works

Built with HTML, CSS, and vanilla JavaScript. Metrics are calculated deterministically; predefined rules identify review signals, and guided questions return evidence-based templates. **No AI model is connected.** Suggested causes are hypotheses, not confirmed explanations. Profitability and ROI are not calculated.

Uploaded data stays in browser memory and is cleared on refresh. The application does not send CSV contents to a server or AI provider. Page assets are loaded over the network.

All demo identities and measurements are synthetic. Cart and checkout counts are illustrative, not observed customer behavior.

## Deploy

Follow [GITHUB_SETUP.md](GITHUB_SETUP.md) to upload the files and enable GitHub Pages. No build tools or dependencies are required.

# Vision — Porter Intelligence

The consumer-facing product engine, in the Porter Intelligence house style: a
lightweight **static site** that turns the in-house Edge model's output into a
"size it to your capital" 10-stock portfolio view (2-year + 20-year backtest vs
the S&P 500). Holds no model code — it just renders a data snapshot.

```
the Edge repo (in-house model)  ──►  export_sauron.py  ──►  vision_data.js  ──►  index.html
```

## Files
- `index.html` — the Vision product UI (capital → 10 positions → dashboard). Loads
  `window.VISION_DATA` from `vision_data.js` (cache-busted), with an N/A fallback.
- `vision_data.js` — **generated** feed: current 10-stock book + 2Y & 20Y backtest
  curves (each vs S&P 500) + headline stats. Do not edit by hand.
- `render.yaml` — static-site blueprint (service name `vision`).

## Product configuration
2-year + 20-year backtests · 1-month rebalance · 75% YoY-revenue-growth mix ·
10-stock equal-weight book.

## Refreshing the data
From the in-house Edge repo (`../quant model`):
```
.venv/Scripts/python.exe export_sauron.py    # rewrites ../vision/vision_data.js
```
Commit + push the updated `vision_data.js` to redeploy fresh picks.

## Hosting
Fully static → Netlify / Vercel / GitHub Pages / Render Static. The page loads the
feed cache-busted (`vision_data.js?v=…`) so updated picks/curves always show.

Performance shown is a historical backtest, net of estimated costs — not a forecast.
Not investment advice.

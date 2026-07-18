# Task notes: distill Tetlock (2007)

In-progress extraction notes for `docs/papers/tetlock-2007.md`. Source paper not stored here (copyright).

Fetch provenance: the queued SSRN link (`docs/WORKING.md`) returned HTTP 403. The author-hosted copy at
`www0.gsb.columbia.edu/faculty/ptetlock/papers/Tetlock_JF_07_Giving_Content_to_Investor_Sentiment.pdf` now
redirects to a faculty bio page and no longer serves the PDF (confirmed dead as of 2026-07-18). The actual
PDF used for this extraction was pulled from `business.columbia.edu/sites/default/files-efs/pubfiles/3097/Tetlock_Media_Sentiment_JF.pdf`,
read locally via `pdftotext -layout` (not committed to the repo).

## Citation
Tetlock, P.C. (2007). "Giving Content to Investor Sentiment: The Role of Media in the Stock Market." *Journal of Finance* 62(3): 1139–1168.

## Data & method
- Source: WSJ "Abreast of the Market" column, daily, Jan 1 1984 – Sep 17 1999 (~4,000 obs, ~250/yr, 16 years)
- Content analysis: General Inquirer (Harvard IV-4 dictionary, 77 word categories), word counts re-centered by day-of-week
- Factor construction: PCA on the 77 categories → single "pessimism" factor; loadings estimated on year *t-1*, applied to year *t* (avoids look-ahead). Average pairwise correlation across yearly loadings = 0.96, so loadings are stable.
- Pessimism factor ≈ linear combo dominated by 4 categories (Negative, Weak, Fail, Fall); Negative + Weak alone explain >57% of factor variance. Also re-run using raw Negative-words and Weak-words categories directly, as robustness/interpretability check.
- Regressions: VAR/OLS, 5 lags of pessimism (+ own lags, volume, day-of-week & January dummies, 1987-crash dummy, Newey-West SE), predicting: Dow Jones daily returns, detrended log NYSE volume, Fama-French SMB (small-minus-big) daily returns.

## Headline results
- 1 SD ↑ pessimism → Dow next-day return **-8.1bps** (t=3.94, p<0.001) — larger than the unconditional mean daily return (6.3–6.4bps)
- Reversal over lags 2–5: **+6.8bps** (p<0.05); net 5-lag sum -1.3bps, not significantly different from zero → full reversion within the week
- Negative-words and Weak-words versions: -4.4bps / -6.0bps day 1, +9.5bps / +10.7bps reversal — same qualitative pattern, three independent measures agree
- High **or** low pessimism (i.e. |pessimism|) → higher next-day NYSE volume, all three measures, p<0.01
- Low Dow returns → higher next-day pessimism (feedback loop): 1% Dow decline → pessimism +5.8% of one SD (p=0.003)
- SMB (small stocks): pessimism predicts negative SMB returns over the *following week*, larger/more persistent than the Dow effect (~7bps cumulative, p<0.002)
- Explanatory power: 5 lags of pessimism explain 1.52% of residual Dow-return variance vs 0.16–0.30% for standard controls (own lags, volume, time dummies) — dominates conventional predictors in *relative* terms, though absolute R² is still small
- Conditional volatility is *higher*, not lower, when pessimism is high → rejects the risk-premium/volatility-proxy explanation

## Robustness checks (all hold, qualitatively)
- Return window shifted to 10am-next-day→close (lets traders react to the afternoon release + morning reprint): effect survives, magnitude falls ≤25% (less than the ≥25% expected if impact were uniformly spread through the day) — impact is concentrated later in the trading day, not front-loaded
- Split sample 1984–91 vs 1992–99: qualitatively similar pattern both halves (3-day decline + 2-day reversal), but *much* stronger/more significant in 1992–99 — no data beyond 1999 to check if this trend continued or reverted
- Winsorizing at 1%: parametric and semi-parametric (lowess) estimates essentially unchanged
- Semi-parametric (lowess) check: monotonic decreasing relationship, ~25bps spread between top and bottom pessimism quintiles, mostly linear except near center

## What's explicitly ruled out
- New-fundamental-information theory (would predict persistence, not reversal) — rejected
- Stale/no-information "sideshow" theory (would predict no effect) — rejected
- Risk-premium/volatility-proxy theory (would predict pessimism ↔ lower volatility) — rejected (finds the opposite sign)
- Bid-ask bounce / microstructure artifact — effect is an order of magnitude larger than typical Dow bid-ask spreads

## Hypothetical trading strategy (author's own caveat-laden benchmark)
- Long/short Dow based on terciles of prior-year Negative-words distribution, 1985–1999 (~3,700 days, 1,281 buys / 1,254 sells)
- Avg daily return 4.4bps, ~7.3% annualized, positive in 12/15 years (p=0.018)
- **Author's own caveat**: typical round-trip cost cutoff for erasing this edge is ~4.4bps — i.e. the strategy is *near breakeven* net of realistic transaction/price-impact/tax costs. Explicitly states "unclear whether... would remain profitable" after costs.
- Strategy is in-sample (same 1984–99 window the factor was estimated over, though yearly PCA loadings avoid pure look-ahead); no out-of-sample holdout period exists (nothing post-1999 tested)

## Caveats relative to our design (SPY/QQQ premarket→close, current era)
- Different instrument/era: Dow Jones + NYSE volume + SMB, 1984–1999, print/newswire-era media — pre-internet, pre-HFT, pre-decimalization market microstructure; no evidence the effect survived into the 2000s+ (paper ends in 1999, published 2007)
- Different sentiment source: hand-curated single WSJ column vs a modern premarket sentiment proxy (social/news/options-flow based) — construction method (General Inquirer word counts) is dated but the *mechanism claim* (temporary sentiment-driven price pressure + reversion) is the transferable part, not the specific data source
- Gross-of-cost edge (7.3%/yr) is explicitly near the author's own breakeven cost estimate — this is not a "found a free lunch" result even on its own terms
- No true out-of-sample test within the paper; the 1984–91/1992–99 split is a robustness check, not a holdout validation, and shows the effect *strengthening* over time within-sample rather than being stable — could indicate the effect is regime/era-dependent rather than a stable law

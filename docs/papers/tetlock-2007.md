# Tetlock (2007) — Giving Content to Investor Sentiment

**Citation:** Tetlock, P.C. (2007). "Giving Content to Investor Sentiment: The Role of Media in the Stock Market." *Journal of Finance* 62(3): 1139–1168.

## Claim

Media pessimism — extracted from the tone of a daily WSJ column — predicts a temporary next-day decline in stock index returns, followed by a near-complete reversion within the week, plus a same-day/next-day spike in trading volume when pessimism is unusually high *or* low. The pattern is consistent with noise-trader/liquidity-trader sentiment theory, not with the column carrying genuine new fundamental information (which would predict persistence, not reversal) or with it being a content-free "sideshow" (which would predict no effect at all).

## Method

Content-analyzed 16 years (1984–1999) of the WSJ "Abreast of the Market" column word-by-word using the General Inquirer's Harvard IV-4 dictionary (77 categories), then took the first principal component as a daily "pessimism" factor (year-*t* factor built from year-*t-1* loadings, to avoid look-ahead). Regressed Dow Jones returns, NYSE volume, and the Fama-French SMB factor on 5 lags of this factor plus standard controls, using OLS/VAR with Newey-West errors.

## Result

A 1 SD pessimism increase predicts an 8.1bp next-day Dow decline (p<0.001), reversed by 6.8bp over the following four days (net effect ≈ 0). Effect replicates using the two underlying GI word categories (Negative, Weak) independently. High-|pessimism| days show elevated volume (p<0.01). Pessimism explains more of next-day return variance (1.52%) than standard predictors (own lags, volume, day-of-week, each <0.3%). A hypothetical long/short strategy on this signal nets ~7.3%/yr gross — but the author's own cost estimate puts realistic transaction/price-impact costs right at the same magnitude as the edge, i.e. plausibly breakeven net of costs.

## Caveats

- **In-sample only, single period.** 1984–1999, Dow/NYSE, no data or test beyond 1999. A within-sample split (1984–91 vs 1992–99) shows the effect getting *stronger* in the second half rather than stable — could mean regime/era dependence, not a durable law.
- **Different instrument and era than our target.** Print-era single-column media source, Dow Jones close-to-close returns, pre-decimalization/pre-HFT microstructure — not SPY/QQQ premarket→close in the current era. The transferable part is the *mechanism* (sentiment → temporary pressure → reversion), not the specific data pipeline.
- **Gross of costs.** The one concrete trading strategy tested is explicitly flagged by the author as likely breakeven-or-worse after realistic frictions.

## Implication for `docs/QUESTIONS.md`

Directionally supports the founding hypothesis's core mechanism — an observable sentiment proxy biasing short-horizon return with reversion, not persistence — which is the shape of thing our premarket→close design is betting on. Does **not** provide evidence this survives on SPY/QQQ, in the current market, or net of costs; those remain fully open. Candidate question to add/track: does an analogous sentiment-pressure-then-reversion pattern exist intraday (premarket→close) on SPY/QQQ in a recent sample, net of realistic costs?

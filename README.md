# quant-research

Trunk repository for a small quantitative trading research project. Docs and curated data only — no code.

**Question:** can modest, consistent returns be extracted from one-day directional trades on SPY/QQQ (or their inverses), entering near the open on premarket sentiment signals and exiting before the close?

**Hypothesis:** market participants cluster (fundamentalists, trend-followers, retail/noise flow, institutional rebalancers); cluster state is estimable from observable proxies and biases the open-to-close move.

**Stance:** falsification-first. Most predictors die out-of-sample; a finding becomes a belief only after surviving review. No-trade is a first-class signal. Goal is pocket money, not riches.

## Map

| Document | Role |
|---|---|
| `docs/REPORT.md` | The final distilled document — current belief state of the project |
| `docs/WORKING.md` | Work in progress: links queued for fetching and distillation |
| `docs/QUESTIONS.md` | Research question index with status (open / reading / answered / falsified) — not yet created |
| `docs/LITERATURE.md` | Reference material index |
| `docs/papers/` | One note per paper read — not yet created |
| `docs/contracts/` | One page per branch repo: inputs, outputs, question answered — not yet created |
| `docs/data/` | Small, curated, hand-reviewed reference data — not yet created |

Transitory communication (findings awaiting merge, open threads) lives in **GitHub issues**; the repo holds only what survived.

## Workflow

Work happens in branch conversations and branch repos (`quant-signals`, `quant-clusters`, `quant-execution`, …), each born from a contract. Results return as issues; periodic compaction folds them into `report.md` and closes them. All commits are made manually by the maintainer after review — the trunk is read-only for tools.

Public trunk, methodological content only. Operational specifics (P&L, sizing, live parameters) live in private branches; findings arrive here already sanitized.

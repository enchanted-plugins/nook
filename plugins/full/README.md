# full — Nook meta-plugin

*Part of [Nook](../../README.md).*

Pulls in all 5 Nook sub-plugins via one dependency resolution pass.

## Install

```
/plugin marketplace add enchanted-plugins/nook
/plugin install full@nook
```

## Installs

| Sub-plugin | Engines | Purpose |
|------------|---------|---------|
| [cost-tracker](../cost-tracker/) | L1 Exponential Smoothing Forecast, L4 Cache-Waste Measurement | Writes ledger + session snapshot + daily rollups; produces forecasts |
| [budget-watcher](../budget-watcher/) | L2 Budget Boundary Detection, L3 Z-Score Cost Anomaly | Fires debounced threshold events + 3σ anomaly detection |
| [rate-card-keeper](../rate-card-keeper/) | — | Holds `shared/rate-card.json`; validates schema + staleness at SessionStart |
| [nook-learning](../nook-learning/) | L5 Gauss Learning (Nook) | Per-developer cost-pattern accumulation across sessions |
| [cost-query](../cost-query/) | — | Developer slash commands: `/nook-cost`, `/nook-forecast`, `/nook-attribute`, `/nook-report` |

## Cherry-picking

Need only one engine? Install the individual sub-plugin:

```
/plugin install cost-tracker@nook       # just L1 + L4 ledger and forecasting
/plugin install budget-watcher@nook     # just L2 + L3 threshold + anomaly alerts
/plugin install cost-query@nook         # just the slash commands
```

Missing sub-plugins degrade gracefully — e.g. `cost-query` without `cost-tracker` shows "no observations yet"; `budget-watcher` without `rate-card-keeper` refuses to observe (cost attribution requires the rate card).

## Why the meta-plugin exists

Five sub-plugins working together is the intended configuration. The meta-plugin makes that one command instead of five. Allay, Flux, Hornet, Reaper, Weaver all ship `full` for the same reason.

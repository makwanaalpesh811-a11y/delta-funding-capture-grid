# Delta Funding Capture — Grid Strategy (2x Leverage)

**Final strategy: Delta Exchange India perpetual futures, funding capture, grid N=20, volume-scaled position, 2x leverage (70% margin).**

## 📊 Result Summary (2x Locked)

| Metric | Value |
|--------|-------|
| Exchange | Delta India (perpetual_futures) |
| Grid | N=20 coins/chunk (volume-ranked) |
| Leverage | **2x (70% margin, compounding)** |
| Coins | 66 (watchlist, all chunks) |
| Trades | 162 (1/day, 167d data) |
| Win rate | 75.9% |
| **Net PnL** | **+$3,229.19** |
| **Final equity** | **$3,429.19** (start $200) |
| **Max drawdown** | **-16.77%** |
| P/L line cross | ❌ NO |
| Monthly positive | 7/7 (100%) |
| Walk-forward | PASS (OOS 76.2% win) |
| Luck check | PASS |

## 🧠 Strategy Logic

### 1. Signal (Funding Capture)
- **Funding NEGATIVE → LONG** | **Funding POSITIVE → SHORT**
- T = funding time (UTC), Entry = (T−1 min) OPEN, Exit = (T+1 min) OPEN
- Fee 0.05% on exit only

### 2. Chunk Selection (|funding| %)
| Chunk | Range | Priority |
|-------|-------|----------|
| C6 | 1.0%+ | Highest |
| C5 | 0.8–1.0% | |
| C4 | 0.6–0.8% | |
| C3 | 0.4–0.6% | |
| C2 | 0.2–0.4% | |
| C1 | 0.1–0.2% | Lowest |

### 3. Grid (N=20 per chunk)
- Har chunk me **top-20 most liquid coins** (24h turnover ranked)
- Priority C6→C1, **1 trade/day** — best coin per day

### 4. Volume-Based Position Sizing (TRAP-AVOID)
```
base_position = 0.5% of 24h turnover, clamped [5, 2000] USDT
leverage_multiplier = 2 * 0.7 * equity / 200  (70% margin, 2x)
position_notional = base_position * leverage_multiplier
```

| 24h Turnover | Base Position |
|-------------|--------------|
| 10k | $50 |
| 100k | $500 |
| 500k+ | $2,000 (cap) |

### 5. Leverage Safety
- **2x = DD -16.8%** — personal capital OK (prop-firm 10% limit se upar)
- **1x = DD -8.6%** — prop-firm safe (10% limit andar)
- 3x+ risky (DD 24%+)

## 📂 Files

| File | Description |
|------|-------------|
| `DELTA_GRID_STRATEGY.md` | Full strategy documentation |
| `delta_grid_2x.json` | 2x leverage equity curve + report |
| `grid_delta_result.json` | Grid backtest results (all N) |
| `delta_grid_equity.json` | N=20 equity curve (1x) |
| `s5_final_trades.csv` | 162 trades (1/day) |
| `s5_final_coins.csv` | 66 coins watchlist |
| `grid_delta_backtest.py` | Grid backtest script |
| `delta_volume.json` | 24h volume data (1158 symbols) |

## ⚠️ Limitations

- Data sirf 167d (7 months) — 12-month consistency unproven
- Volume snapshot current (live me refresh)
- Stress test negative (leverage kam rakho)

## ⚠️ Disclaimer

Backtest only. Past performance ≠ future results. Not financial advice.

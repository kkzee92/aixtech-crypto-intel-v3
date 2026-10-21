# AIxTech crypto intel v0.3: paper-only trading information system

Research harness for automated cryptocurrency **information** and paper strategy evaluation. It does not place live orders, does not store exchange secrets, and is not financial advice.

Derived from and enhancing [zeekiankok92/aixtech-crypto-intel](https://github.com/zeekiankok92/aixtech-crypto-intel).

![Python](https://img.shields.io/badge/python-3.10%2B-blue)
![version](https://img.shields.io/badge/version-0.3.0-blue)
![mode](https://img.shields.io/badge/execution-paper%20only-orange)
![Licence](https://img.shields.io/badge/licence-MIT-green)

## What it does

- Classifies markets into eight asset classes and applies a different research rule to each.
- Labels each series trend, range, or stress, and stands aside in stress.
- Scores a signal (long or short observation), then a risk gate that can shrink or refuse it.
- Applies a declared round-trip cost by asset class in the paper backtest.
- Volatility-scales size and checks concentration. Writes a hash-chained audit log, attests fixture sources, and redacts secret-like strings (including private-key patterns).
- Backtests on **synthetic** candles only. Reports equity, trades, max drawdown, win rate, and approximate Sharpe.

| Asset class | Research rule | Risk cap | Cost |
|---|---|---|---|
| Major (BTC, ETH) | EMA trend outside stress; range RSI reversion (long or short) | 8% | 8 bps |
| Large-cap alt | Breakout with volume; failed-breakout short observation | 4% | 14 bps |
| Stablecoin | 20 bp watch, 50 bp depeg alert. No order | 0% | n/a |
| DeFi | Trend or calm-range mean-reversion; suppressed in stress | 2% | 22 bps |
| Meme | Qualified burst or exhaustion short; 3-bar horizon | 0.5% | 45 bps |
| L2 | Relative strength or weakness versus a non-stress benchmark | 3% | 16 bps |
| RWA | Slow trend; halt on an 8% gap or stress | 2% | 12 bps |
| Perpetual | Negative-funding carry or crowded-funding short observation | 2% | 10 bps |

## Controls

1. Paper-only execution. `HALTED` and any live mode raise `PermissionError`.
2. Trade and withdrawal credential names are refused. No role can place an order.
3. Class size caps, confidence floors, kill switch, drawdown halt, RWA gap halt, stress overlay, concentration limit, volatility scaling.
4. Hash-chained audit log, source attestation, feed integrity, expanded secret redaction.
5. PDPA-style tripwire.

## Honesty

- No live exchange connector is included. Do not add trade keys to this tree.
- Strategy scores describe the synthetic fixture, not future returns.
- This is not legal, compliance, or investment advice.

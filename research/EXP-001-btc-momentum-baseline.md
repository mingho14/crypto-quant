# EXP-001 BTC Momentum Baseline

## Research Question

当 BTC 在 5-minute timeframe 上持续位于 EMA20 上方时，未来短期 return 是否高于正常水平？

## Hypothesis

如果连续 20 根 5-minute candles 的 Open 和 Close 都高于各自的 EMA20，则接下来 12 根 candles（1 小时）的 Expected Return 高于 BTC 无条件未来 1 小时 Expected Return。

## Asset

BTC

## Market

Spot

## Exchange

Binance

## Timeframe

5-minute

## Data

OHLCV，使用 Freqtrade 下载。

## Momentum Condition

TBD

## Prediction Horizon

TBD

## Signal

从 t 开始算，连续 20 根 candles 的 Open 与 Close 大于各自的 EMA20。

## Signal becomes known at

假设 candle 是：

13:00 → 13:05

Signal 最早在 13:06 知道，也就是 t+1 的 open 附近。

## Earliest Execution

保守的 baseline 最早应该在 t+1 的 open 成交。

> 注意：不能使用 candle close 后才能确认的信息，却假设自己成交在同一根 candle 的 close。回测实现时必须显式处理 signal / execution timestamp alignment。

## Transaction Costs

TBD（需要查询 Binance 当前费用，并在接近真实交易的 backtest 中考虑 fees / spread / slippage；如研究 perpetual futures，还要考虑 funding）。

## What result would make me reject the hypothesis?

当 Research Question 的答案是 “No” 时，reject hypothesis。

后续应进一步把 rejection criteria 量化，例如：

- 条件未来 1h return 没有稳定高于 unconditional baseline；
- 差异在 transaction costs 后消失；
- 结果在 out-of-sample / 不同时间段中不稳定；
- 仅依赖非常狭窄参数区间，疑似 overfitting。

## Next Steps

1. 明确定义 EMA20 和连续 20 根 candle 条件的精确计算方式。
2. 定义 forward 12-candle return，确认 timestamp alignment。
3. 先做无交易执行假设的 conditional-return research baseline。
4. 比较 signal 条件下 vs unconditional 的 return distribution。
5. 检查样本数、均值/中位数、volatility、置信区间与 regime dependence。
6. 再进入可交易 backtest，并加入 execution lag 与 transaction costs。

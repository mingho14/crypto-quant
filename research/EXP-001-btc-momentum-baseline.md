# EXP-001 BTC Momentum Baseline

## Research Question

当 BTC 在 5-minute timeframe 上持续位于 EMA20
上方时，未来短期 Return 是否高于正常水平？

## Hypothesis

如果截至当前时刻最近连续 20 根 5-minute candles
的 Open 和 Close 都高于各自 EMA20，

那么接下来 12 根 candles（60 minutes）的
Expected Return 高于 BTC 无条件未来 60 分钟 Expected Return。

## Asset

BTC

## Market

Spot

## Exchange

Binance

## Timeframe

5-minute

## Data

OHLCV  
Source: Freqtrade downloaded Binance historical data

## Momentum Condition

最近连续 20 根 completed candles 全部满足：

Open > EMA20  
AND  
Close > EMA20

## Signal

如果 Momentum Condition 成立：

Signal_t = 1

否则：

Signal_t = 0

## Prediction Horizon

12 candles = 60 minutes

## Signal becomes known at

Candle t 完全收盘之后。

## Earliest Execution

Baseline assumption:  
下一根 candle（t+1）的 Open。

注意：  
真实执行存在 latency / spread / slippage，  
后续需要加入更加现实的 execution model。

## Transaction Costs

TBD

之后查询 Binance 最新手续费，并加入：
- fees
- spread
- slippage

Spot 暂时没有 perpetual funding。

## Hypothesis not supported if

如果 Signal=1 后的未来 60-minute Expected Return
没有高于 BTC 无条件未来 60-minute Expected Return，

则当前实验没有 evidence 支持该 Momentum Hypothesis。

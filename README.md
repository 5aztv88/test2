# TradingView MACD wave divergence and daily Classic pivots

Paste `macd_daily_pivot_signals.pine` into TradingView's Pine Editor, save, and choose **Add to chart**. Use standard candles on intraday or daily charts. BUY/SELL labels draw on the price chart. Enable **Settings → Inputs → MACD → Show MACD histogram** to display the histogram and zero line in a separate pane; it is hidden by default. Hiding it does not change signals. Daily pivot levels remain internal; no local dependencies are needed.

TradingView may retain an empty indicator pane when the histogram is hidden; collapse the pane if needed. After installing this update, remove the old indicator instance and add it again so TradingView applies the new pane placement.

## Broader histogram wave comparison

MACD defaults to 12/26/9, with adjustable lengths and source. A negative wave is a sequence of negative histogram bars; a positive wave is a sequence of positive bars. Exactly zero bars are ignored. An opposite-sign candle closing confirms the preceding wave. The first observed wave is excluded because the loaded chart history may begin partway through it.

For each negative wave, record its lowest histogram value and lowest price. For each positive wave, record its highest histogram value and highest price. These extremes can occur on different candles within the same wave. Compare with up to **5 previous qualifying waves of the same sign**, rather than just neighbouring price swings. A match against any one of those waves is sufficient.

Defaults exclude waves shorter than **3 nonzero histogram bars** and pairs whose price extremes are more than **300 chart bars apart**. These limits and the number of earlier waves are adjustable. Short excluded waves still separate surrounding waves; they are not merged.

| Mode | BUY: compare negative waves | SELL: compare positive waves |
| --- | --- | --- |
| Hidden (reverse), default | Higher price low, lower histogram trough | Lower price high, higher histogram peak |
| Regular (reversal) | Lower price low, higher histogram trough | Higher price high, lower histogram peak |
| Both | Either bullish pattern | Either bearish pattern |

## Daily pivot requirement

The newer negative wave's lowest-price candle must touch daily Classic S2 or S3 for BUY. The newer positive wave's highest-price candle must touch R2 or R3 for SELL. If several candles share the exact price extreme, a touch on any of those candles qualifies. A touch elsewhere in the wave does not qualify.

Touch means the candle's high-low range intersects the level plus/minus the tick tolerance (default 5 ticks). Each candle uses the pivot levels valid on that candle, including when a wave spans multiple days.

Daily levels use the previous completed exchange daily candle regardless of the chart's intraday timeframe. With P = (high + low + close) / 3 and range = high - low: S2 = P - range, S3 = P - 2 × range, R2 = P + range, R3 = P + 2 × range. Session-specific or synthetic candle settings in other indicators may give different values.

## Signal timing and alerts

Signals appear on the close of the first opposite-sign histogram candle, after the newer wave ends. They are not backdated to the price extreme. This is a variable confirmation delay, replacing the former fixed five-bar swing confirmation. An unfinished wave produces no signal. Each completed wave produces at most one signal.

Create alerts using the BUY or SELL condition with **Once Per Bar Close**. Recreate existing TradingView alerts after updating the script because alerts retain a snapshot of the old code. This indicator does not place trades or provide a strategy backtest.

## Validation

Source changes and whitespace were reviewed locally. No Pine compiler or TradingView runtime is available in this environment, so compilation and chart behavior remain unverified. In TradingView, check compilation and use Bar Replay to inspect separate-wave divergence, pivot touches at the price extreme, and signals appearing only after an opposite-sign candle closes.

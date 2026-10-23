# TradingView MACD and daily pivot signals

Paste `macd_daily_pivot_signals.pine` into TradingView's Pine Editor, save it, and choose **Add to chart**. Use standard candles on an intraday or daily chart. No local dependencies are required.

Only BUY/SELL labels appear on the price chart. The MACD histogram and Classic daily S2/S3/R2/R3 levels are calculated internally without drawing lines or an extra pane. MACD defaults to 12/26/9; all lengths are adjustable.

Classic formulas use P = (previous daily high + low + close) / 3 and range = high - low: S2 = P - range, S3 = P - 2 × range, R2 = P + range, R3 = P + 2 × range. The daily source is fixed even on intraday charts.

## Signal rules

The script compares consecutive confirmed price swing lows for buys and swing highs for sells, sampling the MACD histogram at each price swing. The newer swing candle must touch S2/S3 for a buy or R2/R3 for a sell. Touch means its high-low range intersects a level within the configurable tick tolerance. Levels are calculated from the previous completed exchange daily candle; they need not match a separately configured session-specific pivot indicator.

The default **Hidden (reverse)** setting means a higher price low with a lower histogram low for BUY, or a lower price high with a higher histogram high for SELL. If you mean reversal divergence, choose **Regular (reversal)**: a lower price low with a higher histogram low for BUY, or a higher price high with a lower histogram high for SELL. **Both** enables either pattern.

By default, both compared histogram values must be negative for buys and positive for sells. This filter can be disabled. Swing strength, maximum swing separation, and touch tolerance are configurable.

## Confirmation and alerts

Signals appear only at the close of the confirmation candle, by default five bars after the swing. They are not backdated. The level touch is evaluated on the swing candle using the daily levels valid on that candle. This delay is necessary to confirm a swing using bars to its right.

Create alerts using the indicator's BUY or SELL condition and select **Once Per Bar Close**. This indicator does not place trades or provide a strategy backtest.

## Validation

The script has not been compiled or run in TradingView from this environment: no Pine compiler or authenticated TradingView integration is available here. In Pine Editor, verify compilation, inspect signals around S2/S3 and R2/R3, and use Bar Replay to check confirmation timing before relying on alerts.

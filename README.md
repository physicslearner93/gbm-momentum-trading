# S&P 500 Momentum Strategy Using a Geometric Brownian Motion Forecast

Can a daily-calibrated geometric Brownian motion (GBM) forecast, with expected shortfall sizing, produce a trading strategy that beats buying and holding the S&P 500?

## Key findings

- It did not beat buy-and-hold. Over the one-year backtest (June 1, 2020 to May 31, 2021), the strategy turned $1,000,000 into $1,109,960 (11.0% return, 8.3% maximum drawdown). Buying and holding the S&P 500 returned 38.2% with a 9.9% drawdown.
- The notebook explains why: the period was a strong, steady rally. The strategy was long on 211 of 311 days, short on 36 and flat on 64, and it changed position 285 times, so it missed much of the gain.
- Results depended heavily on settings chosen after the fact. A 60-day calibration window lost 8.7% (23.7% drawdown). A 120-day window made 11.0%, a 250-day window 8.5%, and a 20-day forecast horizon made 16.8%. No setting beat buy-and-hold.
- My conclusion in the notebook: I would not trade this with real money. The spread of results is a sign of overfitting risk, it covers one market year, and no transaction or financing costs are included.

## What I did

- Wrote a GBM class that calibrates drift and volatility from past prices, and checked it on simulated paths.
- Loaded S&P 500 prices into SQLite and kept a positions table updated after every trade.
- Forecast the price 10 days ahead each day, with a confidence interval and expected shortfall.
- Coded the signal: go long if the price is below the forecast interval, short if above, flat otherwise. Position size is 5% of capital divided by expected shortfall.
- Compared the strategy with buy-and-hold and re-ran the backtest across lookbacks, interval widths and horizons.
- Listed improvements: walk-forward parameter selection, a cost model, a leverage cap, and testing across bull, bear and sideways markets.

## Tools

Python, NumPy, SciPy, SQLite, pandas, matplotlib.

## Files

| File | What it is |
|---|---|
| `Project.ipynb` | Completed notebook with code, backtest outputs and written interpretation |
| `Project.html` | HTML export of the notebook |
| `SP500.csv` | S&P 500 price history, provided by Udacity |
| `SP500.db` | SQLite database holding the prices and the backtest positions |
| `NOTICE.md` | Terms of use |

## How to view

Open the notebook on GitHub, or in Jupyter. All outputs are saved, so you do not need to rerun it.

## About this project

Completed for the Udacity AI Trading Strategies Nanodegree (passed project review, November 2026). Starter materials and project specifications belong to Udacity. The analysis and write-up are my own. See NOTICE.md. If you are a current Udacity student, do not copy this work; submitting it is a violation of the Udacity Honor Code.

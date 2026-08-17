# Portfolio risk & return analyzer

A Python analysis of the risk, return, and diversification of a five-asset
portfolio (AMZN, GLD, NVDA, NVO, SPY). It ends by building the minimum-variance
portfolio through constrained optimization.

## What it does

- Pulls 5 years of daily price data (2020 to 2024) with `yfinance`
- Computes daily and annualized returns and volatility for each asset
- Analyzes the correlation and covariance structure across the assets
- Builds the minimum-variance portfolio with `scipy.optimize` (SLSQP), holding
  weights to sum to 1 with no short-selling

## Key findings

![Risk vs Return](risk_return_scatter.png)

Gold (GLD) was the main diversifier. It was nearly uncorrelated with the
equities (0.08 to 0.16), while the tech names tracked the S&P 500 closely
(NVDA and SPY correlated at 0.70), which follows from their weight as index
constituents.

Diversification cut risk in a measurable way. An equal-weight portfolio came in
at 23.0% annualized volatility. That is well below the 31.5% average of the
individual assets, and the gap comes entirely from the assets being imperfectly
correlated.

The minimum-variance portfolio (about 65% GLD, 27% SPY, 8% NVO) reached 13.2%
volatility. That is lower than any single asset in it, gold included. A
portfolio can be less risky than its least-risky component.

![Correlation Heatmap](correlation_heatmap.png)

## Limitations and next steps

Minimizing variance ignores return. The optimizer dropped the two highest-return
assets (NVDA and AMZN) and produced a portfolio that is low-risk but also
low-return, at roughly 14%. A more useful version would optimize for
risk-adjusted return (maximum Sharpe ratio) or map the full efficient frontier,
which weighs risk against expected return instead of only minimizing risk.

## Tools

Python, pandas, NumPy, scipy.optimize, matplotlib, seaborn

## Running it

Open `Portfolio_Risk_and_Return_Analyzer.ipynb` in Jupyter and run the cells top
to bottom. It needs `pandas`, `numpy`, `yfinance`, `scipy`, `matplotlib`, and
`seaborn`.

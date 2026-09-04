# SPY Time-Series Analysis & GARCH

A quantitative finance project analyzing the time-series behavior of **SPY daily returns** from 2010 to 2025.

The project investigates whether daily returns contain predictable information from their own past and whether volatility can be modeled and forecasted using a GARCH model.

## Research Question

> Are SPY returns predictable from their own past, and although returns may be difficult to predict, can volatility be modeled and forecasted using GARCH?

## Objectives

This project covers:

- Data collection and cleaning
- Daily return calculation
- Stationarity testing using the Augmented Dickey-Fuller test
- Autocorrelation analysis
- ACF and PACF
- Ljung-Box tests
- AR(1) return modeling
- Out-of-sample forecasting
- Comparison against a naive benchmark
- Volatility clustering
- GARCH(1,1) modeling
- Conditional volatility estimation
- Volatility forecasting

## Dataset

The project downloads historical SPY data using `yfinance`.

- **Asset:** SPY
- **Start:** 2010-01-01
- **End:** 2026-01-01
- **Frequency:** Daily
- **Price data:** Adjusted for corporate actions through `yfinance`'s `auto_adjust=True`

The raw market data is not stored in the repository because it is downloaded automatically when the notebook is run.

## Methodology

### 1. Daily Returns

Simple daily returns are calculated as:

$$
R_t = \frac{P_t-P_{t-1}}{P_{t-1}}
$$

### 2. Stationarity

The Augmented Dickey-Fuller test is used to investigate whether SPY prices and returns contain a unit root.

### 3. Autocorrelation

ACF, PACF, and Ljung-Box tests are used to examine serial dependence in daily returns.

### 4. AR(1)

The autoregressive model is:

$$
R_t = c + \phi R_{t-1} + \epsilon_t
$$

A negative and statistically significant coefficient indicates short-term reversal.

### 5. Out-of-Sample Testing

The data is divided into training and testing periods.

The AR(1) model is evaluated using RMSE and compared against a naive zero-return benchmark.

### 6. Volatility Clustering

Squared returns are used as a proxy for return magnitude:

$$
R_t^2
$$

Their autocorrelation is examined to identify volatility clustering.

### 7. GARCH(1,1)

Conditional variance is modeled as:

$$
\sigma_t^2 =
\omega +
\alpha\epsilon_{t-1}^2 +
\beta\sigma_{t-1}^2
$$

where:

- **ω** represents the baseline variance component
- **α** measures the response to a new shock
- **β** measures volatility persistence

The quantity:

$$
\alpha + \beta
$$

is used as a measure of volatility persistence.

## Key Results

From the model developed in this project:

| Result | Approximate value |
|---|---:|
| AR(1) coefficient | -0.113 |
| AR(1) R² | 0.013 |
| AR(1) test RMSE | 0.01006 |
| Naive test RMSE | 0.01008 |
| GARCH α | 0.166 |
| GARCH β | 0.802 |
| GARCH α + β | 0.968 |

The AR(1) coefficient is statistically significant, but the model explains only a small fraction of daily return variation.

The out-of-sample improvement over the naive benchmark is very small.

In contrast, the GARCH model indicates strong volatility persistence, with α + β close to 1.

## Main Conclusion

The results demonstrate an important distinction in financial time-series modeling:

**Daily return direction is difficult to predict using simple autoregressive information, while volatility exhibits substantially stronger temporal structure.**

The AR(1) model finds evidence of short-term negative autocorrelation, but its practical forecasting improvement is limited. GARCH provides a more useful framework for modeling the time-varying volatility of SPY returns.

## Repository Structure

```text
week7-spy-time-series-garch/
│
├── SPY_TimeSeries_GARCH.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

## Installation

Clone the repository and install the required Python packages:

```bash
git clone <YOUR-GITHUB-REPOSITORY-URL>
cd week7-spy-time-series-garch
pip install -r requirements.txt
```

Then open:

```text
SPY_TimeSeries_GARCH.ipynb
```

in Jupyter Notebook, JupyterLab, or VS Code.

## Requirements

Python 3.9+ is recommended.

The required packages are listed in `requirements.txt`.

## Reproducibility

The notebook downloads the SPY data directly from Yahoo Finance through `yfinance`, so no manually stored dataset is required.

Run the notebook from top to bottom to reproduce the analysis.

Because financial data providers can revise historical data and software packages can change over time, exact numerical results may differ slightly between runs.

## Disclaimer

This project is for educational and research purposes only.

The analysis is not financial advice and does not constitute an investment recommendation.

## Author

**Attila Kalácska-Tornyossy**

Physics BSc → Quantitative Finance

This project is part of a structured quantitative finance learning roadmap.

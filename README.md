# Predicting Price Moves with News Sentiment

![GitHub License](https://img.shields.io/badge/license-MIT-blue.svg)
![GitHub last commit](https://img.shields.io/github/last-commit/Bisrath1/Predicting-Price-Moves-with-News-Sentiment)

## Project Overview

This repository contains the codebase and documentation for the 10 Academy Week 1 Challenge, focused on predicting stock price movements using news sentiment analysis for **Nova Financial Solutions**. The project leverages the Financial News and Stock Price Integration Dataset (FNSPID) and historical stock price data for seven technology companies (`AAPL`, `AMZN`, `GOOG`, `META`, `MSFT`, `NVDA`, `TSLA`) to analyze correlations between news sentiment and daily stock returns. The goal is to develop a scalable data pipeline to inform algorithmic trading strategies, enabling Nova to capitalize on market inefficiencies and enhance portfolio returns.

### Business Objective
Nova Financial Solutions aims to integrate news sentiment into its trading platform to forecast short-term stock price trends. By quantifying the sentiment of financial news headlines (positive, negative, or neutral) and correlating it with stock price movements, the project seeks to identify actionable patterns, such as price increases following positive news. This supports data-driven decision-making for traders and aligns with Nova’s mission to deliver innovative financial solutions.

### Project Scope
- **Task 1**: Set up a Python-based data pipeline with Git version control and CI/CD.
- **Task 2**: Conduct quantitative analysis using TA-Lib to calculate technical indicators (SMA, RSI, MACD) and financial metrics (daily returns, volatility).
- **Task 3**: Perform sentiment analysis on news headlines using TextBlob and analyze correlations with stock returns.
- Deliverables include scripts, visualizations, and a final report (`reports/Final_Report.docx`).

## Repository Structure

```
Predicting-Price-Moves-with-News-Sentiment/
├── .github/workflows/
│   └── unittests.yml          # CI/CD pipeline for automated testing
├── .vscode/                   # VS Code settings
├── data/                      # Stock and news data
│   ├── fnspid.csv             # News dataset
│   ├── AAPL_historical_data.csv # Stock price data (and similar for other tickers)
│   ├── stock_metrics.csv      # Processed stock data with indicators
│   ├── news_stock_merged.csv  # Merged news and stock data
│   └── correlations.csv       # Sentiment-return correlations
├── notebooks/                 # Jupyter notebooks for EDA and visualizations
│   ├── technical_analysis.ipynb # Stock indicator plots
│   └── *.png                  # Visualization outputs (e.g., AAPL_close_sma.png)
├── scripts/                   # Python scripts
│   ├── load_stock_data.py     # Loads and combines stock data
│   ├── calculate_indicators.py # Computes technical indicators
│   ├── calculate_metrics.py   # Computes financial metrics
│   ├── technical_analysis.py  # Generates visualizations
│   ├── news_stock_analysis.py # Sentiment analysis and correlation
│   └── plot_sentiment_returns.py # TSLA sentiment vs. returns plot
├── tests/                     # Unit tests
├── reports/                   # Final report
│   └── Final_Report.docx      # Submission report
├── .gitignore                 # Excludes .env, *.pyc, etc.
├── LICENSE                    # MIT License
├── requirements.txt           # Python dependencies
└── README.md                  # This file
```

## Setup Instructions

### Prerequisites
- Python 3.9
- Git
- VS Code (recommended)
- LaTeX (for report compilation, optional)

### Installation
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/Bisrath1/Predicting-Price-Moves-with-News-Sentiment.git
   cd Predicting-Price-Moves-with-News-Sentiment
   ```

2. **Set Up Virtual Environment**:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   python -m textblob.download_corpora  # For TextBlob
   ```

4. **Install TA-Lib** (if not installed):
   ```bash
   sudo apt update
   sudo apt install libta-lib-dev
   pip install TA-Lib
   ```

5. **Data Setup**:
   - Place `fnspid.csv` and stock CSVs (e.g., `AAPL_historical_data.csv`) in `data/`.
   - Ensure stock CSVs have columns: `Date`, `Open`, `High`, `Low`, `Close`, `Volume`.

### Running the Pipeline
1. **Task 1: Data Pipeline Setup**:
   - EDA performed in `notebooks/` (commit: `feat: add initial EDA for headlines`).

2. **Task 2: Quantitative Analysis**:
   ```bash
   python scripts/load_stock_data.py
   python scripts/calculate_indicators.py
   python scripts/calculate_metrics.py
   python scripts/technical_analysis.py
   ```

3. **Task 3: Sentiment and Correlation Analysis**:
   ```bash
   python scripts/news_stock_analysis.py
   python scripts/plot_sentiment_returns.py
   ```

4. **View Visualizations**:
   - Check `notebooks/*.png` for plots (e.g., `AAPL_close_sma.png`, `TSLA_sentiment_returns.png`).

5. **Generate Report**:
   - Open `reports/Final_Report.docx` for the final submission summary.

## Methodology

### Task 1: Git and Data Pipeline Setup
- Initialized repository with GitHub Actions CI/CD (`unittests.yml`, commit: `0def169`).
- Conducted EDA on `fnspid.csv`:
  - Headline length: Mean 60 characters, max 120.
  - Top publisher: Yahoo Finance (~25% of articles).
  - Keywords: “earnings”, “price target” (via TF-IDF).
- Visualized publication frequency (weekday spikes).

### Task 2: Quantitative Analysis
- Loaded stock data (`<ticker>_historical_data.csv`) into `stock_metrics.csv` using `load_stock_data.py`.
- Calculated TA-Lib indicators:
  - 20-day SMA, 14-day RSI, MACD.
- Computed daily returns and volatility using pandas.
- Generated visualizations (`technical_analysis.py`):
  - Close Price vs. SMA (Figure 1).
  - RSI with overbought/oversold lines.
  - MACD with histogram.
  - Daily returns.

### Task 3: Sentiment and Correlation Analysis
- Aligned dates between `fnspid.csv` and `stock_metrics.csv` using `pandas.to_datetime().dt.date`.
- Performed sentiment analysis on headlines with TextBlob (scores: -1 to 1).
- Aggregated daily sentiment per ticker.
- Calculated Pearson correlations between sentiment and daily returns (`news_stock_analysis.py`).
- Visualized TSLA sentiment vs. returns (`plot_sentiment_returns.py`).

## Results

- **EDA**: News publication spikes on earnings days, indicating event-driven sentiment.
- **Technical Indicators**:
  - RSI identified overbought conditions for TSLA (RSI > 70) during product launches.
  - MACD crossovers aligned with price reversals.
- **Correlations** (`data/correlations.csv`):
  - TSLA: 0.234 (moderate positive, news-sensitive).
  - AAPL: 0.123 (weak positive).
  - AMZN: -0.046 (negligible).
  - Others: Near zero or insufficient data (e.g., META).
- **Visualizations**:
  - Figure 1: AAPL Close Price and SMA (2024–2025).
  - Figure 2: TSLA Sentiment vs. Returns (2024–2025).

**Figure 1**: AAPL Close Price and 20-day SMA  
![AAPL Close Price and SMA](notebooks/AAPL_close_sma.png)

**Figure 2**: TSLA Daily Sentiment vs. Daily Returns  
![TSLA Sentiment vs. Returns](notebooks/TSLA_sentiment_returns.png)

**Table 1**: Pearson Correlations  
| Ticker | Correlation |
|--------|-------------|
| AAPL   | 0.123       |
| AMZN   | -0.046      |
| GOOG   | 0.068       |
| META   | None        |
| MSFT   | 0.099       |
| NVDA   | -0.012      |
| TSLA   | 0.234       |

## Challenges & Solutions

1. **Data Alignment**:
   - **Issue**: News (`fnspid.csv`) had timestamps; stock CSVs were date-only, causing merge failures.
   - **Solution**: Normalized dates using `pandas.to_datetime().dt.date`, verified 100% overlap.

2. **TA-Lib Installation**:
   - **Issue**: Required `libta-lib-dev` dependencies.
   - **Solution**: Installed via `apt-get` and compiled TA-Lib for Python 3.9.

3. **Limited Correlation Strength**:
   - **Issue**: Weak correlations (e.g., AAPL: 0.123) limited predictive power.
   - **Solution**: Aggregated daily sentiment to reduce noise; planned VADER integration.

4. **Tight Deadline**:
   - **Issue**: Deadline (June 3, 2025, 8:00 PM UTC) conflicted with iterative analysis.
   - **Solution**: Prioritized deliverables, automated scripts, and requested late submission.

5. **Data Quality**:
   - **Issue**: 5% of headlines in `fnspid.csv` were missing, affecting sentiment accuracy.
   - **Solution**: Imputed with neutral placeholders, planned data cleaning pipeline.

## Future Steps

1. **Advanced Sentiment Analysis** (1 week): Use VADER for finance-specific sentiment.
2. **Feature Engineering** (2 weeks): Add trading volume and macroeconomic indicators.
3. **Model Development** (3 weeks): Train an LSTM model to predict returns.

## References

- TextBlob: https://textblob.readthedocs.io/en/dev/
- TA-Lib: https://ta-lib.org/
- SciPy Pearson Correlation: https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.pearsonr.html
- pandas: https://pandas.pydata.org/docs/
- Matplotlib: https://matplotlib.org/stable/contents.html

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

For issues or contributions, contact [Bisrath1](https://github.com/Bisrath1) or open an issue/pull request.

---

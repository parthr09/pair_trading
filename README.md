# Pair Trading Strategy for NSE Stocks

A comprehensive pair trading implementation for Indian stock market (NSE) using statistical arbitrage principles. This strategy identifies highly correlated stock pairs and executes mean-reversion trades based on statistical deviation.

## 🚀 Overview

This project implements a statistical arbitrage strategy that:
- Analyzes correlation patterns among NIFTY 500 stocks
- Identifies statistically significant trading pairs using cointegration tests
- Executes automated pair trading with defined entry/exit criteria
- Provides comprehensive risk management and portfolio optimization

## 📊 Key Features

- **Correlation Analysis**: Identifies stock pairs with correlation > 0.5
- **Statistical Testing**: Uses Augmented Dickey-Fuller (ADF) test for stationarity
- **Risk Management**: Implements stop-loss and target ratios based on statistical deviation
- **Portfolio Optimization**: Selects best pairs using Sharpe ratio methodology
- **Performance Analytics**: Comprehensive backtesting with empyrical metrics

## 🛠️ Installation

```bash
pip install pandas numpy matplotlib seaborn yfinance scipy statsmodels empyrical
```

## 📋 Requirements

```python
pandas>=1.3.0
numpy>=1.21.0
yfinance>=0.1.70
matplotlib>=3.5.0
seaborn>=0.11.0
scipy>=1.7.0
statsmodels>=0.13.0
empyrical>=0.5.5
```

## 🏗️ Project Structure

```
pair_trading/
├── pair_trading.ipynb          # Main implementation notebook
├── ind_nifty500list.csv        # NIFTY 500 stock list
├── README.md                   # This file
└── requirements.txt            # Dependencies
```

## 🔧 Usage

### 1. Data Collection
```python
# Load NIFTY 500 stocks and download price data
path = r"ind_nifty500list.csv"
tickers = pd.read_csv(path)
tickers['Symbol'] = tickers['Symbol'] + str('.NS')
download = (tickers['Symbol'].to_list())

# Download last 200 days of data
d2 = date.today() - timedelta(days=200)
df = yf.download(tickers=download, start=d2)['Close']
```

### 2. Correlation Analysis
```python
# Calculate correlation matrix for returns
df2 = df.pct_change().fillna(method='bfill')
corr = df2.corr()

# Filter pairs with correlation > 0.5
Finale = corr_long.loc[corr_long['correlation'] > 0.5]
```

### 3. Statistical Testing
```python
# Run pair trading analysis with ADF test
Trades = run_pair_trading(Finale, df, df2, tickers)
DailyTrades = pd.DataFrame(Trades, columns=[
    'stock1', 'stock2', 'pvalue', 'zscore', 'correlation',
    'Sector1', 'Sector2', 'Current Ratio', 'SL Ratio', 'Target Ratio'
])

# Filter statistically significant pairs (p-value < 0.05)
DailyTrades = DailyTrades.loc[DailyTrades['pvalue'] <= 0.05]
```

### 4. Portfolio Construction
```python
# Build optimized portfolio
FinalPortfolio = build_simple_portfolio(DailyTrades)

# Run performance simulation
trade_log, performance, portfolio_series = simulate_portfolio_performance_fixed(FinalPortfolio)
```

## 📈 Strategy Logic

### Entry Criteria
- **Correlation**: > 0.70 between stock pairs
- **Statistical Significance**: p-value < 0.05 (ADF test)
- **Z-Score Threshold**: |z-score| > 2 (for conservative) or > 4 (for aggressive)

### Position Direction
- **Long Ratio**: When z-score < -2 (ratio is undervalued)
- **Short Ratio**: When z-score > +2 (ratio is overvalued)

### Exit Strategy
- **Target**: Mean ± 1 standard deviation
- **Stop Loss**: Mean ± 3 standard deviations
- **Risk-Reward**: Calculated using Sharpe ratio methodology

## 📊 Performance Metrics

The strategy tracks comprehensive performance metrics:

```python
Performance Summary:
- Total Return (%)     : 3.44
- Annualized Return (%): 10.04
- Volatility (%)       : 1.01
- Sharpe Ratio         : 9.52
- Max Drawdown (%)     : -1.40
- Win Rate (%)         : 33.33
```

## 🔍 Key Functions

### `PairTrade()`
Core function that analyzes individual stock pairs:
- Calculates price ratios and residuals
- Performs ADF test for stationarity
- Determines entry/exit levels

### `build_simple_portfolio()`
Portfolio optimization function:
- Calculates expected returns and risk metrics
- Ranks pairs by Sharpe ratio
- Selects top performing pairs

### `simulate_portfolio_performance_fixed()`
Backtesting engine:
- Simulates sequential trade execution
- Calculates portfolio evolution
- Provides comprehensive performance analytics

## ⚠️ Risk Considerations

- **Market Risk**: Strategy performance depends on market conditions
- **Correlation Breakdown**: Pairs may lose correlation during market stress
- **Transaction Costs**: Real implementation requires consideration of brokerage and impact costs
- **Capital Requirements**: Requires sufficient capital for multiple simultaneous positions

## 🎯 Future Enhancements

- [ ] Real-time data integration with live trading APIs
- [ ] Machine learning models for correlation prediction
- [ ] Dynamic position sizing based on volatility
- [ ] Sector-neutral portfolio construction
- [ ] Options-based pair trading implementation

## 📝 Data Requirements

- **Source**: Yahoo Finance (yfinance)
- **Universe**: NIFTY 500 stocks
- **Timeframe**: 200 trading days for analysis
- **Frequency**: Daily closing prices

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## ⚖️ Disclaimer

This project is for educational and research purposes only. Past performance does not guarantee future results. Always conduct thorough testing and risk assessment before implementing any trading strategy with real capital.

## 📞 Contact

For questions or suggestions, please open an issue on GitHub.

---

**Happy Trading! 📈**

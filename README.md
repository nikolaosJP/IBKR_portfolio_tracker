# IBKR Portfolio Tracker

A comprehensive Python-based portfolio analysis and tracking tool for Interactive Brokers (IBKR) account data. This project provides automated portfolio analytics, performance metrics calculation, visualization, and rebalancing recommendations.

## Features

- **Portfolio Metrics**: Calculate key performance indicators including ROIC, Time-Weighted Return (TWR), and annualized returns
- **Real-time Analysis**: Fetch current market prices using Yahoo Finance for up-to-date portfolio valuation
- **Visualization**: Generate comprehensive charts for portfolio value, P&L, allocation, and performance over time
- **Rebalancing**: Calculate optimal trades to rebalance portfolio to target allocation
- **CSV Import**: Process IBKR CSV exports containing trades, dividends, deposits, withdrawals, and positions

## Project Structure

```
IBKR_portfolio_tracker/
├── data/                   # CSV data files from IBKR (gitignored)
├── src/                    # Core library modules
│   ├── data_loader.py      # Load and parse IBKR transactions and positions
│   ├── metrics.py          # Calculate portfolio performance metrics
│   ├── visualization.py    # Generate charts and summary reports
│   └── rebalancing.py      # Calculate rebalancing trades
└── jupyter/                # Analysis notebooks
    ├── portfolio_analysis.ipynb          # Main automated analysis notebook
    └── verify_calculations.ipynb         # Verification and testing notebook
```

## Installation

### Prerequisites

- Python 3.8+
- Jupyter Notebook (optional, for interactive analysis)

### Dependencies

Install required packages:

```bash
pip install polars yfinance matplotlib numpy
```

## Usage

### 1. Prepare Your Data

Export your IBKR account data as CSV and place it in the `data/` directory with the naming pattern:
```
data/UXXXXXXXX_YYYYMMDD_YYYYMMDD.csv
```

The CSV should include sections for:
- Trades (Stocks and Forex)
- Dividends and Withholding Tax
- Deposits & Withdrawals
- Fees
- Open Positions

### 2. Run the Analysis Notebook

```bash
cd jupyter
jupyter notebook portfolio_analysis.ipynb
```

Run all cells to generate:
- Daily portfolio metrics with real-time prices
- Performance charts (portfolio value, P&L, allocation)
- Comprehensive summary report
- Rebalancing recommendations

### 3. Use as a Python Library

```python
import sys
sys.path.insert(0, '../src')

from data_loader import load_transactions, load_positions
from metrics import calculate_portfolio_metrics
from visualization import plot_portfolio_performance, print_portfolio_summary
from rebalancing import calculate_rebalancing

# Load data
transactions = load_transactions()
positions = load_positions()

# Calculate metrics
portfolio_history = calculate_portfolio_metrics(transactions)

# Visualize
plot_portfolio_performance(portfolio_history, transactions)
print_portfolio_summary(transactions, positions, portfolio_history)

# Get rebalancing recommendations
target_allocation = {'VTI': 72, 'SPY': 6, 'VXUS': 22}
calculate_rebalancing(positions, target_allocation, investment_amount=24000)
```

## Key Metrics Explained

- **ROIC (Return on Invested Capital)**:
  ```
  (Unrealized P&L + Realized P&L + Dividends) / Total Invested Capital × 100
  ```

- **TWR (Time-Weighted Return)**:
  ```
  (Current Equity / Total Contributed) - 1
  ```

- **Annualized TWR**:
  ```
  [(1 + TWR)^(1/years) - 1] × 100
  ```

## Security Notice

⚠️ **Important**: This repository does not include any actual financial data. All CSV files and data outputs are gitignored. Jupyter notebooks have been cleared of all execution outputs to prevent exposure of confidential information.

## License

This project is for personal use. Feel free to adapt it for your own portfolio tracking needs.

## Disclaimer

This tool is for informational and analytical purposes only. It does not constitute financial advice. Always consult with a qualified financial advisor before making investment decisions.

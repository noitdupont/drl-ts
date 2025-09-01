## Deep Reinforcement Learning (DRL) Trading System

[![Release](https://img.shields.io/github/release/0xnu/drl-ts.svg)](https://github.com/0xnu/drl-ts/releases/latest)
[![License](https://img.shields.io/badge/License-Modified_MIT-f5de53?&color=f5de53)](/LICENSE)

It uses [deep reinforcement learning](https://en.wikipedia.org/wiki/Deep_reinforcement_learning) to learn market patterns and automatically make buy, sell, or hold decisions, training itself by testing strategies and learning from outcomes.

> [!WARNING]
> Disclaimer: It is an experimental system; do not use it for actual investment decisions.

> Checkout this [repository](https://github.com/0xnu/deep-reinforcement-learning) if you want to learn more about Deep Reinforcement Learning.

### Interactive Brokers

Here's a guide for setting up Interactive Brokers for the Deep Reinforcement Learning Trading System:

#### Create a Paper Trading Account

+ **Visit Interactive Brokers**: Go to [www.interactivebrokers.co.uk](https://ibkr.com/referral/abiodun557) (for UK)
+ **Open Account**: Click "Open Account" and select "Individual"
+ **Choose Paper Trading**: During setup, ensure you enable paper trading (demo account)
+ **Complete Application**: Fill in all required information
+ **Fund Account**: Paper trading accounts come with virtual money (usually $1M USD)

#### Download and Install Trader Workstation (TWS)

+ **Download TWS**: Go to Client Portal → Trading Platforms → Download TWS
+ **Install**: Run the installer (available for Windows, Mac, Linux)
+ **Alternative**: You can also use IB Gateway (lighter version) instead of full TWS

#### IB Gateway (Recommended for API)

+ **Download**: Client Portal → Trading Platforms → Download IB Gateway
+ **Lighter Option**: Gateway is better for API-only usage (no GUI trading interface)

#### Configure API Settings

##### Enable API Access

+ Login to TWS/Gateway
+ Go to Configuration:
    + TWS: File → Global Configuration → API → Settings
    + Gateway: Configure → Settings → API
+ Enable API:
    + Enable ActiveX and Socket Clients
    + Allow connections from localhost only (127.0.0.1)
    + Read-Only API (for safety during testing)
+ Set Socket Port:
    + Paper Trading: 7497 (default)
    + Live Trading: 7496 (use only when ready for live trading)
+ Client ID: Set to 0 or any number (match this in your Python code)

#### Important Security Settings

```sh
✅ Enable API
✅ Read-Only API (initially)
✅ Allow connections from localhost (127.0.0.1) only
❌ Don't enable "Download open orders on connection"
❌ Don't enable "Allow connections from anywhere"
```

#### Market Data Permissions

##### Enable Required Data

+ **Go to**: Account Management → Market Data Subscriptions
+ Enable:
    + US Securities Snapshot and Futures Value Bundle (if trading US stocks)
    + UK Securities (if trading UK stocks)
    + Real-time quotes for your target markets
+ **Note**: Some data feeds have monthly costs, but basic delayed data is often free

#### Workflow for Using with DRL Trading System

Daily setup process:

+ Start TWS/Gateway:

```sh
# Make sure TWS or Gateway is running
# Login with your paper trading credentials
```

+ Verify API settings:
    + Port: 7497 (paper trading)
    + API enabled
    + Correct client ID

+ Run DRL Trading System:

```sh
# In the notebook/script
if ib_conn.connect():
    print("✅ Ready for trading!")
    # Trading code here
```

#### Testing Checklist

Before running the DRL trading system:

- [x] TWS/Gateway running and logged in
- [x] API settings configured correctly
- [x] Market data permissions enabled
- [x] Test connection script works
- [x] Can retrieve historical data
- [x] Can place paper orders (test manually first)

#### Common Issues and Solutions

Connection problems:

```sh
# If connection fails, check:

# 1. Port number
ib.connect('127.0.0.1', 7497, clientId=1)  # Paper trading
# NOT 7496 (live trading)

# 2. Client ID conflicts
# Try different client IDs: 1, 2, 3, etc.

# 3. API not enabled
# Check TWS: File → Global Configuration → API → Settings
```

#### Market Data Issues

+ **No real-time data**: Enable market data subscriptions
+ **Delayed data**: Normal for free accounts, 15-20 minute delay
+ **Weekend/holidays**: Markets closed, no live data available

#### Interactive Brokers Market Data

Interactive Brokers (IBKR) requires you to maintain a minimum balance of $500 USD (£370 GBP) in your funded account to [subscribe to and receive real-time market data](https://www.interactivebrokers.com/en/pricing/market-data-pricing.php?p=mktDataPricing), not as a one-time fee for data access. This $500 (£370 GBP) balance is a maintenance requirement, in addition to the monthly fees for the specific market data feeds you choose to subscribe to. Whilst basic delayed data may be available, you must have a funded account and select specific data subscriptions to receive live, timely information for trading.

You need to subscribe to these market data for the Trading Systems (DRL and Non-DRL) to work properly:

+ NYSE (Network A/CTA)(L1) - $1.50 / month (£1.11 / month)
+ NASDAQ (Network C/UTP)(L1) - $1.50 / month (£1.11 / month)

#### Paper Trading vs Live Trading

```sh
# Paper Trading (Safe for testing)
PAPER_TRADING_PORT = 7497

# Live Trading (Only when ready!)
LIVE_TRADING_PORT = 7496

# Always start with paper trading!
ib.connect('127.0.0.1', PAPER_TRADING_PORT, clientId=1)
```

#### Safety First

+ Always test with paper trading first
+ Never use live trading until system is thoroughly tested
+ Monitor all trades manually initially
+ Start with small position sizes

Once you complete this setup, **DRL Trading System** will be able to connect to Interactive Brokers and execute paper trades safely for testing and validation.

### Install Dependencies

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install required libraries:

```sh
# Prerequisites
python3 -m venv .venv
source .venv/bin/activate
uv pip install -r requirements.txt
```

### Run the System

Click the `Run` button to run the individual cell of the [Jupyter Notebook](./drl-ts.ipynb).

> Do not run the cell that initializes the Interactive Brokers Live Trading (Live Trading Integration).

### License

This project is licensed under the [Modified MIT License](./LICENSE).

### Copyright

(c) 2025 [Finbarrs Oketunji](https://finbarrs.eu). All Rights Reserved.

---

My non-negotiable fee for a custom enterprise trading system is £150,000. [Let's talk](mailto:f+trading@finbarrs.eu) about your requirements.
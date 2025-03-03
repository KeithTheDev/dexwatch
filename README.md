# 🔍 DexWatch

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)

DexWatch is a high-performance DEX analytics pipeline that tracks token performance, liquidity pairs, and market movements across multiple chains. Built with asyncio, and rotating proxies to bypass rate limiting and deliver high-resolution time-series data, it's designed for reliability and scale.

## ✨ Features

- 🚀 Asynchronous data collection from DexScreener API
- 🔄 Smart proxy rotation with geo-distributed endpoints
- 📊 Real-time token and pair analytics
- 💾 Persistent storage with Redis and ArangoDB
- 📈 Comprehensive chain and DEX statistics
- 🛡️ Built-in rate limiting and error handling
- 📝 Detailed logging and performance metrics

## 🏗️ Architecture

```
src/
├── __init__.py
├── config.py                 # Configuration and constants
├── db/                      # Database operations
├── api/                     # API clients
├── models/                  # Data models
├── services/                # Business logic
└── main.py                  # Entry point
```

## 🚀 Quick Start

### Prerequisites

- Python 3.9+
- Redis
- ArangoDB
- Virtual environment (recommended)

### Installation

1. Clone the repository:

```bash
git clone https://github.com/KeithTheDev/dexwatch.git
cd dexwatch
```

2. Create and activate virtual environment:

```bash
python -m venv venv
source venv/bin/activate  # Unix
# or
.\venv\Scripts\activate  # Windows
```

3. Install dependencies:

```bash
pip install -r requirements.txt
```

4. Configure your environment:

```python
# config.py

# Database Settings
REDIS_URL = "redis://localhost:6379"
ARANGO_URL = "http://localhost:8529"
DB_NAME = "dexwatch"

# Proxy Configuration
PROXY_USERNAME = "your_username" # (optional)
PROXY_PASSWORD = "your_password" # (optional)

# Performance Tuning
CONCURRENCY_LIMIT = 50
BATCH_SIZE = 30
```

### Usage

Run the pipeline:

```bash
python main.py
```

Monitor the analysis:

```bash
tail -f dexwatch.log
```

## 📊 Sample Output

```text
Pipeline Summary:
----------------
Total Runtime: 5.72 seconds
Total Requests: 86
Successful Requests: 86
Failed Requests: 0
Tokens Processed: 83
Success Rate: 100.00%

2025-02-08 13:22:09.549 - config - INFO - [run_pipeline] - Pipeline shutdown complete
2025-02-08 13:22:09.549 - config - INFO - [main] -
=== Analyzing Pair Data ===
2025-02-08 13:22:09.725 - config - INFO - [analyze_pairs] -
=== Chain ID Pair Distribution ===
2025-02-08 13:22:09.725 - config - INFO - [analyze_pairs] -
Chain: solana
2025-02-08 13:22:09.725 - config - INFO - [analyze_pairs] -   Active Tokens: 120
2025-02-08 13:22:09.725 - config - INFO - [analyze_pairs] -   Total Pairs: 253 (92.0% of all pairs)
2025-02-08 13:22:09.726 - config - INFO - [analyze_pairs] -   Total Liquidity: $13,614,997.79
2025-02-08 13:22:09.726 - config - INFO - [analyze_pairs] -   24h Volume: $201,597,841.53
2025-02-08 13:22:09.726 - config - INFO - [analyze_pairs] -   Avg Pairs per Token: 2.1
2025-02-08 13:22:09.726 - config - INFO - [analyze_pairs] -   DEX Distribution:
2025-02-08 13:22:09.726 - config - INFO - [analyze_pairs] -     raydium: 121 pairs (47.8%)
2025-02-08 13:22:09.726 - config - INFO - [analyze_pairs] -     meteora: 69 pairs (27.3%)
2025-02-08 13:22:09.726 - config - INFO - [analyze_pairs] -     pumpfun: 47 pairs (18.6%)
2025-02-08 13:22:09.726 - config - INFO - [analyze_pairs] -     moonshot: 13 pairs (5.1%)
2025-02-08 13:22:09.726 - config - INFO - [analyze_pairs] -     orca: 3 pairs (1.2%)
2025-02-08 13:22:09.726 - config - INFO - [analyze_pairs] -
Chain: base
2025-02-08 13:22:09.726 - config - INFO - [analyze_pairs] -   Active Tokens: 5
2025-02-08 13:22:09.726 - config - INFO - [analyze_pairs] -   Total Pairs: 7 (2.5% of all pairs)
2025-02-08 13:22:09.726 - config - INFO - [analyze_pairs] -   Total Liquidity: $286,107.93
2025-02-08 13:22:09.727 - config - INFO - [analyze_pairs] -   24h Volume: $867,141.57
2025-02-08 13:22:09.727 - config - INFO - [analyze_pairs] -   Avg Pairs per Token: 1.4
2025-02-08 13:22:09.727 - config - INFO - [analyze_pairs] -   DEX Distribution:
2025-02-08 13:22:09.727 - config - INFO - [analyze_pairs] -     uniswap: 7 pairs (100.0%)
2025-02-08 13:22:09.727 - config - INFO - [analyze_pairs] -
Chain: pulsechain
2025-02-08 13:22:09.727 - config - INFO - [analyze_pairs] -   Active Tokens: 2
2025-02-08 13:22:09.727 - config - INFO - [analyze_pairs] -   Total Pairs: 7 (2.5% of all pairs)
2025-02-08 13:22:09.727 - config - INFO - [analyze_pairs] -   Total Liquidity: $50,872.93
2025-02-08 13:22:09.727 - config - INFO - [analyze_pairs] -   24h Volume: $167,232.52
2025-02-08 13:22:09.727 - config - INFO - [analyze_pairs] -   Avg Pairs per Token: 3.5
2025-02-08 13:22:09.727 - config - INFO - [analyze_pairs] -   DEX Distribution:
2025-02-08 13:22:09.728 - config - INFO - [analyze_pairs] -     pulsex: 7 pairs (100.0%)
2025-02-08 13:22:09.728 - config - INFO - [analyze_pairs] -
Chain: ethereum
2025-02-08 13:22:09.728 - config - INFO - [analyze_pairs] -   Active Tokens: 6
2025-02-08 13:22:09.728 - config - INFO - [analyze_pairs] -   Total Pairs: 6 (2.2% of all pairs)
2025-02-08 13:22:09.728 - config - INFO - [analyze_pairs] -   Total Liquidity: $427,254.80
2025-02-08 13:22:09.728 - config - INFO - [analyze_pairs] -   24h Volume: $2,494,532.62
2025-02-08 13:22:09.728 - config - INFO - [analyze_pairs] -   Avg Pairs per Token: 1.0
2025-02-08 13:22:09.728 - config - INFO - [analyze_pairs] -   DEX Distribution:
2025-02-08 13:22:09.728 - config - INFO - [analyze_pairs] -     uniswap: 6 pairs (100.0%)
2025-02-08 13:22:09.728 - config - INFO - [analyze_pairs] -
Chain: xrpl
2025-02-08 13:22:09.729 - config - INFO - [analyze_pairs] -   Active Tokens: 2
2025-02-08 13:22:09.729 - config - INFO - [analyze_pairs] -   Total Pairs: 2 (0.7% of all pairs)
2025-02-08 13:22:09.729 - config - INFO - [analyze_pairs] -   Total Liquidity: $73,609.66
2025-02-08 13:22:09.729 - config - INFO - [analyze_pairs] -   24h Volume: $430,722.32
2025-02-08 13:22:09.729 - config - INFO - [analyze_pairs] -   Avg Pairs per Token: 1.0
2025-02-08 13:22:09.729 - config - INFO - [analyze_pairs] -   DEX Distribution:
2025-02-08 13:22:09.729 - config - INFO - [analyze_pairs] -     xrpl: 2 pairs (100.0%)
```

### Performance Tips

- Increase `max_concurrent` if using more proxies
- Adjust `batch_size` based on API rate limits
- Monitor proxy response times in logs
- Scale batch size with available memory

## 🕒 Scheduling

### Cron Setup

1. Create a wrapper script `run_dexwatch.sh`:

```bash
#!/bin/bash
cd /path/to/dexwatch
source venv/bin/activate
python main.py >> /var/log/dexwatch/pipeline.log 2>&1
```

2. Make executable:

```bash
chmod +x run_dexwatch.sh
```

3. Add cron job:

```bash
# Every 1 minute
*/1 * * * * /path/to/dexwatch/run_dexwatch.sh
```

## 🤝 Contributing

Contributions welcome! Check out our [Contributing Guide](CONTRIBUTING.md) to get started.

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Open a pull request

## 📝 License

MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Support

Join the Telegram: [t.me/IYKYKLabs](https://t.me/IYKYKLabs)
Follow Me on X: [x.com/eth_moon\_](https://x.com/eth_moon_)

## 🙏 Acknowledgments

- DexScreener API team for their excellent documentation
- And most of all our community. If you know, you know.

---

🌟 If this project helps you, please consider giving it a star!

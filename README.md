markdown
# Bootstrap Monte Carlo Stock Simulation

A Python tool that performs a **Bootstrap Monte Carlo simulation** on historical stock data to forecast future price paths. Instead of assuming normal distribution parameters (μ, σ), this model samples randomly from **historical log returns** to model future asset performance.

## Core Features

*   **Non-Parametric Bootstrapping:** Re-samples directly from historical log returns to capture real market anomalies and tail risks.
*   **Inflation Adjustment:** Calculates the real purchasing power of the expected future price using a custom annual inflation rate.
*   **Fee-Adjusted Profit Probability:** Automatically deducts a **1.01% trading fee buffer** (`* 0.9899`) to calculate the true probability of turning a net profit.
*   **Tail-Risk Customization:** Allows flexible parameters to extract targeted worst-case and best-case performance thresholds.
*   **Visual Projections:** Generates a custom `matplotlib` chart showing all generated future price trajectories.

## Getting Started

### Prerequisites

Ensure you have the required libraries installed:

```bash
pip install numpy pandas yfinance matplotlib
```

### Usage Example

```python
from datetime import datetime
# Import or paste the function here

# Run with default settings (1,000 simulations, AAPL, 252 trading days)
bootstrap_monte_carlo_simulation()
```

## Function Arguments & Parameters

| Parameter | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `sim` | `int` | `1000` | The total number of individual price paths to simulate. |
| `start` | `str` | `'2020-01-01'` | Start date for pulling historical asset data (`YYYY-MM-DD`). |
| `end` | `str` | *Dynamic (Today)* | End date for historical data pull. Defaults to the current date. |
| `stock` | `str` | `'AAPL'` | The ticker symbol of the asset to pull from Yahoo Finance. |
| `days_simulated` | `int` | `252` | Trading days into the future to forecast (252 days ≈ 1 year). |
| `value_for_probability_calculation` | `float` | `50` | Target percentage growth threshold to evaluate success probability. |
| `inflation_rate` | `float` | `2` | Annualized inflation rate percentage to calculate real asset value. |
| `worst_outcome_percent` | `float` | `5` | The bottom percentile threshold to quantify downside tail risk. |
| `best_outcome_percent` | `float` | `5` | The top percentile threshold to quantify upside potential. |

## Terminal Outputs Explained

When executed, the script calculates and prints the following metrics:

*   **Today's Price:** The final closed price found in the fetched dataset history.
*   **Median:** The exact 50th percentile mark where half of the paths finished higher and half finished lower.
*   **Expected Price:** The nominal arithmetic mean of all simulated outcomes at day T.
*   **Real Expected Price:** The future price scaled down to match present-day purchasing power relative to your `inflation_rate`.
*   **Worst/Best Cases:** The price boundaries marking the extreme custom percentage tails of your simulation run.
*   **Probability of Profit:** The mathematical probability that the future asset path scales past the i

# Machine Learning Strategies for Intraday Trading (NSE Nifty 50)

## Overview

This repository implements the machine learning methodologies and trading strategies presented in two IEEE conference research papers. The project focuses on the Indian National Stock Exchange (NSE), specifically the Nifty 50 index, to predict intraday stock prices and execute selective trading strategies.

The core objective is to leverage Machine Learning (ML) to predict `HIGH`, `LOW`, and `CLOSE` prices for a given trading day using the day's `OPEN` price and historical data. These predictions are then used to drive algorithmic trading strategies that balance opportunity with risk.

## Papers Implemented

This code is based on the following research:

1. **Enhancing Intraday Trading through Machine Learning: A NSE Nifty 50 Analysis**
* *Focus:* Comparative analysis of ML models (KNN, RF, DT, SVR, LR) for predicting intraday prices.
*Key Finding:* Linear Regression (LR) outperforms complex models like SVR and Random Forest for this specific task, achieving  scores exceeding 0.99.

* [Read the paper](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=10580836)


2. **Precision Balancing: Machine Learning Models and Selective Strategies for Intraday Trading Success**
* *Focus:* Developing selective trading strategies (HYBRID, ModHIGH, ModLOW) based on ML predictions.
*Key Finding:* The **HYBRID** strategy, which combines buy/sell logic with strict selection criteria, achieved a 140% gain over a 30-day testing period.

* [Read the paper](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=10563373)



## Methodology

### 1. Data & Preprocessing

The analysis uses historical stock data (Open, High, Low, Close) from Yahoo Finance for top Nifty 50 contributors.

**Stocks Analyzed:** RELIANCE, TCS, HDFCBANK, ICICIBANK, INFY, BHARTIARTL, HINDUNILVR, ITC, SBIN, LT.
**Input Features:** The primary predictive feature is the `OPEN` price of the current day, combined with historical `OPEN`, `HIGH`, `LOW`, and `CLOSE` data. * **Handling Missing Data:** Null values are handled using mean-refilling techniques.

### 2. Machine Learning Models

The repository evaluates six different regression models:

**Linear Regression (LR):** (Best Performer) Captures the linear relationship between the opening price and the day's high/low.
**Support Vector Regression (SVR):** Tested with and without  initialization.
**K-Nearest Neighbors (KNN)**.
**Decision Tree Regressor**.
**Random Forest Regressor**.

### 3. Trading Strategies

Based on the predictions from the Linear Regression model, the following strategies are explored:

* **HIGH_SELL / LOW_BUY:** Simple strategies that short at predicted highs or long at predicted lows.


* **ModHIGH / ModLOW:** Selective variations that only trade when specific divergence criteria are met.


* **HYBRID:** The optimal strategy that sequentially assesses deviations in High and Low predictions to maximize `percentageGainMin` (a metric for capital efficiency).



## Installation

### Prerequisites

Ensure you have Python installed. You can install the required dependencies using `pip`:

```bash
pip install pandas numpy scikit-learn matplotlib

```

### Directory Structure

To run the script `mlpartpaperstrategy.py`, ensure your directory looks like this:

```
├── mlpartpaperstrategy.py   # Main analysis script
├── README.md                # This file
└── data/                    # Folder containing .csv files for stocks
    ├── RELIANCE.NS.csv
    ├── TCS.NS.csv
    └── ... (other stock csvs)

```

*Note: You may need to update the file paths in `mlpartpaperstrategy.py` to point to your local `data/` directory instead of the Google Drive path (`/content/drive/MyDrive/...`).*

## Usage

1. **Prepare Data:** Download the historical data for the target stocks (e.g., from Yahoo Finance) and place them in your data folder.
2. **Run the Analysis:**
```bash
python mlpartpaperstrategy.py

```


3. **Output:**
* The script will print MAE, MSE, and  scores for each model and stock.


* It generates PDF plots comparing **Actual vs. Predicted** values for `High`, `Low`, and `Adj Close` prices.


* Results are saved to CSV files for further analysis.



## Results Summary

| Model | MAE (Close) | MSE (Close) | R2 Score (Close) |
| --- | --- | --- | --- |
| **Linear Regression** | **52.02** | **6101.04** | **0.999** |
| SVR (y=x) | 3002.33 | 9520590.40 | -0.94 |
| Random Forest | 4203.75 | 21841254.36 | -3.45 |

As detailed in the research, Linear Regression consistently provides the lowest error and highest explained variance for Nifty 50 stocks.

## Citation

If you use this code or strategies in your research, please cite the original IEEE papers:

```bibtex
@INPROCEEDINGS{10580836,
  author={Poptani, Akash},
  booktitle={2024 5th International Conference on Innovative Trends in Information Technology (ICITIIT)}, 
  title={Enhancing Intraday Trading through Machine Learning: A NSE Nifty 50 Analysis}, 
  year={2024},
  doi={10.1109/ICITIIT61487.2024.10580836}
}

@INPROCEEDINGS{10563373,
  author={Poptani, Akash},
  booktitle={2024 4th International Conference on Innovative Practices in Technology and Management (ICIPTM)}, 
  title={Precision Balancing: Machine Learning Models and Selective Strategies for Intraday Trading Success}, 
  year={2024},
  doi={10.1109/ICIPTM59628.2024.10563373}
}

```

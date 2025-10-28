# ds_divya

## Project Overview
This project explores the relationship between **trader behavior** (profitability, risk, trade volume, and leverage) and **market sentiment** (Fear vs Greed) using real datasets from Hyperliquid and the Bitcoin Market Sentiment Index.

The analysis identifies how trading performance metrics align or diverge from market sentiment trends, revealing behavioral patterns and insights that can guide smarter trading strategies.

---

## Folder Structure
```bash
ds_divya/
├── notebook_1.ipynb # Main analysis notebook (run in Google Colab)
├── csv_files/ # Contains input and processed datasets
│ ├── historical.csv # Trader-level historical data (Hyperliquid)
│ ├── fear_greed.csv # Bitcoin Fear & Greed Index dataset
│ ├── processed_traders.csv
│ ├── trades_with_sentiment.csv
│ ├── daily_aggregates.csv
│ └── account_daily_aggregates.csv
├── outputs/ # Saved figures and charts
│ ├── cumulative_pnl_vs_greed.png
│ ├── profit_rate_by_sentiment.png
│ └── (other optional visualizations)
├── ds_report.pdf # Final summary report
└── README.md # Project documentation
```

##  Datasets

### 1. **Bitcoin Market Sentiment Dataset**
- **Columns:** `Timestamp`,`Value`, `Classification`, `Date`,
- **Purpose:** Indicates daily market mood — *Fear* or *Greed*.
- **Source:** Official Fear & Greed Index data (provided link).

### 2. **Historical Trader Data (Hyperliquid)**
- **Columns:** `Account`, `Coin`, `Execution Price`, `Size Tokens`, `Size USD`, `Side`, `Timestamp IST`, `Start Position`, `Direction`, `Closed_Pnl`, `Transaction Hash`,`Order ID`,`Crossed` ,	`Fee`,`Trade ID`,`Timestamp`.
- **Purpose:** Captures every trade with profitability and leverage metrics.
- **Source:** Provided Hyperliquid trader dataset.

---

## Methodology Summary

1. **Data Loading & Cleaning**
   - CSVs loaded using `pandas` from `/csv_files/`.
   - Column names standardized to lowercase with underscores.
   - Datetime fields normalized into a common `date` column.
   - Numeric fields coerced into `float64` with invalid entries handled.

2. **Feature Engineering**
   - Computed **Notional value** per trade.
   - Created **`is_profitable`** boolean flag.
   - Merged market sentiment (Fear/Greed) onto each trade by date.

3. **Aggregation**
   - Built **daily-level metrics**:
     - Total trade volume
     - Net & cumulative PnL
     - Profit rate
     - Sentiment label
   - Saved as `daily_aggregates.csv`.

4. **Visualization**
   - **Cumulative PnL vs Greed periods**
   - **Profit rate by sentiment**
   - All figures saved under `/outputs/`.

5. **Statistical Testing**
   - Used **Mann–Whitney U test** to compare `closed_pnl` distributions during *Fear* vs *Greed* days.

6. **Modeling**
   - Trained a **Random Forest Classifier** predicting if a trader’s day is profitable.
   - Features: `trades`, `total_volume`, `sentiment_greed`.
   - Evaluation metrics: AUC ≈ **0.66**, indicating moderate predictive power.

---

## Key Findings

- Periods of **Greed** generally correlate with higher cumulative profits but increased volatility.
- **Fear** phases show lower volume but more consistent profitability ratios.
- No statistically significant difference in `closed_pnl` distributions (p ≈ 0.10) — suggesting nuanced behavioral effects.
- Simple sentiment-based models can predict profitable days better than random chance.

---

## How to Run (Google Colab)

1. Open [notebook_1.ipynb](https://drive.google.com/file/d/1kMsEwE2puRlMCjcZVt3ukMY96byNArm3/view?usp=drive_link) in **Google Colab**.  

2. Ensure the following folder structure exists in your Colab or local environment:
```bash
ds_divya/
├── csv_files/
├── outputs/
```


3. Upload the two CSVs inside `csv_files/`:
- `historical_data.csv`
- `fear_greed_index.csv`

4. Run all cells sequentially.  
The notebook will automatically:
- Process data  
- Generate visualizations under `/outputs/`  
- Export processed CSVs to `/csv_files/`

5. Review saved plots in `/outputs/` and the final report in `ds_report.pdf`.

---

##  Recommendations for Web3 Trading Team

- Integrate **sentiment-aware position sizing** — increase risk exposure slightly during neutral-to-greed phases, reduce during extreme fear.
- Develop **behavioral dashboards** combining trader-level PnL and aggregated sentiment shifts.
- Explore **longer time horizons** and additional features (leverage trends, liquidity spikes) for predictive modeling improvements.

---

## 👩‍💻 Author
**Divya Monga**  
Data Science Candidate | Web3 Trading Assignment  
*Contact:* linkedin.com/in/divya-ji4  
*Tools:* Python (Pandas, NumPy, Seaborn, Scikit-learn, Matplotlib)

---

## Notes
- All outputs and CSVs are saved to `ds_divya/` following strict submission format.
- Colab link sharing set to *Anyone with the link can view*.
- No local or Drive-dependent paths are required for reproducibility.
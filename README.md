# Trading Behavior vs. Market Sentiment Analysis

This project performs a comprehensive statistical analysis to determine if the Fear & Greed Index can be used as a predictive signal for daily crypto trading behavior.

## Objective

The goal was to analyze how trading behavior (profitability, risk, volume) aligns or diverges from overall market sentiment. The primary objective was to identify statistically significant, hidden trends that could influence smarter trading strategies.

## Key Findings & Actionable Insights

Our analysis disproved a common hypothesis but uncovered a more subtle, predictive signal.

### 1. Sentiment Does NOT Predict Profitability

There is **no statistically significant correlation** between market sentiment (e.g., 'Fear', 'Greed') and daily trading profitability (PnL).

* **Same-Day Test (p-value: 0.2978):** Today's sentiment does not predict today's PnL.
* **Next-Day Test (p-value: 0.4204):** Yesterday's sentiment does not predict today's PnL.

**Conclusion:** Strategies based on sentiment as a direct predictor of *profit* are not supported by this data.

### 2. Sentiment *Does* Predict Next-Day Volume

We found a **statistically significant signal (p-value: 0.0173)** that *yesterday's* sentiment has a predictive effect on *today's* total trading volume.

### 3. The Signal: The "Extreme" Effect

A Tukey's HSD post-hoc test (`p-value: 0.0217`) pinpointed the exact nature of this signal:

* **After an "Extreme Fear" day:** Expect **significantly HIGHER** trading volume. This suggests panic selling or "buy the dip" activity.
* **After an "Extreme Greed" day:** Expect **significantly LOWER** trading volume. This suggests market hesitation and reduced participation at peak euphoria.

**Actionable Insight:** The Fear & Greed Index is not a PnL predictor, but it is a valuable 1-day-ahead **volume and liquidity predictor**.

---

## Methodology

The analysis followed a 4-step "drill-down" process:

1.  **Data Preparation:** Cleaned and merged two datasets: a raw trading history (aggregated to daily PnL, volume, etc.) and a daily market sentiment history (Fear & Greed Index).
2.  **Exploratory Data Analysis (EDA):** Generated 10+ visualizations (boxplots, heatmaps, time-series) to visually inspect for trends.
3.  **Statistical Test 1 (Concurrent ANOVA):** Tested if *today's* sentiment impacts *today's* trading.
    * **Result:** No significant links found.
4.  **Statistical Test 2 (Lagged ANOVA & Tukey's HSD):** Created a 1-day lagged sentiment feature to test if *yesterday's* sentiment impacts *today's* trading.
    * **Result:** Found the significant predictive link to `total_volume_usd` and pinpointed it to the `Extreme Fear` vs. `Extreme Greed` relationship.

---

## Project Structure

```
/
├── README.md             
├── notebook-1.ipynb
├── notebooks/
│   ├── tests.ipynb
├── csv_files/
│   ├── fear_greed_index.csv
│   ├── historical_data.csv
│   ├── history_data_cleaned.csv
│   ├── sentiment_cleaned.csv
│   ├── marged_daily_data.csv
├── outputs/     (Contains all 10+ generated plots)
│   ├── 1_sentiment_distribution.png
│   ├── 5_pnl_by_sentiment_boxplot.png
│   ├── 10_pnl_vs_sentiment_timeseries.png
│   ├── 12_volume_by_lagged_sentiment_boxplot.png
│   └── ... (and 8 other plots)
├── ds_report.pdf

```

## How to Run

1.  Clone this repository.
2.  Install the required libraries:
    ```bash
    pip install pandas matplotlib seaborn statsmodels numpy
    ```
3.  Run the Python/Jupyter Notebook script to regenerate the analysis, plots, and statistical results.

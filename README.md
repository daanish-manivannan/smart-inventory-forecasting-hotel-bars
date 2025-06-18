# Save the generated README content as a README.md file

readme_content = """
# 🍷 Inventory Demand Forecasting & Par Level Recommendation System

### For Hotel Bar Chain Management

---

## 🧠 Problem Statement

A fast-growing hotel chain operating bars across multiple locations faces:
- **Stockouts** of high-demand liquor items.
- **Overstocking** of slow-moving inventory.

These issues lead to increased operational costs and poor guest satisfaction. Hotel managers need a smarter solution to forecast item-level demand and maintain optimal inventory (par levels) to reduce waste and ensure availability.

---

## 🎯 Goal

Develop a **forecasting and inventory recommendation system** that:
- Understands item-level consumption across bars.
- Predicts future demand using time series models.
- Recommends **"par levels"** (target inventory quantity) to maintain.
- Simulates real-world usage via charts and insights for business decisions.

---

## 🗂️ Project Files

| File | Description |
|------|-------------|
| `time_forecasting_assignment.py` | Main script containing forecasting logic, EDA, visualization, and report generation. |
| `Consumption Dataset - Dataset.csv` | Historical item-wise consumption data across different bar locations. |

---

## 📊 Dataset Overview

The dataset includes the following key columns:

- `Date Time Served`: Timestamp of transaction (converted to datetime).
- `Bar Name`: Location of the bar.
- `Brand Name`: Beverage brand consumed.
- `Consumed (ml)`: Quantity of liquor consumed in milliliters.

---

## 🔍 Methodology

1. **Data Aggregation**
   - Resample consumption data weekly and monthly per bar and brand.
2. **Time Series Forecasting**
   - Apply **ARIMA(1,1,1)** model for each `(Bar Name, Brand Name)` group with >12 weeks of data.
   - Forecast next **4 weeks** of consumption.
3. **Safety Stock Calculation**
   - Safety stock = `z * standard deviation` (Z=1.65 for 95% confidence)
4. **Par Level Recommendation**
   - Par level = `Max(Forecasted Consumption) + Safety Stock`
5. **Visualization**
   - Weekly forecasts
   - Monthly summaries
   - Top 5 consuming brands
   - Suggested par levels per bar
   - Heatmaps for monthly brand-level consumption

---

## 📈 Sample Charts Generated

1. **Top 5 Brands by Monthly Consumption**  
   Bar plot to identify high-demand brands.
2. **Weekly Forecast for Top Brands**  
   Line plots of forecasted consumption over 4 weeks.
3. **Safety Stock vs Max Forecast**  
   Compare buffer vs expected usage.
4. **Suggested Par Levels per Bar**  
   Identify optimal inventory needs by bar location.
5. **Monthly Heatmap of Brand Usage**  
   Temporal consumption patterns across all brands.

---

## 🧮 Key Logic

```python
model = ARIMA(weekly, order=(1,1,1))
model_fit = model.fit()
forecast = model_fit.forecast(steps=4)

safety_stock = z * std_dev  # Z=1.65
par_level = forecast.max() + safety_stock

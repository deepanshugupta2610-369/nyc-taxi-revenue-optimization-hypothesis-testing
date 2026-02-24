# nyc-taxi-revenue-optimization-hypothesis-testing
A Statistical Analysis of Payment Behavior and Fare Pricing


# 🚖 NYC Taxi Revenue Optimization  
## 📊 Statistical Analysis of Payment Behavior & Fare Pricing

---

## 🧠 Executive Summary

In a low-margin mobility business, marginal gains per trip compound into significant revenue impact.

This project analyzes **6.4M+ NYC Taxi trip records** to evaluate whether **payment type (Card vs Cash)** influences:

- 💰 Fare Amount  
- 📏 Trip Distance  
- ⏱ Trip Duration  
- 👤 Passenger Behavior  

Using **EDA, Statistical Cleaning, and Independent T-Test**, the analysis validates the existence of a measurable **“Card Premium”** and translates it into actionable business recommendations.

---

## 🎯 Business Problem

Taxi drivers operate on thin margins. Even small variations in fare per ride materially affect total earnings.

### Key Questions:

1. Is there a statistically significant difference in average fare between Card and Cash users?
2. Can payment behavior be leveraged to maximize driver revenue?

---

## 📂 Dataset Overview

**Source:** NYC Taxi Trip Records  
**Initial Size:** ~6.4 Million Rows  

### Relevant Columns Used:

- `passenger_count`
- `payment_type` (Card / Cash)
- `fare_amount`
- `trip_distance`
- `pickup_datetime`
- `dropoff_datetime`

### 🛠 Feature Engineering

```python
duration = (dropoff_datetime - pickup_datetime).dt.total_seconds() / 60

---

### 🧹 Data Cleaning Pipeline

Large-scale transactional data requires structural filtering.

Steps Performed:

✅ Removed duplicate records (~3.3M rows)

✅ Removed null values

✅ Removed negative fares

✅ Removed zero-distance trips

✅ Outlier handling using IQR method:


#📊 Exploratory Data Analysis (EDA)
## 💳 Payment Share

-Card: 67.5%

-Cash: 32.5%

Digital payments dominate transaction volume.

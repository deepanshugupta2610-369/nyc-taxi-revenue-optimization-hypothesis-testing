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

# 🛠 End-to-End Data Processing Pipeline

---

## 1️⃣ Import Libraries

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from scipy.stats import ttest_ind

### Relevant Columns Used:

- `passenger_count`
- `payment_type` (Card / Cash)
- `fare_amount`
- `trip_distance`
- `pickup_datetime`
- `dropoff_datetime`

##🛠 Feature Engineering

```python
duration = (dropoff_datetime - pickup_datetime).dt.total_seconds() / 60

---

###🧹Data Cleaning Pipeline

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


| Metric        | Card      | Cash      |
| ------------- | --------- | --------- |
| Mean Fare     | $14.50    | $11.00    |
| Mean Distance | 6.8 miles | 3.2 miles |
| Market Share  | 67.5%     | 32.5%     |

##🔎 Behavioral Insight

1. Card users take longer trips

2. Card users generate higher average fares

3. Single-passenger rides account for ~60% of total trips

---

📈 Hypothesis Testing
Null Hypothesis (H₀)

There is no difference in average fare between Card and Cash users.

Alternative Hypothesis (H₁)

There is a statistically significant difference in average fare.


🧪 Statistical Method

Independent Two-Sample T-Test

Unequal variance

Large sample size → CLT assumption satisfied


from scipy.stats import ttest_ind

card_fares = df[df['payment_type'] == 'Card']['fare_amount']
cash_fares = df[df['payment_type'] == 'Cash']['fare_amount']

t_stat, p_value = ttest_ind(card_fares, cash_fares, equal_var=False)

print("T-Statistic:", t_stat)
print("P-Value:", p_value)


📌 Result

T-statistic ≈ 169

P-value < 0.05

✅ Conclusion

Reject H₀.
There is a statistically significant difference in average fare.


💎 The “Card Premium” Effect

The analysis confirms:

💰 Higher average fare per trip for Card users

📏 Longer trip distances for Card users

📊 Higher transaction volume for digital payments

This revenue gap is statistically validated — not random variation.


🚀 Strategic Recommendations
1️⃣ Digital Default Strategy

Set card as default payment option for trips beyond distance thresholds.

2️⃣ Micro-Incentivization

Offer loyalty points or small discounts on high-value card transactions.

3️⃣ Trust & Infrastructure

Deploy visible secure-payment badges & contactless NFC terminals to reduce friction for cash-preferring users.


🛠 Tools & Technologies

| Category        | Stack               |
| --------------- | ------------------- |
| Programming     | Python              |
| Data Analysis   | Pandas              |
| Statistics      | SciPy               |
| Visualization   | Matplotlib, Seaborn |
| Environment     | Jupyter Notebook    |
| Version Control | Git & GitHub        |


📌 What This Project Demonstrates

Handling multi-million row datasets

Structured data cleaning methodology

Robust statistical testing

Translating analytics into business strategy

Revenue optimization thinking

Hypothesis-driven analytical workflow



🔮 Future Scope

📊 Multivariate Regression Modeling

🎯 Propensity Modeling (Payment Behavior)

🧪 A/B Testing Framework

📈 Revenue Uplift Simulation

🤖 Predictive Fare Modeling



👤 Author

Deepanshu Gupta
Data Analyst | Revenue Analytics | Statistical Modeling






# 🚖 NYC Taxi Revenue Optimization  
## 📊 Statistical Analysis of Payment Behavior & Fare Pricing

---

## 📦 Importing Libraries

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from scipy.stats import ttest_ind
```

---

## 📂 Relevant Columns Used

- `passenger_count`
- `payment_type` (Card / Cash)
- `fare_amount`
- `trip_distance`
- `pickup_datetime`
- `dropoff_datetime`

---

## 🛠 Feature Engineering

### ⏱ Derived Feature: Trip Duration (Minutes)

```python
# Convert to datetime
df['pickup_datetime'] = pd.to_datetime(df['pickup_datetime'])
df['dropoff_datetime'] = pd.to_datetime(df['dropoff_datetime'])

# Create duration feature
df['duration'] = (
    df['dropoff_datetime'] - df['pickup_datetime']
).dt.total_seconds() / 60

# Remove invalid durations
df = df[df['duration'] > 0]
```

---

## 🧹 Data Cleaning Pipeline

Large-scale transactional data requires structural filtering.

### Steps Performed:

- ✅ Removed duplicate records (~3.3M rows)
- ✅ Removed null values
- ✅ Removed negative fares
- ✅ Removed zero-distance trips
- ✅ Outlier handling using IQR method

```python
Q1 = df['fare_amount'].quantile(0.25)
Q3 = df['fare_amount'].quantile(0.75)
IQR = Q3 - Q1

lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

df = df[
    (df['fare_amount'] >= lower_bound) & 
    (df['fare_amount'] <= upper_bound)
]
```

---

# 📊 Exploratory Data Analysis (EDA)

## 💳 Payment Share

- **Card:** 67.5%
- **Cash:** 32.5%

Digital payments dominate transaction volume.

---

## 💰 Fare & Distance Comparison

| Metric        | Card      | Cash      |
|--------------|-----------|-----------|
| Mean Fare     | $14.50    | $11.00    |
| Mean Distance | 6.8 miles | 3.2 miles |
| Market Share  | 67.5%     | 32.5%     |

---

## 🔎 Behavioral Insights

1. Card users take longer trips  
2. Card users generate higher average fares  
3. Single-passenger rides account for ~60% of total trips  

---

# 📈 Hypothesis Testing

## Null Hypothesis (H₀)

There is no difference in average fare between Card and Cash users.

## Alternative Hypothesis (H₁)

There is a statistically significant difference in average fare.

---

## 🧪 Statistical Method

1. Independent Two-Sample T-Test  
2. Unequal variance assumption  
3. Large sample size → Central Limit Theorem satisfied  

```python
card_fares = df[df['payment_type'] == 'Card']['fare_amount']
cash_fares = df[df['payment_type'] == 'Cash']['fare_amount']

t_stat, p_value = ttest_ind(card_fares, cash_fares, equal_var=False)

print("T-Statistic:", t_stat)
print("P-Value:", p_value)
```

---

## 📌 Result

- T-statistic ≈ 169  
- P-value < 0.05  

### ✅ Conclusion

Reject H₀.  
There is a statistically significant difference in average fare.

---

# 💎 The “Card Premium” Effect

The analysis confirms:

1. 💰 Higher average fare per trip for Card users  
2. 📏 Longer trip distances for Card users  
3. 📊 Higher transaction volume for digital payments  

This revenue gap is statistically validated — not random variation.

---

# 🚀 Strategic Recommendations

### 1️⃣ Digital Default Strategy
Set card as default payment option for trips beyond distance thresholds.

### 2️⃣ Micro-Incentivization
Offer loyalty points or small discounts on high-value card transactions.

### 3️⃣ Trust & Infrastructure
Deploy visible secure-payment badges & contactless NFC terminals to reduce friction for cash-preferring users.

---

# 🛠 Tools & Technologies

| Category        | Stack               |
|---------------|--------------------|
| Programming     | Python              |
| Data Analysis   | Pandas              |
| Statistics      | SciPy               |
| Visualization   | Matplotlib, Seaborn |
| Environment     | Jupyter Notebook    |
| Version Control | Git & GitHub        |

---

# 📌 What This Project Demonstrates

1. Handling multi-million row datasets  
2. Structured data cleaning methodology  
3. Robust statistical testing  
4. Translating analytics into business strategy  
5. Revenue optimization thinking  
6. Hypothesis-driven analytical workflow  

---

# 🔮 Future Scope

- 📊 Multivariate Regression Modeling  
- 🎯 Propensity Modeling (Payment Behavior)  
- 🧪 A/B Testing Framework  
- 📈 Revenue Uplift Simulation  
- 🤖 Predictive Fare Modeling  

---

# 👤 Author

**Deepanshu Gupta**  
Data Analyst | Revenue Analytics | Statistical Modeling  

---

⭐ If you found this project insightful, consider starring the repository.

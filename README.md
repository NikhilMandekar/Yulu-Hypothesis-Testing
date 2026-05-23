#  Yulu Micro-Mobility - Demand Drivers & Hypothesis Testing

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-8CAAE6?style=flat&logo=scipy&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-4C72B0?style=flat)

---

##  Business Problem

Yulu, India's leading micro-mobility provider, experienced a significant dip in revenues and engaged analysts to identify the key variables that drive demand for shared electric cycles. The goal: determine **which factors significantly predict demand** and how well they explain rental behaviour.

---

##  Dataset

| Column | Description |
|---|---|
| `datetime` | Timestamp of the rental |
| `season` | 1: Spring, 2: Summer, 3: Fall, 4: Winter |
| `holiday` | Whether the day is a public holiday |
| `workingday` | 1 if neither weekend nor holiday |
| `weather` | 1 (Clear) to 4 (Heavy Rain/Snow) |
| `temp` / `atemp` | Actual and perceived temperature (°C) |
| `humidity` / `windspeed` | Environmental conditions |
| `casual` / `registered` | User type breakdown |
| `count` | Total rentals (target variable) |

---

##  Approach

### 1. Exploratory Data Analysis
- Profiled distributions of all continuous variables using Seaborn histplots and boxplots
- Detected and treated outliers using IQR-based capping
- Encoded categorical features (season, weather, working day) and inspected their relationship with rental count
- Observed: rental demand peaks in **Fall (Season 3)** and drops sharply in adverse weather

### 2. Hypothesis Testing (SciPy)

**Test 1 | 2-Sample t-test: Does working day affect rentals?**
- H₀: Mean rentals on working days = Mean rentals on non-working days
- Validated normality (Shapiro-Wilk) and equal variance (Levene's test)
- Result: **Statistically significant difference** (p < 0.05) — working day status does affect demand

**Test 2 | ANOVA: Do seasons and weather drive demand variation?**
- H₀: Mean rentals are equal across all seasons / weather categories
- Result: **Both season and weather show significant variation** (p < 0.05) — fleet allocation should be weather and season-aware

**Test 3 | Chi-Square: Is weather dependent on season?**
- H₀: Weather type and season are independent
- Result: **Significant association found** — weather and season are not independent, informing joint demand-forecasting models

---

##  Key Business Recommendations

1. **Deploy more cycles in Fall** - highest demand season; under-supply directly impacts revenue
2. **Reduce fleet on rainy/stormy days** - demand drops sharply in Weather Type 3–4
3. **Run weekday promotions** - working days see different demand patterns; targeted discounts can smooth utilisation
4. **Optimise zone placement near offices** - working-day demand signals commuter use cases
5. **Pair weather APIs with fleet management** - real-time weather data can automate dynamic rebalancing

---

│   └── yulu_data.csv
└── README.md
```

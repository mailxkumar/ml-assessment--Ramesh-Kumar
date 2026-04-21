# Business Case Analysis

## B1 Problem Formulation

### (B1-a)

Target variable: **items_sold**

Input features:

- store_id
- store_size
- location_type
- promotion_type
- competition_density
- footfall
- demographics
- month / seasonality variables

This is a **supervised regression problem** because the target is continuous numeric output.

---

### (B1-b)

Revenue can fluctuate due to price changes and discounts.

Items sold is a more reliable target because it directly measures promotion effectiveness.

This illustrates the principle that the target variable must align closely with the business objective.

---

### (B1-c)

Instead of one global model, use a **hierarchical or segmented model**.

Example:

- separate models by location type
- store-cluster-based models

This captures regional behavioural differences.

---

## B2 Data and EDA Strategy

### (B2-a)

Join keys:

- transactions ↔ store attributes using store_id
- transactions ↔ promotions using promotion_id
- transactions ↔ calendar using transaction_date

Final grain:
**one row = one store per month**

Aggregations:

- total items sold
- avg basket size
- promotion frequency
- avg footfall

---

### (B2-b)

EDA:

1. Promotion-wise sales boxplot
2. Time series trend chart
3. Correlation heatmap
4. Store-location comparison chart

These help identify seasonality, outliers, and location effects.

---

### (B2-c)

This causes class imbalance.

Mitigation:

- stratified sampling
- weighted loss
- promotion oversampling
- balanced evaluation metrics

---

## B3 Model Evaluation and Deployment

### (B3-a)

Use temporal split:

- first 2.5 years = training
- last 6 months = test

Random split causes data leakage.

Metrics:

- RMSE → penalises large errors
- MAE → average absolute error
- MAPE → percentage error

---

### (B3-b)

Use feature importance / SHAP values.

Explain that December may show seasonal shopping behaviour while March may show price-sensitive behaviour.

---

### (B3-c)

Deployment process:

1. Save model with joblib
2. Load monthly store data
3. Apply same preprocessing pipeline
4. Generate recommendations
5. Monitor prediction drift and error metrics
6. Retrain quarterly if degradation occurs

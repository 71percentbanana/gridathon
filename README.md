# Traffic Demand Prediction Solution

## Overview

This project aims to predict traffic demand using machine learning techniques based on spatial, temporal, weather, and road-related features. A CatBoost Regressor was chosen due to its strong performance on mixed numerical and categorical tabular data.

---

## Data Preprocessing

The following preprocessing steps were applied:

### Missing Value Handling

- **Temperature** → Replaced missing values with the median temperature from the training dataset.
- **RoadType** → Missing values replaced with `"Unknown"`.
- **Weather** → Missing values replaced with `"Unknown"`.

---

## Feature Engineering

### 1. Time-Based Features

The `timestamp` column was split into:

- `hour`
- `minute`

To capture cyclical patterns in traffic flow, cyclic encodings were created:

- `hour_sin`
- `hour_cos`
- `minute_sin`
- `minute_cos`

These transformations allow the model to understand that times such as 23:00 and 00:00 are close to one another.

---

### 2. Categorical Interaction Features

To capture interactions between road conditions and weather patterns, the following combined categorical features were created:

- `RoadType_Lanes`
- `Weather_Road`

These features help the model learn relationships that may not be evident from individual columns alone.

---

### 3. Geospatial Features

The provided geohash values were processed to create multiple location granularities:

- `geohash_4`
- `geohash_5`
- `geohash_6`

Additionally, each geohash was decoded into geographic coordinates:

- `latitude`
- `longitude`

These features allow the model to learn location-specific traffic patterns.

---

## Model

### CatBoost Regressor

The final model used was **CatBoostRegressor**.

Key advantages:

- Native handling of categorical features.
- Strong performance on tabular datasets.
- Reduced preprocessing requirements.
- Built-in regularization to reduce overfitting.

### Training Strategy

- **5-Fold Cross Validation**
- **Early Stopping**
- **RMSE Loss Function**

Cross-validation was used to improve generalization and obtain robust performance estimates.

---

## Libraries Used

- Pandas
- NumPy
- PyGeoHash
- Scikit-Learn
- CatBoost

---

## Files Included

- `Gridlock.ipynb` – Complete training and inference pipeline.
- `README.md` – Solution explanation and methodology.

---


# ecommerce-price-prediction
📊 End-to-end regression project predicting retail prices. Features advanced categorical one-hot encoding (2,300+ features) and a rock-solid 0.93 R² generalization score
# E-Commerce Price Prediction Engine 🚀

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Latest-orange.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

An end-to-end machine learning regression project designed to predict retail sales prices using a robust **RandomForestRegressor**. This model handles highly sparse data matrices and achieves a strong **0.93 $R^2$ score**, demonstrating a reliable ability to generalize on unseen retail data.

---

## 📊 Business & Technical Impact
In e-commerce, algorithmic pricing directly influences conversion rates and profit margins. This project simulates an enterprise-level pipeline by:
* **Feature Scale:** Dynamically processing **2,384 distinct dimensions** generated via high-cardinality categorical variables.
* **Reliability:** Validating performance limits using a **5-Fold Cross-Validation** strategy to ensure predictions remain stable across varying market subsets.
* **Predictive Power:** Reaching a final baseline cross-validation score of **0.93 $R^2$**, drastically reducing price variance errors.

---

## 🛠️ Data Pipeline & Engineering Decisions

### 1. Data Sanitization
* The raw retail dataset (`Book1.xlsx`) originally contained **27,555 records**. 
* Implemented strict row-wise truncation on missing variables to ensure high-fidelity feature arrays, retaining a clean modeling footprint of **18,928 rows**.

### 2. High-Cardinality Feature Engineering
* **Features Used:** `market_price`, `rating`, `category`, `sub_category`, `brand`, and `type`.
* **Challenge:** Categorical dimensions spanned thousands of unique entities (e.g., granular brands and explicit product types).
* **Solution:** Built an isolated `ColumnTransformer` preprocessing pipeline utilizing an optimized `OneHotEncoder(handle_unknown='ignore')`. This explicitly transformed columns into uniform string variables, safely expanding the dimensional workspace from 6 base inputs into **2,384 sparse features**.

---

## 📈 Model Performance & Validation Results

The core architecture uses a tuned **RandomForestRegressor** evaluated via a **5-Fold Cross-Validation** strategy to guarantee resilience against data leakage and overfitting.

### Cross-Validation Metrics:
* **Fold 1:** MAE = 28.13 | $R^2$ = 0.93
* **Fold 2:** MAE = 28.87 | $R^2$ = 0.95
* **Fold 3:** MAE = 26.13 | $R^2$ = 0.94
* **Fold 4:** MAE = 30.11 | $R^2$ = 0.92
* **Fold 5:** MAE = 27.99 | $R^2$ = 0.93

### Performance Summary:
* **Average Mean Absolute Error (MAE):** `28.25` ($\pm$ 1.30 variance)
* **Average R-squared ($R^2$ Score):** `0.93` ($\pm$ 0.01 variance)

### 🔍 Overfitting Diagnostic
To evaluate structural generalization, a final validation check was performed on an isolated 80/20 train-test split:
* **Training $R^2$:** `0.99`  |  **Validation $R^2$:** `0.93`
* **Training MAE:** `10.67` |  **Validation MAE:** `28.00`

*Insight:* While the tree model learns deep structures within the training partition ($R^2 = 0.99$), the tight bounds of the Validation $R^2$ ($0.93$) confirm the engine retains exceptional predictive stability on completely novel datasets.

---

## 📦 Project Architecture
```text
├── .gitignore               # Automated exclusions for Python/Jupyter caching
├── LICENSE                  # Permissive open-source MIT License 
├── README.md                # Interactive documentation & business insights
├── Book1.xlsx               # Raw e-commerce sales dataset
└── Untitled0.ipynb          # End-to-end Jupyter Notebook pipeline

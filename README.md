# miniproject_2
### 1. Business Understanding and Goal Definition

* **Core Goal:** Predict whether a customer will be a "No-Show" (target variable: `no_show`) to help the hotel group formulate targeted policies (e.g., overbooking strategies, deposit requirements, cancellation reminders) and minimize economic losses.
* **Evaluation Metrics:**
* Accuracy alone is insufficient due to class imbalance.
* **Primary focus:** **F1-Score** or **ROC-AUC**. We must balance **Precision** and **Recall**.
* *Business Rationale:* Low Precision (misclassifying a guest as a No-Show) may lead to overbooking and guest complaints. Low Recall (missing an actual No-Show) leads to unrecoverable economic loss.

### 2. Exploratory Data Analysis (EDA)

The dataset contains 119,391 records across 15 columns. Key areas for exploration include:

* **Target Variable Distribution:** Statistically check the ratio of `0.0` vs `1.0` in `no_show` to identify class imbalance.
* **Missing Values:** Analyze the percentage of missing data in columns like `price`.
* **Feature Correlation Analysis:**
* **Temporal Dimension:** The "Lead Time" (difference between `booking_month` and `arrival_month`) significantly impacts No-Show rates.
* **Channels and Pricing:** Analyze relationships between `platform` (e.g., Website, Agent), `room` types, `price`, and the target.
* **Demographics/Loyalty:** Analyze the distribution based on `country` and whether the guest is a first-time visitor (`first_time`).

### 3. Data Preprocessing & Feature Engineering

This is critical for model success:

* **Data Cleaning:**
* Normalize `price` (e.g., convert `SGD$ 492.98`, `USD$ 665.37` to a single currency numerical format) and impute `NaN` values.
* Handle minor missing values (e.g., in `num_children`).

* **Feature Engineering:**
* Calculate `Lead Time` (span between booking and arrival).
* Calculate `Total Guests`: `num_adults` + `num_children`.

* **Feature Encoding:**
* Apply One-Hot Encoding or Target Encoding for categorical variables (`branch`, `platform`, `room`, `country`, `first_time`).


* **Data Splitting:** Split into Training and Testing sets (80/20 or 70/30). If necessary, use techniques like `SMOTE` to address class imbalance.

### 4. Model Training & Evaluation (At least 3 models)

To meet project requirements, use three models with different underlying principles:

* **Model A: Logistic Regression**
* *Rationale:* Serves as a baseline; fast computation and high interpretability.


* **Model B: Random Forest**
* *Rationale:* Ensemble learning algorithm; handles non-linear relationships well, is resistant to overfitting, and robust against missing values.


* **Model C: LightGBM or XGBoost**
* *Rationale:* Gradient Boosting Decision Tree (GBDT) based; provides excellent performance on large-scale tabular data, high speed, and accuracy.

### 5. Model Comparison & Comprehensive Evaluation

* **Quantitative Comparison Table:**
Create a table comparing Accuracy, Precision, Recall, F1-Score, ROC-AUC, and training time across the three models.
* **Visual Comparison:** Plot the **ROC Curve** and **PR Curve** to observe the Area Under the Curve (AUC).
* **Business Decisions & Model Selection:**
* Don't just pick the highest score. If LightGBM and Random Forest scores are comparable, consider LightGBM's efficiency, lower memory footprint, and suitability for real-world deployment.
* Justify the selection: (e.g., "LightGBM achieved the highest F1-Score, effectively balancing the prevention of guest complaints due to overbooking with the minimization of No-Show losses.")

### 6. Business Insights & Policy Formulation

* **Feature Importance Analysis:** Identify the top 5 core features (e.g., "Bookings made via Agent with a Lead Time > 3 months have the highest No-Show risk").
* **Policy Recommendations:**
* Implement "Non-refundable" rates or mandatory deposits for high-risk bookings.
* Trigger automated SMS/Email check-in reminders 3 days before arrival.
* Dynamically adjust the hotel's Overbooking Limit based on the predicted probability of No-Show.

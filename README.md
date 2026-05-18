UPI Transaction Anomaly Detection
Abstract
This project applies machine learning to detect anomalous monthly growth in Unified Payments Interface (UPI) transaction volumes in India. Using six years of monthly UPI data (2020–2026), features such as lagged volumes, rolling statistics, and temporal indicators (month, quarter) are engineered. Four supervised classifiers (Logistic Regression, Random Forest, Gradient Boosting, XGBoost) and two unsupervised methods (Isolation Forest, One‑Class SVM) are trained to classify each month as negative growth (‑1), normal growth (0), or positive growth (1). Time series cross‑validation and PCA are used for robust evaluation. STL decomposition provides an additional baseline.

Objective
To build a multi‑class anomaly detection system for UPI transaction volume growth.

To compare the effectiveness of traditional machine learning models vs. unsupervised anomaly detectors on time‑series financial data.

To evaluate models using macro F1‑score, accuracy, and time‑series cross‑validation.

How It Is Different
Multi‑class anomaly labeling: Instead of binary (normal/anomaly), three classes capture both negative and positive extreme growth.

Temporal feature engineering: Uses lag features (1,2,3 months), rolling mean/std (3‑month window), and calendar features (month, quarter) to capture seasonality and momentum.

Time series cross‑validation: Walk‑forward validation (5 splits) respects temporal order, avoiding look‑ahead bias.

STL decomposition baseline: Compares model performance against a statistical decomposition method (seasonal‑trend decomposition using LOESS) to identify residual outliers.

Full pipeline: Includes imputation, scaling, PCA dimensionality reduction, and visualisation of explained variance and 2D projections.

Results
Test set performance (last 15 months):

Model	Macro F1	Accuracy
Logistic Regression	0.60	0.60
Random Forest	0.55	0.60
Gradient Boosting	0.58	0.60
XGBoost	0.63	0.67
Isolation Forest (binary)	0.42	0.73*
One‑Class SVM (binary)	0.42	0.73*
*Unsupervised models evaluated on binary anomaly (any extreme growth).

Time Series Cross‑Validation (XGBoost):

Fold 1 Macro F1: 0.410

Fold 2: 0.296

Fold 3: 0.489

Fold 4: 0.250

Fold 5: 0.667

Average Macro F1: 0.422

PCA analysis: 3 principal components retained 95% of variance, but PCA‑reduced features degraded XGBoost macro F1 to 0.40, suggesting original features are more informative.

Conclusion:
XGBoost outperforms other supervised models on the multi‑class task, achieving the highest macro F1 (0.63) and accuracy (0.67). The low cross‑validation average (0.422) indicates overfitting or limited data for monthly predictions. Unsupervised methods (IF, OCSVM) achieve high accuracy (0.73) on binary anomaly but much lower macro F1, meaning they are biased toward the majority “normal” class. Further work could incorporate more granular (daily/weekly) data or exogenous economic indicators.
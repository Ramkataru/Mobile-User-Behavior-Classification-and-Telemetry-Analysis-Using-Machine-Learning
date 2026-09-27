# Mobile User Behavior Classification and Telemetry Analysis Using Machine Learning

---

## Project Metadata

* **Author:** Ram


* **USN:** 23BTRCO044


* **Department:** Computer Science & Engineering (Internet of Things)


* **Course:** Laboratory Experiment and GitHub Submission


* **Instructor:** Dr. N. Vikram



---

## Abstract

Modern mobile smartphones generate granular behavioral telemetry, including daily application usage durations, screen-on time, battery discharge rates, mobile data consumption, and installed app counts. This project implements an end-to-end machine learning pipeline to classify mobile device users into distinct behavioral categories (ranging from light to extreme usage intensity) based on telemetry indicators and demographic variables.

By benchmarking classical decision trees against ensemble architectures (Random Forest, Extra Trees, and Gradient Boosting), this study evaluates model precision and identifies key feature hierarchies driving resource consumption.

---

## Problem Statement & Objectives

Mobile telemetry analytics provides foundational insights for user segmentation, targeted operating system optimization, dynamic power management, and personalized resource allocation. The core objectives of this study are:

1. **Telemetry Preprocessing:** Standardize tabular telemetry features and encode categorical hardware/demographic attributes.


2. **Behavioral Classification:** Train and evaluate supervised classification models to predict target user behavior classes.


3. **Feature Importance Ranking:** Quantify feature contributions to identify primary drivers of battery drain and mobile data usage.


4. **Literature Benchmarking:** Compare empirical classification performance against contextual usage prediction benchmarks established in mobile computing literature.



---

## Dataset Schema

The experiment utilizes `expanded_user_behavior_dataset.csv`, comprising **1,000 user instances** structured across **11 attributes**.

| Field Name | Data Type | Units / Range | Description |
| --- | --- | --- | --- |
| `User ID` | Integer | Identifier | Unique user record index

 |
| `Device Model` | Categorical | String | Mobile hardware model (e.g., Google Pixel 5, OnePlus 9)

 |
| `Operating System` | Categorical | `Android` / `iOS` | Mobile operating system platform

 |
| `App Usage Time (min/day)` | Integer | minutes/day | Average active app usage time per day

 |
| `Screen On Time (hours/day)` | Float | hours/day | Average daily active screen duration

 |
| `Battery Drain (mAh/day)` | Integer | mAh/day | Average daily battery capacity consumed

 |
| `Number of Apps Installed` | Integer | Count | Total installed applications

 |
| `Data Usage (MB/day)` | Integer | MB/day | Average daily cellular and Wi-Fi data consumed

 |
| `Age` | Integer | Years | User demographic age

 |
| `Gender` | Categorical | `Male` / `Female` | User demographic gender

 |
| **`User Behavior Class`** | **Integer** | **1 to 5** | **Target label indicating user behavior intensity class**<br> |

---

## Methodology & Machine Learning Architecture

```
 Raw Telemetry Data ➔ Data Preprocessing ➔ Stratified Splitting ➔ Model Training ➔ Feature Importance Analysis
 (1000 Rows x 11 Cols)  (Label Encoding/Scaling)  (80/20 Train-Test)   (Tree Ensembles)  (Gini / Permutation)

```

1. **Preprocessing & Encoding:**
* Dropped non-predictive `User ID` values.


* Applied `LabelEncoder` transformation to categorical variables (`Device Model`, `Operating System`, `Gender`).


* Normalized continuous numerical features using `StandardScaler`.


2. **Data Partitioning:**
* Stratified 80/20 Train-Test split maintaining target class proportions.


* 5-Fold Stratified Cross-Validation applied during training to evaluate stability across folds.




3. **Evaluated Algorithms:**
* **Decision Tree Classifier** (Baseline interpretability model)


* **Random Forest Classifier** (Bagging ensemble)


* **Extra Trees Classifier** (Extremely randomized trees ensemble)
* **Gradient Boosting Classifier** (Boosting ensemble)



---

## Experimental Results

| Model Architecture | 5-Fold CV Accuracy | Test Accuracy | Precision (Weighted) | Recall (Weighted) | F1-Score (Weighted) |
| --- | --- | --- | --- | --- | --- |
| **Decision Tree**<br> | 98.88% | 99.00% | 0.9902 | 0.9900 | 0.9900 |
| **Random Forest**<br> | **100.00%** | **100.00%** | **1.0000** | **1.0000** | **1.0000** |
| **Extra Trees** | **100.00%** | **100.00%** | **1.0000** | **1.0000** | **1.0000** |
| **Gradient Boosting** | **100.00%** | **100.00%** | **1.0000** | **1.0000** | **1.0000** |

---

## Key Analytical Insights

1. **Ensemble Performance:** Consistent with findings in mobile telemetry literature (Sarker et al.), tree-based ensemble classifiers demonstrate superior accuracy when predicting user behavior classes from aggregate tabular logs.


2. **Primary Predictive Drivers:** Feature importance evaluations confirm that active behavioral metrics—specifically **App Usage Time**, **Screen On Time**, **Battery Drain**, and **Data Usage**—serve as the strongest drivers of user behavioral intensity classification.


3. **Demographic Influence:** Demographic variables (`Age` and `Gender`) exhibit lower feature importance weights compared to active usage telemetry, indicating that behavior classification is predominantly driven by device usage intensity.



---

## Repository File Organization

```text
├── expanded_user_behavior_dataset.csv  # Raw input telemetry dataset (1000 records)
├── Mobile_User_Behavior_Analysis.ipynb # Google Colab Jupyter Notebook
├── Literature_Review.pdf              # Academic survey and literature review
├── discription.pdf                    # Dataset specification document
├── experiment_results_predictions.csv # Model test predictions export
└── README.md                          # Project documentation

```

---

## How to Run in Google Colab

1. **Clone Repository:**
```bash
git clone https://github.com/YOUR_USERNAME/mobile-user-behavior-classification.git

```


2. **Open Notebook:**
* Open [Google Colab](https://colab.research.google.com/?utm_source=gemini).
* Select **Upload** and select `Mobile_User_Behavior_Analysis.ipynb`.




3. **Load Data & Execute:**
* Upload `expanded_user_behavior_dataset.csv` into the runtime file session.


* Select **Runtime > Run all** to execute preprocessing, model training, cross-validation, and plot generation.



---

## References

1. Sarker, I. H. et al. "ContextPCA: Predicting Context-Aware Smartphone Apps Usage Based on Machine Learning Techniques." *Symmetry*, 12(4), 2020.


2. Sarker, I. H. et al. "Effectiveness Analysis of Machine Learning Classification Models for Predicting Personalized Context-Aware Smartphone Usage." *Journal of Big Data*, 2019.


3. Khorasani, V. "Mobile Device Usage and User Behavior Dataset." *Kaggle*, 2024.

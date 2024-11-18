# Cybersecurity Incident Detection with Machine Learning
## Enhancing Security Operations with Predictive Analytics

### Overview
In today’s fast-evolving cybersecurity landscape, Security Operations Centers (SOCs) are inundated with an overwhelming number of alerts and incidents. This project seeks to address this challenge by leveraging machine learning models to predict and classify cybersecurity incidents, aiding SOC analysts in making more informed decisions and responding to threats faster and more effectively. By using Microsoft’s innovative GUIDE dataset, this work lays the foundation for creating intelligent, automated systems that can help secure enterprise environments from emerging threats.

### Problem Statement
The main objective of this project is to build a machine learning model capable of predicting the triage grade of cybersecurity incidents, helping SOC analysts focus on the most critical threats. The model, trained on the GUIDE dataset, classifies incidents as True Positive (TP), Benign Positive (BP), or False Positive (FP) based on past data and customer feedback. This classification supports guided response systems, assisting analysts with actionable insights for incident management and mitigation.

### Key Use Cases
This project offers valuable solutions across various business functions in the realm of cybersecurity:

- **Automating Incident Triage in SOCs**: By classifying and prioritizing cybersecurity incidents, SOC analysts can streamline response efforts and handle high-priority threats more efficiently.
- **Guided Incident Response**: The model enables automated systems to suggest actions for different types of incidents, accelerating threat resolution.
- **Enhanced Threat Intelligence**: Incorporating historical data, alerts, and customer responses into threat detection results in more accurate identification of malicious activities.
- **Optimizing Enterprise Security**: By reducing false positives, enterprises can ensure that genuine threats are promptly mitigated, improving overall system security.

### Dataset
The dataset used for this project, **GUIDE**, is one of the largest of its kind, providing rich, structured data on cybersecurity incidents:

- **Size & Structure**: It contains over 13 million pieces of evidence, spread across 1 million+ annotated incidents.
- **Incident Types**: Evidence is organized into three hierarchical levels: Evidence (raw data), Alert (aggregated data points), and Incident (comprehensive records of alerts).
- **Security Context**: The dataset features telemetry data from over 6,100 organizations and covers 441 MITRE ATT&CK techniques.
- **Training & Testing Split**: The dataset is divided into a training set (70%) and a test set (30%), ensuring robust evaluation of model performance.

### Data Privacy and Anonymization
Given the sensitivity of cybersecurity data, the GUIDE dataset has undergone rigorous privacy protection processes, including:

- **Pseudo-anonymization**: Hashing sensitive identifiers with SHA1 to preserve privacy while maintaining data integrity.
- **Random ID Replacement**: Substituting original IDs with random IDs to protect anonymity.
- **Temporal Noise**: Modifying timestamps to prevent re-identification of individuals or organizations.

### Metrics for Success
To evaluate the effectiveness of the machine learning models, we use the following metrics:

- **Primary Metric**: Macro-F1 score for accurate triage grade prediction.
- **Secondary Metrics**: Precision and recall for assessing the accuracy of proposed remediation actions.

# Approach

This project focuses on preprocessing and exploratory data analysis (EDA) for both training and testing datasets, followed by model training, evaluation, and testing on a large-scale dataset. Below is the step-by-step breakdown:

---

## Step 1: Preprocessing and EDA for Train and Test Datasets

### 1. Preprocessing:
- Imported necessary libraries and modules.
- Read the train dataset and conducted an initial inspection.
- **Data Cleaning**:
  - Dropped duplicate rows.
  - Dropped rows with 50% or more null values.
  - Removed remaining null values.
- **Feature Engineering**:
  - Extracted `Day`, `Month`, and `Hour` from the `Timestamp` column.

### 2. Exploratory Data Analysis (EDA):
- Visualized distributions and patterns using:
  - Count plot for target column classes.
  - Bar plots for `IncidentGrade` counts by:
    - Category
    - EntityType
    - Evidence
    - Day of the month
    - Month
    - Hour of the day
- Generated a **correlation heatmap** for all numerical columns.
  - Dropped one of two highly correlated columns (≥ 80%) to reduce redundancy and multicollinearity.
- Applied **Label Encoding** for categorical columns.
  - Opted for label encoding instead of one-hot encoding due to the high number of categories.
- Saved the cleaned and processed train dataset.

### 3. Test Dataset:
- Repeated the above preprocessing and EDA steps for the test dataset.

---

## Step 2: Model Training and Testing

### 1. Data Preparation:
- Imported necessary libraries and loaded the preprocessed train dataset.
- Selected the top 15 features using ANOVA feature selection.

### 2. Model Training:
- Trained four models using stratified sampling on the full dataset with 9.8 million rows:
  - Logistic Regression
  - Decision Tree
  - Random Forest
  - XGBoost
- **Observations**:
  - **Random Forest** and **Decision Tree** showed superior performance.
  - Due to the dataset's size, stratified sampling was applied to create a balanced subset of 500,000 rows per class for efficient processing.

### 3. Cross-Validation and Hyperparameter Tuning:
- Applied **cross-validation** for robust evaluation.
- Used **RandomizedSearchCV** for hyperparameter tuning of Decision Tree and Random Forest models.

### 4. Feature Importance Analysis:
- Analyzed feature importance using model-specific measures (e.g., feature importance in Random Forest).

### 5. Error Analysis:
- Identified and analyzed misclassifications for Decision Tree and Random Forest models.

### 6. Final Evaluation:
- Evaluated models on the **test dataset** using key metrics:
  - Accuracy
  - Precision
  - Recall
  - F1-Score
  - Confusion Matrix


# AI-ML-DS-Salary-Analysis-2025
An in-depth analysis of AI/ML/Data Science job market and salary trends for 2024-2030.

# AI Job Market & Salary Trend Analysis 2024-2030

## Table of Contents
- [1. Overview](#1-overview)
- [2. Data Source](#2-data-source)
- [3. Methodology](#3-methodology)
    - [3.1 Data Cleaning & Preprocessing](#31-data-cleaning--preprocessing)
    - [3.2 Exploratory Data Analysis (EDA)](#32-exploratory-data-analysis-eda)
    - [3.3 Model Selection & Training](#33-model-selection--training)
    - [3.4 Model Evaluation](#34-model-evaluation)
- [4. Key Findings & Actionable Insights](#4-key-findings--actionable-insights)
- [5. Tools Used](#5-tools-used)
- [6. Future Work (Optional)](#6-future-work-optional)
- [7. Contact Information](#7-contact-information)

---

## 1. Overview

The rapid advancement of Artificial Intelligence (AI) and Machine Learning (ML) is profoundly reshaping the global job market, leading to a dynamic landscape where understanding salary trends and key influencing factors is crucial. This project aims to provide data-driven insights for aspiring AI/ML/Data Science (DS) professionals to guide their career paths, for companies to optimize their talent acquisition strategies, and for recruiters to benchmark compensation effectively.

My primary goal was to build a robust predictive model for AI/ML/DS job salaries using recent 2024-2030 data and, more importantly, to identify the most significant features driving these compensation trends.

## 2. Data Source

The dataset used for this analysis is **'Data Science, AI & ML Job Salaries in 2025'**, publicly available on Kaggle. This dataset provides current and projected salary information across various AI/ML/DS roles, experience levels, company types, and geographical locations.

* **Link to Dataset:** [Data Science, AI & ML Job Salaries in 2025](https://www.kaggle.com/datasets/adilshamim/data-science-ai-ml-job-salaries-in-2025)

## 3. Methodology

My analytical approach followed a structured machine learning pipeline:

### 3.1 Data Cleaning & Preprocessing

The raw data underwent thorough cleaning and preparation.
* **Duplicate Handling:** Identified and removed duplicate entries (approximately **[YOUR_DUPLICATE_COUNT_HERE]** rows) to ensure the uniqueness and integrity of each job record.
* **Missing Values:** Confirmed that the dataset had **no significant missing values**, streamlining the data imputation phase.
* **Data Leakage Correction:** A critical step involved identifying and addressing **data leakage**. The original `salary` column (which stored salary in local currency) was found to be a direct, un-normalized precursor to the `salary_in_usd` target variable. To build a truly predictive model based on independent factors, the `salary` column was **explicitly removed from the feature set** before model training. This ensures the derived feature importances genuinely reflect causal relationships rather than data redundancy.
* **Feature Encoding:** Categorical features such as `job_title`, `employment_type`, `employee_residence`, and `company_location` were transformed using **One-Hot Encoding**. Ordinal features like `experience_level` and `company_size` were converted using **Ordinal Encoding** to preserve their inherent order. Numerical features like `work_year` and `remote_ratio` were used directly.

### 3.2 Exploratory Data Analysis (EDA)

Extensive Exploratory Data Analysis (EDA) was performed to uncover initial patterns and characteristics of the job market data. Key observations included:

* **Salary Distribution:** The overall distribution of salaries was **right-skewed**, indicating a concentration of jobs at lower to mid-salary ranges, with a long tail extending towards very high compensation for specialized roles.
    ![Salary Distribution](plots/[Salary_Distribution_PLOT_FILENAME].png)
* **Experience Level Impact:** A **clear and consistent positive correlation** was observed between experience level and salary, with median salaries significantly increasing from Entry-level to Executive-level positions.
    ![Salary by Experience Level](plots/[YOUR_SALARY_BY_EXPERIENCE_PLOT_FILENAME].png)
* **Geographical Variations:** Analysis showed substantial differences in average salaries across various company locations, reflecting regional economic factors and talent demand. For instance, countries like the United States typically command higher average salaries.
    ![Average Salary by Top 10 Company Locations](plots/[YOUR_SALARY_BY_LOCATION_PLOT_FILENAME].png)
* **Job Title Specificity:** While overall trends were evident, specific job titles demonstrated distinct average salary ranges, highlighting the value of specialization within the AI/ML/DS domain.

### 3.3 Model Selection & Training

This project tackled a **regression problem**, aiming to predict a continuous numerical value (`salary_in_usd`).
* **Data Split:** The cleaned data was split into training (80%) and testing (20%) sets to ensure robust model evaluation on unseen data.
* **Models Explored:** I experimented with several machine learning models:
    * **Linear Regression:** Served as a baseline to understand the inherent linearity of relationships.
    * **Random Forest Regressor:** An ensemble tree-based model known for its robustness.
    * **LightGBM Regressor:** A highly efficient gradient boosting framework, often delivering state-of-the-art performance on tabular data.
* **Final Model Selection:** **LightGBM Regressor** was chosen as the primary model for final analysis due to its superior performance and efficiency compared to Linear Regression and Random Forest.

### 3.4 Model Evaluation

The performance of the re-modeled LightGBM Regressor (after addressing data leakage) was evaluated using standard regression metrics on the test set:

* **Mean Absolute Error (MAE):** **$[YOUR\_MAE\_VALUE]$** (e.g., $24,875.50)
* **Mean Squared Error (MSE):** **$[YOUR\_MSE\_VALUE]$** (e.g., $1,540,123,456.78)
* **Root Mean Squared Error (RMSE):** **$[YOUR\_RMSE\_VALUE]$** (e.g., $39,244.30)
* **R-squared (R2):** **$[YOUR\_R2\_VALUE]$** (e.g., 0.7456)

**Interpretation:** An R-squared value of approximately **[YOUR_R2_VALUE]** indicates that the model can explain about **[YOUR_R2_PERCENTAGE_HERE]%** of the variance in salaries based on the independent features. While this is lower than the initial R-squared (which benefited from data leakage), it represents a **realistic and strong predictive capability** for a complex human-centric variable like compensation. The MAE signifies that, on average, the model's salary predictions are off by roughly **$[YOUR\_MAE\_VALUE]$**.

![Actual vs. Predicted Salaries (Re-modeled LightGBM Regressor)](plots/[YOUR_ACTUAL_VS_PREDICTED_PLOT_FILENAME].png)

## 4. Key Findings & Actionable Insights

The feature importance analysis from the re-modeled LightGBM Regressor provided crucial insights into the factors that genuinely drive salaries in the AI/ML/DS job market:

![Top 20 Feature Importances for Salary Prediction (Re-modeled LightGBM)](plots/[YOUR_FEATURE_IMPORTANCE_PLOT_FILENAME].png)

The most significant drivers of salary, in order of importance, were identified as:

1.  **Experience Level (`ord_experience_level`):** This is by far the most influential factor. As individuals progress from Entry-level to Mid, Senior, and Executive roles, their salary potential increases dramatically. This underscores the premium placed on accumulated expertise and leadership in the field.
2.  **Work Year (`num_work_year`):** The year of the job posting strongly impacts salary. This reflects the dynamic and rapidly growing nature of the AI/ML/DS market, where compensation generally trends upwards over time due to increasing demand and evolving skill sets.
3.  **Employee Residence (`cat_employee_residence_US`):** Whether the employee is based in the United States is a highly significant predictor. The US market, characterized by high demand for tech talent and a higher cost of living, typically offers substantially higher salaries compared to many other regions globally.
4.  **Remote Ratio (`num_remote_ratio`):** The extent of remote work (fully on-site, hybrid, or fully remote) also plays a notable role in salary determination, reflecting evolving work models and talent acquisition strategies.
5.  **Job Title Specificity (`cat_job_title_...`):** While broader factors dominate, specific job titles like 'Machine Learning Engineer', 'Research Scientist', 'Data Engineer', and 'Engineering Manager' are important contributors, indicating the value of specialized technical and leadership roles within the domain.
6.  **Company Location (`cat_company_location_...`):** Beyond employee residence, the company's geographical location also influences salary, often correlating with economic hubs and industry concentration.

**Actionable Recommendations:**

* **For Job Seekers:** Prioritize gaining diverse experience to advance through experience levels. Stay updated with the latest industry trends. Strategically consider job opportunities in high-paying geographical markets like the US, or remote roles offered by companies based in such regions. Specializing in high-demand technical roles (e.g., ML Engineering, Research) can lead to higher compensation.
* **For Companies & Recruiters:** Benchmark compensation effectively by considering not just job title, but critically, the candidate's experience level and geographical location. Acknowledge the market value of remote talent and the competitive nature of the AI/ML/DS job market, especially in rapidly evolving roles.

## 5. Tools Used

* `Python`
* `Pandas` (for data manipulation and analysis)
* `NumPy` (for numerical operations)
* `Scikit-learn` (for data preprocessing, model selection, and evaluation)
* `LightGBM` (for gradient boosting regression model)
* `Matplotlib` & `Seaborn` (for data visualization and plotting)

## 6. Future Work (Optional)

* **Skill-Based Analysis:** Incorporate data on specific technical skills (e.g., Python, SQL, cloud platforms, specific ML frameworks) if such granular data becomes available, to analyze their individual impact on salary.
* **Interaction Effects:** Explore more complex feature engineering, such as interaction terms between highly important features (e.g., how remote ratio affects salaries at different experience levels).
* **Geospatial Analysis:** Conduct a deeper dive into salary variations within countries or specific cities, if more localized data can be sourced.
* **Model Deployment:** Develop a simple web application (e.g., using Flask/Streamlit) to allow users to input their profile details and receive a predicted salary range.

## 7. Contact Information

* **Naveen Lakshman Kumar Basina**
* **LinkedIn:** [https://www.linkedin.com/in/naveen-lakshman/](https://www.linkedin.com/in/naveen-lakshman/)
* **Email:** [naveenklaxman22@gmail.com](mailto:naveenklaxman22@gmail.com)

---

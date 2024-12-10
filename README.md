# LinkedIn Job Posting Views Prediction

## Overview
This project addresses a critical challenge for employers using LinkedIn: **maximizing job post visibility**. With thousands of posts uploaded daily, companies need insights to ensure their listings attract top talent. Using the **LinkedIn Job Postings (2023–2024)** dataset, we developed a **predictive model** to estimate the number of views a job posting will receive and identify key factors driving visibility.

---

## Business Problem
- **Challenge**: Employers struggle to make their job postings stand out in a highly competitive online market.
- **Key Metric**: Views per posting are a critical indicator of reach and engagement.
- **Goal**: Build a predictive model to estimate job post views and identify actionable strategies to enhance visibility and engagement.

---

## Dataset
### Source
- **Dataset**: LinkedIn Job Postings (2023–2024) from Kaggle.
- **Size**: 124,000+ job postings.
- **Features**:
  - **Job Attributes**: Title, description, salary, location, work type, remote allowance, skills, benefits.
  - **Company Attributes**: Size, industry, follower count, location.
  - **Engagement Metrics**: Views and applications.

### Why This Dataset?
- Reflects real-time trends in the job market.
- Highly relevant for soon-to-graduate students navigating the job search process.

---

## Data Preparation
### Key Steps
1. **Data Ingestion**:
   - Loaded multiple CSV files into Databricks.
   - Converted PySpark DataFrames to Pandas for easier manipulation.

2. **Data Cleaning**:
   - Standardized text columns.
   - Addressed missing values in key fields (e.g., job descriptions, skills).
   - Handled duplicates and outliers (e.g., views, salary).

3. **Feature Engineering**:
   - Aggregated benefits and skills into interpretable formats.
   - One-hot encoded categorical variables.
   - Engineered new features like `num_benefits` and principal components using PCA.

4. **Final Dataset**:
   - Created two modeling datasets:
     - **Views Dataset**: Focused on predicting views.
     - **Salary Dataset**: Focused on normalized salary predictions.

---

## Exploratory Data Analysis (EDA)
### Key Insights
- **Skewed View Distribution**: Most job postings receive fewer than 500 views, with a small percentage exceeding 50,000.
- **Engagement Correlations**:
  - **Views ↔ Applications**: Strong positive correlation.
  - **Follower Count ↔ Views**: Higher company follower counts correlate with more views.
- **Feature Trends**:
  - Remote jobs consistently outperform on-site jobs in terms of views.
  - Job posts that list a salary receive more views.

### Visualizations
1. **View Distribution**: Highlighted skewness in view counts.
2. **Feature Relationships**: Bar plots showing average views by remote status, salary listing, and industry.

---

## Model Development
### Tools
- **Databricks AutoML**: Automated experimentation with various algorithms.
- **Modeling Pipeline**:
  - Handled multicollinearity with Variance Inflation Factor (VIF).
  - Integrated PCA to capture variance efficiently.
  - Selected a subset of columns for feature engineering.

### Best Models
- **SGD Regressor** (MAE): Most robust for view predictions.
- **XGBoost Regressor** (R²): Performed well for goodness-of-fit metrics.

### Evaluation Metrics
- **MAE**: Measures average absolute prediction error.
- **R²**: Captures the proportion of variance explained by the model.

---

## Deployment
### Strategy
- **Batch Deployment**: Provides predictions for multiple job postings at once, suitable for employers posting jobs in bulk.
- **Implementation**: Deployed the best-performing model using Databricks' model registry.

---

## Model Monitoring
### Tools
- **EvidentlyAI**:
  - **Data Drift Monitoring**: Tracks shifts in feature distributions over time.
  - **Regression Performance**: Monitors MAE for new data against the training dataset.

---

## Results
1. **Predictive Insights**:
   - Accurately predicts the number of views per job posting.
   - Provides employers with actionable strategies to improve visibility.
2. **Feature Importance**:
   - Key drivers include salary listing, remote work options, and company follower count.
3. **Business Value**:
   - Enables companies to optimize job posts and improve engagement.
   - Offers insights for platforms like LinkedIn to enhance recommendation systems.

---

## Next Steps
1. Integrate the model into a user-facing application.
2. Explore real-time predictions for dynamic job posting optimization.
3. Enhance feature engineering to capture seasonality and temporal trends.

---

## Contributors
- [Your Name]
- [Team Member Name]

Feel free to reach out with questions or suggestions!

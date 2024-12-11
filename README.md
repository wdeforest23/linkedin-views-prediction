# LinkedIn Job Posting Views Prediction

![Title Slide](images/ML%20Ops%20Final%20Presentation%20Draft.jpg)

## Overview
This project addresses a critical challenge for employers using LinkedIn: **maximizing job post visibility**. With thousands of posts uploaded daily, companies need insights to ensure their listings attract top talent. Using the **LinkedIn Job Postings (2023–2024)** dataset, we developed a **predictive model** to estimate the number of views a job posting will receive and identify key factors driving visibility.

---

## Business Problem

![Business Problem](images/Business%20Problem.jpg)

- **Challenge**: Employers struggle to make their job postings stand out in a highly competitive online market.
- **Key Metric**: Views per posting are a critical indicator of reach and engagement.
- **Goal**: Build a predictive model to estimate job post views and identify actionable strategies to enhance visibility and engagement.

---

## Data
### Source
- **Dataset**: [LinkedIn Job Postings (2023–2024) from Kaggle](https://www.kaggle.com/datasets/arshkon/linkedin-job-postings/data)
- **Size**: 124,000+ job postings.
- **Features**:
  - **Job Attributes**: Title, description, salary, location, work type, remote allowance, skills, benefits + more
  - **Company Attributes**: Size, industry, follower count, HQ location + more

### Why This Dataset?
- Reflects real-time trends in the job market.
- Highly relevant for soon-to-graduate students navigating the job search process.

---

## Data Preparation
### Database Diagram
![LinkedIn Job Posting Database Diagram](images/db_diagram.png)

### Key Steps
1. **Data Ingestion**:
   - Loaded the 10 CSV files seen in the above database diagram into Databricks.
   - Saved as PySpark DataFrames for easier versioning.

2. **Data Cleaning**:
   - Standardized text columns.
   - Addressed missing values in key fields (e.g., job descriptions, skills).
   - Handled duplicates and outliers (e.g., views, salary).

3. **Feature Engineering**:
   - Aggregated benefits and skills into interpretable formats.
   - One-hot encoded categorical variables.
   - Engineered new features like `num_benefits` and `salary_listed`

4. **Final Datasets**:
   - Created two modeling datasets:
     - **Views Dataset**: Focused on predicting views.
         - **Rows**: 116,422
         - **Columns**: 145
     - **Salary Dataset**: Focused on normalized salary predictions.
         - **Rows**: 33,473
         - **Columns**: 145

---

## Exploratory Data Analysis (EDA)

![EDA 1](images/EDA%201.jpg)

### Key Insights
- **Views Feature has a Right-skewed Distribution**: Most job postings receive fewer than 50 views, with a small percentage exceeding 50.
- **Engagement Correlations**:
  - **Views ↔ Applications**: Strong positive correlation.
      - This led us to remove the `applications` feature to avoid collinearity with `views`

![EDA 2](images/EDA%202.jpg)

- **Feature Trends**:
  - Majority of posts in the dataset occur during April 2024.
  - The job industries with the largest number of posts include healthcare, tech, and professional services.
  - The states with the largest number of posts are California, Texas, and New York.
  - The most frequent skills listed in job postings include information technology, sales, and management.

![EDA 3](images/EDA%203.jpg)

- **Feature Relationships**:
  - On average, tech, entertainment, and agriculture are the industries which receive the largest number of views.
  - Job posting with strategy/planning, analyst, and product management skills listed have the largest number of views, on average.
  - Including the salary as well as having remote work as an option both receive more views than not including them.

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
 
Test data was modified by changing features such as remote allowance and salary listing. The changed data was used with the deployed model, and observations were validated using EvidentlyAI's regression and data drift monitoring

---

## Results
1. **Predictive Insights**:
   - Accurately predicts the number of views per job posting.
   - Provides employers with actionable strategies to improve visibility.
2. **Feature Importance**:
   - 
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
- William DeForest
- Linda Ji
- Joon Park
- Christina Song

## Dataset License
The dataset used in this project is the [LinkedIn Job Postings Dataset (2023–2024)]([https://www.kaggle.com/your-dataset-link](https://www.kaggle.com/datasets/arshkon/linkedin-job-postings/data)), licensed under the [Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)](https://creativecommons.org/licenses/by-sa/4.0/).

### Attribution
- **Dataset Author(s)**: [Arsh Koneru, Zoey Yu Zou]
- **Link to Dataset**: [[URL to Kaggle Dataset](https://www.kaggle.com/datasets/arshkon/linkedin-job-postings/data)]
- **License**: [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)

Any modifications to the dataset for this project have been noted in the repository.

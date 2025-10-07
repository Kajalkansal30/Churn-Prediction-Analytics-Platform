# 🚀 Churn Prediction Analytics Platform (End-to-End ML & Business Insights Engine)

This project is a **universal business intelligence and ML engine** designed to take raw company data from any domain (finance, marketing, telecom, operations, etc.) and deliver automated analytics, predictive modeling, business insights, and deployable dashboards. It demonstrates full-stack skills in data engineering, analytics, machine learning, business reasoning, and deployment.

## 🧩 Concept Overview
The platform processes datasets to:
- **Automate analytics & visualization**: Clean data, perform EDA, and generate interactive dashboards.
- **Predictive modeling**: Build ML models for classification (e.g., churn prediction), regression, or clustering.
- **Business insights & recommendations**: Translate results into actionable strategies with quantified impact.
- **Deployability**: Allow users to upload new datasets for instant analysis and predictions.

This project is **domain-flexible** — here, we apply it to telecom churn prediction, but it can adapt to finance (fraud detection), marketing (customer segmentation), or operations (failure prediction).

## 📊 Dataset Used
We use the **Telco Customer Churn Dataset** from Kaggle (https://www.kaggle.com/datasets/blastchar/telco-customer-churn). This dataset contains customer information for a telecom company, including demographics, services, billing, and churn status. It's ideal for demonstrating churn prediction, a common business problem.

- **Key Features**: Customer ID, tenure, monthly charges, total charges, services (internet, phone, etc.), contract type, payment method, and churn label.
- **Size**: ~7,000 rows, 21 columns.
- **Business Relevance**: Predict which customers are likely to churn, enabling targeted retention strategies.

## 📂 Tech Stack
| Layer              | Tools                                                                 |
|--------------------|-----------------------------------------------------------------------|
| Data Engineering   | Python, Pandas, SQLite                                     |
| Analytics          | Pandas, Matplotlib, Seaborn, Pandas Profiling               |
| Modeling           | Scikit-learn, XGBoost, SHAP (for interpretability)                     |
| Storage            | SQLite (telco.db)                                                     |
| Visualization      | Matplotlib, Seaborn                                                   |

## 🧱 Project Breakdown (Modular Skill Layers)

### 1️⃣ Data Engineering + Analytics Layer
**Objective**: Ingest raw data, clean it, and store it in a database for analysis.

**Step-by-Step Process**:
1. **Data Ingestion**: Load the CSV file (`ChurnDataset.csv`) using Pandas. Calculate an MD5 checksum for integrity verification.
2. **ETL Pipeline**: 
   - Handle missing values (e.g., convert 'TotalCharges' to numeric, coercing errors to NaN).
   - Remove duplicates based on 'customerID'.
   - Encode binary columns ('Yes'/'No' to 1/0).
   - Convert categorical columns to appropriate types.
   - Bin 'tenure' into groups (e.g., 0-12 months).
3. **Storage**: Save cleaned data to SQLite database (`data/telco.db`) in tables like `telco_raw`, `telco_cleaned`, and `telco_features`.
4. **Skills Demonstrated**: SQL queries, data cleaning, ETL automation, file integrity checks.

**Output Files**:
- `Processed/telco_raw.csv`: Raw ingested data.
- `Processed/telco_cleaned.csv`: Cleaned data.
- SQLite tables for querying.

### 2️⃣ Exploratory Data Analysis (EDA) & Dashboard Layer
**Objective**: Analyze data distributions, correlations, and KPIs to uncover insights.

**Step-by-Step Process**:
1. **KPI Calculation**:
   - Total customers, overall churn rate, average monthly charges, total revenue.
   - Revenue and churn by contract type.
   - Service adoption rates (e.g., StreamingTV, TechSupport).
   - Tenure distribution.
2. **Visualizations**:
   - Histograms for tenure distribution.
   - Bar plots for churn by internet service type.
   - Use Pandas Profiling for automated reports (`telco_sweetviz_report.html`, `telco_eda_report.html`).
3. **Business Storytelling**: Identify trends, e.g., "Fiber optic users have higher churn rates."
4. **Skills Demonstrated**: Data visualization, KPI tracking, automated reporting, business analytics.

**Outputs**:
- HTML reports for interactive EDA.
- Key metrics stored in a dictionary for reference.

### 3️⃣ Predictive Modeling Layer
**Objective**: Build and evaluate ML models to predict churn.

**Step-by-Step Process**:
1. **Feature Engineering**:
   - Create 'num_services' (sum of subscribed services).
   - Calculate 'avg_monthly_ratio' (TotalCharges / tenure).
   - Add 'is_senior_and_no_support' (binary for seniors without tech support).
   - Save engineered features to `Processed/telco_features.csv`.
2. **Preprocessing**:
   - Split data into train/test (80/20, stratified).
   - Impute missing values, scale numeric features.
3. **Model Training**:
   - Train Logistic Regression, Random Forest, and XGBoost.
   - Handle class imbalance with class weights.
4. **Evaluation**:
   - Metrics: Precision, Recall, F1-Score, ROC-AUC.
   - Confusion matrices and Precision-Recall curves.
   - Compare models (e.g., XGBoost often performs best).
5. **Interpretability**: Use SHAP/LIME (not implemented here, but recommended for explaining predictions).
6. **Skills Demonstrated**: Feature engineering, model selection, evaluation, handling imbalanced data.

**Results** (Example from Random Forest):
- ROC-AUC: ~0.85
- Precision for churn class: ~0.6
- Recall: ~0.7

### 4️⃣ Business Insights & Recommendations Layer
**Objective**: Translate ML results into actionable business strategies.

**Step-by-Step Process**:
1. **Impact Quantification**:
   - Estimate retention savings: Predicted churners × average monthly revenue.
   - Example: Retaining 200 predicted churners saves ~$20,000/month.
2. **Insights**:
   - "Customers with high spending but low engagement → Target with loyalty offers."
   - "Seniors without tech support have higher churn → Provide free support."
   - "Fiber optic users churn more → Investigate service quality."
3. **Recommendations**:
   - Prioritize retention for top 10% customers (Pareto principle).
   - Segment by contract type for personalized marketing.
4. **Skills Demonstrated**: Business impact analysis, data-driven decision-making, storytelling.

### 5️⃣ Deployment & Automation Layer
**Objective**: Make the platform user-friendly and deployable.

**Step-by-Step Process** (Suggested Implementation):
1. **Build a Streamlit App**:
   - Upload new datasets.
   - Automatically clean, analyze, and predict.
   - Display dashboards, model results, and insights.
2. **API Integration**: Use Flask for REST APIs to serve predictions.
3. **Automation**: Schedule ETL with Airflow (not implemented).
4. **MLOps**: Version models, monitor performance.
5. **Skills Demonstrated**: Deployment, API building, automation, user interface design.

**To Deploy**:
- Install Streamlit: `pip install streamlit`
- Run: `streamlit run app.py` (create `app.py` with dashboard code).
- Host on Heroku/AWS for public access.

## 🚀 How to Run the Project
1. **Prerequisites**: Python 3.8+, install dependencies: `pip install pandas sqlalchemy scikit-learn xgboost matplotlib seaborn sweetviz pandas-profiling statsmodels`
2. **Clone/Download**: Place files in `c:/Users/kansa/ChurnPrediction`.
3. **Run Notebook**: Open `ChurnProject.ipynb` in Jupyter and execute cells sequentially.
4. **Outputs**: Check `Processed/` for CSVs, `data/telco.db` for database, HTML reports for EDA.
5. **Experiment**: Modify dataset or parameters for other domains.

## 💼 Recruiter Impression
This project showcases:
- **Technical Grounding**: ETL, ML, visualization.
- **Business Understanding**: KPIs, insights, impact quantification.
- **Scalability**: Modular design for any domain.
- **Transferability**: Adaptable to Amex (fraud), Goldman (risk), Ciena (network failures).

## 📈 Future Enhancements
- Add SHAP for model explainability.
- Deploy on Streamlit/Heroku.
- Integrate with real APIs (e.g., Kaggle API for data).
- Expand to regression (revenue forecasting) or clustering (customer segmentation).

For questions or contributions, open an issue/PR on GitHub!


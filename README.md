# 🏥 Using ChatGPT as a Data Analytics Copilot (Healthcare)
## ◼️ Project Goal & Motivation 🎯

The primary goal of this project is to demonstrate how to use **ChatGPT** effectively as a Data Analytics Copilot throughout a complete healthcare analytics workflow.

Rather than replacing analytical thinking, **ChatGPT** is used to:

1. Improve reasoning speed.

2. Ask better analytical questions.

3. Assist with data cleaning and visualization.

4. Reduce friction during EDA and modeling.

5. Support decision-making while keeping the analyst fully in control.

This project is inspired by **Luke Barousse’s** course on using **ChatGPT** for Data Analytics, where **ChatGPT** is positioned as a thinking partner, not a shortcut.

## ◼️ How ChatGPT Is Used (Copilot Mindset) 🧠
ChatGPT is used deliberately and transparently across the project to:

- 🧩 Clarify dataset and column meanings.

- 🧹 Suggest data cleaning strategies (validated by me).

- 📊 Generate visualization ideas and code.

- 🔍 Help reason through EDA findings.

- 🧠 Assist with feature engineering logic.

- 📈 Discuss modeling choices and limitations.

All outputs from **ChatGPT** are reviewed, adapted, and validated by me (the analyst).

## ◼️ Prompting Strategy (Core Skill Demonstrated) ✍️ 

One goal of this course is how to form good prompts as it impacts directly on the analytical quality, the strategies for it include:

- Providing context (domain + objective).
- Specifying the role of ChatGPT (e.g., “act as a healthcare data analyst”).
- Asking for options, not answers.
- Iteratively refining prompts based on results.

## ◼️ Data Source 📂

The dataset was sourced from Kaggle and selected to support an analysis of Hospital Length of Stay. According to its description, the data originates from the OECD database, which limits coverage to OECD member countries, and spans the period 1990 to 2018.

<p align="center">
  <a href="https://www.kaggle.com/datasets/babyoda/healthcare-investments-and-length-of-hospital-stay">-> Dataset <-</a>
</p>

## ◼️ Project Structure 🏗️

The project consists on the following structure of notebooks:

1. **Data Understanding** ->
Understand the structure, scope, and limitations of the healthcare dataset before any transformation.

2. **Data Cleaning** ->
Prepare the dataset for analysis by improving consistency and usability.

3. **Exploratory Data Analysis** -> 
Explore patterns, distributions, and relationships in the healthcare data.

4. **Feature Engineering** -> 
Prepare features for modeling and analytical use.

5. **Length of Stay Prediction Model** ->
Build and evaluate a simple, interpretable predictive model.

## ◼️ Methodology 🔬



### **Data Understanding**

#### Prompt example ->

```
- I'm a data analyst studying a dataset for Healthcare Investments and Length of Hospital Stay.
- Based on these column names and data types, explain what each variable likely represents and which ones may be important for analysis from the dataset uploaded.
```

#### Analysis example ->
```
🛏️ **Hospital_Stay** -  (float64)

Average length of hospital stay (days)

🎯 TARGET VARIABLE

1. This is what you want to explain or predict

2. Central healthcare efficiency metric

⚠️ Highly sensitive to:

1. Technology availability

2. Capacity (beds)

3. Long-term investment effects
```
This provides an initial understanding of what the variables represent and how the information can be used. By loading the data and reviewing the columns, we can then confirm both the definitions and the actual content.

### **Data Cleaning**
#### Prompt example ->
```
- Based on the column names and data types, check if there are missing values or data that doesn't correspond to the columns.
- What are reasonable strategies to handle missing data for a healthcare dataset, and what are the trade-offs of each approach?
```

#### Analysis example ->
```
🏥 3. Group-based imputation (RECOMMENDED)

🔹 Example:
hospital_stay imputed by location-year mean

🔹 Pros:
✅ Preserves structure
✅ Context-aware

🔹 Cons:
❌ Slightly more complex

🔥 Best fit for your dataset type
```

This allows us to quickly identify which parts of the dataset require cleaning or reframing, as well as where null values may need to be filled or removed to improve analysis quality.

### **Exploratory Data Analysis**
#### Prompt example ->
```
- I want to explore patterns in hospital length of stay. 
- What plots would you recommend to understand distributions and group differences, and why?
```
#### Analysis example ->
```
📅 Line plot over Time (by Location)

Why

🔹Your data is longitudinal

🔹Captures trend, not noise

🔹Shows convergence/divergence across countries

📌 Insight you get:

“Are hospital stays decreasing over time as investment increases?”
```

This provides a brief understanding of which variables can be analyzed, which items are under study, and how certain variables depend on others in order to later predict behavior.

### **Feature Engineering**
#### Prompt example ->
```
- Given these variables, which features would you keep or exclude for modeling hospital length of stay?
- Explain your reasoning and mention potential risks like leakage or bias.
```

#### Analysis example ->
```
💰 mri_units

Why keep

🔹Proxy for diagnostic investment

🔹Central explanatory variable

Interpretation

Hypothesis: more MRI → faster diagnosis → ↓ LOS

⚠️ Risk

🔹Correlated with wealth → confounding
```

This helps us identify which variables should be taken into account and which should be discarded based on the quantity and quality of the information.

### **Length of Stay Prediction Model**
#### Prompt example ->
```
- Help me frame hospital length of stay as a regression problem.
- What assumptions should I be aware of when modeling this target?
```

#### Analysis example ->
```
🎯 1. Framing Hospital Length of Stay as a Regression Problem
🔢 Target (Y)

🔹hospital_stay (continuous, numeric)

🔹Interpreted as average days per country-year

➡️ This is a continuous outcome → regression, not classification.
```

This allows us to ask relevant questions and consider which models are best suited to make predictions based on the selected information.

## ◼️ Results 📈
In the results section, the two notebooks worth highlighting are Exploratory Data Analysis and Length of Stay Prediction Model, as these are where the data is actively analyzed and the hospital length of stay is predicted.

For this project we specifically analyze the information in Australia, here are the results:

### **Exploratory Data Analysis**
To identify which variables may influence length of stay, we focus on Australia as a case study to better understand the patterns in the data. Below are the plots generated from this analysis.

##### Length of Stay Over the Years
![](/EDA_Plots/Length%20of%20Stay%20vs%20Time%20AUS.png)

##### Influence of MRI Units Quantity on Length of Stay
![](/EDA_Plots/Influence%20of%20MRI%20Units.png)

##### Influence of CTE Scanners Quantity on Length of Stay
![](/EDA_Plots/Influence%20of%20CT%20Scanners.png)

##### Influence of Hospital Beds Quantity on Length of Stay
![](/EDA_Plots/Influence%20of%20Hospital%20Beds.png)

Over time, the average length of hospital stay in Australia has decreased, coinciding with increased investment in healthcare infrastructure. This trend is reflected in the growth of hospital beds, MRI units, and CT scanners. As diagnostic and treatment resources become more widely available, clinical processes can be completed more efficiently, reducing the amount of time patients need to remain hospitalized for procedures.


### **Length of Stay Prediction Model**

Based on the available information, the regression model was built using only data from Australia. Data from other countries were excluded because differences in healthcare systems, policies, and infrastructure investment strategies would make cross-country comparisons inappropriate and could introduce bias into the analysis.

```python
## Linear Regression Model – Predicting Hospital Length of Stay (Australia)
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error

# Filter Australia only
df_aus = df[df["location"] == "AUS"].sort_values("time")

# Features and target
X = df_aus[["mri_units", "ct_scanners", "hospital_beds"]]
y = df_aus["hospital_stay"]

# Time-aware split (last year as test)
X_train, X_test = X.iloc[:-1], X.iloc[-1:]
y_train, y_test = y.iloc[:-1], y.iloc[-1:]

# Train model
model = LinearRegression()
model.fit(X_train, y_train)

# Evaluate
y_pred = model.predict(X_test)
mse = mean_squared_error(y_test, y_pred)
rmse = np.sqrt(mse)

print("MSE:", mse)
print("RMSE:", rmse)

```
RESULTS:
-> **MSE:** 0.025069
-> **RMSE:** 0.158332

Finally, we forecast Hospital Length of Stay for Australia (2025 Projection):

```python
# Refit model on all AUS data
model.fit(X, y)

# Extrapolate predictors to 2025
last_year = df_aus["time"].max()
years_ahead = 2025 - last_year

avg_growth = X.diff().mean()
future_features = X.iloc[-1] + years_ahead * avg_growth
future_features = future_features.values.reshape(1, -1)

los_2025 = model.predict(future_features)[0]

print("Predicted hospital stay in 2025 (AUS):", los_2025)
```
RESULT:
**Predicted hospital stay in 2025 (AUS):** 3.365.

## ◼️ Tools Used ⚙️

- Python: Core programming language for data cleaning, analysis, visualization, and modeling.

- Jupyter Notebooks: Interactive environment for exploratory analysis, documentation, and iterative workflows.

- Visual Studio Code (VSCode): Primary development environment for writing, running, and managing notebooks and scripts.

- Git: Version control system used to track changes and manage the project lifecycle.

- GitHub: Repository hosting, collaboration, and project documentation.

- ChatGPT: Used as a Data Analytics Copilot to assist with prompting, data cleaning strategies, visualization ideas, and analytical reasoning.

## ◼️ Key Takeaways 📌

- Prompt engineering is a core data skill

- ChatGPT accelerates thinking, not judgment

- Healthcare analytics requires careful interpretation

- Simple models + strong reasoning outperform complexity


## ◼️ Project Conclusions 🧭


- Due to the limited size and structure of the dataset, linear regression was selected as the most appropriate and interpretable modeling approach for this problem.

- Although the model produced a low RMSE, this metric is not a strong indicator of predictive performance because the evaluation relied on a single-year test set.

- The prediction for hospital length of stay in 2025 should be interpreted with caution, based on the following considerations:

  1. The estimated value represents a scenario-based projection, not a precise forecast.

  2. The extrapolation assumes continued growth in CT scanners, MRI units, and hospital beds, which may not hold in practice, as such investments depend on external factors such as government policy and funding decisions.


## ◼️ Recommendation 💡
⭐ Using ChatGPT as a data analytics copilot is highly recommended for speeding up the workflow, especially during data understanding, cleaning, and exploratory analysis. By offloading repetitive and boilerplate tasks, it frees up time to focus on deeper thinking—such as selecting meaningful features, questioning assumptions, and carefully evaluating the predictive model. When used critically, ChatGPT becomes a strong productivity booster rather than a replacement for analytical judgment.
 
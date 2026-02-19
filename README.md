# Using ChatGPT as a Data Analytics Copilot

## Project Overview
This project demonstrates how ChatGPT can be used as a copilot to support
data analytics workflows, including data cleaning, EDA, feature engineering,
and machine learning, while keeping the analyst in control of decisions.

## Dataset
Google Search job postings dataset focused on data roles in the US.

## Key Questions
- How do salaries vary by role, location, and platform?
- What factors most influence salary levels?
- Can we predict yearly salary using job metadata?

## Tools & Technologies
- Python (pandas, matplotlib, scikit-learn)
- CatBoost
- Jupyter Notebooks (VSCode)
- ChatGPT (as an analytical assistant)

## How ChatGPT Was Used
- Column understanding & documentation
- Regex-based data cleaning suggestions
- Model selection reasoning
- Validation of analytical assumptions

## Key Takeaways
- High-cardinality categorical data requires careful model selection
- Gradient boosting models outperform random forests in this scenario
- ChatGPT accelerates analysis but does not replace analytical judgment

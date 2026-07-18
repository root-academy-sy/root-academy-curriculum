# Week 6 — Machine Learning: Regression

**Course:** Introduction to Data Science
**Week Topic:** Predict a Continuous Value

## Main Goal

Week 6 introduces supervised machine learning through regression. Students learn how a model uses input features to predict a numeric target such as price, salary, score, or sales.

## Key Ideas

- Regression predicts continuous numeric values.
- Features are the input columns used for prediction.
- The target is the value we want to predict.
- Train/test split helps us evaluate a model on unseen data.
- Errors show how far predictions are from real values.

## Basic Workflow

| Step | Purpose |
|---|---|
| Load data | Read the dataset |
| Choose features and target | Decide inputs and output |
| Split data | Separate training and testing data |
| Train model | Learn from training data |
| Predict | Generate predictions |
| Evaluate | Measure model error |

## Example Code

```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score

df = pd.read_csv("data/employee_data_cleaned.csv")

X = df[["attendance"]]
y = df["score"]

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

model = LinearRegression()
model.fit(X_train, y_train)

predictions = model.predict(X_test)

print("MAE:", mean_absolute_error(y_test, predictions))
print("MSE:", mean_squared_error(y_test, predictions))
print("R2:", r2_score(y_test, predictions))
```

## Next Level Preview

In the paid course, students will use more features, stronger preprocessing, feature engineering, and model comparison for regression projects.



---

**Next:** [Lab →](lab.ipynb) | [Assignment →](assignment.ipynb)

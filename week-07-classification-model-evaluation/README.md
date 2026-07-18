# Week 7 — Classification & Model Evaluation

**Course:** Introduction to Data Science
**Week Topic:** Predict a Category, Then Compare Models

This week combines two closely related topics: training a classification
model, and evaluating whether it — or a simpler alternative — is actually any
good. In practice these two skills are always used together, so we cover
them in the same week.

# Part 1: Classification

## Main Goal

Classification models predict categories such as pass/fail, high/low risk, yes/no, or customer type.

## Classification vs Regression

| Regression | Classification |
|---|---|
| Predicts a number | Predicts a category |
| Salary, price, score | Pass/fail, yes/no, type |

## Example Workflow

```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report

df = pd.read_csv("data/employee_data_cleaned.csv")
df["high_performer"] = df["score"] >= 80

X = df[["attendance"]]
y = df["high_performer"]

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

model = DecisionTreeClassifier(random_state=42)
model.fit(X_train, y_train)

predictions = model.predict(X_test)

print("Accuracy:", accuracy_score(y_test, predictions))
print(confusion_matrix(y_test, predictions))
print(classification_report(y_test, predictions))
```

## Next Level Preview

In the paid course, students will learn stronger classification workflows, imbalance handling, feature encoding, and deeper metric interpretation.



---

# Part 2: Model Evaluation and Improvement

## Main Goal

Training a model is not enough. A data scientist must evaluate whether the model performs well and compare it with simple alternatives.

## Important Metrics

| Task | Metrics |
|---|---|
| Regression | MAE, MSE, R2 |
| Classification | Accuracy, precision, recall, F1-score, confusion matrix |

## Simple Model Comparison

```python
from sklearn.linear_model import LogisticRegression
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score

models = {
    "Logistic Regression": LogisticRegression(),
    "Decision Tree": DecisionTreeClassifier(random_state=42)
}

for name, model in models.items():
    model.fit(X_train, y_train)
    predictions = model.predict(X_test)
    print(name, accuracy_score(y_test, predictions))
```

## Next Level Preview

In the paid course, students will learn cross-validation, hyperparameter tuning, preprocessing pipelines, and professional model reports.



---

**Next:** [Lab →](lab.ipynb) | [Assignment →](assignment.ipynb)

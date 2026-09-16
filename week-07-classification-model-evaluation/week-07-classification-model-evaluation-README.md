# Week 7 — Train Your First Model, Classification & Model Evaluation

**Course:** Introduction to Data Science
**Week Topic:** Train a Regression Model, Then a Classification Model, Then Check if Either is Any Good

This week has three parts. First you actually train the regression model
whose theory you learned last week. Then you train a classification model —
a model that predicts a category instead of a number. Then you learn how to
check whether any model you build is actually good, or just lucky.

# Part 1: Training Your First Model (Regression)

## Recap From Last Week

- **Regression** predicts a **number**, not a category.
- **Features** are the inputs we give the model; the **target** is what we want it to predict.
- We train on part of the data, then test on data the model hasn't seen, to check **generalization** — not just memorization.
- A model that's too simple and misses the pattern is **underfitting**; one that memorizes the training data too closely is **overfitting**.
- Good data in, good results out — a model can only learn the patterns that exist in the data it's given.

Today, all of these ideas stop being theory and become something you can actually run.

## Why Start With Regression?

Regression is the simplest place to start learning the full machine learning process, because:

- The target is a number, so it's easy to check "how far off" a prediction is.
- The whole workflow — load, split, train, predict, evaluate — is short and easy to follow end-to-end.
- Once you understand this loop, almost every other ML task (classification, later in this same week) follows the same basic shape.

Real-world regression examples: predicting a house's price, a delivery time, a salary, or — like today — an employee's score.

## Meet the Dataset

We'll use `employee_data_cleaned.csv`, the same dataset we've been working with all course.

- **Feature (input):** `attendance`
- **Target (output):** `score`

We're asking: *if we know an employee's attendance, can we predict their score?*

## What is Linear Regression?

Linear Regression is the simplest way a machine can learn a rule that connects your features to a number. It tries to draw the "best-fit line" through your data — the line that keeps predictions as close as possible to the real answers.

If attendance and score tend to move together, Linear Regression finds the straight-line relationship between them, then uses that line to guess a score for an employee it hasn't seen before.

## Example Workflow

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

print("Coefficient:", model.coef_[0])
print("Intercept:", model.intercept_)
```

## What Each Step is Doing

1. **Load data** — `pd.read_csv(...)` reads the file into a DataFrame we can work with.
2. **Choose features and target** — `X` holds the input column(s), `y` holds the column we want to predict.
3. **Split data** — `train_test_split` sets aside 20% of the data purely for testing, so the model is judged on data it never trained on.
4. **Train** — `.fit()` is where the actual "learning" happens: the model looks at the training data and finds the best relationship between attendance and score.
5. **Predict** — `.predict()` uses that learned relationship on the test data.
6. **Evaluate** — we compare the predictions to the real scores using error metrics.

## Understanding the Line

Under the hood, linear regression is trying to draw the best-fitting straight line through the data:

```
score = intercept + (coefficient × attendance)
```

- The **coefficient** tells you how much the score changes for every extra point of attendance.
- The **intercept** is the predicted score when attendance is 0 (a theoretical starting point, not always realistic).

You printed these yourself above with `model.coef_` and `model.intercept_` — it's a nice way to "see" what the model actually learned, instead of treating it as a black box.

## Reading the Metrics

| Metric | What it tells you | Good direction |
|---|---|---|
| **MAE** (Mean Absolute Error) | On average, how far off predictions are, in the same units as the target | Lower is better |
| **MSE** (Mean Squared Error) | Like MAE, but penalizes big mistakes more heavily | Lower is better |
| **R²** (R-squared) | What % of the variation in the target your features explain | Closer to 1 is better |

**A quick gut-check:** if your MAE is 5 and scores range from 0–100, that's a pretty good model. If your MAE is 5 and scores range from 0–10, that same "5" would actually be a bad model. Always read error metrics next to the scale of your target — a number like "MAE: 4" means nothing on its own.

## Is Your Regression Model Actually Good? Compare It to a Baseline

A model is only impressive if it beats doing nothing clever at all. The simplest possible "model" is guessing the *average* score every single time:

```python
baseline_prediction = y_train.mean()
baseline_mae = (y_test - baseline_prediction).abs().mean()

print("Baseline MAE:", baseline_mae)
print("Model MAE:", mean_absolute_error(y_test, predictions))
```

If your trained model's MAE isn't meaningfully lower than the baseline's, it hasn't really learned anything useful yet — that's a sign to revisit your features or check your data quality.

## Connecting Back to Overfitting & Underfitting

Remember the Student A vs. Student B idea from last week?

- If your model does great on training data but much worse on test data → it may be **overfitting** (memorizing).
- If your model does poorly on both → it may be **underfitting** (too simple, or missing useful features).
- The goal is a model that does reasonably well on **both** — that's a sign it actually **generalized**.

With only one feature (`attendance`), don't be surprised if the model's performance is decent but not amazing — that's expected, and a preview of why more features usually help.

## Common Mistakes to Avoid

- Forgetting to split data before training (leads to misleadingly good results).
- Judging a model only by R² without checking MAE/MSE in real units.
- Using a feature that's actually a duplicate or proxy of the target (data leakage).
- Comparing MAE/MSE across two different datasets or targets without checking the scale first.
- Reading too much into results from a single feature — one column rarely tells the whole story.

## What You Just Did

You trained your first machine learning model. It looked at attendance data, found a pattern, and used that pattern to predict scores it had never seen before. This exact loop — load, split, train, predict, evaluate — is the core process behind almost every machine learning project you'll build, including the classification model you're about to train next.

---

# Part 2: Classification Foundations

## Main Goal

Classification means teaching a model to sort things into groups. Not a
number — a group. Like: yes or no. Pass or fail. Spam or not spam.

## Classification vs Regression

| Regression | Classification |
|---|---|
| Predicts a number | Predicts a group |
| Example: salary, price, score | Example: pass/fail, yes/no, spam/not spam |

## Where You Already See Classification

- Email app deciding: **spam** or **not spam**
- Bank deciding: **approve** or **reject** a loan
- Doctor's app deciding: **sick** or **healthy**
- Your phone camera deciding: **is this a face** or **not**

All of these are the same idea: look at the data, pick one group out of a
few possible groups.

## How Does a Classifier "Decide"?

We will use a model called a **Decision Tree**. It works by asking simple
yes/no questions, one after another, like a flowchart.

For our employee data, it might ask:

> "Is attendance above 85%?"
> - Yes → probably a high performer
> - No → ask one more question, or make a guess

The tree tries many possible questions on the training data and picks the
ones that sort employees into the cleanest groups. You don't write these
questions yourself — the model finds them on its own when you call `.fit()`.

## Types of Classification

| Type | How many groups? | Example |
|---|---|---|
| **Binary** | Only 2 | High performer or not |
| **Multiclass** | 3 or more | Bronze / Silver / Gold customer |

This week we use **binary** classification: "high performer" or "not."

## Train Your First Classification Model

We follow the same six steps as regression, just with a category as the target instead of a number.

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

What each line does:

- `df["high_performer"] = df["score"] >= 80` — this creates our target. It
  turns the number `score` into a simple True/False group.
- `X` — the input we use to guess (attendance).
- `y` — the answer we want to predict (high performer or not).
- `.fit()` — the model looks at the training data and learns the pattern.
- `.predict()` — the model guesses on data it has never seen.
- The `print` lines — we check how good the guesses were.

## Reading the Confusion Matrix

The confusion matrix is just a small table that shows what the model got
right and wrong:

| | Predicted: Not High Performer | Predicted: High Performer |
|---|---|---|
| **Actually: Not High Performer** | Correct (True Negative) | Wrong — false alarm (False Positive) |
| **Actually: High Performer** | Wrong — missed it (False Negative) | Correct (True Positive) |

Simple way to remember it:

- **True** = the model was right.
- **False** = the model was wrong.
- **Positive** = the model said "yes, high performer."
- **Negative** = the model said "no, not a high performer."

## Try This Yourself

Say your model was tested on 20 employees, and the results were:

- 12 correct "not high performer"
- 5 correct "high performer"
- 2 false alarms
- 1 missed high performer

Question: how many predictions were correct in total, out of 20? (Add the
two correct numbers, divide by 20.) We'll use this same example in Part 3.

---

# Part 3: Is Your Model Actually Good?

## Main Goal

Training a model is easy. Knowing if it's actually **good** is the harder,
more important skill. This part teaches you how to check that, and how to
compare two models against each other.

## Why "Accuracy" Alone Can Lie to You

Imagine a doctor's test where only 1 out of 20 patients is actually sick. A
lazy "model" that always says **"healthy"** would be right 19 out of 20
times — 95% accuracy! But it would miss every single sick patient. That
model is useless, even though the accuracy number looks great.

This is why we use more than one metric.

## The Main Metrics

| Metric | Simple meaning |
|---|---|
| **Accuracy** | Out of everyone, how many did we get right? |
| **Precision** | Out of everyone we said "yes" to, how many were really "yes"? |
| **Recall** | Out of everyone who was really "yes," how many did we catch? |
| **F1-score** | One number that balances precision and recall together |

Using the example from Part 2 (12 correct "no," 5 correct "yes," 2 false
alarms, 1 missed case):

- **Precision** = 5 ÷ (5 + 2) = **71%** — most of our "yes" guesses were right, but not all.
- **Recall** = 5 ÷ (5 + 1) = **83%** — we caught most of the real "yes" cases, missing only 1.

Precision and recall answer different questions. A model can be good at one
and bad at the other. That's why both numbers matter, not just accuracy.

## Compare Your Model to a Simple Guess (Baseline)

Before trusting your model, check: is it actually better than just guessing
the most common answer every time?

```python
baseline_prediction = y_train.mode()[0]
baseline_accuracy = (y_test == baseline_prediction).mean()

print("Baseline accuracy:", baseline_accuracy)
print("Model accuracy:", accuracy_score(y_test, predictions))
```

If your model's accuracy is barely better than this simple guess, it hasn't
really learned much yet.

## A Second Model: Logistic Regression

Even though the name has "Regression" in it, this model is actually used
for classification. Instead of asking yes/no questions like a Decision Tree,
it gives a **probability** — like "80% chance this is a high performer" —
and then turns that into a final yes/no answer.

| | Decision Tree | Logistic Regression |
|---|---|---|
| How it thinks | Asks yes/no questions, step by step | Gives a probability, then decides |
| Easy to explain? | Yes — very visual | A bit less visual, but often reliable |

We don't know in advance which model will do better on our data. That's why
we test both and compare.

## Comparing Two Models

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

Both models are trained and tested on the exact same data split, so the
comparison is fair.

## New Words This Week

- **Coefficient / intercept** — the numbers a regression model learns to draw its best-fit line
- **Classification** — predicting a group, not a number
- **Confusion matrix** — a small table showing correct and wrong guesses
- **False positive** — the model said "yes" but it was actually "no"
- **False negative** — the model said "no" but it was actually "yes"
- **Precision** — how trustworthy the model's "yes" answers are
- **Recall** — how many real "yes" cases the model actually found
- **Baseline** — the simplest possible guess, used to check if your model is really learning

## Next Level Preview

In the paid course, students go further with both tasks: regularization and feature scaling for regression, and cross-validation, hyperparameter tuning, and imbalance handling for classification.

---

**Next:** [Lab →](lab.ipynb) | [Assignment →](assignment.ipynb)

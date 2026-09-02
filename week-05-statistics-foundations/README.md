# Week 5 — Statistics Foundations

**Course:** Introduction to Data Science
**Week Topic:** Statistical Analysis Project
**Prerequisites:** Week 4 (Pandas basics), Python environment with pandas, scipy, seaborn installed

## Main Goal

Week 5 introduces the statistical thinking needed for data science. The goal is to understand how statistics helps us summarize data, compare groups, understand variation, and avoid misleading conclusions — including some of the traps that catch beginners.

By the end of this week, students should be able to:

1. Explain the difference between descriptive and inferential statistics
2. Calculate mean, median, mode, range, variance, and standard deviation
3. Understand distributions, skewness, and outliers
4. Compare groups using summary statistics
5. Interpret correlation without confusing it with causation
6. Use Pandas and SciPy for statistical analysis
7. Write a clear statistical finding from a dataset

## 1. Why Statistics Matters in Data Science

Statistics turns raw data into reliable information. Without it, we focus on individual values and miss the bigger pattern. It answers questions like: What is typical? How much do values vary? Are two groups different? Are two variables related — and can we trust that relationship?

Knowing one employee scored 95 tells you almost nothing on its own. Knowing the average score, how spread out scores are, and how departments differ gives you something you can actually act on.

## 2. Descriptive vs Inferential Statistics

| Type | Purpose | Example |
|---|---|---|
| Descriptive statistics | Summarize the data we have | Average score of employees in a dataset |
| Inferential statistics | Use sample data to make conclusions about a larger population | Estimate the average score of all employees from a sample |

This week focuses mainly on descriptive statistics, with a light introduction to inference — mainly through **standard error**, which tells us how much a sample mean might differ from the true population mean.

```python
import numpy as np

standard_error = df["score"].std() / np.sqrt(len(df))
print(standard_error)
```

A smaller sample gives a larger standard error — meaning less confidence that the sample mean reflects reality.

## 3. Measures of Center

| Measure | Meaning | Weakness |
|---|---|---|
| Mean | The arithmetic average | Sensitive to outliers |
| Median | The middle value after sorting | Ignores magnitude of extremes |
| Mode | The most frequent value | Unstable on continuous data |

```python
import pandas as pd

df = pd.read_csv("data/employee_data_cleaned.csv")

print(df["score"].mean())
print(df["score"].median())
print(df["score"].mode())  # can return more than one value if there's a tie
```

**Rule of thumb:** if `mean` and `median` are far apart, your data is skewed — check the distribution before trusting the mean.

## 4. Measures of Spread

| Measure | Meaning |
|---|---|
| Range | Maximum minus minimum |
| Variance | Average squared distance from the mean |
| Standard deviation | Typical distance from the mean (same units as the data) |

```python
score_range = df["score"].max() - df["score"].min()
print(score_range)
print(df["score"].var())
print(df["score"].std())
```

Variance is in squared units (e.g. "points²"), which isn't intuitive — that's why we usually report standard deviation instead, since it's back in the original units.

## 5. Distributions and Skewness

A distribution shows how values are spread across a variable.

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.histplot(data=df, x="score", bins=10, kde=True)
plt.title("Score Distribution")
plt.show()

print("Skewness:", df["score"].skew())
```

- **Skew ≈ 0** → roughly symmetric
- **Skew > 0** → right-tailed (a few very high values pull the mean up)
- **Skew < 0** → left-tailed (a few very low values pull the mean down)

Skewness explains *why* mean and median disagree — it's the same idea as the rule of thumb in Section 3, just measured directly.

## 6. Outliers

An outlier is a value very different from the rest of the data. It can be real or a data entry mistake — investigate before removing.

For bounded data (like a 0–100 score), simple range checks work:

```python
print(df["score"].describe())

low_scores = df[df["score"] < 0]
high_scores = df[df["score"] > 100]
```

For unbounded data, use the **IQR method** instead, which doesn't assume known limits:

```python
Q1 = df["score"].quantile(0.25)
Q3 = df["score"].quantile(0.75)
IQR = Q3 - Q1

lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

outliers = df[(df["score"] < lower_bound) | (df["score"] > upper_bound)]
print(outliers)
```

Values beyond 1.5×IQR from the quartiles are flagged as outliers — this is the same rule boxplots use.

## 7. Comparing Groups

```python
department_stats = df.groupby("department")["score"].agg(["count", "mean", "median", "std", "min", "max"])
print(department_stats)
```

Always check `count` alongside `mean` — a group with only one or two records isn't reliable, no matter how different its average looks.

## 8. Correlation

Correlation measures the relationship between two numeric variables, from -1 to 1.

| Correlation | Meaning |
|---|---|
| Close to 1 | Strong positive relationship |
| Close to -1 | Strong negative relationship |
| Close to 0 | Weak or no *linear* relationship |

```python
pearson_corr = df["attendance"].corr(df["score"])  # default method
spearman_corr = df["attendance"].corr(df["score"], method="spearman")

print(pearson_corr, spearman_corr)
```

Pandas' default (**Pearson**) only detects *linear* relationships — two variables can be strongly related in a curved way and still show a Pearson correlation near 0. **Spearman** correlation checks for any consistent increasing/decreasing pattern, not just a straight line, so it's a useful second check.

**Correlation is not causation.** If attendance and score are correlated, we cannot say attendance *caused* the score to rise — a third factor (motivation, study habits) could be driving both.

## 9. Common Mistakes to Avoid

- Reporting the mean without checking skew or outliers first
- Comparing group averages without checking group size
- Treating a near-zero Pearson correlation as "no relationship" (it might just be non-linear)
- Removing outliers without investigating whether they're real

## 10. Simple Statistical Report

A report should combine numbers with plain-language interpretation. Deliverable: a short markdown writeup (`report.md`) alongside your notebook, covering the summary stats, group comparison, and correlation below, plus 2–3 sentences on what they mean.

```python
summary = df[["score", "attendance"]].describe()
print(summary)

department_summary = df.groupby("department")["score"].agg(["count", "mean", "std"])
print(department_summary)

print(df["attendance"].corr(df["score"]))
```

## Week 5 Summary

Week 5 covered central tendency, spread, distributions and skewness, outlier detection (both bounded and IQR methods), group comparison, and correlation — including where correlation can mislead. These ideas carry directly into machine learning, where understanding your data statistically comes before trusting any model built on it.

---

**Previous:** [← Week 4](../week_4/README.md) | **Next:** [Lab →](lab.ipynb) | [Assignment →](assignment.ipynb)
# Week 5 — Statistics Foundations

**Course:** Introduction to Data Science
**Week Topic:** Statistical Analysis Project

## Main Goal

Week 5 introduces the statistical thinking needed for data science. Students do not need advanced mathematics at this stage. The goal is to understand how statistics helps us summarize data, compare groups, understand variation, and avoid misleading conclusions.

By the end of this week, students should be able to calculate descriptive statistics, understand distributions, compare groups, interpret correlation, and explain basic statistical findings in simple language.

- Explain the difference between descriptive and inferential statistics.
- Calculate mean, median, mode, range, variance, and standard deviation.
- Understand distributions and outliers.
- Compare groups using summary statistics.
- Interpret correlation without confusing it with causation.
- Use Pandas and SciPy for simple statistical analysis.
- Write clear statistical findings from a dataset.

## 1. Why Statistics Matters in Data Science

Statistics helps us turn raw data into reliable information. Without statistics, we may focus on individual values and miss the bigger pattern. Statistics helps answer questions such as: What is typical? How much do values vary? Are two groups different? Are two variables related?

For example, knowing that one employee scored 95 is useful, but knowing the average score, score distribution, and department differences gives a much clearer picture.

## 2. Descriptive vs Inferential Statistics

| Type | Purpose | Example |
|---|---|---|
| Descriptive statistics | Summarize the data we have | Average score of employees in a dataset |
| Inferential statistics | Use sample data to make conclusions about a larger population | Estimate the average score of all employees from a sample |

In this introductory course, Week 5 focuses mainly on descriptive statistics, with a light introduction to inference.

## 3. Measures of Center

Measures of center describe a typical value in the data.

| Measure | Meaning |
|---|---|
| Mean | The arithmetic average |
| Median | The middle value after sorting |
| Mode | The most frequent value |

```python
import pandas as pd

df = pd.read_csv("data/employee_data_cleaned.csv")

print(df["score"].mean())
print(df["score"].median())
print(df["score"].mode())
```

The mean is sensitive to outliers. The median is often better when the data contains very high or very low values.

## 4. Measures of Spread

Measures of spread describe how much values vary.

| Measure | Meaning |
|---|---|
| Range | Maximum minus minimum |
| Variance | Average squared distance from the mean |
| Standard deviation | Typical distance from the mean |

```python
score_range = df["score"].max() - df["score"].min()
print(score_range)
print(df["score"].var())
print(df["score"].std())
```

A low standard deviation means values are close to the mean. A high standard deviation means values are more spread out.

## 5. Distributions

A distribution shows how values are spread across a variable. For example, a score distribution can show whether most students scored high, low, or around the middle.

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.histplot(data=df, x="score", bins=10)
plt.title("Score Distribution")
plt.show()
```

## 6. Outliers

An outlier is a value that is very different from the rest of the data. Outliers can be real, or they can be data entry mistakes. They should be investigated before being removed.

```python
print(df["score"].describe())

low_scores = df[df["score"] < 0]
high_scores = df[df["score"] > 100]

print(low_scores)
print(high_scores)
```

## 7. Comparing Groups

Statistics becomes more useful when we compare groups. For example, we may compare average score by department.

```python
department_stats = df.groupby("department")["score"].agg(["count", "mean", "median", "std", "min", "max"])
print(department_stats)
```

When comparing groups, we should look at both the average and the number of records. A group with only one or two records may not be reliable.

## 8. Correlation

Correlation measures the relationship between two numeric variables. It ranges from -1 to 1.

| Correlation | Meaning |
|---|---|
| Close to 1 | Strong positive relationship |
| Close to -1 | Strong negative relationship |
| Close to 0 | Weak or no linear relationship |

```python
correlation = df["attendance"].corr(df["score"])
print(correlation)
```

Correlation does not prove causation. If attendance and score are related, we cannot immediately say attendance caused the score to increase. Other factors may be involved.

## 9. Simple Statistical Report

A statistical report should include both numbers and interpretation. Students should explain what the statistics mean in plain language.

```python
summary = df[["score", "attendance"]].describe()
print(summary)

department_summary = df.groupby("department")["score"].agg(["count", "mean", "std"])
print(department_summary)

print(df["attendance"].corr(df["score"]))
```

## 10. Week 5 Summary

Week 5 introduced the statistical foundations needed for data science. Students learned how to summarize central tendency, measure variation, inspect distributions, identify outliers, compare groups, and interpret correlation carefully. These ideas prepare students for machine learning, where statistical thinking helps us understand data and evaluate results.



---

**Next:** [Lab →](lab.ipynb) | [Assignment →](assignment.ipynb)

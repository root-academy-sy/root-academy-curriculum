# Week 4 — Data Visualization with Matplotlib and Seaborn

**Course:** Introduction to Data Science
**Week Topic:** Build a Visual Report

## Main Goal

Week 4 teaches students how to communicate data using charts. Students will learn how to choose the right chart type, create visualizations with Matplotlib and Seaborn, improve chart readability, and write short interpretations.

- Explain why visualization is important in data science.
- Choose appropriate chart types for different questions.
- Create bar charts, line charts, histograms, box plots, and scatter plots.
- Use Matplotlib for basic plotting control.
- Use Seaborn for statistical visualizations.
- Add titles, labels, legends, and readable formatting.
- Build a simple visual report from a cleaned dataset.

## 1. Why Data Visualization Matters

Data visualization helps people understand patterns quickly. Tables are useful, but charts often make trends, comparisons, distributions, and unusual values easier to see.

A good chart can answer a question clearly. A poor chart can confuse the audience or even lead to wrong conclusions. The goal is not to create decoration. The goal is to communicate information honestly and clearly.

## 2. Choosing the Right Chart

| Question | Good Chart Type |
|---|---|
| Compare categories | Bar chart |
| Show change over time | Line chart |
| Show distribution | Histogram or box plot |
| Show relationship between two numeric variables | Scatter plot |
| Compare distributions across groups | Box plot |
| Show counts by category | Count plot |

## 3. Matplotlib Basics

Matplotlib is a foundational Python visualization library. It gives detailed control over charts. Many other libraries are built on top of it.

```python
import matplotlib.pyplot as plt

departments = ["IT", "HR", "Finance", "Marketing"]
average_scores = [85, 78, 90, 82]

plt.bar(departments, average_scores)
plt.title("Average Score by Department")
plt.xlabel("Department")
plt.ylabel("Average Score")
plt.show()
```

The plt.show() command displays the chart. In Jupyter Notebook, charts often appear automatically, but using plt.show() is still a good habit for beginners.

## 4. Line Charts

Line charts are useful for showing change over time.

```python
months = ["Jan", "Feb", "Mar", "Apr", "May"]
sales = [1200, 1500, 1400, 1800, 2100]

plt.plot(months, sales, marker="o")
plt.title("Monthly Sales")
plt.xlabel("Month")
plt.ylabel("Sales")
plt.show()
```

## 5. Histograms

A histogram shows the distribution of a numeric variable. It helps us see whether values are low, high, spread out, or concentrated.

```python
plt.hist(df["score"], bins=10)
plt.title("Distribution of Scores")
plt.xlabel("Score")
plt.ylabel("Number of Employees")
plt.show()
```

## 6. Scatter Plots

A scatter plot shows the relationship between two numeric variables. Each point represents one record.

```python
plt.scatter(df["attendance"], df["score"])
plt.title("Attendance vs Score")
plt.xlabel("Attendance")
plt.ylabel("Score")
plt.show()
```

Scatter plots help us see whether two variables may be related. However, a visible relationship does not automatically prove causation.

## 7. Seaborn Basics

Seaborn is a visualization library built on top of Matplotlib. It is useful for creating clean statistical charts with less code.

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.barplot(data=df, x="department", y="score")
plt.title("Average Score by Department")
plt.show()
```

## 8. Count Plots

A count plot shows how many records belong to each category.

```python
sns.countplot(data=df, x="performance_category")
plt.title("Number of Employees by Performance Category")
plt.xlabel("Performance Category")
plt.ylabel("Count")
plt.xticks(rotation=30)
plt.show()
```

## 9. Box Plots

A box plot summarizes the distribution of a numeric variable and can help detect outliers. It is especially useful when comparing groups.

```python
sns.boxplot(data=df, x="department", y="score")
plt.title("Score Distribution by Department")
plt.xlabel("Department")
plt.ylabel("Score")
plt.show()
```

## 10. Pairing Charts with Questions

Students should avoid making random charts. Each chart should answer a question.

| Question | Chart |
|---|---|
| Which department has the highest average score? | Bar chart |
| How are scores distributed? | Histogram |
| Are there score outliers by department? | Box plot |
| Is attendance related to score? | Scatter plot |
| How many employees are in each category? | Count plot |

## 11. Improving Chart Readability

- Use a clear title.
- Label the x-axis and y-axis.
- Avoid overcrowded charts.
- Rotate long category labels when needed.
- Use colors to clarify, not distract.
- Start with simple charts before adding styling.
- Make sure the chart answers one main question.
```python
plt.figure(figsize=(8, 5))
sns.barplot(data=df, x="department", y="score")
plt.title("Average Employee Score by Department")
plt.xlabel("Department")
plt.ylabel("Average Score")
plt.xticks(rotation=30)
plt.tight_layout()
plt.show()
```

## 12. Saving Charts

Charts can be saved as image files and included in reports or presentations.

```python
plt.figure(figsize=(8, 5))
sns.histplot(data=df, x="score", bins=10)
plt.title("Distribution of Employee Scores")
plt.xlabel("Score")
plt.ylabel("Count")
plt.tight_layout()
plt.savefig("score_distribution.png", dpi=300)
plt.show()
```

## 13. Writing Chart Interpretations

A visual report should include short interpretations. Students should explain what the chart shows and why it matters.

Weak interpretation: This is a chart of scores.

Stronger interpretation: Most employee scores are between 70 and 90, with a small number above 90. This suggests performance is generally satisfactory, but only a few employees are in the excellent range.

## 14. Mini Visual Report Workflow

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv("data/employee_data_cleaned.csv")

plt.figure(figsize=(8, 5))
sns.barplot(data=df, x="department", y="score")
plt.title("Average Score by Department")
plt.xlabel("Department")
plt.ylabel("Average Score")
plt.tight_layout()
plt.show()

plt.figure(figsize=(8, 5))
sns.histplot(data=df, x="score", bins=10)
plt.title("Distribution of Scores")
plt.xlabel("Score")
plt.ylabel("Count")
plt.tight_layout()
plt.show()

plt.figure(figsize=(8, 5))
sns.scatterplot(data=df, x="attendance", y="score", hue="department")
plt.title("Attendance vs Score")
plt.xlabel("Attendance")
plt.ylabel("Score")
plt.tight_layout()
plt.show()
```

## 15. Common Beginner Mistakes

- Creating a chart without a clear question.
- Forgetting titles and axis labels.
- Using a pie chart when a bar chart would be clearer.
- Using too many colors.
- Not rotating long category labels.
- Interpreting correlation as causation.
- Showing too many variables in one chart.

## 16. Week 4 Summary

Week 4 focused on communicating data visually. Students learned how to choose chart types, create visualizations with Matplotlib and Seaborn, improve readability, save charts, and write interpretations. These skills prepare students to produce clearer EDA reports and later explain machine learning results more effectively.



---

**Next:** [Lab →](lab.ipynb) | [Assignment →](assignment.ipynb)

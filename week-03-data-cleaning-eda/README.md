# Week 3 — Data Cleaning and Exploratory Data Analysis

**Course:** Introduction to Data Science
**Week Topic:** Build a Full EDA Notebook

## Main Goal

Week 3 teaches students how to move from simply loading a dataset to understanding it deeply. Students will learn the practical workflow of data cleaning and exploratory data analysis, usually called EDA.

By the end of this week, students should be able to inspect a dataset, identify data quality problems, clean common issues, ask useful analytical questions, calculate summaries, and organize their work in a complete notebook.

- Understand the purpose of exploratory data analysis.
- Describe common data quality problems.
- Inspect missing values, duplicates, inconsistent categories, and outliers.
- Clean text, numeric, and categorical columns.
- Use summary statistics to understand a dataset.
- Ask and answer basic analytical questions using Pandas.
- Write clear notes inside a notebook to explain each step.

## 1. What Is Exploratory Data Analysis?

Exploratory Data Analysis is the process of investigating a dataset before building reports, dashboards, or machine learning models. EDA helps us understand what the data contains, what problems exist, and what patterns may be useful.

EDA is not only about writing code. It is also about asking questions. A data scientist should constantly ask what each column means, whether the values make sense, whether there are missing or duplicated records, and what the data can or cannot tell us.

## 2. Why Data Cleaning Comes Before Analysis

Real datasets are rarely clean. They may contain missing values, inconsistent names, impossible values, duplicated rows, wrong data types, and spelling differences. If we analyze messy data without cleaning it, our conclusions may be wrong.

For example, if a department appears as IT, it, I.T., and Information Technology, Pandas will treat them as different departments. A simple groupby analysis would produce misleading results.

## 3. Common Data Quality Problems

| Problem | Example | Possible Fix |
|---|---|---|
| Missing values | Blank score | Fill, remove, or investigate |
| Duplicates | Same employee repeated | Remove if truly duplicated |
| Wrong data type | Score stored as text | Convert to numeric |
| Inconsistent categories | HR and Human Resources | Standardize labels |
| Extra spaces | IT | Use strip() |
| Outliers | Age = 250 | Investigate and decide |

## 4. The EDA Workflow

- Load the dataset.
- Inspect rows, columns, data types, and basic summaries.
- Check missing values and duplicates.
- Clean column names and values.
- Fix data types.
- Handle missing values.
- Investigate outliers and unusual values.
- Create useful new columns.
- Ask questions and calculate summaries.
- Write conclusions.

## 5. Loading and Inspecting Data

```python
import pandas as pd

df = pd.read_csv("data/employee_data.csv")

print(df.head())
print(df.shape)
print(df.info())
print(df.describe())
```

The goal of this first step is to understand the basic structure of the dataset. Students should avoid cleaning immediately before they understand the columns and values.

## 6. Cleaning Column Names

Column names should be consistent and easy to type. A good style is lowercase with underscores.

```python
df.columns = df.columns.str.strip()
df.columns = df.columns.str.lower()
df.columns = df.columns.str.replace(" ", "_")

print(df.columns)
```

## 7. Checking Missing Values

```python
missing_counts = df.isna().sum()
missing_percent = (df.isna().mean() * 100).round(2)

missing_summary = pd.DataFrame({
    "missing_count": missing_counts,
    "missing_percent": missing_percent
})

print(missing_summary)
```

Missing values should be handled carefully. Removing rows is simple but may remove too much information. Filling values is useful, but students should explain why the chosen method makes sense.

## 8. Handling Missing Values

```python
df["score"] = df["score"].fillna(df["score"].median())
df["department"] = df["department"].fillna("Unknown")

df = df.dropna(subset=["employee_id"])
```

In this example, missing scores are filled with the median score, missing departments are labeled Unknown, and rows without an employee ID are removed because the ID is essential.

## 9. Checking and Removing Duplicates

```python
print(df.duplicated().sum())

duplicates = df[df.duplicated()]
print(duplicates)

df = df.drop_duplicates()
```

Students should inspect duplicates before removing them. Sometimes repeated rows are errors; other times they may represent repeated events.

## 10. Cleaning Text Values

Before cleaning, it helps to look at what is actually inside a column. This is how we spot the problem in the first place.

```python
print(df["department"].unique())
print(df["department"].value_counts())
```

This might show something like `IT`, `it`, `I.T.`, and `Information Technology` — four different spellings of the same department. Now that we've seen the problem, we can fix it.

```python
df["department"] = df["department"].str.strip()
df["department"] = df["department"].str.upper()

df["department"] = df["department"].replace({
    "HUMAN RESOURCES": "HR",
    "I.T.": "IT",
    "INFORMATION TECHNOLOGY": "IT"
})
```

Text cleaning is especially important for categorical analysis. Inconsistent categories create incorrect summaries.

## 11. Fixing Data Types

```python
df["score"] = pd.to_numeric(df["score"], errors="coerce")
df["attendance"] = pd.to_numeric(df["attendance"], errors="coerce")
df["hire_date"] = pd.to_datetime(df["hire_date"], errors="coerce")
```

The errors='coerce' option changes invalid values into missing values. After using it, students should check missing values again.

## 12. Detecting Outliers

An outlier is a value that is very different from most other values. Outliers are not always mistakes, but they should be investigated.

```python
print(df["score"].describe())

very_low_scores = df[df["score"] < 0]
very_high_scores = df[df["score"] > 100]

print(very_low_scores)
print(very_high_scores)
```

For a score column expected to be between 0 and 100, values below 0 or above 100 are probably invalid.

**Common mistake:** Don't delete an outlier just because it looks big or unusual. First check if it's realistic. An age of 250 is clearly an error, but a salary that looks unusually high might just belong to a senior employee. Investigate before deciding.

## 13. Creating New Columns

```python
def performance_category(score):
    if score >= 90:
        return "Excellent"
    elif score >= 80:
        return "Good"
    elif score >= 60:
        return "Satisfactory"
    else:
        return "Needs Improvement"

df["performance_category"] = df["score"].apply(performance_category)
df["attendance_flag"] = df["attendance"] >= 80
```

New columns help transform raw data into information that is easier to analyze and explain.

## 14. Asking Good EDA Questions

- How many records and columns does the dataset contain?
- Which columns have missing values?
- What is the average score?
- Which department has the highest average score?
- How many employees are in each performance category?
- Is attendance related to performance?
- Are there unusual or impossible values?

## 15. Answering Questions with Pandas

```python
print(df["score"].mean())
print(df["performance_category"].value_counts())

department_summary = df.groupby("department")["score"].agg(["count", "mean", "min", "max"])
print(department_summary)

attendance_summary = df.groupby("attendance_flag")["score"].mean()
print(attendance_summary)

correlation = df["score"].corr(df["attendance"])
print(correlation)
```

The correlation is a number between -1 and 1. A value close to 1 means high attendance tends to go with high scores. A value close to 0 means there isn't much of a relationship. This directly answers the question from section 14: is attendance related to performance?

**Common mistake:** Don't fill in missing values right away without asking why they're missing. A missing score might be random, or it might mean something specific, like an employee who joined too recently to be reviewed. Think about the reason before choosing fillna or dropna.

## 16. Writing EDA Notes

A good EDA notebook should not be only code. It should include short explanations before and after important steps. Students should write what they are checking, what they found, and what decision they made.

Example note: The score column had two missing values. Because the number of missing values was small and the score distribution was not strongly affected, we filled missing scores using the median score.

## 17. Mini Case Study: Employee EDA

Students will work with an employee dataset containing employee name, department, score, attendance, hire date, and salary. The goal is to clean the dataset and produce a short EDA summary.

```python
import pandas as pd

df = pd.read_csv("data/employee_data.csv")

df.columns = df.columns.str.strip().str.lower().str.replace(" ", "_")
df = df.drop_duplicates()

df["department"] = df["department"].str.strip().str.upper()
df["department"] = df["department"].replace({
    "HUMAN RESOURCES": "HR",
    "INFORMATION TECHNOLOGY": "IT",
    "I.T.": "IT"
})

df["score"] = pd.to_numeric(df["score"], errors="coerce")
df["attendance"] = pd.to_numeric(df["attendance"], errors="coerce")

df["score"] = df["score"].fillna(df["score"].median())
df["attendance"] = df["attendance"].fillna(df["attendance"].median())

def performance_category(score):
    if score >= 90:
        return "Excellent"
    elif score >= 80:
        return "Good"
    elif score >= 60:
        return "Satisfactory"
    else:
        return "Needs Improvement"

df["performance_category"] = df["score"].apply(performance_category)

print(df.groupby("department")["score"].mean())
print(df["performance_category"].value_counts())
```

## 18. EDA Checklist

Before considering your notebook complete, check that you can answer all of these:

- [ ] How many rows and columns does the dataset have?
- [ ] Which columns had missing values, and what did you do about them?
- [ ] Were there any duplicate rows? Did you remove them?
- [ ] Are all columns the correct data type (numbers as numbers, dates as dates)?
- [ ] Did you find any outliers? What did you decide to do with them?
- [ ] Did you answer at least three of the analytical questions from section 14?
- [ ] Did you write short notes explaining your decisions?

## 19. Week 3 Summary

Week 3 focused on the practical workflow of data cleaning and exploratory data analysis. Students learned how to inspect data, clean common issues, create useful columns, ask analytical questions, and organize findings in a notebook. These skills prepare students for Week 4, where they will turn analysis results into visual reports.



---

**Next:** [Lab →](lab.ipynb) | [Assignment →](assignment.ipynb)

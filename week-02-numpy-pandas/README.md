# Week 2 — Python for Data Science: NumPy and Pandas

**Course:** Introduction to Data Science
**Week Topic:** Load and Clean a Real Dataset

## Main Goal

In Week 1, we used basic Python structures such as lists, dictionaries, loops, functions, and files. This week, we move from basic Python to the two most important Python libraries for data science: **NumPy** and **Pandas**.

The goal is to understand how data scientists load, inspect, clean, and summarize tabular data — and to start thinking of data as rows and columns rather than only as individual variables or lists.

By the end of this week, you should be able to:

- Explain why NumPy and Pandas are useful in data science
- Create and use NumPy arrays for numerical data
- Load a CSV file into a Pandas DataFrame
- Inspect a dataset using common Pandas commands
- Select columns and filter rows
- Identify missing values and duplicated rows
- Clean simple messy data
- Create new columns from existing columns
- Calculate basic summaries using Pandas

## 1. From Plain Python to Data Science Libraries

In Week 1, we represented a small dataset as a list of dictionaries:

```python
students = [
    {"name": "Ali", "department": "IT", "grade": 85},
    {"name": "Maya", "department": "HR", "grade": 92},
    {"name": "Sara", "department": "IT", "grade": 78}
]
```

This works for a few records, but imagine 10,000 students, 30 columns, missing values, and mixed data types — writing loops for every operation would become slow and hard to maintain.

Data science libraries solve this. They provide ready-made tools for common data tasks: loading files, selecting columns, filtering rows, calculating summaries, and cleaning missing values.

Two libraries matter most at the beginning:

- **NumPy** — fast numerical calculations and arrays
- **Pandas** — working with tabular data such as CSV and Excel files

## 2. What Is NumPy?

NumPy is a Python library for numerical computing. Its main object is the **array** — similar to a Python list, but designed for fast mathematical operations.

A normal Python list:
```python
grades = [80, 90, 75, 88]
```

A NumPy array:
```python
import numpy as np

grades = np.array([80, 90, 75, 88])
print(grades)
```

The convention is to import NumPy as `np` — not required by Python, but standard style among data scientists.

## 3. Why NumPy Is Useful

With a normal Python list, adding 5 points to every grade requires a loop:
```python
grades = [80, 90, 75, 88]
new_grades = []

for grade in grades:
    new_grades.append(grade + 5)

print(new_grades)
```

With NumPy, the operation applies directly to the entire array:
```python
import numpy as np

grades = np.array([80, 90, 75, 88])
new_grades = grades + 5
print(new_grades)
```

This is called **vectorized computation** — applying an operation to many values at once. Vectorized operations are usually faster and easier to read.

NumPy also provides useful statistical functions:
```python
import numpy as np

grades = np.array([80, 90, 75, 88])
print(np.mean(grades))
print(np.median(grades))
print(np.min(grades))
print(np.max(grades))
print(np.std(grades))
```

These calculate the mean, median, minimum, maximum, and standard deviation — common summaries in data analysis.

## 4. NumPy Arrays

A NumPy array can be one-dimensional or multi-dimensional. A one-dimensional array looks like a simple list of values:
```python
import numpy as np

scores = np.array([70, 85, 90, 60])
print(scores)
```

A two-dimensional array looks like a table or matrix:
```python
data = np.array([
    [85, 90, 88],
    [70, 75, 80],
    [92, 95, 91]
])
print(data)
```

Here, each row could represent one student, and each column one exam. Use `.shape` to check an array's dimensions:
```python
print(data.shape)
```

A shape of `(3, 3)` means 3 rows and 3 columns.

## 5. What Is Pandas?

Pandas is a Python library for data analysis — one of the most important tools in data science because it makes working with tables easy.

The main Pandas object is the **DataFrame** — like a table with rows and columns, similar to an Excel sheet or database table. The convention is to import Pandas as `pd`.

```python
import pandas as pd
```

A DataFrame can be created manually from a dictionary:
```python
import pandas as pd

data = {
    "name": ["Ali", "Maya", "Sara"],
    "department": ["IT", "HR", "IT"],
    "score": [85, 92, 78]
}

df = pd.DataFrame(data)
print(df)
```

In real data science work, we usually load data from a file instead of typing it manually.

## 6. Loading CSV Files

A CSV file is a comma-separated values file — one of the most common formats for tabular data. Each row is one record, columns separated by commas.

Example CSV data:
```
name,department,score,attendance
Ali,IT,85,90
Maya,HR,92,95
Sara,IT,78,80
```

To load a CSV file into Pandas, use `read_csv()`:
```python
import pandas as pd

df = pd.read_csv("employee_scores.csv")
print(df)
```

After loading, `df` becomes a DataFrame — the name `df` is commonly used because it stands for DataFrame. Datasets should be placed in the same folder as the notebook/script, or use the correct file path.

## 7. Inspecting a Dataset

After loading a dataset, the first step is **inspection**, not cleaning or modeling — we need to understand what the dataset contains.

| Command | Purpose |
|---|---|
| `df.head()` | Shows the first 5 rows |
| `df.tail()` | Shows the last 5 rows |
| `df.shape` | Shows number of rows and columns |
| `df.columns` | Shows column names |
| `df.info()` | Shows column types and missing values |
| `df.describe()` | Shows summary statistics for numeric columns |

```python
print(df.head())
print(df.shape)
print(df.columns)
print(df.info())
print(df.describe())
```

A good data scientist inspects data before doing analysis — this helps prevent mistakes caused by wrong assumptions.

## 8. Understanding Rows, Columns, and Data Types

A DataFrame is made of rows and columns. Each row usually represents one record; each column represents one variable or feature.

| Column | Meaning |
|---|---|
| name | Employee name |
| department | Employee department |
| score | Performance score |
| attendance | Attendance percentage |

Common Pandas data types:

- `int64` — whole numbers
- `float64` — decimal numbers
- `object` — usually text
- `bool` — True or False values
- `datetime64` — dates and times

Data types matter because calculations only work correctly when values are stored in the right format — a numeric column stored as text may need converting before analysis.

## 9. Selecting Columns

Select one column:
```python
scores = df["score"]
print(scores)
```

Select multiple columns using a list of column names:
```python
selected = df[["name", "score"]]
print(selected)
```

## 10. Filtering Rows

Filtering means selecting rows that match a condition — one of the most common data analysis tasks.

Employees with score ≥ 80:
```python
high_scores = df[df["score"] >= 80]
print(high_scores)
```

Employees from the IT department:
```python
it_employees = df[df["department"] == "IT"]
print(it_employees)
```

Combine conditions using `&` (and) and `|` (or) — each condition in parentheses:
```python
strong_attendance = df[(df["score"] >= 80) & (df["attendance"] >= 90)]
print(strong_attendance)
```

## 11. Missing Values

Real datasets often contain missing values — information may not have been collected, entered incorrectly, lost during transfer, or not applicable. In Pandas, missing values often appear as `NaN` (Not a Number).

Check missing values:
```python
print(df.isna())
print(df.isna().sum())
```

The first shows True/False per cell; the second counts missing values per column.

Common ways to handle missing values:

- Remove rows with missing values
- Fill missing numeric values with the mean or median
- Fill missing text values with a label such as `"Unknown"`
- Leave missing values if they're meaningful and will be handled later

```python
# Drop rows with missing values
df_clean = df.dropna()

# Fill missing scores with the average score
average_score = df["score"].mean()
df["score"] = df["score"].fillna(average_score)

# Fill missing departments with "Unknown"
df["department"] = df["department"].fillna("Unknown")
```

There's no single correct method — the best choice depends on the meaning of the data and the purpose of the analysis.

## 12. Duplicated Rows

A duplicated row appears more than once in a dataset, which can skew analysis by counting the same record multiple times.

```python
# Check duplicated rows
print(df.duplicated().sum())

# Remove duplicated rows
df = df.drop_duplicates()
```

Before removing duplicates, check whether they're truly mistakes — in some datasets, similar-looking rows may represent different events.

## 13. Renaming Columns

Column names should be clear and easy to use. Messy names may contain spaces, capital letters, or unclear labels.

```python
df = df.rename(columns={
    "Employee Name": "name",
    "Dept": "department",
    "Performance Score": "score"
})
```

A common practice is lowercase column names with underscores — easier to write and read.

## 14. Changing Data Types

Numeric data is sometimes stored as text, often due to symbols, spaces, or inconsistent formatting in the original file.

```python
# Check data types
print(df.dtypes)

# Convert a column to numeric
df["score"] = pd.to_numeric(df["score"])
```

If some values can't convert, use `errors='coerce'` — invalid values become missing values:
```python
df["score"] = pd.to_numeric(df["score"], errors="coerce")
print(df["score"].isna().sum())  # check for new missing values after conversion
```

## 15. Creating New Columns

Creating new columns is called **feature engineering** — building useful new information from existing data.

```python
# A pass column based on score
df["passed"] = df["score"] >= 60

# A total score from two columns
df["final_score"] = (df["score"] * 0.7) + (df["attendance"] * 0.3)

# A category using a function
def classify_score(score):
    if score >= 90:
        return "Excellent"
    elif score >= 80:
        return "Good"
    elif score >= 60:
        return "Satisfactory"
    else:
        return "Needs Improvement"

df["category"] = df["score"].apply(classify_score)
```

`apply()` applies a function to each value in a column.

## 16. Sorting Data

```python
# Lowest to highest
df_sorted = df.sort_values("score")

# Highest to lowest
df_sorted = df.sort_values("score", ascending=False)
```

Sorting is useful for finding top performers, lowest values, recent dates, or priority records.

## 17. Grouping and Summarizing Data

Grouping lets us calculate summaries by category — e.g. average score by department:
```python
department_average = df.groupby("department")["score"].mean()
```

Multiple summaries at once:
```python
summary = df.groupby("department")["score"].agg(["count", "mean", "min", "max"])
print(summary)
```

Grouping is one of the most powerful ideas in data analysis — it lets us compare groups instead of only looking at the whole dataset.

## 18. Saving Cleaned Data

After cleaning, save the cleaned version so it can be reused without repeating the cleaning steps:
```python
df.to_csv("employee_scores_cleaned.csv", index=False)
```

`index=False` prevents Pandas from saving the DataFrame index as an extra column. In real projects, keep the original raw dataset unchanged and save a separate cleaned dataset.

## 19. Mini Case Study: Cleaning Employee Scores

Loading a messy employee dataset, inspecting it, cleaning it, and calculating useful summaries.

Example messy CSV file:
```
Employee Name,Dept,Score,Attendance
Ali,IT,88,92
Maya,HR,74,85
Omar,Finance,91,90
Lina,IT,,78
Sara,HR,95,
Ali,IT,88,92
```

**Step 1: Load the dataset**
```python
import pandas as pd

df = pd.read_csv("employee_scores.csv")
```

**Step 2: Inspect the dataset**
```python
print(df.head())
print(df.shape)
print(df.info())
print(df.isna().sum())
print(df.duplicated().sum())
```

**Step 3: Rename columns**
```python
df = df.rename(columns={
    "Employee Name": "name",
    "Dept": "department",
    "Score": "score",
    "Attendance": "attendance"
})
```

**Step 4: Remove duplicates**
```python
df = df.drop_duplicates()
```

**Step 5: Handle missing values**
```python
df["score"] = df["score"].fillna(df["score"].mean())
df["attendance"] = df["attendance"].fillna(df["attendance"].mean())
```

**Step 6: Create a performance category**
```python
def classify_score(score):
    if score >= 90:
        return "Excellent"
    elif score >= 80:
        return "Good"
    elif score >= 60:
        return "Satisfactory"
    else:
        return "Needs Improvement"

df["category"] = df["score"].apply(classify_score)
```

**Step 7: Calculate summaries**
```python
print(df["score"].mean())
print(df["score"].max())
print(df["score"].min())

department_summary = df.groupby("department")["score"].agg(["count", "mean", "min", "max"])
print(department_summary)
```

**Step 8: Save the cleaned dataset**
```python
df.to_csv("employee_scores_cleaned.csv", index=False)
```

This case study introduces the main workflow you'll repeat many times in data science: **load, inspect, clean, transform, summarize, and save.**

## 20. Good Habits When Working With Data

- Always inspect the dataset before cleaning it
- Do not change the original raw data file
- Use clear variable names
- Check data types before calculating
- Check missing values before and after cleaning
- Be careful before removing rows
- Document the cleaning steps so another person can understand what was done
- Save the cleaned dataset with a clear filename

## 21. Common Beginner Mistakes

**Forgetting to import the library**
```python
# Incorrect
df = pd.read_csv("data.csv")

# Correct
import pandas as pd
df = pd.read_csv("data.csv")
```

**Wrong file path** — if Pandas can't find the file, it raises a `FileNotFoundError`. Make sure the file is in the same folder as the notebook, or provide the correct path.

**Confusing parentheses and brackets**
```python
df["score"]   # select a column — square brackets
df.head()     # call a method — parentheses
```

**Not checking missing values** — if ignored, averages and models may be affected. Always check with `isna().sum()`.

**Overwriting data too early** — beginners sometimes overwrite the original DataFrame before understanding the data. Inspect first, then clean step by step.

## 22. Week 2 Summary

This week, we moved from basic Python to practical data science tools. NumPy introduced fast numerical arrays and vectorized calculations. Pandas introduced the DataFrame, the main structure for working with tabular data.

We learned how to load a CSV file, inspect a dataset, select columns, filter rows, check missing values, remove duplicates, rename columns, change data types, create new columns, group data, and save a cleaned dataset.

These skills are the foundation for Week 3, where we'll use data cleaning and exploratory data analysis to build a full EDA notebook.

---

**Next:** [Lab →](lab.ipynb) | [Assignment →](assignment.ipynb)

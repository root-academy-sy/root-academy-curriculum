# Week 1 — Python Foundations for Data Science

**Course:** Introduction to Data Science
**Week Topic:** Python Foundations Refresher

## Main Goal

This week, we review and practice the most important Python concepts needed for data science. The goal isn't to learn every detail of Python, but to become comfortable with the parts of Python that are used repeatedly when working with data.

By the end of this week, you should be able to:

- Understand what data science is and how Python is used in data science
- Write and run simple Python programs
- Use variables and basic data types
- Work with strings, lists, and dictionaries
- Use conditions and loops to process data
- Write simple functions
- Read from and write to files
- Build a small Python program that analyzes simple data

## 1. What Is Data Science?

Data science is the process of using data to understand problems, discover patterns, make decisions, and sometimes make predictions.

Organizations collect large amounts of data every day — from students, employees, customers, websites, financial systems, hospital records, surveys, or machines. Raw data by itself is usually not useful: it may be messy, incomplete, difficult to understand, or too large to analyze manually. Data science helps turn raw data into useful information.

For example, data science can help answer questions such as:

- Which students are at risk of failing a course?
- What are the most common reasons employees leave a company?
- Which product is selling the most?
- How can we predict future sales?
- Which customers are likely to stop using a service?
- How can we detect unusual behavior in financial transactions?

A typical data science project follows several steps:

1. **Collect data** — gathered from files, databases, surveys, websites, sensors, or other systems
2. **Clean data** — real data often contains missing values, spelling mistakes, duplicated records, or incorrect formats
3. **Explore data** — calculate summaries, compare groups, and search for patterns
4. **Visualize data** — charts and graphs help reveal trends, relationships, and unusual values
5. **Build models** — in some projects, machine learning models are used to make predictions or classify new cases
6. **Communicate results** — explain findings clearly so people can make better decisions

Python is one of the most popular languages for data science because it's readable, flexible, and supported by powerful libraries such as NumPy, Pandas, Matplotlib, Seaborn, and Scikit-learn. This course starts with Python basics, then gradually moves toward real data analysis and machine learning.

## 2. Why Python for Data Science?

Python is widely used in data science because it's easy to read and has many tools for working with data:

- Simple syntax compared to many other programming languages
- Works for small scripts and large applications alike
- Strong libraries for data analysis and machine learning
- Works well with files such as CSV, Excel, text files, and databases
- Used by companies, universities, researchers, and software developers

A simple example — calculating an average:

```python
grades = [80, 90, 75, 88]
average = sum(grades) / len(grades)
print(average)
```

This stores a list of grades, calculates the average, and prints the result. Later, we'll use libraries such as Pandas to do this more efficiently with real datasets — but understanding the Python foundations behind them comes first.

## 3. Running Python Code

Python code can be written and executed in different environments. The two most common for this course:

**Python script files** — a file ending in `.py`, useful for a complete program:

```python
name = "Ali"
grade = 85

print(name)
print(grade)
```

**Jupyter Notebook** — an interactive environment where code is written in cells that run separately. Notebooks are very popular in data science because they combine code, explanations, tables, charts, and results — great for analysis and reporting.

**`print()`** displays output on the screen:

```python
print("Welcome to Data Science")
```
```
Welcome to Data Science
```

## 4. Variables

A variable is a name used to store a value.

```python
student_name = "Maya"
student_age = 22
student_grade = 87.5
```

Variables make programs easier to understand and reuse — instead of writing the same value many times, we store it once and use the variable name.

```python
price = 20
quantity = 3
total = price * quantity
print(total)
```
```
60
```

In data science, variables store values, datasets, calculations, and results. **Good variable names matter** — a variable name should describe what the value represents.

Good examples:
```python
student_count = 30
average_score = 82.5
department_name = "IT"
```

Poor examples:
```python
x = 30
a = 82.5
thing = "IT"
```

Short names like `x` are sometimes acceptable in mathematics, but descriptive names are better for readable code.

## 5. Basic Data Types

**Integer** — a whole number:
```python
age = 25
number_of_students = 40
```

**Float** — a decimal number:
```python
average_grade = 86.7
salary = 1500.50
```

**String** — text, written inside quotation marks:
```python
name = "Sara"
department = "Computer Science"
```

**Boolean** — either `True` or `False`, useful for decisions:
```python
passed = True
is_absent = False

grade = 75
passed = grade >= 60
print(passed)
```
```
True
```

Understanding data types matters — if a number is stored as text, Python may not calculate with it correctly:

```python
grade = "85"        # stored as text
grade = int("85")   # converted to an integer so Python can use it in calculations
```

## 6. Operators and Expressions

**Arithmetic operators:**
```python
a = 10
b = 3
print(a + b)   # addition
print(a - b)   # subtraction
print(a * b)   # multiplication
print(a / b)   # division
print(a // b)  # integer division
print(a % b)   # remainder
print(a ** b)  # exponent
```

**Comparison operators** compare two values and return `True` or `False`:
```python
grade = 85
print(grade > 80)
print(grade < 60)
print(grade == 85)
print(grade != 90)
```

A common beginner mistake is confusing `=` (assignment) with `==` (comparison).

**Logical operators** (`and`, `or`, `not`) combine conditions:
```python
grade = 85
attendance = 90
print(grade >= 60 and attendance >= 70)

score = 75
print(score >= 60 and score < 90)  # checks whether score is between 60 and 89
```

## 7. Strings

A string is a sequence of characters, used for text data — names, departments, cities, product names, categories, and so on.

```python
student_name = "Lina"
course_name = "Introduction to Data Science"
```

**Concatenation** joins strings together:
```python
first_name = "Ali"
last_name = "Hassan"
full_name = first_name + " " + last_name
print(full_name)
```

**f-strings** insert variables into text:
```python
name = "Maya"
grade = 88
print(f"{name} scored {grade}")
```

**Common string methods:**
```python
text = "  Data Science  "
print(text.lower())    # lowercase
print(text.upper())    # uppercase
print(text.strip())    # removes extra spaces from the start/end

message = "Python is hard"
new_message = message.replace("hard", "powerful")
print(new_message)

line = "Ali,IT,88"
parts = line.split(",")
print(parts)
```

`split()` is especially important because many datasets are stored in text files where values are separated by commas.

## 8. Lists

A list stores a collection of values in one variable.

```python
grades = [85, 90, 78, 92, 66]
scores = [70, 85, 90]
names = ["Ali", "Maya", "Sara"]
student = ["Ali", 21, 85.5]
```

**Accessing items** by index (Python indexing starts at 0):
```python
grades = [85, 90, 78]
print(grades[0])
print(grades[1])
print(grades[2])
```

**Adding items** with `append()`:
```python
grades = [85, 90, 78]
grades.append(88)
print(grades)
```

**Useful built-in functions:**
```python
grades = [85, 90, 78, 92, 66]
print(len(grades))
print(sum(grades))
print(max(grades))
print(min(grades))

average = sum(grades) / len(grades)
print(average)
```

Lists are useful in data science because they let us store and process multiple values.

## 9. Dictionaries

A dictionary stores data as key-value pairs — useful for representing one record.

```python
student = {
    "name": "Rana",
    "age": 21,
    "grade": 87
}
```

**Accessing values:**
```python
print(student["name"])
print(student["grade"])
```

**Updating and adding values:**
```python
student["grade"] = 90
student["department"] = "Computer Science"
print(student)
```

**List of dictionaries** — in data science, a dataset can be represented as a list of dictionaries, where each dictionary is one record and the full list is the dataset:

```python
students = [
    {"name": "Ali", "grade": 85},
    {"name": "Maya", "grade": 92},
    {"name": "Sara", "grade": 78}
]
```

| name | grade |
|---|---|
| Ali | 85 |
| Maya | 92 |
| Sara | 78 |

Later, Pandas DataFrames will make this type of data much easier to manage.

## 10. Conditions

Conditions let a program make decisions using `if`.

```python
grade = 75
if grade >= 60:
    print("Passed")
```

**if-else:**
```python
grade = 55
if grade >= 60:
    print("Passed")
else:
    print("Failed")
```

**if-elif-else** for multiple conditions:
```python
score = 88
if score >= 90:
    print("Excellent")
elif score >= 80:
    print("Good")
elif score >= 60:
    print("Pass")
else:
    print("Fail")
```

Python checks conditions top to bottom and stops at the first true condition — order matters. Conditions are useful in data science for classification, such as pass/fail, high/medium/low, active/inactive, or normal/suspicious.

## 11. Loops

A loop repeats code — important because datasets usually contain many records, and loops let us process all of them automatically.

**`for` loop:**
```python
grades = [85, 90, 78, 92]
for grade in grades:
    print(grade)
```

**Looping through names:**
```python
names = ["Ali", "Maya", "Sara"]
for name in names:
    print(f"Hello, {name}")
```

**Counting with loops:**
```python
grades = [85, 45, 70, 55, 90]
passed_count = 0

for grade in grades:
    if grade >= 60:
        passed_count = passed_count + 1

print(passed_count)
```

**Looping through a list of dictionaries:**
```python
students = [
    {"name": "Ali", "grade": 85},
    {"name": "Maya", "grade": 92},
    {"name": "Sara", "grade": 58}
]

for student in students:
    print(student["name"], student["grade"])
```

## 12. Functions

A function is a reusable block of code that performs a specific task — it helps organize code and avoid repetition.

```python
def greet_student(name):
    print(f"Hello, {name}")

greet_student("Ali")
greet_student("Maya")
```

**Functions with return values:**
```python
def calculate_average(grades):
    average = sum(grades) / len(grades)
    return average

grades = [80, 90, 70]
result = calculate_average(grades)
print(result)
```

In data science, we often repeat the same operations — calculate an average, clean a text value, classify a score, count missing values, or calculate performance categories. Functions let us reuse that logic:

```python
def classify_score(score):
    if score >= 90:
        return "Excellent"
    elif score >= 80:
        return "Good"
    elif score >= 60:
        return "Pass"
    else:
        return "Fail"

print(classify_score(95))
print(classify_score(72))
print(classify_score(50))
```

Functions make code cleaner, easier to test, and easier to maintain.

## 13. File Input and Output

Data is often stored in files. Before using advanced tools like Pandas, it's useful to understand basic file reading and writing.

**Writing to a file:**
```python
file = open("summary.txt", "w")
file.write("Data Science Week 1 Summary")
file.close()
```
`"w"` means write mode — if the file already exists, it will be overwritten.

**Reading from a file:**
```python
file = open("summary.txt", "r")
content = file.read()
file.close()
print(content)
```

**Using `with open`** — automatically closes the file after use:
```python
with open("summary.txt", "w") as file:
    file.write("This file was created using Python.")

with open("summary.txt", "r") as file:
    content = file.read()

print(content)
```

**Reading lines from a file** — e.g. a file `grades.txt` with one grade per line:
```python
grades = []

with open("grades.txt", "r") as file:
    for line in file:
        grade = int(line.strip())
        grades.append(grade)

print(grades)
```

`strip()` removes extra spaces/newlines, `int()` converts text to a number, `append()` adds the grade to the list. File I/O matters because data science often begins with loading data from files.

## 14. Mini Case Study: Student Grade Analyzer

Using Python basics to analyze student grades, starting with a small dataset as a list of dictionaries — each dictionary represents one student, and the list represents the full dataset:

```python
students = [
    {"name": "Ali", "grade": 85},
    {"name": "Maya", "grade": 92},
    {"name": "Sara", "grade": 78},
    {"name": "Omar", "grade": 55},
    {"name": "Lina", "grade": 67}
]
```

**Step 1: Print all students**
```python
for student in students:
    print(student["name"], student["grade"])
```

**Step 2: Calculate the average grade**
```python
total = 0
for student in students:
    total = total + student["grade"]

average = total / len(students)
print(f"Average grade: {average}")
```

**Step 3: Find the highest and lowest grade**
```python
grades = []
for student in students:
    grades.append(student["grade"])

highest = max(grades)
lowest = min(grades)
print(f"Highest grade: {highest}")
print(f"Lowest grade: {lowest}")
```

**Step 4: Count passed and failed students**
```python
passed_count = 0
failed_count = 0

for student in students:
    if student["grade"] >= 60:
        passed_count = passed_count + 1
    else:
        failed_count = failed_count + 1

print(f"Passed students: {passed_count}")
print(f"Failed students: {failed_count}")
```

**Step 5: Classify each student**
```python
def classify_grade(grade):
    if grade >= 90:
        return "Excellent"
    elif grade >= 80:
        return "Good"
    elif grade >= 60:
        return "Pass"
    else:
        return "Fail"

for student in students:
    category = classify_grade(student["grade"])
    print(f"{student['name']} - {student['grade']} - {category}")
```

**Step 6: Write a summary to a file**
```python
with open("grade_summary.txt", "w") as file:
    file.write(f"Average grade: {average}\n")
    file.write(f"Highest grade: {highest}\n")
    file.write(f"Lowest grade: {lowest}\n")
    file.write(f"Passed students: {passed_count}\n")
    file.write(f"Failed students: {failed_count}\n")
```

This small example shows the basic logic behind data analysis: store data, loop through records, calculate summaries, classify values, and save results. In Week 2, we'll use NumPy and Pandas to do similar tasks more efficiently with real datasets.

## 15. Common Beginner Mistakes

**Forgetting quotation marks around strings**
```python
# Incorrect
name = Ali

# Correct
name = "Ali"
```

**Using `=` instead of `==`**
```python
# Incorrect
if grade = 90:
    print("Excellent")

# Correct
if grade == 90:
    print("Excellent")
```

**Wrong indentation**
```python
# Incorrect
if grade >= 60:
print("Passed")

# Correct
if grade >= 60:
    print("Passed")
```
Python uses indentation to understand which code belongs inside a condition, loop, or function.

**Mixing strings and numbers**
```python
# Incorrect
grade = "85"
new_grade = grade + 5

# Correct
grade = int("85")
new_grade = grade + 5
```

**Accessing a dictionary with the wrong key**
```python
# Incorrect
student = {"name": "Ali", "grade": 85}
print(student["score"])

# Correct
print(student["grade"])
```
The key must exist in the dictionary.

## 16. Week 1 Summary

This week, we reviewed the Python foundations needed for data science: data science is about using data to understand problems, discover patterns, and support decision-making. We practiced core Python concepts, including variables, data types, operators, strings, lists, dictionaries, conditions, loops, functions, and file input/output — and built a small student grade analyzer using plain Python.

These skills prepare us for working with real datasets. In Week 2, we'll move from basic Python structures to professional data science tools, especially NumPy and Pandas.

---

**Next:** [Lab →](lab.ipynb) | [Assignment →](assignment.ipynb)

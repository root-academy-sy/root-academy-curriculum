# Root Academy — Python for Data Science

An 8-week, project-based introductory curriculum that takes learners from Python
fundamentals to a comfortable, working data science workflow — loading data,
cleaning it, exploring it, visualizing it, understanding basic statistics, and
completing a guided mini project — using real-world style case studies (e.g.
employee performance analysis) as the backbone of each week's assignment and lab.

> 🔗 Website: [root-academy](https://github.com/mohamad-755/root-academy)

## Who this is for

- Beginners with little to no programming background who want a structured,
  hands-on path into data science with Python.
- Self-learners who want lecture notes, guided labs, and assignments (with
  solutions) in one place.

## What you'll be able to do by the end

- Write foundational Python for data work
- Load, clean, and explore real datasets with pandas
- Visualize data and communicate basic findings
- Understand core statistics concepts
- Build a small guided capstone project end-to-end

*This program is intentionally introductory — it builds real, usable skills
without going deep into advanced workflows (SQL, dashboards, hypothesis
testing, model tuning, portfolio-level projects). Those live in Root
Academy's next-level course for learners who want to go further.*

## Program structure

Each week follows the same four-part structure:

| Component | Purpose |
|---|---|
| **README (lecture notes)** | Core concepts and explanations for the week |
| **Lab** | Guided, hands-on practice completed during/after the lecture |
| **Lab Solution** | Reference solution to the lab |
| **Assignment** | Independent case-study exercise to reinforce the week's topic |
| **Assignment Solution** | Reference solution to the assignment |

## 8-Week Roadmap

| Week | Topic | Case Study / Theme |
|---|---|---|
| [Week 1](week-01-python-foundations/) | Python Foundations for Data Science | Employee Performance Analysis |
| [Week 2](week-02-numpy-pandas/) | NumPy and Pandas | Cleaning Employee Scores |
| Week 3 | [Data Cleaning and EDA](week-03-data-cleaning-eda/) | Employee EDA (pick capstone dataset) |
| Week 4 | [Data Visualization](week-04-data-visualization/) | Visual report (capstone) |
| Week 5 | [Statistics Foundations](week-05-statistics-foundations/) | Statistical analysis (capstone) |
| Week 6 | [ML: Regression](week-06-regression/) | Predict a continuous value (capstone) |
| Week 7 | [Classification & Model Evaluation](week-07-classification-model-evaluation/) | Predict a category + compare models (capstone) |
| Week 8 | [Capstone Project & Presentation](week-08-capstone/) | Final capstone + presentation |

> Update this table as each week's content is finalized and moved into the repo.

## Getting started

**Fastest way to start (no install):** open [Week 1's lab directly in Google
Colab](https://colab.research.google.com/github/mohamad-755/root-academy-curriculum/blob/main/week-01-python-foundations/lab.ipynb).

Or, for the full setup:

1. Read [`resources/setup-guide.md`](resources/setup-guide.md) to choose
   between **Google Colab** (recommended, zero setup) and a **local VS Code**
   setup.
2. If going local, clone this repo:
   ```bash
   git clone https://github.com/mohamad-755/root-academy-curriculum.git
   cd root-academy-curriculum
   ```
   New to Git? Check [`resources/git-basics.md`](resources/git-basics.md).
3. Start with [Week 1](week-01-python-foundations/) and work through each folder in order.
4. Questions? See the [`resources/faq.md`](resources/faq.md).

## Repo structure

```
root-academy-curriculum/
├── README.md
├── LICENSE
├── requirements.txt
├── syllabus.md
├── week-01-python-foundations/
│   ├── README.md
│   ├── assignment.ipynb
│   ├── assignment-solution.ipynb
│   ├── lab.ipynb
│   └── lab-solution.ipynb
├── week-02-numpy-pandas/
│   ├── README.md
│   ├── assignment.ipynb
│   ├── assignment-solution.ipynb
│   ├── lab.ipynb
│   ├── lab-solution.ipynb
│   └── data/
│       └── employee_scores.csv
├── week-03-data-cleaning-eda/
│   ├── README.md
│   ├── assignment.ipynb
│   ├── assignment-solution.ipynb
│   ├── lab.ipynb
│   ├── lab-solution.ipynb
│   └── data/
│       ├── employee_data.csv
│       └── employee_data_cleaned.csv
├── week-04-data-visualization/
│   ├── README.md
│   ├── assignment.ipynb
│   ├── assignment-solution.ipynb
│   ├── lab.ipynb
│   ├── lab-solution.ipynb
│   └── data/
│       └── employee_data_cleaned.csv
├── week-05-statistics-foundations/
│   ├── README.md
│   ├── assignment.ipynb
│   ├── assignment-solution.ipynb
│   ├── lab.ipynb
│   ├── lab-solution.ipynb
│   └── data/
│       └── employee_data_cleaned.csv
├── week-06-regression/
│   ├── README.md
│   ├── assignment.ipynb
│   ├── assignment-solution.ipynb
│   ├── lab.ipynb
│   ├── lab-solution.ipynb
│   └── data/
│       └── employee_data_cleaned.csv
├── week-07-classification-model-evaluation/
│   ├── README.md
│   ├── assignment.ipynb
│   ├── assignment-solution.ipynb
│   ├── lab.ipynb
│   ├── lab-solution.ipynb
│   └── data/
│       └── employee_data_cleaned.csv
├── week-08-capstone/
│   ├── README.md
│   ├── assignment.ipynb
│   ├── assignment-solution.ipynb
│   ├── lab.ipynb
│   ├── lab-solution.ipynb
│   └── data/
│       └── employee_data_cleaned.csv
└── resources/
    ├── setup-guide.md
    ├── git-basics.md
    └── faq.md
```

## License

This work is licensed under [CC BY-NC-SA 4.0](LICENSE) — free to share and adapt with
attribution, for non-commercial use, under the same license. See [`LICENSE`](LICENSE)
for full terms.

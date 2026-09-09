# Week 6 — Introduction to AI & Machine Learning

**Course:** Introduction to Data Science
**Week Topic:** How Machines Learn from Data

## Main Goal

This week, before we write any code, we learn what AI and Machine Learning actually mean, and how a machine "learns" from data. This is the foundation for training our first real model next week.

## 1. What is AI?

**Artificial Intelligence (AI)** means building computer systems that can do things that normally need human thinking — like understanding language, recognizing images, or making decisions.

**Machine Learning (ML)** is one way to build AI. Instead of a person writing exact rules by hand, we give the computer data, and it finds the patterns on its own.

**Deep Learning** is a more advanced type of ML. It uses "neural networks," which are loosely inspired by the human brain. It's used for things like image recognition and chatbots.

```
AI  >  Machine Learning  >  Deep Learning
(the big idea)   (learns from data)   (uses neural networks)
```

## 2. AI vs. Normal Programming

This is the most important idea in the whole course, so let's compare it to programming you already know.

| | Normal Programming | Machine Learning |
|---|---|---|
| You give the computer | Data + rules you write | Data + the correct answers |
| The computer gives you | An answer | The rules (this is the "model") |
| Example | `if attendance > 90: grade = "A"` | Show it thousands of past attendance/grade pairs, and it figures out the rule itself |

In short: normally, **you** write the rules. In ML, **the computer** finds the rules for you.

## 3. Where You Already See AI Every Day

- **Netflix / YouTube / Spotify** suggesting what to watch or listen to next
- **Email spam filters** deciding spam vs. not spam
- **Google Maps** predicting how long your trip will take
- **Face unlock** on your phone
- **Siri / Google Assistant** understanding what you say

You use ML systems every day without noticing — the goal this week is to understand what's happening behind them.

## 4. How Does a Machine "Learn"?

A machine learns in 3 simple steps:

1. It looks at many examples (data).
2. It finds the pattern that connects the input to the correct answer.
3. It uses that pattern to guess the answer for new examples it hasn't seen before.

This is similar to how you learn to spot a spam email after seeing enough spam and non-spam examples.

## 5. Good Data In, Good Results Out

A model is only as good as the data we give it. If the data is messy, incomplete, or unfair, the model will learn the wrong patterns — and it won't know it's wrong.

Some simple examples:

- If a hiring model only sees resumes from one group of people, it may unfairly favor that group later — even if no one meant for that to happen.
- If attendance data has typos or missing values, the model learns from that noise instead of the real pattern.

This is why cleaning your data carefully (something you've already been doing in earlier weeks) matters so much.

## 6. The Real Goal: Generalization, Not Memorizing

A model isn't useful just because it matches the data it trained on — a simple lookup table could do that. A model is useful when it can make good guesses on **new data it has never seen before**. This is called **generalization**, and it's the whole point of machine learning.

**A simple way to think about it:** imagine two students preparing for an exam.

- Student A memorizes last year's exam answers word for word. They'll do great if the *same* exam repeats, but poorly on a new one.
- Student B actually understands the topic. They can handle new questions they've never seen.

We want our model to be like Student B.

This idea is *why*, next week, we won't test our model on the same data it trained on — we'll save some data it has never seen, just to check if it really "understood."

**Two ways this can go wrong** (just the basic idea for now — we'll go deeper later in the course):

| Problem | What it means | Like Student... |
|---|---|---|
| **Underfitting** | The model is too simple and misses the real pattern | Barely studied — does badly on everything |
| **Overfitting** | The model memorizes the training data too closely | Memorized last year's exam — does badly on a new one |

## 7. Types of Machine Learning

| Type | What it means | Example |
|---|---|---|
| Supervised Learning | The data already has correct answers (labels); the model learns to predict them | Predicting a student's score from their attendance |
| Unsupervised Learning | The data has no answers; the model finds hidden groups on its own | Grouping customers by shopping habits |
| Reinforcement Learning | The model learns by trial and error, getting rewards or penalties | A robot learning to walk |

Root Academy focuses on **supervised learning**, since it's the easiest starting point.

## 8. The Two Supervised Learning Tasks

| Task | Predicts | Example |
|---|---|---|
| Regression | A number | Predicting a house's price |
| Classification | A category | Predicting spam or not spam |

Next week, we start with **regression** — predicting a number — since it's the simplest way to see the whole ML process in action.

## 9. Features and Target (with an Example)

- **Features** = the inputs we use to make a prediction
- **Target** = the answer we're trying to predict

Look at one row of example data:

| attendance | study_hours | prior_score | **score (target)** |
|---|---|---|---|
| 92% | 5 | 78 | 85 |

Here, `attendance`, `study_hours`, and `prior_score` are the **features**. `score` is the **target** — the thing we want to predict.

Quick question to think about: if you only knew the attendance, could you guess the score? What if you also knew the study hours? More good features usually means better guesses — this idea comes back later in the course.

## 10. Key Vocabulary to Know Before Next Week

- **Model** — the "learner" that finds patterns in data
- **Features** — the input columns used to make a prediction
- **Target** — the value we're trying to predict
- **Training** — the process of the model learning from data
- **Prediction** — the model's guess on new data
- **Generalization** — how well a model performs on new data it hasn't seen
- **Overfitting** — when a model memorizes the training data too closely
- **Underfitting** — when a model is too simple to find the real pattern

## 11. The Machine Learning Steps (Preview)

This is the exact process we'll follow in code next week:

1. **Load data** — bring the dataset into our program
2. **Choose features and target** — decide what we use as input and what we predict
3. **Split data** — separate it into training data and testing data
4. **Train** — let the model find patterns in the training data
5. **Predict** — use the model on the testing data it hasn't seen
6. **Evaluate** — check how close the predictions were to the real answers

## 12. Why This Matters

Learning these ideas first makes next week's code much easier to follow. You'll already know *why* we split the data, *why* we measure error, and *what* the model is actually doing behind the scenes.

---

**Next:** [Lab →](lab.ipynb) | [Assignment →](assignment.ipynb)

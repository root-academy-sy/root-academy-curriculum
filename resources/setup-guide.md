# Getting Started — Running the Notebooks

You have two ways to work through this course. **We recommend Google Colab
for this free course** — it needs zero setup. VS Code (local setup) is there
for when you're ready for a more professional workflow.

## Option A: Google Colab (recommended — start here)

No installation required. Everything runs in your browser.

1. Go to [colab.research.google.com](https://colab.research.google.com).
2. Click **File → Open notebook → GitHub**.
3. Paste the repo URL: `https://github.com/mohamad-755/root-academy-curriculum`
4. Pick the notebook you want (e.g. `week-01-python-foundations/lab.ipynb`).

Or open a specific notebook directly with a link in this format:
```
https://colab.research.google.com/github/mohamad-755/root-academy-curriculum/blob/main/<path-to-notebook>
```
Example for Week 1's lab:
```
https://colab.research.google.com/github/mohamad-755/root-academy-curriculum/blob/main/week-01-python-foundations/lab.ipynb
```

**Saving your work:** Colab won't save changes back to the course repo. Use
**File → Save a copy in Drive** to keep your own editable copy.

## Option B: VS Code (local setup — for when you're ready to go further)

This is closer to a professional data science workflow, and it's what we
recommend once you're comfortable with the basics — or if you're already
heading toward Root Academy's next-level course, which assumes this kind of
setup.

### 1. Install Python

Install Python 3.10+ from [python.org](https://www.python.org/downloads/) or
via a distribution like [Anaconda](https://www.anaconda.com/download).

### 2. Create a virtual environment

```bash
python -m venv venv
source venv/bin/activate      # macOS/Linux
venv\Scripts\activate         # Windows
```

### 3. Install required packages

From the repo root:

```bash
pip install -r requirements.txt
```

This installs everything needed across the program:
```
pandas
numpy
matplotlib
seaborn
scikit-learn
jupyter
```

### 4. Install VS Code + extensions

- Install [VS Code](https://code.visualstudio.com/)
- Install the **Python** extension and the **Jupyter** extension from the
  Extensions panel

### 5. Open and run notebooks

Open the cloned `root-academy-curriculum` folder in VS Code, navigate to a
week's folder, and open `lab.ipynb` or `assignment.ipynb` directly — VS Code
runs notebook cells natively once the Jupyter extension is installed.

## Which should I use?

| | Colab | VS Code |
|---|---|---|
| Setup time | None | ~15–20 min |
| Works on any device | Yes | Needs a capable computer |
| Good for | This free course | Building real project habits, going further |
| Git workflow | Not needed | See [`git-basics.md`](git-basics.md) |

Start with Colab. Switch to VS Code whenever you're ready to work locally —
there's no wrong choice, and you can always change later.

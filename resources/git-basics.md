# Git & GitHub Basics

> If you're working in **Google Colab**, you don't need any of this — Colab
> opens notebooks straight from GitHub without cloning anything. This guide
> is for the **VS Code / local setup** track (see
> [`setup-guide.md`](setup-guide.md)).

## Getting the course materials

```bash
git clone https://github.com/mohamad-755/root-academy-curriculum.git
cd root-academy-curriculum
```

## Keeping your copy up to date

New weeks will be added over time. To pull the latest content:

```bash
git pull origin main
```

## Working on labs/assignments without conflicts

If you want to edit notebooks locally and keep your own changes safe from
being overwritten by future `git pull`s, consider:

- Making a copy of each week's notebook before editing (e.g.
  `lab.ipynb` → `lab-my-work.ipynb`), or
- Forking the repo on GitHub and working in your own fork.

## Common commands

| Command | What it does |
|---|---|
| `git clone <url>` | Download a copy of the repo |
| `git pull` | Get the latest changes |
| `git status` | See what's changed |
| `git add .` | Stage changes |
| `git commit -m "message"` | Save a snapshot of your changes |
| `git push` | Upload your commits (only if you have write access / your own fork) |

Comfortable with Git and want a local, professional workflow long-term? This
is exactly the kind of setup Root Academy's next-level course builds on.

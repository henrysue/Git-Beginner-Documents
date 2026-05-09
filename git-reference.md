# Git Quick Reference

## What is Git?

Git is a tool that tracks changes to your files over time. Think of it like a "save game" feature for your project — you can take snapshots as you work, look back at older versions, and share your work with others.

A **repository** (or "repo") is just a folder that Git is tracking. The **remote** is the online copy of that folder, usually hosted on a service like GitHub.

## The Mental Model

When you change a file, Git treats it as living in one of three places:

1. **Working directory** — the actual files on your computer that you edit.
2. **Staging area** — a list of changes you've marked as "ready to save."
3. **Repository** — the permanent history of saved snapshots (commits).

Most Git commands move changes between these three places.

---

## Setup Commands

### `git clone <url>`
**What it does:** Downloads a copy of an online repo onto your computer.
**When to use:** The very first time you want to work on an existing project. You only do this once per project.
**Example:** `git clone https://github.com/someone/cool-project.git`

### `git init`
**What it does:** Turns the current folder into a new Git repo.
**When to use:** When you're starting a brand-new project from scratch on your own computer (not downloading one).

---

## Checking What's Going On

### `git status`
**What it does:** Shows which files have changed, which are staged, and which are untracked.
**When to use:** All the time. Run it whenever you're unsure about the state of things — it's free and tells you what to do next.

### `git log`
**What it does:** Shows the history of saved snapshots (commits).
**When to use:** When you want to see who changed what and when. Press `q` to exit.

### `git diff`
**What it does:** Shows the actual line-by-line changes you've made since the last save.
**When to use:** Before saving changes, when you want a careful look at exactly what you're about to commit.

---

## Saving Your Work

These three commands are the heart of Git. You'll use them constantly.

### `git add <file>`
**What it does:** Marks a file's changes as "ready to save." This is called *staging*.
**When to use:** After editing files, when you've decided those changes are worth keeping.
**Tip:** `git add .` stages every changed file in the folder at once.

### `git commit -m "your message"`
**What it does:** Saves a permanent snapshot of all staged changes, with a short note explaining what you did.
**When to use:** Once you've staged the changes you want to save together. Write a clear message — your future self will thank you.
**Example:** `git commit -m "Fix typo on the about page"`

### `git push`
**What it does:** Uploads your local commits to the remote (e.g., GitHub) so others can see them.
**When to use:** After committing, when you're ready to share your work or back it up online.

---

## Staying in Sync

### `git pull`
**What it does:** Downloads the latest changes from the remote and merges them into your local copy.
**When to use:** Before you start working, especially if other people are also making changes. This avoids conflicts.

---

## Branching (Intermediate)

A **branch** is a parallel version of your project where you can experiment without affecting the main version.

### `git branch`
**What it does:** Lists all your branches and shows which one you're on.

### `git switch <branch-name>`
**What it does:** Moves you to a different branch.
**Example:** `git switch main`

### `git switch -c <new-branch-name>`
**What it does:** Creates a new branch and switches to it.
**When to use:** When trying something experimental that you don't want to mess up the main version with.

---

## The Golden Rule

When in doubt, run **`git status`**. It will almost always tell you what's happening and suggest your next step.

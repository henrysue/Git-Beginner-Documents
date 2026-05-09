# Understanding Git: A Guide for Everyone

This document explains what Git is, why it exists, and how people use it day-to-day. It's written for non-programmers, so we'll lean on analogies and walk through realistic scenarios — from "just me, working alone" all the way to "I'm one of fifty people contributing to a huge product."

---

## Part 1: What Problem Does Git Solve?

Imagine you're writing a long essay. You save it as `essay.docx`. The next day you make some edits, but you're worried you might want the old version back, so you save a copy called `essay_v2.docx`. Then `essay_final.docx`. Then `essay_final_REAL.docx`. Then `essay_final_REAL_use_this_one.docx`.

Now imagine three friends are also editing the same essay. They email versions back and forth. Someone makes changes to a paragraph that another person had already deleted. Someone forgets which version is the latest. Two people edit the same sentence in different ways, and now nobody knows which one is "right."

This is what programming used to feel like before Git. The work is collaborative, the files are constantly changing, and tiny mistakes can be costly. Git was built to solve all of these problems at once:

- **Keeping a complete history** of every change, so you can always go back.
- **Letting many people work at the same time** without overwriting each other.
- **Combining everyone's work** in a controlled, reviewable way.
- **Trying experiments safely**, knowing you can throw them away if they don't pan out.
- **Understanding who changed what, when, and why.**

Git isn't only useful for code — people use it for writing books, managing legal documents, designing websites, and tracking research notes. Anywhere multiple versions of files exist, Git can help.

---

## Part 2: How Git Thinks About Your Work

To use Git well, it helps to understand the mental model. Git keeps three "places" your work can live in:

### 1. The Working Directory
This is just the regular folder on your computer. The files you see in Finder or File Explorer. When you edit a document, you're editing the working directory.

### 2. The Staging Area
This is a kind of "loading dock" where you put changes you've decided are worth saving. Staging is Git's way of letting you batch up related changes so you can save them as a single, meaningful unit.

For example, you might fix a typo in one file and rewrite an entire chapter in another. Even though both are modified, you can stage and save them separately so the history stays clean.

### 3. The Repository
This is the permanent record of every saved snapshot — what Git calls **commits**. Once something is committed, it's in the history forever (well, almost — but for our purposes, treat it as permanent).

### The Remote
On top of those three, there's usually a **remote** — an online copy of the repository hosted somewhere like GitHub. This is what lets multiple people share work. Your local copy and the remote talk to each other through two commands: `push` (send my work up) and `pull` (get the latest down).

### Commits Tell a Story
Every commit has a message describing what changed and why. A good history reads like a logbook: "Add login page," "Fix typo in homepage heading," "Update prices for 2026." Months later, someone (often your future self) can scroll back and understand exactly how the project got to where it is.

### Branches: Parallel Timelines
A **branch** is an alternate timeline for your project. The default branch (usually called `main`) is the official, working version. When you want to try something new, you create a branch off of `main`, work on it freely, and only merge it back into `main` once it's good.

Think of `main` as the published version of a book, and a branch as a draft chapter you're working on in a separate notebook. Until you decide it's ready, your draft never touches the published version.

---

## Part 3: The Simple Case — Working Alone

Let's start with the easiest scenario: it's just you, working on your own project, with no branches and no collaborators. This is the workflow you use most when you're learning.

### Scenario: Building a personal website

**Day 1.** You create a new project on GitHub and clone it to your laptop. You add a homepage file, then run:

```
git add index.html
git commit -m "Add homepage"
git push
```

Three commands, three jobs: stage the change, save a snapshot with a note, send it to GitHub.

**Day 2.** You add an "About Me" page. Same routine.

```
git add about.html
git commit -m "Add about page"
git push
```

**Day 3.** You realize the homepage has a broken link. You fix it.

```
git add index.html
git commit -m "Fix broken link on homepage"
git push
```

That's it. You're keeping a tidy history of your project, and every commit is backed up to GitHub. If you ever break something, you can scroll back through the history and see exactly when it broke.

This is the mainline workflow: every commit lands directly on `main`, in a single clean line, like beads on a string.

---

## Part 4: Working with One or Two Others

Now let's add a friend. You're both working on the same website.

### Scenario: A two-person project with no overlap

You're working on the homepage. Your friend is working on the contact page. You're not touching the same files, so things go smoothly.

**Morning.** Both of you run `git pull` to get the latest. You each work on your own file, commit, and push.

If your friend pushes first, when you try to push, Git will say: "Wait — there's something new on the remote you don't have yet. Pull first." So you run `git pull`, which downloads their changes (the new contact page) and merges them with yours. Now both your work and theirs are combined locally. Then you `git push`, and you're synced up.

The golden rule is: **pull before you push.** If you do this consistently, most days nothing weird happens.

### Scenario: Both editing the same file (no conflict)

You and your friend both edit `homepage.html`, but in different sections — they fix the footer, you change the hero image. When you pull their changes, Git is smart enough to recognize that you're working in different parts of the file. It combines both edits automatically. This is called an **automatic merge**.

### Scenario: Both editing the same line — a conflict

This is the first situation that can trip up beginners. You both edit the *same line* of the homepage's title tag. Maybe you change it to "Welcome to My Site" and your friend changes it to "Home — Cool Stuff."

When you try to pull or merge, Git can't know which version is correct. It stops and tells you there's a **merge conflict**. Inside the file, Git inserts markers showing both versions:

```
<<<<<<< your version
<title>Welcome to My Site</title>
=======
<title>Home — Cool Stuff</title>
>>>>>>> their version
```

Your job is to open the file, decide what the right answer is (maybe a combination of both), delete the marker lines, and save the file. Then:

```
git add homepage.html
git commit -m "Resolve conflict in homepage title"
git push
```

Conflicts feel scary the first time, but they're really just Git asking, "Hey, two people changed this — which version do you want?" You answer the question and move on.

---

## Part 5: Larger Teams — How Real Companies Use Git

In a real product team — say, fifty engineers working on a banking app — letting everyone commit directly to `main` would be chaos. Mistakes would land in production constantly. So companies use a more structured workflow built around **branches** and **pull requests**.

### The Feature Branch Workflow

When an engineer starts a new task — say, "add the ability to download a statement as PDF" — they don't touch `main` directly. They create a new branch:

```
git switch -c add-pdf-download
```

They work on this branch for a few hours or a few days. They commit as often as they like. The commits live only on their branch — `main` is undisturbed.

When they're done, they push the branch:

```
git push -u origin add-pdf-download
```

Then they open a **pull request** (PR) on GitHub. A pull request is a formal way of saying: "Hey team, I'd like to add this work into `main`. Please review."

### Code Review

Before the branch can merge into `main`, teammates read through the changes. They leave comments: "Did you consider this case?" "This variable name is confusing." "Looks good!" The author updates the branch (more commits!) and pushes again. Once everyone's satisfied — and any automated tests pass — the PR is **approved** and merged.

This process catches bugs early, spreads knowledge across the team (people learn what others are working on), and keeps `main` in a clean, working state at all times.

### Scenario: Your branch falls behind

You started a feature branch on Monday. By Friday, ten other PRs have been merged into `main`. Your branch is now "behind" — it doesn't have those new changes. Before merging your work, you usually need to update your branch with the latest from `main`. Two common ways to do this:

- **Merge `main` into your branch.** This brings the latest changes in, and Git records a "merge commit." Simple but creates extra history entries.
- **Rebase onto `main`.** This is like picking up your branch's commits and reapplying them on top of the latest `main`. The history stays linear and clean. More elegant, but trickier — if there are conflicts, you resolve them one commit at a time.

Either way, you may have to resolve conflicts during this update. Once your branch is up to date and tests pass, your PR can be merged.

### Scenario: A bug is found in production — the hotfix

It's Tuesday morning. Customers can't log in. Something that shipped yesterday is broken. The team needs to fix it *right now*, but you're in the middle of a feature branch with half-finished work.

The standard pattern:

1. Save your half-finished work without committing it: `git stash`. This tucks your changes away in a safe place.
2. Switch back to `main`: `git switch main` and `git pull`.
3. Create a hotfix branch: `git switch -c hotfix-login-bug`.
4. Fix the bug, commit, push, open a PR, get it reviewed and merged urgently.
5. Switch back to your feature branch and bring your work back: `git stash pop`.

This way, the urgent fix doesn't get tangled up with your in-progress work, and your in-progress work doesn't accidentally ship before it's ready.

### Scenario: Someone merged something that broke production

A PR got approved, merged into `main`, deployed — and immediately broke things. The team doesn't have time to investigate right now; they just want to undo it.

The safe move is `git revert`. This creates a *new* commit that undoes the changes from the bad one, without erasing the history. The bad commit is still in the log (so people can study it later), but its effects are gone. Production is healthy again. The author of the bad PR can investigate at their leisure and try again.

`git revert` is preferred over `git reset` in this situation because revert is non-destructive and safe to use on shared branches — nobody else's work is disrupted.

### Scenario: You committed something sensitive

You accidentally committed a password or an API key. **Don't push.** If you haven't pushed yet, you can rewrite your local history to remove the commit. If you've already pushed, the situation is more serious — the secret should be considered exposed, rotated immediately (generate a new password/key), and the repository's history scrubbed by someone experienced. Most enterprise teams have automated tools that scan for this kind of mistake and alert security.

### Scenario: You committed to the wrong branch

You meant to create a feature branch, but you committed three changes directly to `main` by mistake. The fix:

1. Create a new branch from where you are: `git switch -c my-feature-branch`. This branch now contains all your commits.
2. Switch back to `main`: `git switch main`.
3. Reset `main` back to where it was before your accidental commits: `git reset --hard origin/main`.

Your work is preserved on the new branch, and `main` is clean again. This is the kind of thing where it's worth asking a teammate to double-check before running `git reset --hard`, since it's one of the few Git commands that can throw away work if used carelessly.

### Scenario: Long-lived release branches

Larger products often maintain multiple versions in parallel. A bank might have `main` (next release), `release/2026-q1` (currently shipping), and `release/2025-q4` (still supported for some customers). A serious bug found in the older release might need to be fixed in all three branches. Engineers use a command called `git cherry-pick` to copy a specific commit from one branch onto another. It's an "I want this exact change applied here too" operation.

---

## Part 6: A Few Habits That Save Pain Later

A handful of small habits make Git much more pleasant in practice.

**Pull before you start working.** If you sit down at your computer and dive straight into edits without pulling first, you may find your changes don't fit cleanly when you try to push. Pulling first ensures you're building on top of the latest version.

**Commit small, commit often.** A commit should ideally do one thing. "Add login page" is good. "Add login page, fix three unrelated bugs, refactor billing system" is bad. Small commits are easier to review, easier to understand later, and easier to undo if something goes wrong.

**Write commit messages your future self can understand.** "Stuff" and "fixed it" are useless three months later. "Fix off-by-one error in date picker on mobile Safari" is gold.

**Run `git status` constantly.** It's free, it's fast, and it tells you exactly what state you're in. When something feels weird, your first instinct should be `git status`.

**Don't rewrite history that other people have.** Once you've pushed a branch and others may have based work on it, leave the history alone. Fix problems by adding new commits (like `git revert`) rather than altering the past. Rewriting shared history is the Git equivalent of pulling the rug out from under your teammates.

---

## Part 7: When Things Feel Broken

Most "I broke Git" situations are recoverable. Git is conservative — it almost never throws work away, even when it looks like it has. A few comforting facts:

- Committed work is essentially permanent. Even if a commit seems to vanish, it's usually still in Git's database for at least 30 days, retrievable with a command called `git reflog`.
- The remote is a backup. As long as you've pushed recently, your work is safe somewhere even if your local copy gets corrupted.
- Branches are cheap. If you're worried about messing up, create a new branch first as a safety net: `git switch -c safety-copy`. Then experiment freely on the original.

When in doubt, stop and ask someone. Most Git problems are easy for an experienced user to untangle in a few minutes, and much harder to fix after you've tried five things in a panic.

---

## Final Thoughts

Git has a reputation for being intimidating, and to be fair, the deepest parts of it really are complicated. But the everyday workflow — pull, edit, add, commit, push — is genuinely simple, and it's enough to handle 90% of what most people need to do. The more complex stuff (branches, merges, rebases, conflicts) makes a lot more sense once you have the basics in your fingers.

The single most important thing to remember is the mental model: **working directory → staging area → repository → remote**. Almost every Git command is moving changes between those four places. If you understand where you are and where you want your changes to go, you can usually figure out the right command — or at least ask the right question.

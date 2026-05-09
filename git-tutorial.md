# Your First Git Workflow: A Beginner Tutorial

This tutorial walks you through the most common Git workflow: getting a copy of a project, making a change, and sharing it back. By the end, you'll have done a real round trip with Git.

## Before You Start

You'll need:
- Git installed on your computer (run `git --version` in your terminal to check).
- A GitHub account (or similar — GitLab, Bitbucket, etc.).
- A repo to practice on. If you don't have one, create an empty repo on GitHub called `git-practice` and add a README when prompted.

We'll use the terminal (Command Prompt on Windows, Terminal on Mac/Linux). Don't worry — you only need a handful of commands.

---

## Step 1: Clone the Repository

Cloning means downloading a copy of the project to your computer.

On the GitHub page for your repo, click the green **Code** button and copy the URL. Then in your terminal:

```
cd Desktop
git clone https://github.com/your-username/git-practice.git
```

The first line moves you into your Desktop folder (you can choose anywhere). The second downloads the repo into a new folder called `git-practice`.

Now move into that folder:

```
cd git-practice
```

You're inside your repo. Everything from here on happens in this folder.

---

## Step 2: Check the Current State

Always a good habit:

```
git status
```

You should see a message like "nothing to commit, working tree clean." That means there are no unsaved changes — you're starting from a clean slate.

---

## Step 3: Make a Change

Open the `README.md` file in any text editor (TextEdit, Notepad, VS Code — whatever you have). Add a new line at the bottom, like:

```
Hello! I'm learning Git.
```

Save the file and close the editor.

---

## Step 4: See What Changed

Back in the terminal:

```
git status
```

This time Git will tell you that `README.md` has been modified. To see *exactly* what changed:

```
git diff
```

You'll see your new line marked with a green `+`, meaning it was added. Press `q` to exit.

---

## Step 5: Stage the Change

You need to tell Git "yes, I want to save this change." That's called staging:

```
git add README.md
```

Run `git status` again. Now `README.md` is listed under "Changes to be committed" — it's ready to save.

> **Tip:** If you've changed multiple files and want to stage them all at once, you can use `git add .` (the dot means "everything in the current folder").

---

## Step 6: Commit the Change

A commit is a permanent snapshot. Always include a short message describing what you did:

```
git commit -m "Add greeting to README"
```

You'll see a confirmation. Your change is now saved in the local history. But it's still only on your computer — the online version on GitHub doesn't know about it yet.

---

## Step 7: Push to GitHub

Send your commit to the remote:

```
git push
```

You may be asked for your GitHub credentials the first time. After it finishes, refresh your repo's page on GitHub — you'll see your new line in the README, along with your commit message in the history.

🎉 You've just done a complete Git workflow.

---

## The Cycle to Remember

For everyday use, you'll repeat these steps:

```
1. git pull              ← grab any updates from others (do this first!)
2. (edit your files)
3. git status            ← see what changed
4. git add <files>       ← stage the changes you want to save
5. git commit -m "..."   ← save a snapshot
6. git push              ← share it
```

That's 95% of what most people use Git for. The rest you can learn as you need it.

---

## Common Beginner Pitfalls

**"I forgot to write a commit message and now I'm stuck in a weird editor!"**
You're in Vim. Press `Esc`, then type `:q!` and press Enter to exit without committing. Next time, remember the `-m "message"` flag.

**"It says my push was rejected."**
Someone else pushed changes before you. Run `git pull` first, then try `git push` again.

**"I committed something I didn't mean to."**
Don't panic. To undo the most recent commit but keep your changes: `git reset --soft HEAD~1`. Ask for help before trying anything more drastic — Git rarely loses work, but undo commands can be tricky.

**"Help, I don't know what state I'm in."**
Run `git status`. It almost always tells you what's going on and what to do next.

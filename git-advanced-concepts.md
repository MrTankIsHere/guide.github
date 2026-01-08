# Git & GitHub: Advanced Concepts

This document covers some important Git concepts and commands that were not included in the main `git-steps.md` guide. Mastering these will help you manage your projects more effectively and recover from mistakes.

---

## 1. Ignoring Files: `.gitignore`

A `.gitignore` file specifies intentionally untracked files that Git should ignore (it just ignore the files that are in that repo/folder). Files already tracked by Git are not affected.

### Why is this important?

You often have files and directories in your project that you don't want to commit, such as:
*   Dependencies (`node_modules/`, `vendor/`)
*   Build output (`dist/`, `build/`)
*   Log files (`*.log`)
*   Secrets and credentials (`.env`, `credentials.json`)

### How to use it

1.  Create a file named `.gitignore` in the root of your repository.
2.  Add patterns for the files and directories you want to ignore. Each line represents a pattern.

**Example `.gitignore` for a Node.js project:**

```
# Dependencies
node_modules/

# Logs
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Environment variables
.env

# Build output
dist/
```

---

## 2. Viewing Changes: `git diff`

The `git diff` command is used to track the difference between changes made on a file.

### Common Use Cases:

*   **`git diff`**: Shows changes in your working directory that are not yet staged.
*   **`git diff --staged`**: Shows changes that are staged but not yet committed.
*   **`git diff <branch-name>`**: Shows differences between your current branch and another branch.
*   **`git diff <commit-hash-1> <commit-hash-2>`**: Shows differences between two specific commits.

**Example:**

After editing a file, run `git diff` to see your changes:

```bash
git diff
```

**Output:**
```diff
diff --git a/README.md b/README.md
index 1234567..abcdefg 100644
--- a/README.md
+++ b/README.md
@@ -1,3 +1,3 @@
 # My awesome project
 
-This is a test project.
+This is a very cool project.

```

---

## 3. `git fetch` vs. `git pull`

Both commands are used to download new data from a remote repository, but they behave differently.

*   **`git fetch`**: Downloads all the new commits, branches, and tags from the remote repository, but it **does not** merge them into your local branch. This is useful if you want to see what others have been working on without merging the changes into your local repository just yet.

*   **`git pull`**: Is essentially a `git fetch` followed by a `git merge`. It downloads the new changes and immediately tries to merge them into your current branch. This can lead to merge conflicts if your local changes overlap with the remote changes.

**Workflow with `git fetch`:**

1.  `git fetch origin`
2.  `git log main..origin/main` (to see the changes on the remote `main` branch)
3.  `git merge origin/main` (to merge the changes)

This workflow gives you more control and allows you to review changes before integrating them.

---

## 4. Undoing Commits: `git reset` and `git revert`

These two commands let you undo changes, but in very different ways.

### `git revert`

`git revert` is the safest way to undo changes. It creates a **new commit** that is the inverse of the specified commit. This doesn't alter the existing commit history.

**When to use it:**
When you want to undo a commit that has already been pushed to a shared remote repository.

**Example:**

```bash
# Revert the last commit
git revert HEAD
```

### `git reset`

`git reset` is more powerful and can be dangerous. It moves the `HEAD` pointer to a specified commit, effectively "removing" any commits that came after it.

*   **`git reset --soft <commit-hash>`**: Moves `HEAD`, but keeps the changes from the "removed" commits staged.
*   **`git reset --mixed <commit-hash>`** (default): Moves `HEAD` and unstages the changes.
*   **`git reset --hard <commit-hash>`**: Moves `HEAD` and **discards all changes**. Use with extreme caution.

**When to use it:**
On your local branches, before you've pushed your changes. **Never use `git reset` on a shared branch that others are using.**

**Example:**

```bash
# Go back to the commit before the last one, and discard all changes
git reset --hard HEAD~1
```

---

## 5. Recovering from Mistakes: `git reflog`

`git reflog` is your safety net. It shows a log of where your `HEAD` has been. Every time you switch branches, commit, reset, or do anything that changes `HEAD`, a new entry is added to the reflog.

If you ever mess up (e.g., you did a `git reset --hard` and lost some commits), the reflog can help you recover.

**How to use it:**

1.  Run `git reflog` to see the history of your `HEAD`.
2.  Find the commit you want to go back to.
3.  Use `git reset` or `git checkout` to restore that commit.

**Example:**

```bash
git reflog
```

**Output:**

```
abcdefg HEAD@{0}: reset: moving to HEAD~1
1234567 HEAD@{1}: commit: Add new feature
c0ff333 HEAD@{2}: checkout: moving from main to my-feature-branch
...
```

To restore the commit you accidentally reset, you could do:
```bash
git reset --hard 1234567
```

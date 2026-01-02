# Git & GitHub: The Complete Guide

This guide is your one-stop resource for mastering Git and GitHub. It's structured to take you from the absolute basics to advanced, powerful workflows.

---

## Ⅰ. The Basics: Your First Steps with Git

This section covers the essential commands you'll use every day.

### 1. What is Version Control?

Version control is a system that records changes to a file or set of files over time so that you can recall specific versions later. Think of it as a "save" button for your entire project, but with the ability to go back to any previous save.

### 2. Core Git Concepts

*   **Repository (Repo):** Your project's folder. Git tracks everything inside it.
*   **Commit:** A snapshot of your files at a specific time.
*   **Branch:** A parallel universe for your code. You can create a new branch to work on a new feature without breaking the main project.
*   **HEAD:** A pointer to your current location in the repository (the latest commit in your current branch).

### 3. Installation and Setup

First, you need to have Git on your system.

*   **Linux:** `sudo apt-get install git`
*   **macOS:** `brew install git`
*   **Windows:** Download from [git-scm.com](https://git-scm.com/)

Then, introduce yourself to Git:
```bash
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
```

### 4. Creating Your First Repository

You can either start a new project or clone an existing one.

**To start a new project:**

1.  Create a new folder for your project.
2.  Open a terminal and `cd` into that folder.
3.  Run `git init`.

```bash
mkdir my-project
cd my-project
git init
```
**Output:**
```
Initialized empty Git repository in /home/user/my-project/.git/
```

**To clone an existing project from GitHub:**

```bash
git clone https://github.com/owner/repo-name.git
```
**Output:**
```
Cloning into 'repo-name'...
remote: Counting objects: 100, done.
remote: Compressing objects: 100% (80/80), done.
remote: Total 100 (delta 20), reused 100 (delta 20), pack-reused 0
Receiving objects: 100% (100/100), 15.22 KiB | 0 bytes/s, done.
Resolving deltas: 100% (20/20), done.
```

### 5. The Holy Trinity: `add`, `commit`, `push`

This is your core workflow for saving changes.

1.  **`git add`**: Tell Git which files you want to save in your next commit (this is called "staging").
2.  **`git commit`**: Save the staged files as a new snapshot.
3.  **`git push`**: Send your saved changes to a remote repository (like GitHub).

**Example:**

Let's say you create a new file `README.md`.

```bash
# Create the file
echo "My awesome project" > README.md

# Check the status
git status
```
**Output for `git status`:**
```
On branch main
Your branch is up to date with 'origin/main'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)

    README.md

nothing added to commit but untracked files present (use "git add" to track)
```

Now, let's commit it:

```bash
# Stage the file
git add README.md

# Commit the file
git commit -m "Add README file"
```
**Output for `git commit`:**
```
[main 1234567] Add README file
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```

### 6. Branching: Working in Parallel

Branches are essential for organized development.

*   **Create a new branch:** `git branch my-new-feature`
*   **Switch to the new branch:** `git checkout my-new-feature`
*   **Or do both at once:** `git checkout -b my-new-feature`

**Example:**

```bash
git checkout -b my-new-feature
```
**Output:**
```
Switched to a new branch 'my-new-feature'
```

Now, any commits you make will be on this new branch, separate from the `main` branch.

### 7. Merging: Combining Your Work

Once your feature is complete, you'll want to merge it back into the `main` branch.

1.  Switch back to the `main` branch: `git checkout main`
2.  Merge your feature branch: `git merge my-new-feature`

**If there are no conflicts,** the merge will be seamless.

---

## Ⅱ. Intermediate: Collaborating and Working with Remotes

This section focuses on teamwork and using platforms like GitHub.

### 1. Working with Remote Repositories

A "remote" is a shared repository that all team members can push to and pull from.

*   **List your remotes:** `git remote -v`
*   **Add a new remote:** `git remote add origin https://github.com/owner/repo-name.git`
    *   `origin` is the conventional name for the primary remote.
*   **Push to a remote:** `git push origin main`
*   **Pull from a remote:** `git pull origin main`

### 2. Forking and Pull Requests (The GitHub Workflow)

This is the most common way to contribute to open-source projects or collaborate in a team.

1.  **Fork a repository:** On GitHub, click the "Fork" button. This creates a personal copy of the project under your account.
2.  **Clone your fork:** `git clone https://github.com/your-username/repo-name.git`
3.  **Create a branch:** `git checkout -b my-changes`
4.  **Make your changes, then add and commit them.**
5.  **Push your branch to your fork:** `git push origin my-changes`
6.  **Create a Pull Request:** On GitHub, you'll see a prompt to create a Pull Request from your `my-changes` branch. A Pull Request is a formal proposal to merge your changes into the original project.
7.  **Code Review:** Others can now review your code, add comments, and suggest changes.
8.  **Merge:** Once approved, a project maintainer will merge your Pull Request.

### 3. Resolving Merge Conflicts

Sometimes, Git can't automatically merge changes because two people edited the same line of a file. This is a **merge conflict**.

When this happens, Git will stop the merge and tell you which files have conflicts. Open the conflicted files in your editor, and you'll see something like this:

```
<<<<<<< HEAD
This is the content from your current branch.
=======
This is the content from the other branch.
>>>>>>> other-branch-name
```

You need to manually edit the file to resolve the conflict, then save it. Once resolved:

1.  `git add .`
2.  `git commit` (no need for a message, Git provides one)

### 4. `git log`: Your Project's Diary

`git log` shows you the commit history. Here are some useful variations:

*   `git log --oneline`: A condensed view.
*   `git log --graph --oneline --decorate`: Shows the commit history as a graph.
*   `git log --stat`: Shows which files were changed in each commit.

---

## Ⅲ. Advanced: Supercharging Your Workflow

This section covers advanced tools and techniques for power users.

### 1. Interactive Rebase: `git rebase -i`

This is one of Git's most powerful features. It lets you rewrite your commit history.

**Use cases:**

*   **Squashing commits:** Combine multiple small commits into one larger one.
*   **Reordering commits.**
*   **Editing commit messages.**

**Example:** Squash the last 3 commits:

```bash
git rebase -i HEAD~3
```

This will open an editor with a list of the last 3 commits. Change `pick` to `squash` (or `s`) for the commits you want to merge into the one above them.

### 2. Cherry-Picking: `git cherry-pick`

Apply a specific commit from one branch to another, without merging the whole branch.

```bash
git cherry-pick <commit-hash>
```

### 3. Stashing: `git stash`

Temporarily shelve your current changes so you can work on something else.

```bash
# Stash your changes
git stash

# Later, to get them back
git stash pop
```

### 4. GitHub Actions: Automate Everything

GitHub Actions allows you to create custom workflows that run automatically in response to events (like a push or a Pull Request).

**Common use cases:**

*   **Continuous Integration (CI):** Automatically build and test your code every time you push.
*   **Continuous Deployment (CD):** Automatically deploy your application to a server.

**Example: A simple CI workflow**

Create a file at `.github/workflows/ci.yml`:

```yaml
name: CI

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Run a one-line script
      run: echo "Hello, world!"
```

This workflow will run on every push and pull request, checking out your code and printing "Hello, world!".

### 5. GitHub Pages: Host Your Website for Free

Host a static website directly from your GitHub repository.

1.  Go to your repository's **Settings** tab.
2.  Scroll down to the **GitHub Pages** section.
3.  Choose a source (e.g., the `main` branch) and a folder (usually `/root` or `/docs`).
4.  Your site will be published at `https://your-username.github.io/repo-name`.

### 6. The GitHub CLI (`gh`)

Do almost everything on GitHub from your terminal.

*   `gh repo clone owner/repo`
*   `gh pr create` (interactively create a pull request)
*   `gh pr list`
*   `gh issue create`
*   `gh release create <tag>`

---

## Ⅳ. Git Best Practices

*   **Commit small, logical changes.**
*   **Write clear and descriptive commit messages.**
*   **Use branches for everything.**
*   **Don't commit secrets.**
*   **Keep your `main` branch clean and deployable.**

This expanded guide should give you a solid foundation and a path to becoming a Git and GitHub expert. Happy coding!
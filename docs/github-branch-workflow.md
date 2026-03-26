# Pull latest from GitHub and work on a new branch

Use this when you want the newest code from GitHub on a fresh branch for local changes.

## 1. Get the latest from GitHub

```bash
git fetch origin
```

`fetch` updates your local view of `origin/*` without changing your checked-out files yet.

## 2. Update your default branch (recommended before branching)

If your new branch should start from the same commit as the remote default branch (e.g. `main`):

```bash
git checkout main
git pull origin main
```

`pull` runs `fetch` plus a merge (or rebase, depending on your Git config). If you already ran `fetch`, `pull` still applies the updates to `main`.

## 3. Create and switch to a new branch

Pick a short, descriptive name (for example `feature/login-fix`):

```bash
git checkout -b your-branch-name
```

Your new branch now points at the same commit as the updated default branch.

## 4. Work and commit locally

After editing files:

```bash
git add -p
# or: git add <files>

git commit -m "Describe your change"
```

Repeat as needed.

## 5. Push the branch to GitHub

When you are ready to share or open a pull request:

```bash
git push -u origin your-branch-name
```

The `-u` flag sets the upstream branch so later you can use `git push` and `git pull` without extra arguments.

---

## One-liner variant

If you do not need to update local `main` first, you can branch directly from the remote:

```bash
git fetch origin
git checkout -b your-branch-name origin/main
```

Replace `main` with your default branch name if it differs (for example `master`).

---

## Uncommitted work

If you have uncommitted changes when switching branches:

- **Stash:** `git stash -u`, switch or create the branch, then `git stash pop`
- **Or** commit on the current branch first, then branch—whichever fits your workflow

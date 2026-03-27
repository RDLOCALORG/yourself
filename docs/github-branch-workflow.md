# Git workflow: clone → feature branch → test → commit → PR → merge

End-to-end steps for this repository. Defaults used below:

| Item | Value |
|------|--------|
| **Organization** | **RDLOCALORG** |
| **Repository** | **yourself** |
| **Default branch** | **main** |
| **Remote** | **origin** → `https://github.com/RDLOCALORG/yourself.git` |

**Example branches used in this project** (names are descriptive—create your own for new work):

| Branch | Typical use |
|--------|-------------|
| **`feature/yourself`** | Broader feature work (e.g. owners API, workflow doc) |
| **`feature/add-baby-yoda-logo`** | Focused change (e.g. Flask header logo + doc tweaks) |

GitHub may show a redirect if the repo was moved under the org; use **`git remote set-url origin https://github.com/RDLOCALORG/yourself.git`** so `origin` matches.

---

## 1. Clone the repository to your machine

```bash
git clone https://github.com/RDLOCALORG/yourself.git
cd yourself
```

SSH: `git clone git@github.com:RDLOCALORG/yourself.git`

Org repo list: [github.com/orgs/RDLOCALORG/repositories](https://github.com/orgs/RDLOCALORG/repositories)

---

## 2. Update `main` before you branch

```bash
git fetch origin
git checkout main
git pull origin main
```

---

## 3. Create and switch to a feature branch

```bash
git checkout -b feature/add-baby-yoda-logo
```

Use any clear name, e.g. `feature/yourself`, `fix/login-validation`.

---

## 4. Work on your changes

Edit files. Use `git status` to see what changed.

---

## 5. Test your changes locally

- **Automated tests:** e.g. `./mvnw test` (needs a **JDK** on your machine)
- **Flask app:** `cd find_about_yourself && python3 -m pip install -r requirements.txt && python3 app.py` → open [http://127.0.0.1:5000](http://127.0.0.1:5000)

Fix failures before you push.

---

## 6. Commit your changes

Nothing is committed until you **stage** (`git add`) then **commit**:

```bash
git status
git diff
git add docs/github-branch-workflow.md find_about_yourself/templates/index.html
# or: git add -A   (watch for unwanted files, e.g. accidental nested clones)
git commit -m "Add baby Yoda logo and update workflow doc"
```

If `git commit` says **nothing to commit**, you likely skipped `git add` or there are no file changes.

---

## 7. Push the feature branch to GitHub

First time pushing **`feature/add-baby-yoda-logo`**:

```bash
git push -u origin feature/add-baby-yoda-logo
```

After that, on the same branch:

```bash
git push
```

**If push fails with `GH007` / private email:** adjust [GitHub → Settings → Emails](https://github.com/settings/emails) (allow command-line pushes or use your `@users.noreply.github.com` address in `git config user.email`), then amend or push again.

---

## 8. Create a pull request (PR)

**Base:** `main` ← **Compare:** your branch (e.g. **`feature/add-baby-yoda-logo`**).

### In the browser

1. Repo: [github.com/RDLOCALORG/yourself](https://github.com/RDLOCALORG/yourself)
2. **Pull requests** → **New pull request**, or use the banner after a push.
3. Confirm **base:** `main`, **compare:** `feature/add-baby-yoda-logo` → **Create pull request**

**Direct compare link:**

`https://github.com/RDLOCALORG/yourself/compare/main...feature/add-baby-yoda-logo`

(Replace the branch name at the end if yours differs.)

### In GitHub Desktop

1. **Current repository:** `yourself`
2. **Current branch:** e.g. **`feature/add-baby-yoda-logo`** (not `main`)
3. **Push origin** if you have unpushed commits
4. Menu **Branch** → **Create pull request** (opens the browser), *or* open the **Pull Requests** tab in the branch dropdown
5. If the branch list is empty: **clear the filter box**, click **Fetch origin**, search the **full** branch name (partial text like `feature/add` may hide matches)

---

## 9. Merge the PR into `main`

On the PR page: **Merge pull request** → confirm (or use squash/rebase if your team prefers).

---

## 10. Update local `main` after the merge

```bash
git checkout main
git pull origin main
```

Optional cleanup:

```bash
git branch -d feature/add-baby-yoda-logo
git push origin --delete feature/add-baby-yoda-logo
```

---

## Shortcut: branch from remote `main` without updating local `main` first

```bash
git fetch origin
git checkout -b feature/add-baby-yoda-logo origin/main
```

---

## Uncommitted work when switching branches

- **Stash:** `git stash -u`, switch branch, `git stash pop`
- **Or** commit on the current branch first

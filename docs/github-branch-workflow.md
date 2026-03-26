# Git workflow: clone → feature branch → test → commit → PR → merge

End-to-end steps for working on GitHub with a feature branch and merging back into `main`. Organization **`RDLOCALORG`**, repository **`yourself`**. Branch names below are examples—pick your own. This repo uses **`main`** as the default branch.

---

## 1. Clone the repository to your machine

```bash
git clone https://github.com/RDLOCALORG/yourself.git
cd yourself
```

Use SSH if you prefer: `git clone git@github.com:RDLOCALORG/yourself.git`

Org repo list: [github.com/orgs/RDLOCALORG/repositories](https://github.com/orgs/RDLOCALORG/repositories)

---

## 2. Update the default branch before you branch

So your feature branch starts from the latest `main`:

```bash
git fetch origin
git checkout main
git pull origin main
```

If your default branch is not `main`, replace it (for example `master`).

---

## 3. Create and switch to a feature branch

Pick a short, descriptive name (examples: `feature/add-owner`, `fix/login-validation`):

```bash
git checkout -b your-branch-name
```

---

## 4. Work on your changes

Edit files in your editor. Use `git status` often to see what changed.

---

## 5. Test your changes locally

Run whatever your project uses **before** you commit. Examples:

- **Automated tests:** e.g. `./mvnw test`, `pytest`, `npm test`
- **Run the app:** e.g. `./mvnw spring-boot:run`, `python app.py`, `npm start`

**This repository** has two parts:

- **Java (Spring PetClinic)** at the repo root: needs a JDK installed, then `./mvnw test` or `./mvnw spring-boot:run`
- **Python (Flask)** under `find_about_yourself/`: `cd find_about_yourself && python3 -m pip install -r requirements.txt && python3 app.py`

Fix failures locally before you push.

---

## 6. Commit your changes

```bash
git status
git diff                    # optional: review changes
git add -p                  # or: git add <files>  or  git add -A
git commit -m "Short description of what you changed"
```

Repeat the edit → test → commit cycle as needed.

---

## 7. Push the feature branch to GitHub

First push of the branch:

```bash
git push -u origin your-branch-name
```

Later pushes on the same branch:

```bash
git push
```

`-u` sets the upstream so `git push` / `git pull` know which remote branch to use.

---

## 8. Create a pull request (PR)

1. Open the repo on GitHub: [github.com/RDLOCALORG/yourself](https://github.com/RDLOCALORG/yourself)
2. GitHub often shows a banner **“Compare & pull request”** after a recent push—use that, **or**
3. Go to **Pull requests** → **New pull request**
4. Set **base:** `main` (or your default branch) ← **compare:** `your-branch-name`
5. Add a title and description, then **Create pull request**

Direct compare link (replace `your-branch-name` with your branch):

`https://github.com/RDLOCALORG/yourself/compare/main...your-branch-name`

---

## 9. Merge the PR into `main`

On the PR page, when reviews and checks (if any) are satisfied:

1. Click **Merge pull request** (or your team’s merge option: squash merge, rebase merge)
2. Confirm the merge

The `main` branch on GitHub now includes your work.

---

## 10. Update your local `main` after the merge

```bash
git checkout main
git pull origin main
```

You can delete the feature branch locally if you are done:

```bash
git branch -d your-branch-name
```

(Optional) Delete the remote branch on GitHub from the PR page after merge, or:

```bash
git push origin --delete your-branch-name
```

---

## Shortcut: create a branch from remote `main` without updating local `main` first

```bash
git fetch origin
git checkout -b your-branch-name origin/main
```

---

## Uncommitted work when switching branches

If Git refuses to switch branches because of local changes:

- **Stash:** `git stash -u`, switch branch, then `git stash pop`
- **Or** commit the work on the current branch first

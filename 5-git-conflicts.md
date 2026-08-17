## Task

1. Create a `feature` branch from `main`.
2. On `feature`, modify the same line in `app.py` and commit it.
3. Switch to `main` and modify the same line differently.
4. Commit the change on `main`.
5. Merge `feature` into `main`.
6. Resolve the merge conflict.
7. Commit the resolved merge.
8. Delete the `feature` branch.

## Solution

```bash
# Create and switch to the feature branch
git switch -c feature

# Modify app.py on the feature branch
echo "print('Hello from feature')" > app.py

# Stage and commit the feature change
git add app.py
git commit -m "Update app.py on feature"

# Switch back to main
git switch main

# Make a different change to the same line
echo "print('Hello from main')" > app.py

# Stage and commit the main change
git add app.py
git commit -m "Update app.py on main"

# Merge feature into main — this creates a conflict
git merge feature

# Check which files have conflicts
git status

# Open app.py and resolve the conflict
# Remove the conflict markers and keep the desired code

# Stage the resolved file
git add app.py

# Complete the merge with a commit
git commit -m "Resolve merge conflict"

# Delete the feature branch
git branch -d feature

# Verify the final branch and commit history
git branch
git log --oneline --graph --decorate -5
```

## git log

`git log --oneline --graph --decorate -5` is a convenient way to view the **recent Git history as a compact branch graph**.

Breakdown:

```bash
git log --oneline --graph --decorate -5
```

* **`git log`** → shows the commit history.
* **`--oneline`** → displays each commit on a single, short line instead of showing the full commit details.
* **`--graph`** → draws an ASCII graph showing how branches and merges relate to each other.
* **`--decorate`** → shows labels such as `HEAD`, `main`, and branch names next to commits.
* **`-5`** → shows only the **5 most recent commits**.

For example, after your conflict-resolution exercise, you might see:

```text
*   a1b2c3d (HEAD -> main) Resolve merge conflict
|\
| * d4e5f6g feature: Update app.py
* | h7i8j9k main: Update app.py
|/
* k1l2m3n Add app.py
```

The important part is that you can visually see **where `main` and `feature` diverged and where they were merged**.

It's especially useful when learning branches because `--graph` makes the branch history much easier to understand than a plain `git log`.

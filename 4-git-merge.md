## Task

1. Continue from the previous exercise with the `feature` branch.
2. Switch to `feature` and create another change.
3. Commit the change.
4. Switch to `main`.
5. Merge `feature` into `main`.
6. Verify the changes are on `main`.
7. Delete the `feature` branch.

## Solution

```bash
# Switch to the feature branch
git switch feature

# Create another file on the feature branch
echo "Feature complete!" > feature.txt

# Stage the new file
git add feature.txt

# Commit the change
git commit -m "Complete feature"

# Switch back to main
git switch main

# Merge the feature branch into main
git merge feature

# Verify the feature changes are now on main
ls

# Delete the feature branch after merging
git branch -d feature

# Verify that the feature branch has been deleted
git branch
```

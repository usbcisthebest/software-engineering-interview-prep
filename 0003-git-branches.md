## Task

1. Start on the `main` branch.
2. Create a new branch called `feature`.
3. Switch to the `feature` branch.
4. Create a new file called `feature.py`.
5. Commit the file.
6. Switch back to `main`.
7. Verify that `feature.py` is not present on `main`.
8. Switch back to `feature` and verify the file is present.

## Solution

```bash
# Make sure you're on the main branch
git switch main

# Create a new branch called feature
git branch feature

# Switch to the feature branch
git switch feature

# Create a new file on the feature branch
echo "print('Hello from feature')" > feature.py

# Stage the new file
git add feature.py

# Commit the new file
git commit -m "Add feature.py"

# Switch back to the main branch
git switch main

# List files to verify feature.py is not on main
ls

# Switch back to the feature branch
git switch feature

# List files to verify feature.py is present
ls
```

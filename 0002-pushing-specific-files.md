## Task

1. Create `app.py`, `README.md`, and `notes.txt`.
2. Add only `app.py` to the staging area.
3. Commit `app.py`.
4. Stage all remaining files.
5. Remove `notes.txt` from the staging area without deleting it.
6. Commit and push the remaining changes.

## Solution

```bash
# Create three files
echo "print('Hello World')" > app.py
echo "# My Project" > README.md
echo "Temporary notes" > notes.txt

# Add only app.py to the staging area
git add app.py

# Commit only app.py
git commit -m "Add app.py"

# Stage all remaining files
git add .

# Remove notes.txt from the staging area without deleting it
git restore --staged notes.txt

# Commit the staged README.md
git commit -m "Add README"

# Push the commits to the remote repository
git push
```

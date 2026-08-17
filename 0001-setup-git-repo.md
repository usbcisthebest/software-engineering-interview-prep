## Task

1. Initialize a Git repository.
2. Create `sample.txt` with some content.
3. Stage and commit the file.
4. Add a remote repository as `origin`.
5. Rename the branch to `main` and push it.
6. Create two more files and push the changes.
7. Create `foo.py`, stage everything, then unstage only `foo.py` without deleting it.

## Solution

```bash
# Initialize a new Git repository
git init

# Create a sample file with some content
echo "This is a sample file." > sample.txt

# Stage the sample file
git add sample.txt

# Commit the staged file
git commit -m "Initial commit: Add sample.txt"

# Connect the local repository to the remote repository 
# HTTPS example: https://github.com/username/my-great-project.git 
# SSH example: git@github.com:username/my-great-project.git
git remote add origin YOUR_REMOTE_URL

# Rename the current branch to main
git branch -M main

# Push main to the remote and set the upstream branch
git push -u origin main

# Create two additional files
echo "# My Project" > README.md
echo "print('Hello, Git!')" > hello.py

# Stage all new and modified files
git add .

# Commit the changes
git commit -m "Add README and hello script"

# Push the changes to the remote repository
git push
```

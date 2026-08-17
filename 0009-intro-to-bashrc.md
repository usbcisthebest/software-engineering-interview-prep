## Task 1: Environment Variables

1. Create an environment variable in the current terminal.
2. Verify that it works.
3. Open a new terminal and verify that the variable does not persist.
4. Add the variable to `.bashrc`.
5. Reload `.bashrc` and verify that the variable is available.
6. Open a new terminal and verify that it persists.

## Task 2: Aliases

1. Create an alias called `gs` for `git status`.
2. Verify that the alias works.
3. Open a new terminal and verify that the alias does not persist.
4. Add the alias to `.bashrc`.
5. Reload `.bashrc`.
6. Verify that the alias now works.
7. Open a new terminal and verify that the alias persists.

## Solution

### Task 1

1. Set an environment variable: `export PROJECT_NAME="my-project"`
2. Verify it: `echo $PROJECT_NAME`
3. Open a new terminal and check it: `echo $PROJECT_NAME`
4. Open `.bashrc`: `vim ~/.bashrc`
5. Add:

```bash id="2by7cd"
export PROJECT_NAME="my-project"  # Set an environment variable for Bash sessions
```

6. Save and exit Vim: `:wq`
7. Reload `.bashrc`: `source ~/.bashrc`
8. Verify it: `echo $PROJECT_NAME`
9. Open a new terminal and verify again: `echo $PROJECT_NAME`

### Task 2

1. Create the alias: `alias gs='git status'`
2. Verify it: `gs`
3. Open a new terminal and run `gs` to see that the alias does not persist.
4. Open `.bashrc`: `vim ~/.bashrc`
5. Add:

```bash id="n4m7yx"
alias gs='git status'  # Create a shortcut for git status
```

6. Save and exit Vim: `:wq`
7. Reload `.bashrc`: `source ~/.bashrc`
8. Verify the alias: `gs`
9. Open a new terminal and run `gs` to verify that the alias persists.

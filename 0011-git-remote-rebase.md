## Tasks

### Task 1: Pull with Rebase

Create a situation where your local and remote branches diverge:

```text
        C  ← local commit
       /
A---B
       \
        D  ← remote commit
```

1. Create a local commit.
2. Create a different commit on the remote repository.
3. Try a regular `git pull` and observe the error.
4. Resolve the divergence using `git pull --rebase`.
5. Verify the resulting history.

### Task 2: Pull with No-Rebase

Repeat the same scenario:

```text
        C  ← local commit
       /
A---B
       \
        D  ← remote commit
```

1. Create a local commit.
2. Create a different commit on the remote repository.
3. Try a regular `git pull` and observe the error.
4. Resolve the divergence using `git pull --no-rebase`.
5. Verify the resulting history.

## Solution

### Task 1: Pull with Rebase

1. Create a new branch: `git switch -c rebase-demo`
2. Create a local change: `echo "Local change" > local.txt`
3. Commit it: `git add local.txt && git commit -m "Add local change"`
4. Create a different commit on the remote repository, for example by adding `remote.txt` through GitHub.
5. Try a regular pull: `git pull`
6. Observe the error asking you to specify how to reconcile the divergent branches.
7. Pull using rebase: `git pull --rebase`
8. View the history: `git log --oneline --graph --decorate -5`

After the rebase:

```text
A---B---D---C'
```

The local commit is replayed on top of the remote commit.

### Task 2: Pull with No-Rebase

1. Create a new branch: `git switch -c merge-demo`
2. Create a local change: `echo "Local change" > local.txt`
3. Commit it: `git add local.txt && git commit -m "Add local change"`
4. Create a different commit on the remote repository, for example by adding `remote.txt` through GitHub.
5. Try a regular pull: `git pull`
6. Observe the error asking you to specify how to reconcile the divergent branches.
7. Pull using merge: `git pull --no-rebase`
8. View the history: `git log --oneline --graph --decorate -5`

After the merge:

```text
        C
       / \
A---B     M
       \ /
        D
```

The two histories are preserved and Git creates a merge commit.

## Task

Practice rebasing and merging local branches.

### Task 1: Rebase

Start with this history:

```text
A---B  main
     \
      C  feature
```

1. Create a `feature` branch from `main`.
2. Add and commit a change on `feature`.
3. Switch to `main` and add a different commit.
4. Switch back to `feature`.
5. Rebase `feature` onto `main`.
6. Verify the history.

The goal is to bring the latest `main` changes into `feature` and then replay the feature commits on top:

```text
A---B---D---C'  feature
        ↑
       main
```

### Task 2: Merge

Repeat the same branching scenario:

```text
A---B---D  main
     \
      C  feature
```

1. Create a `merge-demo` branch from `main`.
2. Add and commit a change on `merge-demo`.
3. Switch to `main` and add a different commit.
4. Switch back to `merge-demo`.
5. Merge `main` into `merge-demo`.
6. Verify the history.

## Solution

### Task 1: Rebase

1. Create and switch to the feature branch: `git switch -c feature`
2. Create a feature change: `echo "Feature change" > feature.txt`
3. Commit it: `git add feature.txt && git commit -m "Add feature"`
4. Switch to main: `git switch main`
5. Create a main change: `echo "Main change" > main.txt`
6. Commit it: `git add main.txt && git commit -m "Add main change"`
7. Switch back to feature: `git switch feature`
8. Rebase feature onto main: `git rebase main`
9. View the history: `git log --oneline --graph --decorate -5`

`git rebase main` brings the latest `main` changes into the current `feature` branch and then replays the feature commits on top of them.

Result:

```text
A---B---D---C'  feature
        ↑
       main
```

### Task 2: Merge

1. Create and switch to the merge branch: `git switch -c merge-demo`
2. Create a feature change: `echo "Feature change" > merge-feature.txt`
3. Commit it: `git add merge-feature.txt && git commit -m "Add merge feature"`
4. Switch to main: `git switch main`
5. Create a main change: `echo "Main change" > merge-main.txt`
6. Commit it: `git add merge-main.txt && git commit -m "Add main change"`
7. Switch back to merge-demo: `git switch merge-demo`
8. Merge main into the current branch: `git merge main`
9. View the history: `git log --oneline --graph --decorate -5`

Result:

```text
        C
       / \
A---B---D---M  merge-demo
```

The merge brings `main` into `merge-demo` while preserving the existing branch history.

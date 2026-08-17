## Task

1. Open `notes.txt` using Vim.
2. Add three lines of text.
3. Save and exit.
4. Reopen the file and add a fourth line.
5. Save and exit.
6. Reopen the file to verify the changes.

## Solution

1. Open the file: `vim notes.txt`
2. Enter insert mode: press `i`
3. Insert:

```text
Line 1
Line 2
Line 3
```

4. Exit insert mode: press `Esc`
5. Save and exit: type `:wq` and press `Enter`
6. Reopen the file: `vim notes.txt`
7. Go to the end: press `G`
8. Create a new line: press `o`
9. Insert:

```text
Line 4
```

10. Exit insert mode: press `Esc`
11. Save and exit: type `:wq` and press `Enter`
12. Verify the file: `vim notes.txt`

## Task 1: Using Vim

1. Create `profile.txt` using Vim.
2. Add five lines of text.
3. Navigate through the file.
4. Add a new line.
5. Delete, copy, and paste a line.
6. Search for a word.
7. Replace the word and undo the replacement.
8. Save and exit.

## Task 2: Line Numbers

1. Enable absolute line numbers.
2. Enable relative line numbers.
3. Verify both are displayed.
4. Disable relative line numbers.
5. Verify only absolute line numbers are displayed.
6. Disable absolute line numbers.
7. Verify that no line numbers are displayed.

## Solution

### Task 1

1. Open the file: `vim profile.txt`
2. Enter insert mode: press `i`
3. Insert:

```text id="w6s1ak"
Name: John
Role: Software Engineer
Location: Dublin
Language: Python
Experience: 5 years
```

4. Exit insert mode: press `Esc`
5. Move down: press `j`
6. Move up: press `k`
7. Go to the first line: press `gg`
8. Go to the last line: press `G`
9. Add a line below: press `o`
10. Insert:

```text id="u9f2lo"
Company: Example Corp
```

11. Exit insert mode: press `Esc`
12. Delete the current line: press `dd`
13. Copy the current line: press `yy`
14. Paste below: press `p`
15. Search for `Python`: type `/Python` and press `Enter`
16. Replace `Python`: press `cw`, type `Java`, then press `Esc`
17. Undo the replacement: press `u`
18. Save and exit: type `:wq` and press `Enter`

### Task 2

1. Open the file: `vim profile.txt`
2. Enable absolute line numbers: `:set number`
3. Enable relative line numbers: `:set relativenumber`
4. Verify both are displayed.
5. Disable relative line numbers: `:set norelativenumber`
6. Verify only absolute line numbers are displayed.
7. Disable absolute line numbers: `:set nonumber`
8. Verify that no line numbers are displayed.
9. Save and exit: `:wq`

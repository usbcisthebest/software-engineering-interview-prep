## Task

Configure Vim using `~/.vimrc` so your preferred settings are applied automatically every time Vim starts.

1. Open your `~/.vimrc` file.
2. Enable absolute line numbers.
3. Disable relative line numbers.
4. Enable syntax highlighting.
5. Set indentation to 4 spaces.
6. Save the configuration.
7. Open a new Vim session and verify the settings.

## Solution

1. Open the Vim configuration file: `vim ~/.vimrc`
2. Enter insert mode: press `i`
3. Add the following configuration:

```vim
set number              " Show absolute line numbers
set norelativenumber    " Disable relative line numbers
syntax on               " Enable syntax highlighting
set tabstop=4           " Display a tab as 4 spaces
set shiftwidth=4        " Use 4 spaces for indentation
set expandtab           " Convert tabs to spaces
```

4. Exit insert mode: press `Esc`
5. Save and exit: type `:wq` and press `Enter`
6. Open a new Vim session: `vim test.py`
7. Verify that absolute line numbers are displayed.
8. Verify that relative line numbers are disabled.
9. Verify that syntax highlighting is enabled.
10. Verify that pressing `Tab` inserts spaces instead of a tab character.

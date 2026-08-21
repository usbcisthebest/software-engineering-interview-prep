## Task 1: Create a script that backs up a file

Create `backup.sh` that accepts a filename and creates a copy with `.bak` appended to its name.

For example:

```text
books.db → books.db.bak
```

### Solution

```bash
#!/bin/bash

file=$1

if [ ! -f "$file" ]; then
    echo "File does not exist: $file"
    exit 1
fi

cp "$file" "$file.bak"

echo "Backup created: $file.bak"
```

Run:

```bash
./backup.sh books.db
```

Here, `exit 1` indicates that the script failed. A successful script can use `exit 0`.

---

## Task 2: Create a script that counts files in a directory

Create `count-files.sh` that accepts a directory and prints how many regular files it contains.

### Solution

```bash
#!/bin/bash

directory=$1

if [ ! -d "$directory" ]; then
    echo "Directory does not exist: $directory"
    exit 1
fi

count=$(find "$directory" -type f | wc -l)

echo "Number of files: $count"
```

Run:

```bash
./count-files.sh .
```

`find` finds the files, while `wc -l` counts them.

The result is stored using **command substitution**:

```bash
count=$(...)
```

---

## Task 3: Create a script using functions

Create `file-info.sh` that checks a file and displays its size and permissions.

### Solution

```bash
#!/bin/bash

file=$1

check_file() {
    if [ ! -f "$file" ]; then
        echo "File does not exist: $file"
        exit 1
    fi
}

show_size() {
    ls -lh "$file"
}

show_permissions() {
    stat -f "%Sp" "$file"
}

check_file
show_size
show_permissions
```

Run:

```bash
./file-info.sh books.db
```

Functions allow us to split a script into smaller, reusable pieces.

---

## Task 4: Process multiple files

Create `list-files.sh` that accepts multiple filenames and reports whether each file exists.

For example:

```bash
./list-files.sh books.db users.db config.txt
```

### Solution

```bash
#!/bin/bash

for file in "$@"
do
    if [ -f "$file" ]; then
        echo "$file: exists"
    else
        echo "$file: missing"
    fi
done
```

`$@` represents **all arguments** passed to the script.

The `for` loop processes each argument one at a time.

---

## Task 5: Build a command-based utility

Create `books.sh` that accepts a command:

```text
./books.sh list
./books.sh count
```

For `list`, display the contents of `books.txt`.

For `count`, display the number of lines in the file.

### Solution

```bash
#!/bin/bash

case "$1" in
    list)
        cat books.txt
        ;;
    count)
        wc -l < books.txt
        ;;
    *)
        echo "Usage: ./books.sh {list|count}"
        exit 1
        ;;
esac
```

For example:

```bash
./books.sh list
```

runs:

```bash
cat books.txt
```

while:

```bash
./books.sh count
```

runs:

```bash
wc -l < books.txt
```

The `case` statement is useful when a script supports multiple commands.

## Task 1: Find large files

Create `find-large.sh` that accepts a directory and finds files larger than 10 MB.

For example:

```bash
./find-large.sh .
```

### Solution

```bash
#!/bin/bash

directory=$1

if [ ! -d "$directory" ]; then
    echo "Directory does not exist: $directory"
    exit 1
fi

find "$directory" -type f -size +10M
```

The important part is:

```bash
find "$directory" -type f -size +10M
```

It searches the directory for regular files larger than 10 MB.

---

## Task 2: Search a log file for errors

Create `find-errors.sh` that accepts a log file and displays lines containing `ERROR`.

### Solution

```bash
#!/bin/bash

file=$1

if [ ! -f "$file" ]; then
    echo "File does not exist: $file"
    exit 1
fi

grep "ERROR" "$file"
```

Run:

```bash
./find-errors.sh app.log
```

You can also count the errors:

```bash
grep "ERROR" "$file" | wc -l
```

Here `|` sends the output of `grep` to `wc`.

---

## Task 3: Create a timestamped backup

Create `backup.sh` that creates a backup with the current date and time in its filename.

For example:

```text
books.db
→
books.db.2026-08-21-2230.bak
```

### Solution

```bash
#!/bin/bash

file=$1

if [ ! -f "$file" ]; then
    echo "File does not exist: $file"
    exit 1
fi

timestamp=$(date +"%Y-%m-%d-%H%M")
backup="$file.$timestamp.bak"

cp "$file" "$backup"

echo "Backup created: $backup"
```

The command:

```bash
date +"%Y-%m-%d-%H%M"
```

generates the timestamp.

We capture its output using command substitution:

```bash
timestamp=$(...)
```

---

## Task 4: Find old log files

Create `clean-logs.sh` that finds `.log` files older than 7 days.

For safety, the first version should **only display the files** rather than delete them.

### Solution

```bash
#!/bin/bash

directory=$1

if [ ! -d "$directory" ]; then
    echo "Directory does not exist: $directory"
    exit 1
fi

find "$directory" -name "*.log" -type f -mtime +7
```

The important part is:

```bash
-mtime +7
```

which finds files whose modification time is more than 7 days old.

Once you're confident about the files being selected, they could be deleted with:

```bash
find "$directory" -name "*.log" -type f -mtime +7 -delete
```

Be careful with `-delete` because the files are permanently removed.

---

## Task 5: Create a simple system information script

Create `system-info.sh` that displays:

* current user
* hostname
* current directory
* current date
* disk usage

### Solution

```bash
#!/bin/bash

echo "User: $(whoami)"
echo "Hostname: $(hostname)"
echo "Directory: $(pwd)"
echo "Date: $(date)"
echo "Disk usage:"
df -h
```

Run:

```bash
./system-info.sh
```

This combines several commands using **command substitution**.

For example:

```bash
$(whoami)
```

runs `whoami` and puts its output into the `echo` command.

---

## Task 6: Create a compressed archive of a directory

Create `backup-directory.sh` that accepts a directory and creates a compressed `.tar.gz` archive.

For example:

```bash
./backup-directory.sh my-project
```

should create:

```text
my-project.tar.gz
```

### Solution

```bash
#!/bin/bash

directory=$1

if [ ! -d "$directory" ]; then
    echo "Directory does not exist: $directory"
    exit 1
fi

tar -czf "$directory.tar.gz" "$directory"

echo "Archive created: $directory.tar.gz"
```

The command:

```bash
tar -czf "$directory.tar.gz" "$directory"
```

creates a compressed archive.

The options mean:

```text
-c  create an archive
-z  compress using gzip
-f  specify the archive filename
```

So:

```bash
tar -czf backup.tar.gz my-project
```

means:

> Create a gzip-compressed archive called `backup.tar.gz` containing `my-project`.

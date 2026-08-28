## Task 1: Create a path to a file

Your application stores its book data inside a `data` directory. Create a `Path` object pointing to `books.json` inside that directory, then print the path.

### Solution

```python
from pathlib import Path

books_file = Path("data") / "books.json"

print(books_file)
```

Output:

```text
data/books.json
```

`Path` represents a filesystem path. Using `/` to combine paths is clearer and more portable than manually building strings such as `"data/books.json"`.

---

## Task 2: Check whether a file exists

Before your application tries to read `books.json`, check whether the file actually exists. Print an appropriate message.

### Solution

```python
from pathlib import Path

books_file = Path("data/books.json")

if books_file.exists():
    print("Books file exists")
else:
    print("Books file does not exist")
```

Output:

```text
Books file exists
```

`exists()` returns `True` if the path exists and `False` otherwise.

---

## Task 3: Check whether a path is a file or directory

Your application receives a path from a user. Determine whether the path points to a file, a directory, or something that does not exist.

### Solution

```python
from pathlib import Path

path = Path("data")

if path.is_file():
    print("This is a file")
elif path.is_dir():
    print("This is a directory")
else:
    print("Path does not exist")
```

Output:

```text
This is a directory
```

Use:

* `is_file()` to check for a file
* `is_dir()` to check for a directory

---

## Task 4: Create a directory

Your application needs a directory called `backups` to store backup files. Create it if it doesn't already exist.

### Solution

```python
from pathlib import Path

backup_dir = Path("backups")

backup_dir.mkdir(exist_ok=True)

print("Backup directory is ready")
```

Output:

```text
Backup directory is ready
```

`mkdir()` creates a directory.

`exist_ok=True` prevents an error if the directory already exists.

---

## Task 5: List files in a directory

A log-processing script needs to see all the files inside a `logs` directory. List each item in the directory.

### Solution

```python
from pathlib import Path

logs_dir = Path("logs")

for path in logs_dir.iterdir():
    print(path)
```

Example output:

```text
logs/app.log
logs/error.log
logs/access.log
```

`iterdir()` returns the items directly inside a directory.

---

## Task 6: Find all log files

Your application stores different types of files in a directory, but you only want to process `.log` files.

Use `glob()` to find them.

### Solution

```python
from pathlib import Path

logs_dir = Path("logs")

for file in logs_dir.glob("*.log"):
    print(file)
```

Example output:

```text
logs/app.log
logs/error.log
logs/access.log
```

`glob("*.log")` finds paths matching the pattern.

The `*` means "any number of characters".

---

## Task 7: Get information about a file

A backup tool needs to display the filename and file extension of a file.

### Solution

```python
from pathlib import Path

file = Path("books.json")

print("Name:", file.name)
print("Extension:", file.suffix)
```

Output:

```text
Name: books.json
Extension: .json
```

Useful `Path` properties include:

```text
name    → books.json
stem    → books
suffix  → .json
```

---

## Task 8: Rename a file

An application has created a file called `old_books.json`, but the filename should be changed to `books.json`.

### Solution

```python
from pathlib import Path

old_file = Path("old_books.json")
new_file = Path("books.json")

old_file.rename(new_file)

print("File renamed")
```

Output:

```text
File renamed
```

`rename()` changes the file's name or location.

---

## Task 9: Delete a file

A temporary file is no longer needed. Delete `temp.txt`.

### Solution

```python
from pathlib import Path

file = Path("temp.txt")

if file.exists():
    file.unlink()
    print("File deleted")
else:
    print("File does not exist")
```

Output:

```text
File deleted
```

`unlink()` deletes a file.

---

## Task 10: Find and process JSON files

A program stores several JSON files inside a `data` directory. Find every `.json` file and print its filename.

### Solution

```python
from pathlib import Path

data_dir = Path("data")

for file in data_dir.glob("*.json"):
    print("Found:", file.name)
```

Example output:

```text
Found: books.json
Found: users.json
Found: settings.json
```

This combines `pathlib` with a pattern you'll use frequently:

```python
for file in directory.glob("*.extension"):
```

It allows your program to process files based on their type instead of hardcoding every filename.

## Task 1: Save a note to a file

Create a Python program that saves a note to a file called `notes.txt`.

### Solution

```python
note = "Buy groceries after work"

with open("notes.txt", "w") as file:
    file.write(note)

print("Note saved")
```

Output:

```text
Note saved
```

`"w"` opens a file for writing. It creates the file if it does not exist and overwrites its contents if it already exists.

---

## Task 2: Read a saved note

Read the contents of `notes.txt` and display the note.

### Solution

```python
with open("notes.txt", "r") as file:
    note = file.read()

print(note)
```

Output:

```text
Buy groceries after work
```

`read()` reads the entire contents of the file.

---

## Task 3: Add a new entry to a log file

An application writes events to `app.log`. Add a new entry without removing the existing entries.

### Solution

```python
log_entry = "User logged in\n"

with open("app.log", "a") as file:
    file.write(log_entry)

print("Log entry added")
```

Output:

```text
Log entry added
```

`"a"` opens a file for appending. New content is added to the end of the file.

---

## Task 4: Read a log file one line at a time

A log file contains multiple entries. Read and process each line individually.

### Solution

```python
with open("app.log", "r") as file:
    for line in file:
        print(line.strip())
```

Example output:

```text
User logged in
User created a project
User logged out
```

Iterating over a file reads it one line at a time. `strip()` removes the newline character from the end before printing.

---

## Task 5: Save a list of tasks

You have a list of tasks that should be saved to a file, with one task per line.

### Solution

```python
tasks = [
    "Reply to emails",
    "Finish report",
    "Create backup",
]

with open("tasks.txt", "w") as file:
    for task in tasks:
        file.write(task + "\n")

print("Tasks saved")
```

Output:

```text
Tasks saved
```

The file will contain:

```text
Reply to emails
Finish report
Create backup
```

---

## Task 6: Handle a missing file

Try to read a configuration file. If it does not exist, display a helpful message instead of crashing the program.

### Solution

```python
try:
    with open("config.txt", "r") as file:
        config = file.read()

    print(config)

except FileNotFoundError:
    print("Configuration file not found")
```

Output if the file does not exist:

```text
Configuration file not found
```

`FileNotFoundError` is raised when Python tries to open a file for reading that does not exist.

---

## Task 7: Write and read a file using `with`

Create a file, write a message to it, then read and display the saved message.

### Solution

```python
with open("message.txt", "w") as file:
    file.write("Hello from Python!")

with open("message.txt", "r") as file:
    message = file.read()

print(message)
```

Output:

```text
Hello from Python!
```

Using:

```python
with open(...) as file:
```

automatically closes the file when the block finishes, even if an error occurs.

---

## Task 8: Create an empty file

Create an empty file called `report.txt`.

### Solution

```python
with open("report.txt", "w"):
    pass

print("File created")
```

Output:

```text
File created
```

Opening a file with `"w"` creates it if it does not already exist. The `pass` statement means that nothing is written to the file.

> Note: If `report.txt` already exists, `"w"` will overwrite its contents. If you only want to create a new file and fail when it already exists, use `"x"` mode.

```python
with open("report.txt", "x"):
    pass
```

---

## Task 9: Delete a file

Delete an old temporary file called `temp.txt`.

### Solution

```python
import os

os.remove("temp.txt")

print("File deleted")
```

Output:

```text
File deleted
```

`os.remove()` deletes a file.

If the file might not exist, check before deleting it:

```python
import os

if os.path.exists("temp.txt"):
    os.remove("temp.txt")
    print("File deleted")
else:
    print("File not found")
```

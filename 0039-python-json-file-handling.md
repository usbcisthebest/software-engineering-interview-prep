## Task 1: Read application settings from a JSON file

An application stores its settings in `config.json`. Read the file and display the configured theme.

Assume `config.json` contains:

```json
{
    "theme": "dark",
    "notifications": true
}
```

### Solution

```python
import json

with open("config.json", "r") as file:
    config = json.load(file)

print(config["theme"])
```

Output:

```text
dark
```

`json.load()` reads JSON from a file and converts it into a Python object.

---

## Task 2: Save user preferences to a JSON file

A user selects preferences in an application. Save those preferences to `preferences.json`.

### Solution

```python
import json

preferences = {
    "theme": "dark",
    "notifications": True,
    "language": "en",
}

with open("preferences.json", "w") as file:
    json.dump(preferences, file)

print("Preferences saved")
```

Output:

```text
Preferences saved
```

`json.dump()` converts a Python object to JSON and writes it directly to a file.

The file will contain:

```json
{"theme": "dark", "notifications": true, "language": "en"}
```

---

## Task 3: Update a value in a JSON file

An application stores settings in `config.json`. Change the theme from `dark` to `light` and save the updated settings.

### Solution

```python
import json

with open("config.json", "r") as file:
    config = json.load(file)

config["theme"] = "light"

with open("config.json", "w") as file:
    json.dump(config, file)

print("Theme updated")
```

Output:

```text
Theme updated
```

The process is:

```text
Read JSON → Update Python object → Write JSON
```

---

## Task 4: Save multiple books to a JSON file

You have several books represented as Python dictionaries. Save them as a list in `books.json`.

### Solution

```python
import json

books = [
    {
        "title": "1984",
        "author": "George Orwell",
        "year": 1949,
    },
    {
        "title": "Dune",
        "author": "Frank Herbert",
        "year": 1965,
    },
]

with open("books.json", "w") as file:
    json.dump(books, file)

print("Books saved")
```

Output:

```text
Books saved
```

The resulting JSON file represents a list of book objects.

---

## Task 5: Add a book to an existing JSON file

Read the books from `books.json`, add a new book, and save the updated list back to the file.

### Solution

```python
import json

with open("books.json", "r") as file:
    books = json.load(file)

new_book = {
    "title": "Foundation",
    "author": "Isaac Asimov",
    "year": 1951,
}

books.append(new_book)

with open("books.json", "w") as file:
    json.dump(books, file)

print("Book added")
```

Output:

```text
Book added
```

Unlike a CSV file, JSON data is usually loaded into a Python object, modified, and then written back to the file.

---

## Task 6: Handle missing or invalid JSON data

Read `config.json`. If the file is missing or contains invalid JSON, display a helpful message instead of crashing the program.

### Solution

```python
import json

try:
    with open("config.json", "r") as file:
        config = json.load(file)

    print(config)

except FileNotFoundError:
    print("Configuration file not found")

except json.JSONDecodeError:
    print("Configuration file contains invalid JSON")
```

Output when the file is missing:

```text
Configuration file not found
```

Output when the JSON is invalid:

```text
Configuration file contains invalid JSON
```

`json.JSONDecodeError` is raised when Python cannot parse the contents as valid JSON.

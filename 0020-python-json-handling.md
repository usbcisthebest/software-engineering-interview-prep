# Handling JSON in Python

## Objective

Learn how to convert between Python objects, JSON strings, and JSON files.

---

## Task 1: Convert a book to JSON

Create a Python dictionary representing this book:

* ID: `1`
* Title: `1984`
* Author: `George Orwell`

Convert it to a JSON string and print the result and its type.

### Solution

```python
import json

book = {
    "id": 1,
    "title": "1984",
    "author": "George Orwell"
}

json_string = json.dumps(book)

print(json_string)
print(type(json_string))
```

Output:

```text
{"id": 1, "title": "1984", "author": "George Orwell"}
<class 'str'>
```

`json.dumps()` converts a **Python object → JSON string**.

---

## Task 2: Convert JSON to a Python object

Given this JSON string:

```text
{"id": 1, "title": "1984", "author": "George Orwell"}
```

Convert it to a Python object and print the object and its type.

### Solution

```python
import json

json_string = '{"id": 1, "title": "1984", "author": "George Orwell"}'

book = json.loads(json_string)

print(book)
print(type(book))
```

Output:

```text
{'id': 1, 'title': '1984', 'author': 'George Orwell'}
<class 'dict'>
```

`json.loads()` converts a **JSON string → Python object**.

---

## Task 3: Save a book as JSON

Take this Python dictionary and save it to a file called `book.json`:

```python
book = {
    "id": 2,
    "title": "Dune",
    "author": "Frank Herbert"
}
```

Then print the book and its type.

### Solution

```python
import json

book = {
    "id": 2,
    "title": "Dune",
    "author": "Frank Herbert"
}

with open("book.json", "w") as file:
    json.dump(book, file)

```

`json.dump()` writes a **Python object → JSON file**.

---

## Task 4: Read a JSON file

The file `book.json` contains:

```json
{
    "id": 2,
    "title": "Dune",
    "author": "Frank Herbert"
}
```

Read the file into Python and print the book and its type.

### Solution

```python
import json

with open("book.json", "r") as file:
    book = json.load(file)

print(book)
print(type(book))
```

Output:

```text
{'id': 2, 'title': 'Dune', 'author': 'Frank Herbert'}
<class 'dict'>
```

`json.load()` converts a **JSON file → Python object**.

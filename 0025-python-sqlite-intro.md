# Introduction to SQLite with Python

## Objective

Learn the basics of SQLite using Python's built-in `sqlite3` module.

We'll create a small books database and learn how to:

* create a database
* create a table
* insert data
* read data
* update data
* delete data

## Tasks

1. Create a SQLite database.
2. Create a `books` table.
3. Insert books into the table.
4. Read books from the database.
5. Update a book.
6. Delete a book.

---

## Task 1: Create a SQLite database

Create a database called `books.db`.

### Solution

```python
import sqlite3

connection = sqlite3.connect("books.db")

print("Database created")

connection.close()
```

Output:

```text
Database created
```

If `books.db` doesn't exist, SQLite creates it automatically.

If you run the above code in `database.py` file then `books.db` will be auto-created in the same directory:

```
my-project/
├── database.py
└── books.db
```

---

## Task 2: Create a `books` table

Create a table with:

* `id`
* `title`
* `author`

The `id` should uniquely identify each book.

### Solution

```python
import sqlite3

connection = sqlite3.connect("books.db")

cursor = connection.cursor()

cursor.execute("""
    CREATE TABLE books (
        id INTEGER PRIMARY KEY,
        title TEXT,
        author TEXT
    )
""") # execute = run SQL

connection.commit() # commit = save changes

print("Books table created")

connection.close()
```

Output:

```text
Books table created
```

`PRIMARY KEY` means each book gets a unique ID.

---

## Task 3: Insert books

Insert these two books:

```text
1984 — George Orwell
Dune — Frank Herbert
```

### Solution

```python
import sqlite3

connection = sqlite3.connect("books.db")
cursor = connection.cursor()

cursor.execute(
    "INSERT INTO books (title, author) VALUES (?, ?)",
    ("1984", "George Orwell")
)

cursor.execute(
    "INSERT INTO books (title, author) VALUES (?, ?)",
    ("Dune", "Frank Herbert")
)

connection.commit()

print("Books inserted")

connection.close()
```

Output:

```text
Books inserted
```

The `?` placeholders allow us to safely provide values separately from the SQL statement.

---

## Task 4: Read the books

Read all books from the database and print them.

### Solution

```python
import sqlite3

connection = sqlite3.connect("books.db")
cursor = connection.cursor()

cursor.execute("SELECT * FROM books")

books = cursor.fetchall()

for book in books:
    print(book)

connection.close()
```

Output:

```text
(1, '1984', 'George Orwell')
(2, 'Dune', 'Frank Herbert')
```

Each row is returned as a Python tuple.

---

## Task 5: Update a book

Change the title of book `1` from `1984` to `Animal Farm`.

### Solution

```python
import sqlite3

connection = sqlite3.connect("books.db")
cursor = connection.cursor()

cursor.execute(
    "UPDATE books SET title = ? WHERE id = ?",
    ("Animal Farm", 1)
)

connection.commit()

print("Book updated")

connection.close()
```

Output:

```text
Book updated
```

Verify the change:

```python
cursor.execute("SELECT * FROM books")

for book in cursor.fetchall():
    print(book)
```

Output:

```text
(1, 'Animal Farm', 'George Orwell')
(2, 'Dune', 'Frank Herbert')
```

---

## Task 6: Delete a book

Delete book `2` from the database.

### Solution

```python
import sqlite3

connection = sqlite3.connect("books.db")
cursor = connection.cursor()

cursor.execute(
    "DELETE FROM books WHERE id = ?",
    (2,)
)

connection.commit()

print("Book deleted")

connection.close()
```

Output:

```text
Book deleted
```

Verify:

```python
cursor.execute("SELECT * FROM books")

for book in cursor.fetchall():
    print(book)
```

Output:

```text
(1, 'Animal Farm', 'George Orwell')
```

The second book has been removed.

## Task 1: Create a SQLite database and open it using the SQLite command-line tool

Create a database called `books.db` and open it with SQLite.

### Solution

```bash
sqlite3 books.db
```

You should see:

```text
SQLite version ...
Enter ".help" for usage hints.
sqlite>
```

---

## Task 2: Create a `books` table with an ID, title, and author

Create a table called `books`. Each book should have a unique ID, a title, and an author.

### Solution

```sql
CREATE TABLE books (
    id INTEGER PRIMARY KEY,
    title TEXT,
    author TEXT
);
```

---

## Task 3: Add two books to the `books` table

Insert these books:

* `1984` by `George Orwell`
* `Dune` by `Frank Herbert`

### Solution

```sql
INSERT INTO books (title, author)
VALUES ('1984', 'George Orwell');

INSERT INTO books (title, author)
VALUES ('Dune', 'Frank Herbert');
```

---

## Task 4: Retrieve all books from the database

Write a query that displays every book and all of its columns.

### Solution

```sql
SELECT * FROM books;
```

Output:

```text
1|1984|George Orwell
2|Dune|Frank Herbert
```

---

## Task 5: Retrieve only the title and author of every book

Write a query that displays only the `title` and `author` columns.

### Solution

```sql
SELECT title, author FROM books;
```

Output:

```text
1984|George Orwell
Dune|Frank Herbert
```

---

## Task 6: Find all books written by George Orwell

Use `WHERE` to return only books whose author is `George Orwell`.

### Solution

```sql
SELECT * FROM books
WHERE author = 'George Orwell';
```

Output:

```text
1|1984|George Orwell
```

---

## Task 7: Find the book with ID 2

Use the book's ID to retrieve a single book.

### Solution

```sql
SELECT * FROM books
WHERE id = 2;
```

Output:

```text
2|Dune|Frank Herbert
```

---

## Task 8: Change the title of book 1

Update book `1` so that its title changes from `1984` to `Animal Farm`.

### Solution

```sql
UPDATE books
SET title = 'Animal Farm'
WHERE id = 1;
```

Verify the change:

```sql
SELECT * FROM books
WHERE id = 1;
```

Output:

```text
1|Animal Farm|George Orwell
```

---

## Task 9: Delete book 2 from the database

Remove the book with ID `2`.

### Solution

```sql
DELETE FROM books
WHERE id = 2;
```

Verify the deletion:

```sql
SELECT * FROM books;
```

Output:

```text
1|Animal Farm|George Orwell
```

---

## Task 10: Close the SQLite session

Exit the SQLite command-line tool.

### Solution

```text
.quit
```

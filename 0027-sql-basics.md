## Task 1: Find books published after a specific year

Create a `books` table with a `year` column and find all books published after 2000.

### Solution

```sql
CREATE TABLE books (
    id INTEGER PRIMARY KEY,
    title TEXT,
    author TEXT,
    year INTEGER
);

INSERT INTO books (title, author, year) VALUES
    ('1984', 'George Orwell', 1949),
    ('Dune', 'Frank Herbert', 1965),
    ('The Road', 'Cormac McCarthy', 2006),
    ('The Martian', 'Andy Weir', 2011);

SELECT * FROM books
WHERE year > 2000;
```

Output:

```text
3|The Road|Cormac McCarthy|2006
4|The Martian|Andy Weir|2011
```

---

## Task 2: Find books matching multiple conditions

Find books published after 2000 **and** written by an author whose name is `Andy Weir`.

Then find books published before 2000 **or** after 2010.

### Solution

```sql
SELECT * FROM books
WHERE year > 2000
AND author = 'Andy Weir';
```

```sql
SELECT * FROM books
WHERE year < 2000
OR year > 2010;
```

---

## Task 3: Sort books by publication year

Display all books from newest to oldest.

### Solution

```sql
SELECT * FROM books
ORDER BY year DESC;
```

To sort from oldest to newest:

```sql
SELECT * FROM books
ORDER BY year ASC;
```

`ASC` is ascending order, while `DESC` is descending order.

---

## Task 4: Return only a limited number of books

Return the three newest books.

### Solution

```sql
SELECT * FROM books
ORDER BY year DESC
LIMIT 3;
```

You can use `OFFSET` to skip results.

For example, skip the first two books and return the next two:

```sql
SELECT * FROM books
ORDER BY year DESC
LIMIT 2 OFFSET 2;
```

---

## Task 5: Search for books by part of their title

Find all books whose title contains the word `The`.

### Solution

```sql
SELECT * FROM books
WHERE title LIKE '%The%';
```

`%` means "any number of characters".

For example:

```sql
LIKE 'The%'
```

means the title **starts with** `The`.

```sql
LIKE '%The'
```

means the title **ends with** `The`.

---

## Task 6: Count the books and find the earliest and latest publication years

Use aggregate functions to find:

* the number of books
* the earliest publication year
* the latest publication year

### Solution

```sql
SELECT COUNT(*) FROM books;

SELECT MIN(year) FROM books;

SELECT MAX(year) FROM books;
```

You can also calculate the average publication year:

```sql
SELECT AVG(year) FROM books;
```

---

## Task 7: Group books by author

Find how many books each author has in the database.

### Solution

```sql
SELECT author, COUNT(*)
FROM books
GROUP BY author;
```

Output:

```text
Andy Weir|1
Cormac McCarthy|1
Frank Herbert|1
George Orwell|1
```

`GROUP BY` combines rows that have the same value and lets aggregate functions such as `COUNT()` operate on each group.

---

## Task 8: Find authors who have more than one book

Add another book by George Orwell and then find authors who have more than one book.

### Solution

```sql
INSERT INTO books (title, author, year)
VALUES ('Animal Farm', 'George Orwell', 1945);
```

Now use `GROUP BY` with `HAVING`:

```sql
SELECT author, COUNT(*)
FROM books
GROUP BY author
HAVING COUNT(*) > 1;
```

Output:

```text
George Orwell|2
```

`WHERE` filters individual rows, while `HAVING` filters groups created by `GROUP BY`.

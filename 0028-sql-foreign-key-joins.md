## Task 1: Create an authors table and connect books to authors

Create two related tables:

* `authors` — stores author information
* `books` — stores book information

Each book should reference its author using `author_id`.

### Solution

```sql
CREATE TABLE authors (
    id INTEGER PRIMARY KEY,
    name TEXT
);

CREATE TABLE books (
    id INTEGER PRIMARY KEY,
    title TEXT,
    year INTEGER,
    author_id INTEGER,
    FOREIGN KEY (author_id) REFERENCES authors(id)
);
```

The `author_id` column in `books` is a **foreign key**.

It points to the `id` of an author in the `authors` table.

---

## Task 2: Add authors and books using the relationship

Add these authors:

```text
George Orwell
Frank Herbert
Andy Weir
```

Then add books associated with the correct author.

### Solution

```sql
INSERT INTO authors (name)
VALUES ('George Orwell');

INSERT INTO authors (name)
VALUES ('Frank Herbert');

INSERT INTO authors (name)
VALUES ('Andy Weir');
```

Now add the books:

```sql
INSERT INTO books (title, year, author_id)
VALUES ('1984', 1949, 1);

INSERT INTO books (title, year, author_id)
VALUES ('Animal Farm', 1945, 1);

INSERT INTO books (title, year, author_id)
VALUES ('Dune', 1965, 2);

INSERT INTO books (title, year, author_id)
VALUES ('The Martian', 2011, 3);
```

Notice that the books don't store the author's name.

They store the author's ID:

```text
1984         → author_id 1
Animal Farm  → author_id 1
Dune         → author_id 2
The Martian  → author_id 3
```

---

## Task 3: Use a JOIN to display each book with its author's name

The `books` table only contains `author_id`. Write a query that displays:

```text
book title | year | author name
```

### Solution

```sql
SELECT books.title, books.year, authors.name
FROM books
JOIN authors ON books.author_id = authors.id;
```

Output:

```text
1984|1949|George Orwell
Animal Farm|1945|George Orwell
Dune|1965|Frank Herbert
The Martian|2011|Andy Weir
```

The `JOIN` connects the two tables using:

```text
books.author_id = authors.id
```

---

## Task 4: Find all books written by a specific author

Find all books written by George Orwell.

### Solution

```sql
SELECT books.title, books.year
FROM books
JOIN authors ON books.author_id = authors.id
WHERE authors.name = 'George Orwell';
```

Output:

```text
1984|1949
Animal Farm|1945
```

---

## Task 5: Add a third related table for book reviews

Create a `reviews` table where each review belongs to a book.

Each review should contain:

* an ID
* review text
* rating
* `book_id`

### Solution

```sql
CREATE TABLE reviews (
    id INTEGER PRIMARY KEY,
    text TEXT,
    rating INTEGER,
    book_id INTEGER,
    FOREIGN KEY (book_id) REFERENCES books(id)
);
```

Add some reviews:

```sql
INSERT INTO reviews (text, rating, book_id)
VALUES ('A fantastic book', 5, 1);

INSERT INTO reviews (text, rating, book_id)
VALUES ('Very thought-provoking', 4, 1);

INSERT INTO reviews (text, rating, book_id)
VALUES ('An amazing science fiction novel', 5, 3);
```

Now the relationships are:

```text
authors
   │
   │ author_id
   ▼
books
   │
   │ book_id
   ▼
reviews
```

---

## Task 6: Display books together with their reviews

Write a query that displays the book title, review text, and rating.

### Solution

```sql
SELECT books.title, reviews.text, reviews.rating
FROM books
JOIN reviews ON books.id = reviews.book_id;
```

Output:

```text
1984|A fantastic book|5
1984|Very thought-provoking|4
Dune|An amazing science fiction novel|5
```

This demonstrates how multiple related tables can be combined using foreign keys and `JOIN`.

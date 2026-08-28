## Task 1: Read a CSV file

You have a `books.csv` file containing a list of books. Read the file and print each row.

Assume `books.csv` contains:

```text
title,author,year
1984,George Orwell,1949
Dune,Frank Herbert,1965
The Hobbit,J.R.R. Tolkien,1937
```

### Solution

```python
import csv

with open("books.csv", "r") as file:
    reader = csv.reader(file)

    for row in reader:
        print(row)
```

Output:

```text
['title', 'author', 'year']
['1984', 'George Orwell', '1949']
['Dune', 'Frank Herbert', '1965']
['The Hobbit', 'J.R.R. Tolkien', '1937']
```

`csv.reader()` reads each row as a list.

---

## Task 2: Write book data to a CSV file

You have a list of books and want to save it to `books.csv` so it can be opened by other programs or spreadsheet applications.

### Solution

```python
import csv

books = [
    ["1984", "George Orwell", 1949],
    ["Dune", "Frank Herbert", 1965],
    ["The Hobbit", "J.R.R. Tolkien", 1937],
]

with open("books.csv", "w") as file:
    writer = csv.writer(file)

    writer.writerow(["title", "author", "year"])
    writer.writerows(books)

print("Books saved")
```

Output:

```text
Books saved
```

The file will contain:

```text
title,author,year
1984,George Orwell,1949
Dune,Frank Herbert,1965
The Hobbit,J.R.R. Tolkien,1937
```

`writerow()` writes one row, while `writerows()` writes multiple rows.

---

## Task 3: Read CSV data using column names

Reading rows by position can become confusing. Use the column names from the CSV file to access each book's information.

### Solution

```python
import csv

with open("books.csv", "r") as file:
    reader = csv.DictReader(file)

    for book in reader:
        print(book["title"])
        print(book["author"])
        print(book["year"])
        print()
```

Output:

```text
1984
George Orwell
1949

Dune
Frank Herbert
1965

The Hobbit
J.R.R. Tolkien
1937
```

`csv.DictReader()` reads each row as a dictionary using the header row as the keys.

For example:

```python
{
    "title": "1984",
    "author": "George Orwell",
    "year": "1949",
}
```

---

## Task 4: Add a new book to an existing CSV file

A new book needs to be added to `books.csv` without removing the books already stored in the file.

### Solution

```python
import csv

new_book = ["Foundation", "Isaac Asimov", 1951]

with open("books.csv", "a") as file:
    writer = csv.writer(file)
    writer.writerow(new_book)

print("Book added")
```

Output:

```text
Book added
```

`"a"` opens the file in append mode, so the new row is added to the end of the file.

---

## Task 5: Search for a book by title

Create a program that searches `books.csv` for a book title entered in the code and displays the matching book.

### Solution

```python
import csv

search_title = "Dune"

with open("books.csv", "r") as file:
    reader = csv.DictReader(file)

    for book in reader:
        if book["title"] == search_title:
            print(book)
```

Output:

```text
{'title': 'Dune', 'author': 'Frank Herbert', 'year': '1965'}
```

`DictReader` makes it easy to access values by column name instead of remembering positions such as `row[0]` or `row[1]`.

---

## Task 6: Find information from CSV data

Read `books.csv`, count the total number of books, and display books published after the year 1950.

### Solution

```python
import csv

count = 0

with open("books.csv", "r") as file:
    reader = csv.DictReader(file)

    for book in reader:
        count += 1

        if int(book["year"]) > 1950:
            print(book["title"])

print("Total books:", count)
```

Output:

```text
Dune
Foundation
Total books: 4
```

Values read from a CSV file are strings, so:

```python
book["year"]
```

returns a string such as:

```text
"1965"
```

We use `int()` before comparing it with a number:

```python
int(book["year"]) > 1950
```

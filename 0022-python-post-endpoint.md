# Creating a Book with `POST`

## Tasks

1. Create a `POST /books` endpoint that accepts a book as JSON.
2. Create the book and return it with `201 Created`.
3. Fetch the newly created book using `GET /books/<id>`.

---

## Task 1: Create a `POST /books` endpoint

Modify the server so it accepts a JSON book sent in the request body.

### Solution

Add this `do_POST()` method to the server:

```python
def do_POST(self):
    if self.path == "/books":

        content_length = int(self.headers["Content-Length"])

        data = self.rfile.read(content_length)

        json_string = data.decode()

        book_data = json.loads(json_string)

        print(book_data)
```

Now send a book using `curl`:

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{"title":"The Hobbit","author":"J.R.R. Tolkien"}' \
  http://localhost:8080/books
```

The server receives the JSON and converts it into a Python dictionary.

---

## Task 2: Create the book and return it

Update the endpoint so that it creates a new book, assigns an ID, and returns the book with `201 Created`.

### Solution

```python
def do_POST(self):
    if self.path == "/books":

        content_length = int(self.headers["Content-Length"])

        data = self.rfile.read(content_length)

        json_string = data.decode()

        book_data = json.loads(json_string)

        book = {
            "id": len(books) + 1,
            "title": book_data["title"],
            "author": book_data["author"]
        }

        books.append(book)

        response = json.dumps(book).encode()

        self.send_response(201)
        self.send_header("Content-Type", "application/json")
        self.end_headers()

        self.wfile.write(response)
```

Send the request:

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{"title":"The Hobbit","author":"J.R.R. Tolkien"}' \
  http://localhost:8080/books
```

Response:

```json
{
  "id": 3,
  "title": "The Hobbit",
  "author": "J.R.R. Tolkien"
}
```

`201 Created` means the server successfully created a new resource.

---

## Task 3: Fetch the new book with `GET`

Use the ID returned by the `POST` request to retrieve the newly created book.

### Solution

```bash
curl http://localhost:8080/books/3
```

Response:

```json
{
  "id": 3,
  "title": "The Hobbit",
  "author": "J.R.R. Tolkien"
}
```

You can also verify that it was added to the collection:

```bash
curl http://localhost:8080/books
```

The response should now include the new book.

The important distinction is:

```text
POST /books
→ creates a book

GET /books/3
→ retrieves that book
```

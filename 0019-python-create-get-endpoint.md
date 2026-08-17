# Creating `GET` Endpoints for Books

## Objective

Create two endpoints:

```text
GET /books       → return all books
GET /books/1     → return one book
```

The focus is on **HTTP endpoints and `curl`**, not Python.

---

## Task 1: Create `GET /books`

Create a server that returns a list of books when `GET /books` is requested.

### Solution

```python
from http.server import HTTPServer, BaseHTTPRequestHandler
import json


books = [
    {"id": 1, "title": "1984", "author": "George Orwell"},
    {"id": 2, "title": "Dune", "author": "Frank Herbert"}
]


class Handler(BaseHTTPRequestHandler):

    def do_GET(self):

        if self.path == "/books":
            self.send_response(200)
            self.send_header("Content-Type", "application/json")
            self.end_headers()

            response = json.dumps(books)
            self.wfile.write(response.encode())


server = HTTPServer(("localhost", 8080), Handler)

print("Server running on port 8080")
server.serve_forever()
```

Test it:

```bash
curl http://localhost:8080/books
```

---

## Task 2: Create `GET /books/<id>`

Extend the server so that `/books/1` returns book `1`.

### Solution

Add this to `do_GET()`:

```python
elif self.path.startswith("/books/"):

    book_id = int(self.path.split("/")[-1])

    book = None

    for item in books:
        if item["id"] == book_id:
            book = item
            break

    if book:
        self.send_response(200)
        self.send_header("Content-Type", "application/json")
        self.end_headers()

        response = json.dumps(book)
        self.wfile.write(response.encode())

    else:
        self.send_response(404)
        self.end_headers()

        self.wfile.write(b"Book not found")
```

Test:

```bash
curl http://localhost:8080/books/1
```

Try a book that doesn't exist:

```bash
curl -i http://localhost:8080/books/99
```

You should get:

```text
404 Not Found
```

The API now supports:

```text
GET /books     → list all books
GET /books/1   → get book 1
GET /books/99  → 404 Not Found
```

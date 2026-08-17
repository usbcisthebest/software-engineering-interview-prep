# HTTP Methods and Status Codes with `curl`

## Objective

In this exercise, you'll use `curl` to interact with a small local **Books API**.

**The focus is HTTP, not Python.** The Python server is provided only so we have a real API to interact with. Don't worry about understanding the Python code yet.

You'll practice:

* HTTP methods: `GET`, `POST`, `PUT`, `PATCH`, `DELETE`
* Request and response bodies
* HTTP status codes
* Verifying changes with subsequent requests
* Common client and server errors

## Setup

Create a file called `server.py` and paste the following code:

```python
from http.server import BaseHTTPRequestHandler, HTTPServer
import json

books = {
    1: {"id": 1, "title": "1984", "author": "George Orwell"},
    2: {"id": 2, "title": "Dune", "author": "Frank Herbert"}
}


class Handler(BaseHTTPRequestHandler):

    def send_json(self, status, data):
        body = json.dumps(data).encode()
        self.send_response(status)
        self.send_header("Content-Type", "application/json")
        self.send_header("Content-Length", str(len(body)))
        self.end_headers()
        self.wfile.write(body)

    def read_json(self):
        length = int(self.headers.get("Content-Length", 0))
        body = self.rfile.read(length)
        return json.loads(body)

    def do_GET(self):
        if self.path == "/books":
            self.send_json(200, list(books.values()))
            return

        if self.path == "/error":
            self.send_json(500, {"error": "Something went wrong"})
            return

        if self.path == "/limited":
            self.send_response(429)
            self.send_header("Content-Type", "application/json")
            self.send_header("Retry-After", "10")
            self.end_headers()
            self.wfile.write(b'{"error": "Too many requests"}')
            return

        if self.path.startswith("/books/"):
            book_id = int(self.path.split("/")[-1])
            book = books.get(book_id)

            if book:
                self.send_json(200, book)
            else:
                self.send_json(404, {"error": "Book not found"})
            return

        self.send_json(404, {"error": "Not found"})

    def do_POST(self):
        if self.path != "/books":
            self.send_json(404, {"error": "Not found"})
            return

        try:
            data = self.read_json()
        except (json.JSONDecodeError, UnicodeDecodeError):
            self.send_json(400, {"error": "Invalid JSON"})
            return

        if "title" not in data or "author" not in data:
            self.send_json(400, {"error": "title and author are required"})
            return

        book_id = max(books.keys(), default=0) + 1
        book = {
            "id": book_id,
            "title": data["title"],
            "author": data["author"]
        }

        books[book_id] = book
        self.send_json(201, book)

    def do_PUT(self):
        if not self.path.startswith("/books/"):
            self.send_json(404, {"error": "Not found"})
            return

        book_id = int(self.path.split("/")[-1])

        if book_id not in books:
            self.send_json(404, {"error": "Book not found"})
            return

        try:
            data = self.read_json()
        except (json.JSONDecodeError, UnicodeDecodeError):
            self.send_json(400, {"error": "Invalid JSON"})
            return

        if "title" not in data or "author" not in data:
            self.send_json(400, {"error": "title and author are required"})
            return

        books[book_id] = {
            "id": book_id,
            "title": data["title"],
            "author": data["author"]
        }

        self.send_json(200, books[book_id])

    def do_PATCH(self):
        if not self.path.startswith("/books/"):
            self.send_json(404, {"error": "Not found"})
            return

        book_id = int(self.path.split("/")[-1])

        if book_id not in books:
            self.send_json(404, {"error": "Book not found"})
            return

        try:
            data = self.read_json()
        except (json.JSONDecodeError, UnicodeDecodeError):
            self.send_json(400, {"error": "Invalid JSON"})
            return

        books[book_id].update(data)
        self.send_json(200, books[book_id])

    def do_DELETE(self):
        if not self.path.startswith("/books/"):
            self.send_json(404, {"error": "Not found"})
            return

        book_id = int(self.path.split("/")[-1])

        if book_id not in books:
            self.send_json(404, {"error": "Book not found"})
            return

        deleted = books.pop(book_id)
        self.send_json(200, deleted)

    def do_OPTIONS(self):
        self.send_json(405, {"error": "Method not allowed"})


server = HTTPServer(("localhost", 8080), Handler)
print("Books API running at http://localhost:8080")
server.serve_forever()
```

Start it:

`python3 server.py`

Keep this terminal open and use a second terminal for `curl`.

## Tasks

### Task 1: GET

Retrieve all books.

### Solution

`curl -i http://localhost:8080/books`

You should see `200 OK` and the two books.

`200 OK` means the request succeeded.

### Task 2: GET a specific book

Retrieve book `1`.

### Solution

`curl -i http://localhost:8080/books/1`

You should receive:

```json
{
  "id": 1,
  "title": "1984",
  "author": "George Orwell"
}
```

with `200 OK`.

### Task 3: GET a missing book

Try to retrieve book `999`.

### Solution

`curl -i http://localhost:8080/books/999`

You should receive `404 Not Found`.

`404` means the requested resource doesn't exist.

### Task 4: POST

Create a new book.

### Solution

`curl -i -X POST -H "Content-Type: application/json" -d '{"title":"The Hobbit","author":"J.R.R. Tolkien"}' http://localhost:8080/books`

You should receive `201 Created` and the new book.

### Task 5: Verify the POST

Retrieve book `3`.

### Solution

`curl -i http://localhost:8080/books/3`

You should see `The Hobbit`.

The pattern is:

```text
POST → 201 Created
GET  → 200 OK → verify
```

### Task 6: PUT

Replace book `3`.

### Solution

`curl -i -X PUT -H "Content-Type: application/json" -d '{"title":"The Hobbit: An Unexpected Journey","author":"J.R.R. Tolkien"}' http://localhost:8080/books/3`

You should receive `200 OK`.

Verify:

`curl http://localhost:8080/books/3`

The title should now be `"The Hobbit: An Unexpected Journey"`.

### Task 7: PATCH

Change only the title.

### Solution

`curl -i -X PATCH -H "Content-Type: application/json" -d '{"title":"The Hobbit"}' http://localhost:8080/books/3`

Verify:

`curl http://localhost:8080/books/3`

The title should be `"The Hobbit"` while the author remains unchanged.

### Task 8: DELETE

Delete book `3`.

### Solution

`curl -i -X DELETE http://localhost:8080/books/3`

You should receive `200 OK`.

Verify:

`curl -i http://localhost:8080/books/3`

You should now receive `404 Not Found`.

### Task 9: Bad Request — `400`

Send invalid JSON.

### Solution

`curl -i -X POST -H "Content-Type: application/json" -d '{"title":}' http://localhost:8080/books`

You should receive:

```text
400 Bad Request
```

`400` means the request itself is invalid.

### Task 10: Method Not Allowed — `405`

Try an unsupported method.

### Solution

`curl -i -X OPTIONS http://localhost:8080/books`

You should receive:

```text
405 Method Not Allowed
```

`405` means the resource exists, but that HTTP method isn't allowed.

### Task 11: Too Many Requests — `429`

Request the rate-limited endpoint.

### Solution

`curl -i http://localhost:8080/limited`

You should receive:

```text
429 Too Many Requests
Retry-After: 10
```

`429` means the client has made too many requests and should wait before trying again.

### Task 12: Internal Server Error — `500`

Request the error endpoint.

### Solution

`curl -i http://localhost:8080/error`

You should receive:

```text
500 Internal Server Error
```

`500` means something went wrong on the server while processing the request.

## HTTP Methods

| Method   | Purpose          |
| -------- | ---------------- |
| `GET`    | Retrieve         |
| `POST`   | Create/submit    |
| `PUT`    | Replace          |
| `PATCH`  | Partially update |
| `DELETE` | Delete           |

## Status Codes

| Code  | Meaning               |
| ----- | --------------------- |
| `200` | OK                    |
| `201` | Created               |
| `400` | Bad Request           |
| `404` | Not Found             |
| `405` | Method Not Allowed    |
| `429` | Too Many Requests     |
| `500` | Internal Server Error |

The broad categories are:

```text
1xx - Information
2xx → Success
3xx - Redirects
4xx → Client-side/request problem
5xx → Server-side problem
```

### The request/response model

```text
curl
 │
 │ HTTP request
 │ method + URL + headers + body
 ↓
Server
 │
 │ HTTP response
 │ status + headers + body
 ↓
curl
```

The key lesson is that **HTTP methods describe what we're asking the server to do, while status codes tell us what happened to the request**.

## Reference Sites

* [httpbin.io](https://httpbin.io/?utm_source=chatgpt.com) — HTTP request/response testing.
* [Postman Echo](https://postman-echo.com/?utm_source=chatgpt.com) — HTTP testing and request inspection.
* [HTTPBingo](https://httpbingo.org/?utm_source=chatgpt.com) — HTTPBin-compatible testing service.

# Updating a Book with `PATCH`

## Tasks

1. Create a `PATCH /books/<id>` endpoint.
2. Update only the fields provided in the request.
3. Fetch the book with `GET` to verify the change.

---

## Task 1: Create a `PATCH /books/<id>` endpoint

Allow a client to update part of an existing book.

For example, change only the title of book `1`.

### Solution

Add `do_PATCH()` to the server:

```python
def do_PATCH(self):
    if self.path.startswith("/books/"):

        book_id = int(self.path.split("/")[-1])

        content_length = int(self.headers["Content-Length"])
        data = self.rfile.read(content_length)

        book_data = json.loads(data.decode())

        for book in books:
            if book["id"] == book_id:

                if "title" in book_data:
                    book["title"] = book_data["title"]

                if "author" in book_data:
                    book["author"] = book_data["author"]

                response = json.dumps(book).encode()

                self.send_response(200)
                self.send_header("Content-Type", "application/json")
                self.end_headers()

                self.wfile.write(response)
                return

        self.send_response(404)
        self.end_headers()
```

---

## Task 2: Update a book

Change only the title of book `1`.

### Solution

```bash
curl -X PATCH \
  -H "Content-Type: application/json" \
  -d '{"title":"Animal Farm"}' \
  http://localhost:8080/books/1
```

Response:

```json
{
  "id": 1,
  "title": "Animal Farm",
  "author": "George Orwell"
}
```

Notice that the **author was not changed**.

That's the main idea behind `PATCH`: update **part of a resource**.

---

## Task 3: Verify the change

Fetch the book with `GET`.

### Solution

```bash
curl http://localhost:8080/books/1
```

The response should show:

```json
{
  "id": 1,
  "title": "Animal Farm",
  "author": "George Orwell"
}
```

So the workflow is:

```text
PATCH /books/1
→ update the book

GET /books/1
→ verify the change
```

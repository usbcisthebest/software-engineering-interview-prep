# Deleting a Book with `DELETE`

## Tasks

1. Create a `DELETE /books/<id>` endpoint.
2. Delete an existing book.
3. Use `GET` to verify that the book was deleted.

---

## Task 1: Create a `DELETE /books/<id>` endpoint

Add a `do_DELETE()` method that finds a book by ID and removes it.

### Solution

```python id="7q2mxf"
def do_DELETE(self):
    if self.path.startswith("/books/"):

        book_id = int(self.path.split("/")[-1])

        for book in books:
            if book["id"] == book_id:
                books.remove(book)

                self.send_response(204)
                self.end_headers()
                return

        self.send_response(404)
        self.end_headers()
```

A successful `DELETE` returns `204 No Content`.

---

## Task 2: Delete a book

Delete book `2`:

```bash id="k8v3nd"
curl -i -X DELETE http://localhost:8080/books/2
```

You should receive:

```text id="f4r9qw"
HTTP/1.0 204 No Content
```

The book has now been removed from the server's `books` list.

---

## Task 3: Verify the deletion

Try to fetch the deleted book:

```bash id="m6x1pt"
curl -i http://localhost:8080/books/2
```

You should receive:

```text id="z3w7kc"
HTTP/1.0 404 Not Found
```

You can also check all books:

```bash id="q9v5rm"
curl http://localhost:8080/books
```

Book `2` should no longer appear.

The workflow is:

```text
DELETE /books/2
→ delete the book

GET /books/2
→ 404 Not Found
```

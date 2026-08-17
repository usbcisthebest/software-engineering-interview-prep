# Encoding and Decoding JSON

## Objective

Learn how `encode()` and `decode()` work with JSON data.

* `encode()` converts a string into bytes.
* `decode()` converts bytes into a string.
* `json.dumps()` and `json.loads()` convert between Python objects and JSON strings.

---

## Task 1: Encode and decode JSON

Create a Python book, convert it to a JSON string, encode it into bytes, then decode the bytes back into a string.

### Solution

```python id="7h3m1q"
import json

book = {
    "id": 1,
    "title": "1984"
}

json_string = json.dumps(book)
data = json_string.encode()

print(json_string)
print(data)
print(type(json_string))
print(type(data))

json_string = data.decode()

print(json_string)
print(type(json_string))
```

Output:

```text id="2p8v6k"
{"id": 1, "title": "1984"}
b'{"id": 1, "title": "1984"}'
<class 'str'>
<class 'bytes'>
{"id": 1, "title": "1984"}
<class 'str'>
```

`encode()` converts **string → bytes**.

`decode()` converts **bytes → string**.

---

## Task 2: Encode JSON for an HTTP response

Modify the HTTP server so that it converts a Python book into JSON and then into bytes before sending it.

### Solution

```python id="m4q7zw"
import json
from http.server import HTTPServer, BaseHTTPRequestHandler


class Handler(BaseHTTPRequestHandler):

    def do_GET(self):
        book = {
            "id": 1,
            "title": "1984"
        }

        json_string = json.dumps(book)
        data = json_string.encode()

        self.send_response(200)
        self.send_header("Content-Type", "application/json")
        self.end_headers()

        self.wfile.write(data)


server = HTTPServer(("localhost", 8080), Handler)

print("Server running on port 8080")
server.serve_forever()
```

Start the server:

```bash id="q8x2nc"
python3 server.py
```

Then:

```bash id="v5m9kp"
curl http://localhost:8080
```

Output:

```text id="z3w6rs"
{"id": 1, "title": "1984"}
```

`wfile.write()` expects bytes, which is why we use `encode()`.

---

## Task 3: Decode and load JSON from an HTTP response

Using a Python HTTP client, request the book from the server and convert the response into a Python dictionary.

### Solution

```python id="b6k2mt"
import json
from urllib.request import urlopen

response = urlopen("http://localhost:8080")

data = response.read()

book = json.loads(data.decode())

print(book)
print(type(book))
```

Output:

```text id="r9v4qx"
{'id': 1, 'title': '1984'}
<class 'dict'>
```

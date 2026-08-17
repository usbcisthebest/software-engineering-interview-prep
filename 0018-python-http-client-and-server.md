
## Objective

Create a tiny HTTP server and communicate with it using `curl` and a Python HTTP client.

---

## Task 1: Create and start an HTTP server

Create `server.py` with a server that listens on port `8080` and responds to `GET` requests.

### Solution

```python id="y8w4kq"
from http.server import HTTPServer, BaseHTTPRequestHandler


class Handler(BaseHTTPRequestHandler):
    def do_GET(self):
        self.send_response(200)
        self.end_headers()
        self.wfile.write(b"Hello from my server!")


server = HTTPServer(("localhost", 8080), Handler)

print("Server running on port 8080")
server.serve_forever()
```

Start it:

```bash id="x9p2mz"
python3 server.py
```

You should see:

```text id="q4n7vs"
Server running on port 8080
```

Keep this terminal open.

---

## Task 2: Use `curl` and a Python client

Use `curl` to send a GET request to the server. Then create a Python HTTP client that makes the same request.

### Solution

With `curl`:

```bash id="s7k3wp"
curl -i http://localhost:8080
```

You should see:

```text id="c5m8rx"
HTTP/1.0 200 OK
...

Hello from my server!
```

Now create `client.py`:

```python id="n2v6qh"
from urllib.request import urlopen

response = urlopen("http://localhost:8080")

print(response.status)
print(response.read().decode())
```

Run:

```bash id="r4t9yk"
python3 client.py
```

Output:

```text id="j6p1wd"
200
Hello from my server!
```

Both `curl` and the Python program are **HTTP clients** communicating with the same server.

---

## Task 3: Stop the server

Stop the HTTP server and verify that clients can no longer connect.

### Solution

In the server terminal, press:

```text id="m8q3vz"
Ctrl+C
```

Then try:

```bash id="k5w2rx"
curl http://localhost:8080
```

or:

```bash id="b7n4yp"
python3 client.py
```

Both should fail because the server is no longer running.

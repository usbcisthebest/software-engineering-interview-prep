## Understanding HTTP Headers

### Task

You are debugging an HTTP service and want to understand **HTTP headers**. Use `curl` with `httpbin.io` to inspect request and response headers.

1. Make a request and view the response headers.
2. Identify common response headers.
3. Send a custom request header.
4. Use `httpbin.io` to verify the request header.
5. Compare request headers with response headers.

### Solution

1. View the response headers: `curl -I https://httpbin.io/get`

You might see:

```text
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 256
Server: gunicorn
Date: Mon, 17 Aug 2026 14:05:00 GMT
```

The first line is the **status line**, not a header.

The lines below it are HTTP headers:

```text
Content-Type: application/json
Content-Length: 256
Server: gunicorn
Date: Mon, 17 Aug 2026 14:05:00 GMT
```

2. Make a normal request and see both the headers and body: `curl -i https://httpbin.io/get`

3. Send a custom request header: `curl -H "X-My-Header: hello" https://httpbin.io/headers`

`-H` adds a header to the HTTP request:

```text
X-My-Header: hello
```

4. `httpbin.io/headers` returns the request headers it received, so you should see your custom header in the JSON response.

5. Compare the two directions:

```text
Your machine                         httpbin.io
     │                                   │
     │  Request headers                  │
     │ ────────────────────────────────> │
     │                                   │
     │  Response headers                 │
     │ <──────────────────────────────── │
     │                                   │
```

### Request vs Response Headers

**Request headers** are sent by the client to the server:

```text
GET /get HTTP/1.1
Host: httpbin.io
X-My-Header: hello
```

**Response headers** are sent by the server back to the client:

```text
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 256
```

### Common headers

`Content-Type` — describes the format of the body.

`Content-Length` — describes the size of the body.

`Host` — identifies the server being requested.

`User-Agent` — identifies the client making the request.

`Accept` — tells the server which response formats the client can accept.

### Key idea

HTTP headers are **metadata attached to an HTTP request or response**.

```text
Request
├── Headers
└── Body

Response
├── Status
├── Headers
└── Body
```

`curl -i` is particularly useful while learning because it lets you see the **response headers and body together**.

### Reference Sites

These are useful for experimenting with HTTP headers and requests:

* [httpbin.io](https://httpbin.io/?utm_source=chatgpt.com) — the main site used in this exercise; provides endpoints for inspecting requests and responses.
* [Postman Echo](https://postman-echo.com/?utm_source=chatgpt.com) — lets you inspect request headers, methods, query parameters, and other HTTP details.
* [HTTPBingo](https://httpbingo.org/?utm_source=chatgpt.com) — another HTTP testing service with functionality similar to httpbin.

## `curl` vs `wget`

In this exercise, you'll use two common command-line tools for working with resources over HTTP.

### Task 1: Using `curl`

Use `curl` with `httpbin.io` to inspect and interact with an HTTP service.

1. Make a basic GET request.
2. View the response headers.
3. View both the headers and response body.
4. Send a query parameter.
5. Send a custom request header.
6. Save the response to a file.

### Solution

1. Make a GET request: `curl https://httpbin.io/get`

2. View response headers: `curl -I https://httpbin.io/get`

3. View headers and body: `curl -i https://httpbin.io/get`

4. Send a query parameter: `curl "https://httpbin.io/get?name=alice"`

5. Send a custom header: `curl -H "X-Test: hello" https://httpbin.io/headers`

6. Save the response to a file: `curl -o response.json https://httpbin.io/get`

### Useful `curl` options

`-i` — include response headers in the output.

`-I` — make a HEAD request and show the response headers.

`-H` — add a request header.

`-o` — save the response to a file.

### Task 2: Using `wget`

Use `wget` to download resources from `httpbin.io`.

1. Download a file.
2. Choose the filename for the downloaded file.
3. Download a webpage.

### Solution

1. Download a file: `wget https://httpbin.io/robots.txt`

2. Choose the filename: `wget -O robots.txt https://httpbin.io/robots.txt`

3. Download a webpage: `wget https://httpbin.io/`

### Useful `wget` options

`-O` — save the downloaded content using the specified filename.

`-r` — recursively download linked resources.

`--mirror` — maintain a local mirror using a collection of options designed for mirroring.

---

### `wget`: Recursive Downloading vs Mirroring

These two options are related but have different purposes.

`-r` means **recursive downloading**:

```bash
wget -r https://example.com
```

It tells `wget` to follow links and recursively download resources.

Think:

```text
-r
↓
"Follow links and download more resources."
```

`--mirror` is intended to **maintain a local copy of a website**:

```bash
wget --mirror https://example.com
```

It enables recursive downloading along with other settings useful for mirroring, such as timestamp checking.

Think:

```text
--mirror
↓
"Create/update a local copy of this website."
```

So the distinction is:

```text
-r          → recursive downloading
--mirror    → recursive downloading + mirroring-oriented settings
```

### `curl` vs `wget`

A useful mental model for now:

```text
curl → make requests and interact with services
wget → download resources
```

There is significant overlap—`curl` can download files—but `wget` has convenient features such as recursive downloading and website mirroring.

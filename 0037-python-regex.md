Great next topic. We can keep it beginner-friendly and practical, with tasks increasing from simple pattern matching to extracting and validating real-world data.

## Task 1: Check whether text contains a word

A log message may contain the word `ERROR`. Check whether the word appears in the message.

### Solution

```python
import re

message = "ERROR: Database connection failed"

match = re.search(r"ERROR", message)

if match:
    print("Error found")
else:
    print("No error found")
```

Output:

```text
Error found
```

`re.search()` looks for a pattern anywhere in a string.

---

## Task 2: Find all error codes

A log message contains several error codes. Extract all codes that start with `ERR-` followed by three digits.

```text
ERR-101 ERR-404 ERR-500
```

### Solution

```python
import re

message = "Errors: ERR-101 ERR-404 ERR-500"

codes = re.findall(r"ERR-\d{3}", message)

print(codes)
```

Output:

```text
['ERR-101', 'ERR-404', 'ERR-500']
```

* `\d` matches a digit.
* `{3}` means exactly three digits.
* `findall()` returns all matches.

---

## Task 3: Extract email addresses from text

A text file contains email addresses. Extract all email addresses from the text.

### Solution

```python
import re

text = """
Contact alice@example.com or bob@test.org
for more information.
"""

emails = re.findall(r"[\w.-]+@[\w.-]+\.\w+", text)

print(emails)
```

Output:

```text
['alice@example.com', 'bob@test.org']
```

The pattern looks for text before and after `@`, followed by a domain extension.

---

## Task 4: Validate a username

A website allows usernames containing only letters, numbers, and underscores. A username must also be between 3 and 20 characters long.

### Solution

```python
import re

username = "alice_123"

pattern = r"^[A-Za-z0-9_]{3,20}$"

if re.fullmatch(pattern, username):
    print("Valid username")
else:
    print("Invalid username")
```

Output:

```text
Valid username
```

`re.fullmatch()` checks whether the **entire string** matches the pattern.

* `[A-Za-z0-9_]` allows letters, numbers, and underscores.
* `{3,20}` requires between 3 and 20 characters.

---

## Task 5: Extract information from a log line

Extract the date, log level, and message from a log entry.

```text
2026-08-25 INFO Server started
```

### Solution

```python
import re

line = "2026-08-25 INFO Server started"

pattern = r"(\d{4}-\d{2}-\d{2}) (\w+) (.+)"

match = re.match(pattern, line)

if match:
    date = match.group(1)
    level = match.group(2)
    message = match.group(3)

    print(f"Date: {date}")
    print(f"Level: {level}")
    print(f"Message: {message}")
```

Output:

```text
Date: 2026-08-25
Level: INFO
Message: Server started
```

Parentheses create **groups**, which let you extract individual parts of a match.

---

## Task 6: Replace sensitive information

A log contains an email address that should not be displayed. Replace every email address with `[REDACTED]`.

### Solution

```python
import re

text = "User alice@example.com logged in"

clean_text = re.sub(
    r"[\w.-]+@[\w.-]+\.\w+",
    "[REDACTED]",
    text,
)

print(clean_text)
```

Output:

```text
User [REDACTED] logged in
```

`re.sub()` replaces text that matches a pattern.

---

## Task 7: Extract URLs from text

Extract all HTTP and HTTPS URLs from a piece of text.

### Solution

```python
import re

text = """
Visit https://example.com
or http://test.com/docs
"""

urls = re.findall(r"https?://[^\s]+", text)

print(urls)
```

Output:

```text
['https://example.com', 'http://test.com/docs']
```

`https?` means the `s` is optional, so it matches both `http` and `https`.

---

## Task 8: Build a simple password validator

Validate a password using these rules:

* At least 8 characters
* Contains an uppercase letter
* Contains a lowercase letter
* Contains a digit
* Contains a special character

### Solution

```python
import re

password = "Secure123!"

valid = (
    len(password) >= 8
    and re.search(r"[A-Z]", password)
    and re.search(r"[a-z]", password)
    and re.search(r"\d", password)
    and re.search(r"[^A-Za-z0-9]", password)
)

if valid:
    print("Valid password")
else:
    print("Invalid password")
```

Output:

```text
Valid password
```

Each `re.search()` checks whether the password contains at least one character matching that rule.

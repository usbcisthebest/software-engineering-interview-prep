## Task 1: Clean user input

A user enters their name into a form, but accidentally adds spaces before and after it. Clean the value before storing or displaying it.

```text
  Alice Smith  
```

### Solution

```python
name = "  Alice Smith  "

clean_name = name.strip()

print(clean_name)
```

Output:

```text
Alice Smith
```

`strip()` removes whitespace from both ends of a string.

---

## Task 2: Format an email address

A user enters their email address using uppercase letters. Convert it to lowercase before storing it.

```text
ALICE@EXAMPLE.COM
```

### Solution

```python
email = "ALICE@EXAMPLE.COM"

email = email.lower()

print(email)
```

Output:

```text
alice@example.com
```

`lower()` converts all letters to lowercase.

You can use `upper()` when you need the opposite:

```python
email.upper()
```

---

## Task 3: Format a person's name

A user enters their name in lowercase. Format it so that each word starts with a capital letter.

```text
john smith
```

### Solution

```python
name = "john smith"

formatted_name = name.title()

print(formatted_name)
```

Output:

```text
John Smith
```

`title()` capitalizes the first letter of each word.

`capitalize()` only capitalizes the first character of the entire string:

```python
"john smith".capitalize()
```

Output:

```text
John smith
```

---

## Task 4: Clean text from one side

A text file contains values with unwanted whitespace at the beginning or end. Remove whitespace from only the appropriate side.

### Solution

```python
text = "   Python   "

print(text.lstrip())
print(text.rstrip())
```

Output:

```text
Python   
   Python
```

* `lstrip()` removes whitespace from the left.
* `rstrip()` removes whitespace from the right.
* `strip()` removes whitespace from both sides.

---

## Task 5: Replace text in a message

Your application displays an order status to a customer. The order has now shipped, so replace `pending` with `shipped`.

### Solution

```python
message = "Your order is pending"

updated_message = message.replace("pending", "shipped")

print(updated_message)
```

Output:

```text
Your order is shipped
```

`replace()` returns a new string with the specified text replaced.

---

## Task 6: Convert comma-separated data into a list

You receive a list of tags from a form as one comma-separated string. Convert it into a Python list so the application can process each tag separately.

```text
python,api,sqlite,shell
```

### Solution

```python
tags = "python,api,sqlite,shell"

tag_list = tags.split(",")

print(tag_list)
```

Output:

```text
['python', 'api', 'sqlite', 'shell']
```

`split()` divides a string into a list using the specified separator.

---

## Task 7: Create a sentence from a list

Your application has a list of technologies and needs to display them as a readable comma-separated string.

### Solution

```python
technologies = ["Python", "SQLite", "Linux"]

text = ", ".join(technologies)

print(text)
```

Output:

```text
Python, SQLite, Linux
```

`join()` combines items from a list into one string.

---

## Task 8: Check whether a message contains an error

A log-processing script needs to determine whether a message contains the word `error`.

### Solution

```python
message = "Connection error: server unavailable"

if "error" in message:
    print("Error found")
else:
    print("No error found")
```

Output:

```text
Error found
```

Use `in` when you only need to know whether the text exists.

If you also need its position, use `find()`:

```python
position = message.find("error")

print(position)
```

Output:

```text
11
```

`find()` returns `-1` when the text cannot be found.

---

## Task 9: Count errors in a log message

A monitoring script receives a log message containing several errors. Count how many times `error` appears.

### Solution

```python
message = "error: connection error: timeout error"

count = message.count("error")

print(count)
```

Output:

```text
3
```

`count()` returns the number of occurrences.

---

## Task 10: Validate a numeric input

A user enters their age into a form. Check whether the value contains only digits before converting it to an integer.

### Solution

```python
age = "25"

if age.isdigit():
    print("Valid age")
else:
    print("Please enter a number")
```

Output:

```text
Valid age
```

`isdigit()` returns `True` when all characters are digits.

---

## Task 11: Validate a username

A website requires usernames to contain only letters and numbers. Check whether the username meets this requirement.

### Solution

```python
username = "alice123"

if username.isalnum():
    print("Valid username")
else:
    print("Username can only contain letters and numbers")
```

Output:

```text
Valid username
```

`isalnum()` returns `True` when all characters are letters or digits.

You can also check specifically for letters with `isalpha()`:

```python
"alice".isalpha()
# True
```

---

## Task 12: Check whether input contains only spaces

A form field should not accept a value that consists entirely of spaces. Check the input before accepting it.

### Solution

```python
value = "   "

if value.isspace():
    print("Input cannot contain only spaces")
else:
    print("Input accepted")
```

Output:

```text
Input cannot contain only spaces
```

`isspace()` returns `True` when all characters are whitespace.

---

## Task 13: Check a filename extension

A file-upload feature only accepts Python files. Check whether the filename ends with `.py`.

### Solution

```python
filename = "server.py"

if filename.endswith(".py"):
    print("Python file")
else:
    print("Not a Python file")
```

Output:

```text
Python file
```

`endswith()` checks how a string ends.

You can similarly check how a string begins:

```python
filename.startswith("server")
```

This returns `True` for `server.py`.

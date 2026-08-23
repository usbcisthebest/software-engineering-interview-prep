## Task 1: Add an item to a shopping cart

A customer adds a new product to their existing shopping cart. Add the product to the end of the list.

### Solution

```python
cart = ["Laptop", "Mouse"]

cart.append("Keyboard")

print(cart)
```

Output:

```text
['Laptop', 'Mouse', 'Keyboard']
```

`append()` adds one item to the end of a list.

---

## Task 2: Combine two attendee lists

Two teams submit separate lists of people attending an event. Combine the second list with the first list.

### Solution

```python
morning_attendees = ["Alice", "Bob"]
afternoon_attendees = ["Charlie", "David"]

morning_attendees.extend(afternoon_attendees)

print(morning_attendees)
```

Output:

```text
['Alice', 'Bob', 'Charlie', 'David']
```

`extend()` adds all items from another iterable to the existing list.

---

## Task 3: Add an urgent ticket to a specific position

A support team keeps tickets in a list. An urgent ticket needs to be placed at the beginning so it can be handled first.

### Solution

```python
tickets = ["Password reset", "Login issue", "Billing question"]

tickets.insert(0, "URGENT: Production outage")

print(tickets)
```

Output:

```text
['URGENT: Production outage', 'Password reset', 'Login issue', 'Billing question']
```

`insert(index, item)` adds an item at a specific position.

---

## Task 4: Remove a cancelled order

An order is cancelled and should be removed from the list of pending orders.

### Solution

```python
orders = ["ORD-101", "ORD-102", "ORD-103"]

orders.remove("ORD-102")

print(orders)
```

Output:

```text
['ORD-101', 'ORD-103']
```

`remove()` removes the first matching value from a list.

---

## Task 5: Process the next item in a queue

A program keeps tasks in a list. Process the first task and remove it from the queue.

### Solution

```python
tasks = ["Send email", "Generate report", "Create backup"]

current_task = tasks.pop(0)

print("Processing:", current_task)
print("Remaining:", tasks)
```

Output:

```text
Processing: Send email
Remaining: ['Generate report', 'Create backup']
```

`pop(index)` removes and returns an item.

---

## Task 6: Clear completed notifications

A user has viewed all their notifications. Remove every notification from the list.

### Solution

```python
notifications = [
    "New message",
    "Password changed",
    "New login detected",
]

notifications.clear()

print(notifications)
```

Output:

```text
[]
```

`clear()` removes all items from a list.

---

## Task 7: Find the position of a product

A warehouse system stores product IDs in a list. Find the position of a specific product.

### Solution

```python
products = ["P-100", "P-200", "P-300"]

position = products.index("P-200")

print(position)
```

Output:

```text
1
```

`index()` returns the position of the first matching item.

Remember that Python list indexes start at `0`.

---

## Task 8: Count repeated error codes

A monitoring system collects error codes from several requests. Count how many times a specific error occurred.

### Solution

```python
errors = [404, 500, 404, 200, 404, 500]

count = errors.count(404)

print(count)
```

Output:

```text
3
```

`count()` returns the number of times a value appears in a list.

---

## Task 9: Sort customer names

A customer dashboard needs to display names in alphabetical order.

### Solution

```python
customers = ["Charlie", "Alice", "Bob"]

customers.sort()

print(customers)
```

Output:

```text
['Alice', 'Bob', 'Charlie']
```

`sort()` changes the existing list.

To sort in reverse order:

```python
customers.sort(reverse=True)
```

---

## Task 10: Show recent activity first

An application stores activity from oldest to newest, but the UI should display the newest activity first.

### Solution

```python
activity = [
    "Logged in",
    "Updated profile",
    "Uploaded document",
]

activity.reverse()

print(activity)
```

Output:

```text
['Uploaded document', 'Updated profile', 'Logged in']
```

`reverse()` reverses the order of the existing list.

---

## Task 11: Copy a default configuration

A program has a default list of enabled features. Create a separate copy before modifying it for a specific user.

### Solution

```python
default_features = ["search", "notifications", "dark_mode"]

user_features = default_features.copy()

user_features.remove("dark_mode")

print("Default:", default_features)
print("User:", user_features)
```

Output:

```text
Default: ['search', 'notifications', 'dark_mode']
User: ['search', 'notifications']
```

`copy()` creates a separate list.

This is useful because modifying `user_features` does not change `default_features`.

Yes. I'd reorder the lesson so it progresses from **interactive input → multiple input → arguments → pipes/files → direct stdin/stdout**.

## Task 1: Read a value from standard input

Write a program that asks the user for their name and prints a greeting.

### Solution

```python
name = input("Enter your name: ")

print(f"Hello, {name}!")
```

Example:

```text
Enter your name: Alice
Hello, Alice!
```

`input()` reads text from **standard input (`stdin`)**.

`print()` writes text to **standard output (`stdout`)**.

---

## Task 2: Read multiple values from standard input

Ask the user for two numbers and print their sum.

### Solution

```python
first = input("Enter the first number: ")
second = input("Enter the second number: ")

total = int(first) + int(second)

print(total)
```

Example:

```text
Enter the first number: 10
Enter the second number: 20
30
```

`input()` always returns a string, so `int()` converts the values to integers.

---

## Task 3: Read multiple lines using `input()`

Write a program that allows the user to enter several names, one per line. Stop when the user enters an empty line.

### Solution

```python
names = []

while True:
    name = input("Enter a name: ")

    if name == "":
        break

    names.append(name)

print(names)
```

Example:

```text
Enter a name: Alice
Enter a name: Bob
Enter a name: Charlie
Enter a name:
['Alice', 'Bob', 'Charlie']
```

This is useful when the program is interacting directly with a user.

---

## Task 4: Accept input from command-line arguments

Create a program that accepts a person's name as a command-line argument and prints a greeting.

Run it like this:

```bash
python greet.py Alice
```

### Solution

```python
import sys

name = sys.argv[1]

print(f"Hello, {name}!")
```

Output:

```text
Hello, Alice!
```

`sys.argv` contains the arguments passed to the program.

For:

```bash
python greet.py Alice
```

the values are approximately:

```text
sys.argv[0] → greet.py
sys.argv[1] → Alice
```

Command-line arguments are useful when a program needs input without interactively asking the user.

---

## Task 5: Accept multiple command-line arguments

Create a program that accepts several names as arguments and prints a greeting for each one.

For example:

```bash
python greet.py Alice Bob Charlie
```

### Solution

```python
import sys

for name in sys.argv[1:]:
    print(f"Hello, {name}!")
```

Output:

```text
Hello, Alice!
Hello, Bob!
Hello, Charlie!
```

`sys.argv[1:]` gives us all arguments after the program name.

---

## Task 6: Read input from a pipe

Create `read_name.py` that reads a name from standard input and prints a greeting.

### Solution

```python
import sys

name = sys.stdin.readline().strip()

print(f"Hello, {name}!")
```

Run it:

```bash
echo "Alice" | python read_name.py
```

Output:

```text
Hello, Alice!
```

Here, `echo` sends its output to the Python program through a **pipe**.

`sys.stdin` provides direct access to standard input.

---

## Task 7: Read multiple lines from standard input

Create a program that reads several lines from `stdin` and prints each name in uppercase.

### Solution

```python
import sys

for line in sys.stdin:
    print(line.strip().upper())
```

Create `names.txt`:

```text
alice
bob
charlie
```

Run:

```bash
python uppercase.py < names.txt
```

Output:

```text
ALICE
BOB
CHARLIE
```

The `<` redirects the contents of `names.txt` to the program's standard input.

This is different from `input()`: `sys.stdin` is convenient when the program can receive an unknown number of lines from a pipe or redirected file.

---

## Task 8: Write directly to standard output

Create a program that writes information about a book directly to standard output.

### Solution

```python
import sys

book = "The Hobbit"

sys.stdout.write(f"Book: {book}\n")
```

Output:

```text
Book: The Hobbit
```

`print()` also writes to standard output, but `sys.stdout.write()` provides more direct control over the output.

---

## Task 9: Redirect standard output to a file

Create a program that prints several book names and save its output to a file.

### Solution

Create `books.py`:

```python
print("The Hobbit")
print("Dune")
print("1984")
```

Run:

```bash
python books.py > books.txt
```

The program still writes to **standard output**, but `>` redirects that output into `books.txt`.

The file will contain:

```text
The Hobbit
Dune
1984
```

---

## Task 10: Build a simple line counter

Create a program that reads text from standard input and prints the total number of lines received.

### Solution

```python
import sys

count = 0

for line in sys.stdin:
    count += 1

print(f"Lines: {count}")
```

Run it with a file:

```bash
python line_count.py < books.txt
```

Output:

```text
Lines: 3
```

This combines standard input, iteration, and standard output into a useful command-line program.

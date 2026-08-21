## Task 1: Create and run your first shell script

Create a file called `hello.sh` that prints `Hello, World!`.

### Solution

Create the file:

```bash
touch hello.sh
```

Add the following:

```bash
#!/bin/bash

echo "Hello, World!"
```

Make the script executable:

```bash
chmod +x hello.sh
```

Run it:

```bash
./hello.sh
```

Output:

```text
Hello, World!
```

---

## Task 2: Store and use a variable

Create a script that stores your name in a variable and prints a greeting.

### Solution

```bash
#!/bin/bash

name="Alice"

echo "Hello, $name!"
```

Run:

```bash
./hello.sh
```

Output:

```text
Hello, Alice!
```

Assign a variable without spaces around `=`:

```bash
name="Alice"
```

Use `$` to read its value:

```bash
echo "$name"
```

---

## Task 3: Use a command-line argument

Create a script that accepts a name as its first command-line argument and prints a greeting.

For example:

```bash
./greet.sh Alice
```

should print:

```text
Hello, Alice!
```

### Solution

```bash
#!/bin/bash

name=$1

echo "Hello, $name!"
```

Run:

```bash
./greet.sh Alice
```

Output:

```text
Hello, Alice!
```

`$1` represents the first argument passed to the script.

---

## Task 4: Read input from the user

Create a script that asks the user for their name and then prints a greeting.

### Solution

```bash
#!/bin/bash

echo "What is your name?"
read name

echo "Hello, $name!"
```

Example:

```text
What is your name?
Alice
Hello, Alice!
```

`read` waits for user input and stores it in the specified variable.

---

## Task 5: Check whether a file exists

Create a script that accepts a filename as its first argument and checks whether the file exists.

### Solution

```bash
#!/bin/bash

file=$1

if [ -f "$file" ]; then
    echo "File exists"
else
    echo "File does not exist"
fi
```

Run:

```bash
./check-file.sh books.db
```

The condition:

```bash
[ -f "$file" ]
```

checks whether the specified path exists and is a regular file.

---

## Task 6: Print multiple values using a loop

Create a script that prints each book title from a list.

### Solution

```bash
#!/bin/bash

books=("1984" "Dune" "The Hobbit")

for book in "${books[@]}"
do
    echo "$book"
done
```

Output:

```text
1984
Dune
The Hobbit
```

The `for` loop runs once for each item in the `books` array.

---

## Task 7: Repeat an action while a condition is true

Create a script that prints the numbers from `1` to `5`.

### Solution

```bash
#!/bin/bash

number=1

while [ "$number" -le 5 ]
do
    echo "$number"
    number=$((number + 1))
done
```

Output:

```text
1
2
3
4
5
```

`while` continues running as long as its condition is true.

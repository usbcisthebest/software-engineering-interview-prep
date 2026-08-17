## Task

You are given an application log file. Use Bash commands to analyze it.

1. Create `app.log` containing several `INFO`, `WARNING`, and `ERROR` messages.
2. Use `>` to create a file containing only the `ERROR` messages.
3. Use `>>` to append `WARNING` messages to the same file.
4. Use `<` for input redirection.
5. Use `|` to combine commands and process the output.
6. Use `grep` to find specific log levels.
7. Use `wc` to count the number of errors.
8. Use `sort` to sort the messages.
9. Use `uniq` to remove duplicate messages.
10. Use `head` to view the first few results.
11. Use `tail` to view the last few results.

## Solution

```bash
# Create a sample application log
cat > app.log <<EOF
INFO Application started
ERROR Database connection failed
WARNING High memory usage
INFO User logged in
ERROR Database connection failed
INFO Request completed
WARNING High memory usage
ERROR Timeout connecting to API
INFO Application stopped
EOF

# Find ERROR messages and write them to errors.log
grep "ERROR" app.log > errors.log

# Find WARNING messages and append them to errors.log
grep "WARNING" app.log >> errors.log

# Use a pipe to count ERROR messages
grep "ERROR" app.log | wc -l

# Sort the log messages
sort app.log

# Sort messages and remove duplicates
sort app.log | uniq

# Show the first 3 lines
head -n 3 app.log

# Show the last 3 lines
tail -n 3 app.log
```

### Input Redirection: `<`

`<` passes a file's contents to a command through standard input.

For example:

```bash
# Pass errors.log to wc through standard input
wc -l < errors.log
```

With `cat`, `<` is usually redundant:

```bash
cat errors.log
```

and:

```bash
cat < errors.log
```

produce the same output. `cat` already accepts the filename directly, while commands such as `wc` can make more meaningful use of input redirection.

### Using `head` and `tail` with Pipes

`head` and `tail` can be used directly on a file:

```bash
head -n 3 app.log
tail -n 3 app.log
```

But they are especially useful at the end of a pipeline, where they limit the output of another command.

For example, find all errors, sort them, and show only the first 3:

```bash
grep "ERROR" app.log | sort | head -n 3
```

Similarly, show the last 3 matching errors:

```bash
grep "ERROR" app.log | sort | tail -n 3
```

This pattern is very common:

```text
command → filter → sort → head/tail
```

It allows you to process a large amount of output without displaying everything.

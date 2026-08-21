## Task 1: View the permissions, owner, and group of a file

Create a file called `hello.txt` and inspect its permissions, owner, and group.

### Solution

```bash
touch hello.txt

ls -l hello.txt
```

You might see:

```text
-rw-r--r--  1 alice  developers  0 Aug 21 22:00 hello.txt
```

The permission part is:

```text
-rw-r--r--
```

The first character indicates the type:

```text
-  regular file
d  directory
```

The remaining nine characters are divided into three groups:

```text
rw-  r--  r--
 │    │    │
 │    │    └── others
 │    └─────── group
 └──────────── owner
```

### Owner, group, and others

Every file has an **owner** and a **group**.

* **Owner** — the user who owns the file.
* **Group** — a group of users associated with the file.
* **Others** — everyone else.

For example:

```text
-rw-r--r--  1 alice  developers  hello.txt
             │       │
             │       └── group
             └────────── owner
```

Here:

```text
owner  → alice
group  → developers
others → everyone else
```

---

## Task 2: Understand read, write, and execute permissions

Understand what `r`, `w`, and `x` mean for a file.

### Solution

```text
r = read
w = write
x = execute
- = permission not granted
```

For example:

```text
rw-
```

means read and write, while:

```text
r-x
```

means read and execute.

---

## Task 3: Make a shell script executable

Create a simple shell script and make it executable.

### Solution

```bash
echo '#!/bin/bash' > hello.sh
echo 'echo "Hello!"' >> hello.sh
```

Try to run it:

```bash
./hello.sh
```

You may get:

```text
Permission denied
```

Add execute permission:

```bash
chmod +x hello.sh
```

Run it again:

```bash
./hello.sh
```

Output:

```text
Hello!
```

---

## Task 4: Add and remove permissions symbolically

Give the owner execute permission, then remove it again.

### Solution

Add execute permission:

```bash
chmod u+x hello.sh
```

Remove it:

```bash
chmod u-x hello.sh
```

The permission categories are:

```text
u = user (owner)
g = group
o = others
a = all
```

---

## Task 5: Change the owner of a file

Change the owner of `hello.txt` to another user.

### Solution

```bash
sudo chown alice hello.txt
```

Verify the change:

```bash
ls -l hello.txt
```

The owner should now be `alice`.

**Important:** Changing file ownership normally requires administrator/root privileges. A regular user generally cannot change a file's owner to another user.

This restriction prevents users from freely taking ownership of files belonging to other users.

Owner
├── Can usually change permissions
└── Cannot normally change the file's owner

Root/admin
├── Can change permissions
└── Can change ownership

---

## Task 6: Change the group of a file

Change the group of `hello.txt` to `developers`.

### Solution

```bash
sudo chown :developers hello.txt
```

Verify:

```bash
ls -l hello.txt
```

The group should now be `developers`.

---

## Task 7: Change the owner and group together

Change the owner to `alice` and the group to `developers`.

### Solution

```bash
sudo chown alice:developers hello.txt
```

Verify:

```bash
ls -l hello.txt
```

You should see something similar to:

```text
-rw-r--r--  1 alice  developers  0 Aug 21 22:00 hello.txt
```

The general syntax is:

```bash
sudo chown owner:group file
```

---

## Task 8: Set permissions using numeric notation

Set `hello.sh` to permission `755`.

### Solution

```bash
chmod 755 hello.sh
```

The three digits represent:

```text
owner  group  others
  7      5      5
```

The values are:

```text
4 = read
2 = write
1 = execute
```

Therefore:

```text
7 = 4 + 2 + 1 = rwx
5 = 4 + 1     = r-x
5 = 4 + 1     = r-x
```

So `755` means:

```text
rwx  r-x  r-x
```

---

## Task 9: Set a regular file to 644

Set `hello.txt` to permission `644`.

### Solution

```bash
chmod 644 hello.txt
```

Check the result:

```bash
ls -l hello.txt
```

You should see permissions equivalent to:

```text
-rw-r--r--
```

`644` means:

```text
6 = rw-
4 = r--
4 = r--
```

The owner can read and write, while the group and others can only read.

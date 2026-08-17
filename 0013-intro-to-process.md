## Understanding Processes

### Task

You are running a program on a Linux machine. Your goal is to understand what a **process** is and how the operating system identifies and tracks it.

1. Start a simple program.
2. Find the process you started.
3. Identify its PID.
4. Identify its PPID.
5. Find out which user owns the process.
6. Check how long the process has been running.
7. Inspect the process using `ps`.
8. Terminate the process.
9. Verify that it is no longer running.

## Solution

1. Start a long-running process: `sleep 300 &`
2. Find the process: `ps -ef | grep sleep`

### Understanding `ps -ef` Output

You might see:

```text
UID   PID    PPID   C  STIME   TTY      TIME     CMD
501   12345  67890  0  2:10PM  ttys001  0:00.00  sleep 300
501   12346  67890  0  2:10PM  ttys001  0:00.00  grep sleep
```

The important columns are:

| Column  | Meaning                              |
| ------- | ------------------------------------ |
| `UID`   | User that owns the process           |
| `PID`   | Process ID                           |
| `PPID`  | Parent Process ID                    |
| `C`     | CPU utilization indicator            |
| `STIME` | Time the process started             |
| `TTY`   | Terminal associated with the process |
| `TIME`  | CPU time used by the process         |
| `CMD`   | Command that started the process     |

For the `sleep` process:

```text
UID    PID     PPID    CMD
501    12345   67890   sleep 300
       ↑       ↑
       │       └── Parent process
       └────────── Process itself
```

3. Identify the PID from the `PID` column.
4. Identify the parent process from the `PPID` column.
5. Inspect the process in more detail: `ps -p <PID> -o user,pid,ppid,etime,command`
6. Check the output:

```text
USER   PID    PPID   ELAPSED   COMMAND
user   12345  67890  00:02:15  sleep 300
```

7. Terminate the process: `kill <PID>`
8. Verify that it is no longer running: `ps -p <PID>`

### What is a Process?

A **process is a running instance of a program**.

```text
Program:  sleep
Command:  sleep 300
Process:  the running instance of sleep
PID:      12345
PPID:     67890
```

The operating system gives every process a **PID (Process ID)** so it can identify and manage it.

Every process also has a **PPID (Parent Process ID)** identifying the process that created it.

```text
Shell
  │
  └── sleep 300
       │
       ├── PID  = 12345
       └── PPID = 67890
```

The `grep sleep` line you may see in the `ps -ef | grep sleep` output is simply the `grep` command itself. It matches because its command contains the word `sleep`.

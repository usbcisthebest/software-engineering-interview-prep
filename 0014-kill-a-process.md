## Task

You are working on a Linux machine and want to learn how to manage running processes.

1. Start a process.
2. Find its PID.
3. Inspect the process.
4. List all running processes.
5. Find a specific process.
6. Stop the process gracefully.
7. Start another process and force-stop it.
8. Verify that it has stopped.

## Solution

1. Start a process in the background: `ping localhost &`
2. Find its PID: `jobs -l`
3. Inspect it: `ps -p <PID> -o pid,ppid,state,command`
4. List all processes: `ps -ef`
5. Find a process: `ps -ef | grep ping`
6. Stop it gracefully: `kill <PID>`
7. Start another process: `ping localhost &`
8. Force-stop it: `kill -9 <PID>`
9. Verify it stopped: `ps -p <PID>`

## Key concepts

`PID` — unique ID assigned to a process.

`PPID` — PID of the process that created it.

`ps` — lists and inspects processes.

`kill <PID>` — sends `SIGTERM`, asking the process to terminate gracefully.

`kill -9 <PID>` — sends `SIGKILL`, forcing immediate termination.

`&` — runs a command in the background.

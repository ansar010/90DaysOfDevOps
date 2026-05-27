
# Day 02 – Linux Architecture, Processes, and systemd


## Today’s goal is to understand how Linux works under the hood.

You will create a short note that explains:

The core components of Linux (kernel, user space, init/systemd)
How processes are created and managed
What systemd does and why it matters
This is the foundation for all troubleshooting you will do as a DevOps engineer.


## Summary Note

## Core Components of Linux:
**Kernel**: The core that talks to hardware and manages resources.
**User Space**: Where applications run (like browsers, shells, editors).
**Init/Systemd**: The first process (PID 1) that starts and manages all other services.

## Process Management:
A process = a running program.
Kernel creates processes using system calls (fork, exec).
Each process has a unique PID and is managed by the scheduler.

## Systemd:
Modern replacement for init.
Starts services in parallel for faster boot.
Manages dependencies between services.
Provides logging, service monitoring, and system states.
Essential for keeping the system organized and stable.

## In simple terms:
Linux is like a team: the kernel is the manager talking to hardware, user space is where workers (apps) do their job, and systemd is the supervisor that makes sure all workers start on time, don’t crash, and shut down properly.

## What is a system call?
A system call is like a special doorway between user space (where your programs run) and kernel space (where the operating system controls hardware and resources).
Programs in user space cannot directly talk to hardware.
Instead, they ask the kernel to do things for them using system calls.

**Think of it as**: “Hey kernel, I need you to do this for me.”

**System calls in process creation**
When you type pwd in the shell:

Shell calls fork() (system call):
The shell asks the kernel: “Please make a copy of me.”
The kernel creates a new process (child) with its own PID.

Child calls exec() (system call):
The child asks the kernel: “Replace me with the pwd program.”
The kernel loads the pwd binary into memory and starts running it.

Kernel manages everything:
Assigns CPU time, memory, and keeps track of the process until it finishes.

### Simple analogy
System call = phone call to the manager (kernel).
fork() = “Make me a twin.”
exec() = “Now change my twin’s job to run this new program.”
Kernel = the manager who actually makes it happen.

**In one line**:  
A system call is the way user programs ask the kernel to perform privileged tasks like creating processes, reading files, or talking to hardware.

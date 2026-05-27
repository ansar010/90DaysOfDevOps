
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

<img width="250" height="300" alt="linux_boot_flow" src="https://github.com/user-attachments/assets/eba1549d-0d83-4218-ad61-475b9d8d64f3" /> 
Power On → hardware gets electricity.
BIOS/UEFI → initializes hardware and checks devices.
Boot Loader (GRUB) → loads the Linux kernel into memory.
Kernel → starts managing hardware and launches systemd (PID 1).
Systemd → starts essential services and prepares the system.
Finally, you reach User Login and User Space Ready, where applications can run.
In short:Power → BIOS → Bootloader → Kernel → Systemd → User Login                                   
<br><br>
<img width="250" height="300" alt="Linux_Architecture" src="https://github.com/user-attachments/assets/5d1f597c-64cf-41f3-9872-a35479ea07ec" />
User Space at the top (applications, shells, user programs)
Kernel in the middle (CPU, memory, devices, system services)
Systemd (PID 1) below (service management, dependencies, startup/shutdown)
And at the very bottom, the Boot Loader & BIOS/UEFI that kick things off.
This layered view makes it easier to remember:
User Space = where you work
Kernel = the core manager
Systemd = the organizer that starts and controls services


## Explain process states (running, sleeping, zombie, etc.)
## List 5 commands you would use daily

**Process States in Linux**
R (Running): Using CPU or ready to run.
S (Sleeping): Waiting for input; can wake up.
D (Uninterruptible sleep): Waiting for hardware; cannot be interrupted.
Z (Zombie): Finished but parent hasn’t collected status.
T (Stopped): Suspended by user signal.
**Check states with ps, top, or htop.**

**5 Daily Commands**
cd → change directory
ls → list files
cp → copy files
mv → move/rename files
rm → remove files
(bonus: mkdir → create directories)

**In simple terms**
Processes in Linux can be running, waiting, stuck, suspended, or dead-but-not-cleaned-up.
And the daily commands are just your basic navigation (cd, ls) and file handling (cp, mv, rm, mkdir).

# SIGTERM
## Introduction to Signal
- A signal can be defined as a software interrupt or a notification that alerts a process about an event occurring in the system.
- Signals offer a versatile mechanism for efficient event handling and coordination between processes, enhancing the overall functionality and reliability of C programs.
- In other words, signal serve as a mean of communication between a running program (process) and the operating system, allowing the program to respond to various events in an unsynchronized manner.
- There are a few signal functions that can be used and each function has its own usage, such as kill() or raise() functions.

## What is SIGTERM?
- SIGTERM signal is used for terminating a program. The SIGTERM can also be referred as a soft kill because the process that receives the SIGTERM signal may choose to ignore it.

### How to Send SIGTERM?
- 

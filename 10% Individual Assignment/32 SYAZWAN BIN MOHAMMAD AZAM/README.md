`SYAZWAN BIN MOHAMMAD AZAM | 2022867954 | M3CS2554A | ITT440`
# How To Send Signal SIGKILL

## What is SIGKILL?
SIGKILL is a signal which is a method of communication between multiple process. It is commonly used in Unix or Unix-Like operating systems like Linux as a way to immediately terminate a process. A signal are send to a running program as a message to triggers a specific action (terminating or handling error). It a type of Inter Process Communication (IPC) which involves the operating system sending signals to target processes while waiting for instruction to complete, interrupting process execution, and handling the signal.
##Function of SIGKILL 
SIGKILL give command to the process to terminate immediately. This command cannot be ignored or blocked and once the process was killed while it is running threads, those will be killed as well. If the process and its threads cannot be terminated by SIGKILL, this indicates an operating system malfunction

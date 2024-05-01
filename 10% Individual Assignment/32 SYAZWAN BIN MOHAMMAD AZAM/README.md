`SYAZWAN BIN MOHAMMAD AZAM | 2022867954 | M3CS2554A | ITT440`
# SIGKILL

## What is SIGKILL?
SIGKILL is a signal which is a method of communication between multiple process. It is commonly used in Unix or Unix-Like operating systems like Linux as a way to immediately terminate a process. A signal are send to a running program as a message to triggers a specific action (terminating or handling error). It a type of Inter Process Communication (IPC) which involves the operating system sending signals to target processes while waiting for instruction to complete, interrupting process execution, and handling the signal.

## Function of SIGKILL 
SIGKILL give command to the process to terminate immediately. This command cannot be ignored or blocked and once the process was killed while it is running threads, those will be killed as well. If the process and its threads cannot be terminated by SIGKILL, this indicates an operating system malfunction

## How To Send Signal SIGKILL
```c
#include <signal.h>
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>

void sigkill();
int main()
{
  int pid;                                        //get child process
  pid = fork();
  
  if (pid<0)
  {
    perror("fork");
    exit(1);
  }
  if (pid=0)                                      //child
  {  
    signal(SIGKILL, sigkill);
    for (int x =1;; x++);
  }
  else                                            //parent
  {
    printf("\nPARENT: sending SIGKILL\n\n");
    kill(pid, SIGKILL);
    sleep(1);                                     //pause for 1 sec
  }
}
void sigkill()
{
  signal(SIGKILL, sigkill);
  printf("CHILD: I have received a SIGKILL\n");
}
```

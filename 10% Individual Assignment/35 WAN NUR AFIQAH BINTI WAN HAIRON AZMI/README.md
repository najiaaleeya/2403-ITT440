**ITT440 - ASSIGNMENT INDIVIDUAL**

**TOPIC – HOW TO COMPLE FORK PROGRAM IN C**

**WAN NUR AFIQAH BINTI WAN HAIRON AZMI**

**2022484148**


## FORK()

Fork system call is used for creating a new process, which is called child process, 
which runs concurrently with the process that makes the fork() call (parent process). 
After a new child process is created, both processes will execute the next instruction 
following the fork() system call. A child process uses the same pc (program counter), 
same CPU registers, same open files which use in the parent process. It takes no 
parameters and returns an integer value.

### EXAMPLE OF FORK PROGRAM

```
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>
int main()
{
  fork(); 
  printf("Fork testing code\n");
  return 0;
}
```

-	Involve 2 kind of process which are child process and parent process.
- Child process run concurrently with the process that make the fork() call which is the 
parent process.
- Parameters;-
  
  - Negative value (-1)
    
    - Creation of a child process was unsuccessful.
      
  - Zero (0)
    
    - Returned to the newly created child process.
      
  - Positive value (+1)
    
    - Return to the newly created child process.
      
```
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>
#include <stdlib.h>

int main()
{
        pid_t child_pid;
        int child_status;
        child_pid = fork();

        switch (child_pid)
        {
                case -1:
                  perror("fork");
                  exit(1);
                case 0:
                  printf("Hello World!\n");
                  exit(0);
                default:
                  wait(&child_status);
        }
        return 0;
}
```
### OUTPUT -->

```
Hello World!
```

-	The fork( ) system call is used for creating a new process by duplicating the existing process, resulting in two processes running at the same time.
-	If we call fork() twice, it will spawn 2<sup>2</sup> = 4 processes. The formula is 2<sup>n</sup>, whereas n is equal to number of fork() command. Which mean if the amount of fork in the command is 3, resulting the output into 8

### EXAMPLE n=1, 2<sup>1</sup>
```
...
switch (child_pid)
{
  ...
  case 0:
    fork();
    printf("Hello World!\n");
    exit(0);
  ...
}
...
```
### OUTPUT -->

```
Hello World!
Hello World!
```

### EXAMPLE n=2, 2<sup>2</sup>
```
...
switch (child_pid)
{
  ...
  case 0:
    fork();
    fork();
    printf("Hello World!\n");
    exit(0);
  ...
}
...
```
### OUTPUT -->

```
Hello World!
Hello World!
Hello World!
Hello World!
```



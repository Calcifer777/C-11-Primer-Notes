
The functions used for C system programming are included in the following headers:
- `unistd.h` (`fork`)
- `stdlib` (`exit`)
- `sys/wait.h`(`wait`, `waitpid`)
- `sys/types` (`pid_t`)

### [fork](http://man7.org/linux/man-pages/man2/fork.2.html)

`pid_t fork(void);`

Creates a new child process, duplicate of the parent process, that works independently from the spawning process. They two do not share memory. 

On success, the PID of the child process is returned in the parent, and 0 is returned in the child. On failure, -1 is returned in the parent, no child process is created, and errno is set appropriately.

### [wait, waitpid](http://man7.org/linux/man-pages/man2/wait.2.html)

`pid_t wait(int *wstatus);`

`pid_t waitpid(pid_t pid, int *wstatus, int options);`

These system calls are used to wait for state changes in a child of the calling process, and obtain information about the child whose state has changed.

The return value is the pid of the child  process terminated; if no children processes are running at the instant `wait()` is called, returns -1.

If wstatus is not NULL, wait() and waitpid() store status information in the int to which it points. The `wstatus` variable contains  more information than the terminal value of the children process. The first 8 bits are reserved to that additional information. Thus, in order to read meaningfully the return int value of the child  process, either divide the `wstatus` by 2^8=256 or use the macros:
- WIFEXITED(wstatus): returns true if the child terminated normally
- WEXITSTATUS(wstatus): returns the exit status of the child.  This consists of the least significant 8 bits of the status argument that the child specified in a call to exit(3) or exit(2) or as the argument for a return statement in main(). This macro should be employed only if WIFEXITED returned true.

**When a parent process has spawned multilple children processes and it has to wait for the termination of all of them, use the cycle `while(pid=wait(&status) > 0)`**

### [exit()](http://man7.org/linux/man-pages/man3/exit.3.html)

`void exit(int status);`

The exit() function causes normal process termination and the value of status & 0377 is returned to the parent. The exit() function does not return.

### [getpid, getppid](http://man7.org/linux/man-pages/man2/getpid.2.html)

`pid_t getpid(void);`
`pid_t getppid(void);`

getpid() returns the process ID (PID) of the calling process.  

getppid() returns the process ID of the parent of the calling process.  This will be either the ID of the process that created this
process using fork(), or, if that process has already terminated, the ID of the process to which this process has been reparented.

### [exec](http://pubs.opengroup.org/onlinepubs/9699919799/functions/exec.html)

`int exec(char* program_name, char** argv);`

The exec() call replaces the entire current contents of the process with a new program. It loads the program into the current process space and runs it from the entry point.

Returns 0 if the command is successfully executed; -1 if an error occurred.

**The list of arguments must be terminated by a NULL pointer, and, since these are variadic functions, this pointer must be cast `(char *)` NULL.** [In depth](https://stackoverflow.com/questions/22570978/does-execl-needs-null-as-last-parameter)

### [sleep](http://man7.org/linux/man-pages/man3/sleep.3.html)

`unsigned int sleep(unsigned int seconds);`

sleep() causes the calling thread to sleep either until the number of real-time seconds specified in seconds have elapsed or until a signal arrives which is not ignored.

Returns 0 if the requested time has elapsed, or the number of seconds left to sleep, if the call was interrupted by a signal handler.

## Snippets

```c++
#include <stdio.h>      // fprintf
#include <stdlib.h>     //exit
#include <sys/types.h>   
#include <unistd.h>     // fork
#include <sys/wait.h>   // wait

int main (char* program, char** arg_list)
{
    pid_t pid;
    int status;
    pid = fork();
    if(pid < 0){
      fprintf(stderr, "Failed to fork() --- exiting...\n");
      exit(1);
    }
    else if (pid == 0){ // --- inside the child process
        fprintf(stdout, "Child -> PID: %i\n", getpid());
    }
    else{ // --- parent process
        fprintf(stdout, "Parent -> PID: %i\n", getpid());
        while(wait(&status) != pid)
        printf("...\n");
    }
    fprintf(stdout, "Terminating %i...\n", getpid());
    return 0;
}
```

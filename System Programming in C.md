
The functions used for C system programming are included in the `unistd.h` header.



fork()

exit()

wait()
waitpid()

getpid()

getppid()

exec

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
    fprintf(stdout, "Trerminating %i...\n", getpid());
    return 0;
}
```

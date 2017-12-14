
The functions used for C system programming are included in the `unistd.h` header.



fork()

exit()

wait()
waitpid()

getpid()

getppid()

exec

```c++
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>
#include <stdlib.h>
#include <sys/wait.h>

int main() {
    pid_t pid;
    int status;
    fprintf(stdout, "Master -> PID: %i\n", getpid());
    fprintf(stdout, "Forking process...\n");
    pid= fork();
    
    if (pid==0) {
       /* Sono nello slave */
        fprintf(stdout, "Slave -> PID %i\n", getpid());
    } else {
        /* Sono nel master*/
        fprintf(stdout, "Master -> PID %i\n", getpid());;
    }
    
    wait(&status);
    
    return 0;
}
```

# System Calls and File Descriptors

## fork



## open/close(fd)





## exec
> [!important]
> exec.c, replace calling process with an executable file
  how does the shell run a program, e.g.
  $ echo a b c
  a program is stored in a file: instructions and initial memory
  created by the compiler and liso there's a file called echo, containing instructions
 

> [!important]
>   exec() will:
>   - Replaces current process with an executable file, 
>   - Discards instruction and data memory 
>   - Loads instructions and memory from the file
>   - Preserves file descriptors exec(filename, argument-array), argument-array holds command-line arguments; exec passes to main()
  cat user/echo.c
  echo.c shows how a program looks at its command-line arguments

```c
// exec.c: replace a process with an executable file

#include "kernel/types.h"
#include "user/user.h"

int
main()
{
  char *argv[] = { "echo", "this", "is", "echo", 0 };

  exec("echo", argv);

  printf("exec failed!\n");

  exit(0);
}
```

## forkexec - shell idioms
> [!concept]
> 



## dup
> [!uses]
> 1. int fd = dup(old_fd); Duplicate old_fd to the fd so that fd is now another reference to old_fd. If we want to print "hello world" to the standard output, we could do the following, now fd is referring to the standard output.
> ![](Operating%20System%20Interfaces.assets/image-20231205193810049.png)
> 2. dup(old_fd, new_fd); Duplicate old_fd to the new_fd so that new_fd is now another reference to old_fd. In other word, the new_fd is not used anymore.
> 3. See the below code, used in pair with close(). The goal of code like this is to change the file descriptor number that references a currently open file. `dup` allows you to create a new file descriptor number which references the same open file as another file descriptor. The `dup` function guarantees that it will use the lowest possible number. `close` makes a file descriptor available. At the end, file descriptor 1 now references the same file that `pfd` used to, and the `pfd` file descriptor is closed. The reference has effectively been transferred from file descriptor `pfd` to file descriptor 1, which means any read or write to file descriptor 1 is actually read or write to `pfd`, which is really powerful.
```c
close(1);  // Make file descriptor 1 available.
dup(pfd);  // Make file descriptor 1 refer to the same file as pfd.
           // This assumes that file descriptor 0 is currently unavailable, so
           // it won't be used.  If file descriptor 0 was available, then
           // dup would have used 0 instead.
close(pfd); // Make file descriptor pfd available.
```



## wait
> [!important]
> - A call to wait() **blocks the calling process until one of its child processes exits or a signal is received**. After child process terminates, parent continues its execution after wait system call instruction.
> - Not the other way around. A child process cannot wait for a parent process, which is a deadlock kind of.
> - If you `fork` multiple times, then the parent process will have to `wait` multiple times for all child process to terminate. For example, if the parent process calls fork() three times, and the chile processes' ids are 0,1,2, then the parent process has to call `wait(&status)` three times, each time one of the child process exit(0); One of the `wait(&status)` will capture that system event and the operating system will put the information of that child process (like child process id) into the status variable so that the parent process know which child processes of the three actually returns.
> 







# I/O Re-direction
## echo content > output_file
```c
#include "kernel/types.h"
#include "user/user.h"
#include "kernel/fcntl.h"

// redirect.c: run a command with output redirected

int
main()
{
  int pid;

  pid = fork();
  if(pid == 0){
    close(1); // Close fd 1, making it available 
    open("output.txt", O_WRONLY|O_CREATE);
	// open syscall finds the least fd number that's available, which is 1 that we have just made available. 
    char *argv[] = { "echo", "this", "is", "redirected", "echo", 0 };
    exec("echo", argv); // exec syscall, execute the echo with fd 1 referring to the output.txt.
    // Note that in the implementation of echo, echo reads from fd 0 and write to fd 1, so with I/O Redirection above, echo is writing to output.txt now.
    printf("exec failed!\n");
    exit(1);
  } else {
    wait((int *) 0);
  }

  exit(0);
}
```



## cat < input_file
```c
char* argv[2];
argv[0] = "cat";
argv[1] = 0;
if(fork() == 0) {
	close(0);
	open("input.txt", O_RDONLY);
	exec("cat", argv);
}
```


# Pipes and Syscall
## wc
> [!def]
> ![](Operating%20System%20Interfaces.assets/image-20231205200219010.png)![](Operating%20System%20Interfaces.assets/image-20231205200233315.png)
> Here, the child process close the p[1] before exec(). The reason is that `wc` system call is going to read from file descriptor zero, which has been redirected to the read end of the pipe. And if we ever try to read from the read end of the pipe by any thread, the read is going to block until there is really nothing more in the write end of the pipe. 
> 
> When is there really nothing more to expect in the write end of the pipe?
> - `It is when the write end of the pipe is closed.` If the write end is present in multiple threads, then all of them should be responsible to close the write end at the end of their logic flow. So we have to close the write end of the pipe in both process to ensure that there is really nothing more to expect.




## grep

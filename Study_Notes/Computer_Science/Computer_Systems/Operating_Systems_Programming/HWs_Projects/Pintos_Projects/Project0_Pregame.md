# Task 0: Finding the faulting Instruction
> [!task]
> - First compile the `proj-pregame/src/tests/userprog/do-nothing.c` with `make`
> ![](Project0_Pregame.assets/image-20240404192309162.png)
> - Then direct to `proj-pregame/src/userprog/build/tests/userprog/do-nothing.result` and observe:
> ![](Project0_Pregame.assets/image-20240404173606142.png)
> 	- The virtual memory that the program tries to access from userspace is `0xc0000008`. This memory is not allocated for user program. It is protected segment. The current process doesn't have the permission to access this memory address.
> 	- The virtual address of the instruction that resulted in the crash is given in the `%eip` register, which shows `0x8048915`.
> 	- We disassemable the object code with `objdump -D do-nothing.o > do-nothing-dump.txt`
> 	- We can also disassemble the executable file with `objdump -x -d do-nothing` to see the function that the program was in before it crashed. Since `%eip = 0x8048915`, we know that when program crashes, it is in the `_start` function.
> ![](Project0_Pregame.assets/image-20240404192129327.png)
> 
> The `_start` function is located in the `proj-pregame/src/lib/user`: 
> 
> ![](Project0_Pregame.assets/image-20240404193852362.png)
> 
> The testing framework expected Pintos to output `do-nothing: exit(162)`. This is the standard message that Pintos prints when a process exits (you’ll encounter this again in Project Userprog). However, as shown in the diff, Pintos did not output this message.
> 
> If `main()` function in `do-nothing.c` returns `162` successfully, then the only place that the crash could happen is the `_start` function.
> 
> We notice that from the `do-nothing-dump-exec.txt` file we see that the function is trying to execute `mov 0xc(%ebp), %eax`, since `%ebp = 0xbffffffc`, `0xc(%ebp)` is exactly `0xc0000008`, which is the portion of memory that is right above the stack frame of `_start` function, which is not permissible to user program.







# Task 1: Step through the crash



# Task 2: Debug
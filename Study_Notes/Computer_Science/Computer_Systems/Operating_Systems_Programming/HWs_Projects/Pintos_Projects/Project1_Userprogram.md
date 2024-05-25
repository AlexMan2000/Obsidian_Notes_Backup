# Doc
> [!note]
> https://pkuflyingpig.gitbook.io/pintos/project-description/lab2-user-programs/your-tasks

# Task 1: Argument Passing
> See https://www.youtube.com/watch?v=RbsE0EQ9_dY

## Overview
> [!task]
> ![](Project1_Userprogram.assets/image-20240517134642520.png)![](Project1_Userprogram.assets/image-20240517134558371.png)



## Functions to modify
> [!important]
> ![](Project1_Userprogram.assets/image-20240517134612569.png)



## Tokenizing
> [!important]
> Function provided by `stdlib.c`
> ![](Project1_Userprogram.assets/image-20240517144939986.png)



## Interruption Frame
> [!important]
> ![](Project1_Userprogram.assets/image-20240517145033003.png)![](Project1_Userprogram.assets/image-20240517145047384.png)
> The above is the virtual address space of the operating system.
> - If we are in user space, when we call `int N`, the operating system will push the user program's registers' values onto interrupt frame and set the `esp` to be the top of the kernel stack. **In short, it saves all the registers onto the interrupt frame and suspend the user space execution.**
> - If we are in kernel space, to trap into the user space, we have to initialize a interrupt frame to save the kernel register values and also when we call `iret`, the operating system will set the `esp` to be the top of the user stack. **In short, it resumes user space execution**
> - The operating system will initialize a new interrupt frame for each newly created thread. Once created, it serves as register saving purposes to hold everything the user program need to resume execution.




### Get into the kernel
> [!important]
> ![](Project1_Userprogram.assets/image-20240517150249767.png)![](Project1_Userprogram.assets/image-20240517150411175.png)



### Get out of Kernel
> [!important]
> ![](Project1_Userprogram.assets/image-20240517150601047.png)![](Project1_Userprogram.assets/image-20240517151719458.png)





## Function Calling Convention
> [!important]
> ![](Project1_Userprogram.assets/image-20240517161834952.png)![](Project1_Userprogram.assets/image-20240517172601284.png)![](Project1_Userprogram.assets/image-20240517173955944.png)
> 




## Code Implementations
> [!code]
```c
/* Starts a new thread running a user program loaded from
   FILENAME.  The new thread may be scheduled (and may even exit)
   before process_execute() returns.  Returns the new process's
   process id, or TID_ERROR if the thread cannot be created. 


   @param file_name: the program(with arguments to be executed), e.g. ls -ahl

   */
pid_t process_execute(const char* file_name) {
  char* fn_copy;
  tid_t tid;

  sema_init(&temporary, 0);
  /* Make a copy of FILE_NAME.
     Otherwise there's a race between the caller and load(). */
  fn_copy = palloc_get_page(0);
  if (fn_copy == NULL)
    return TID_ERROR;

  strlcpy(fn_copy, file_name, PGSIZE);

  /* Here file_name is ls -ahl 
     We need to tokenize it into "ls" and "-ahl"
     The "ls" will be the first argument for thread_create
     "ls -ahl" will be fn_copy
  */

  char* delimiter_pointer;
  char* executable_name = strtok_r(file_name, " ", delimiter_pointer);

  /* Create a new thread to execute FILE_NAME. */
  /* 创建一个新的内核线程
      1. 创建一个thread_t 结构体
      2. 分配内核栈
      3. 将函数start_process作为线程执行函数
      4. 将线程加入READY队列供CPU调度
   */
  tid = thread_create(executable_name, PRI_DEFAULT, start_process, fn_copy);
  if (tid == TID_ERROR)
    palloc_free_page(fn_copy);
  return tid;
}

/* A thread function that loads a user process and starts it
   running. */
static void start_process(void* file_name_) {
  
  char file_name[strlen((char *) file_name_) + 1];
  strlcpy(file_name, file_name_, strlen((char *) file_name_) + 1);

  struct thread* t = thread_current();
  struct intr_frame if_;
  bool success, pcb_success;


  /* Allocate process control block */
  struct process* new_pcb = malloc(sizeof(struct process));
  success = pcb_success = new_pcb != NULL;


  // Parse the filename
  /* 
     file_name_: "ls arg1 arg2"
     we need to parse it into "ls", "arg1 arg2..."
  */

  char *program_name, *save_ptr;
  program_name = strtok_r(file_name, " ", &save_ptr); // Remember the & before save_ptr since we are modifying where saveptr points to


  /* Initialize process control block */
  if (success) {
    // Ensure that timer_interrupt() -> schedule() -> process_activate()
    // does not try to activate our uninitialized pagedir
    new_pcb->pagedir = NULL;
    t->pcb = new_pcb;

    // Continue initializing the PCB as normal
    t->pcb->main_thread = t;
    strlcpy(t->pcb->process_name, t->name, sizeof t->name);
  }

  /* Initialize interrupt frame and load executable. */
  if (success) {
    memset(&if_, 0, sizeof if_);
    if_.gs = if_.fs = if_.es = if_.ds = if_.ss = SEL_UDSEG;
    if_.cs = SEL_UCSEG;
    if_.eflags = FLAG_IF | FLAG_MBS;
    
    // Load the ELF(executable) into memory and set up the user stack
    success = load(program_name, &if_.eip, &if_.esp);
  }

  /* Handle failure with succesful PCB malloc. Must free the PCB */
  if (!success && pcb_success) {
    // Avoid race where PCB is freed before t->pcb is set to NULL
    // If this happens, then an unfortuantely timed timer interrupt
    // can try to activate the pagedir, but it is now freed memory
    struct process* pcb_to_free = t->pcb;
    t->pcb = NULL;
    free(pcb_to_free);
  }


   /* If everthing is successful.
    Continue and push the arguments onto the user stack 
  */
  push_arguments(&if_.esp, file_name_);


  // printf("STACK SET. ESP: %p\n", if_.esp);
  // hex_dump((uintptr_t)if_.esp, if_.esp, 100, true);

  /* Clean up. Exit on failure or jump to userspace */
  palloc_free_page(file_name_); // This line will free the file_name, so use it before freeing
  if (!success) {
    sema_up(&temporary);
    thread_exit();
  }

  /* Start the user process by simulating a return from an
     interrupt, implemented by intr_exit (in
     threads/intr-stubs.S).  Because intr_exit takes all of its
     arguments on the stack in the form of a `struct intr_frame',
     we just point the stack pointer (%esp) to our stack frame
     and jump to it. */

  // movl %0, %%esp will set the esp to the top of the interrupt frame(edi)
  asm volatile("movl %0, %%esp; jmp intr_exit" : : "g"(&if_) : "memory");
  NOT_REACHED();
}



/*
   @param esp: Pointer to the stack pointer
   @param argument_string "ls arg1 arg2"
*/
void push_arguments(void** esp, char* argument_string) {
  int argc = 0;
  int bytes_count = 0;
  char* token, *save_ptr;
  char original_string[strlen(argument_string) + 1];
  strlcpy(original_string, argument_string, strlen(argument_string) + 1);


  // Get the total number of arguments, stored it in the argc
  for (token = strtok_r(argument_string, " ", &save_ptr);
        token != NULL;
        token = strtok_r(NULL, " ", &save_ptr)) {
      argc++;
  }

  char** argv_temp[argc];
  argc = 0;
   /* Calculate where the top of the stack should be after allocating all the 
    argument space and alignment.
  */
  for (token = strtok_r(original_string, " ", &save_ptr);
        token != NULL;
        token = strtok_r(NULL, " ", &save_ptr)) {
      int bytes_arg = strlen(token) + 1;
      *esp -= bytes_arg;
      argv_temp[argc++] = *esp;  // Starting address of the argument string e.g. "arg1" is saved at 0xbffffffde
      strlcpy(*esp, token, bytes_arg); // strcpy will copy the null terminator at the end
      bytes_count += bytes_arg;
  }

  // Stack Align to multiple of 4 bytes
  // Number of empty bytes to pad
  int bytes_to_pad = (int) *esp - ((int)*esp & 0xfffffffc);
  *esp = (void *) ((int) *esp & 0xfffffffc);
  memset(*esp, 0, bytes_to_pad);

  // Push argv addresses
  *esp -= 0x4;
  memset(*esp, 0, 4); // Used to terminate the argv[]
  for (int i = argc - 1; i >= 0; i--) {
    *esp -= 0x4;
    memcpy(*esp, &argv_temp[i], 4);
  }

  // Push argv
  void* argv_start = *esp; // An address
  *esp -= 0x4;
  memcpy(*esp, &argv_start, 4);

  // Push argc
  *esp -= 0x4;
  memcpy(*esp, &argc, 4);

  // Push fake return address, never return actually
  *esp -= 0x4;
  memset(*esp, 0x0, 4);
}
```



## Tests
> [!test]
> Tests related are `tests/userprog/args.c`, which involves five subtests:
> `args-none, args-single, args-many, args-multiple, args-dbl-space`





# Task 2: Process Control Syscalls
> [!overview]
> 需要修改`userprog/syscall.c`中的`syscall_handler`函数使其能够支持更多的系统调用。
> 
> **参考:** https://huaweidevelopers.csdn.net/659b5fd1dafaf23eeaee458d.html?dp_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpZCI6MTYxMDQwOSwiZXhwIjoxNzE3MjQ1NzQ4LCJpYXQiOjE3MTY2NDA5NDgsInVzZXJuYW1lIjoibTBfNDYwODAwODkifQ.rqhXbIcsoWzV4KX0oQvI5_V9JDIHZsiDzqqmEF9w4QE




## Preliminaries
### Syscall Procedures
> [!important]
> 当用户调用`read/write/exit/exec()`等方法时，实际上是调用了`lib/user/syscall.c`中的方法, 我们以`pid_t exec(const char* file)`举例:
```c
pid_t exec(const char* file) { return (pid_t)syscall1(SYS_EXEC, file); }
```
> [!exp]
> 该方法会创建一个新的进程(里面包含一个主线程)执行名为`file`的程序，同时返回新创建的主线程的`tid_t`作为该进程的`pid_t`。注意到函数体内调用了一个宏`syscall1(SYS_EXEC, file)`。
> 
> 这个宏会将用户传入的参数`file`作为该系统调用的第二个参数，同时将系统调用的第一个参数设置为系统调用号(在`lib/syscall-nr.h`中定义)，并按照`80x86 calling convention`的方式将这两个参数压入栈，调用`int $0x30`后`userprog/syscall.c`中的`syscall_handler`就可以通过`intr_frame`获取这两个参数, 然后进行系统调用的分发处理。
```c
/* Invokes syscall NUMBER, passing argument ARG0, and returns the
   return value as an `int'. */
#define syscall1(NUMBER, ARG0)                                      
  ({                                                                
    int retval;                                                     
    asm volatile("pushl %[arg0]; pushl %[number]; int $0x30; addl $8, %%esp"                       
                 : "=a"(retval)                                     
                 : [number] "i"(NUMBER), [arg0] "g"(ARG0)           
                 : "memory");                                      
    retval;                                                        
  })
```
> [!exp] syscall_handler
> 在`syscall_handler`函数中，我们可以通过`interrupt frame`获取用户传入的参数值，一般`args[0]`就是系统调用号，`args[1],....`都是系统调用所需的参数，比如`exec(const char* file)`就需要`file`参数，可以通过`args[1]`获取。
```c
static void syscall_handler(struct intr_frame* f) {

  uint32_t* args = ((uint32_t*)f->esp);
...  
}
```

 
 


### Accessing User provided Memory
> [!important]
> 很多时候，用户在系统调用的时候会传入地址值，比如`exec(const char* file)`传入的就是文件名的起始地址。系统调用程序需要对这个地址值进行验证看其是否合法。
> - 在`userprog/pagedir.c`中有一个`pagedie_get_page(void* pagedir, void* vaddr)`方法用于检查`vaddr`是否存在于`page table`中，如果存在说明该虚拟内存已经被映射到对应的物理内存。否则，表明该虚拟内存未分配，不可用。
> - 在`threads/vaddr.h`中有一个`is_user_vaddr(const void* vaddr)`方法用于检查一个虚拟内存地址是否是用户地址空间中的地址，即是否小于`PHYS_BASE(0xc0000000)`。
> 
> 我们可以使用这两个方法判断用户传入的地址值是否合法，从而保护内核态免受攻击。




## Code Implementations
### SYS_PRACTICE




### SYS_EXIT




### SYS_HALT





### SYS_EXEC(Medium)
> [!task]
> ![](Project1_Userprogram.assets/image-20240525192907801.png)



### SYS_WAIT(Very Hard)
> [!task]
> See [Simple Scheduling](../../3_Synchronizations/Thread_Synchonization.md#Simple%20Scheduling) example.
> ![](Project1_Userprogram.assets/image-20240525165909556.png)
> 


> [!exp] Hints
> ![](Project1_Userprogram.assets/image-20240525165819620.png)![](Project1_Userprogram.assets/image-20240525170024886.png)![](Project1_Userprogram.assets/image-20240525170011673.png)







## Tests





# Task 3: File Operation Syscalls

## Preliminaries


## Code Implementations
### SYS_CREATE


### SYS_REMOVE



### SYS_OPEN


### SYS_FILESIZE


### SYS_READ


### SYS_WRITE


### SYS_SEEK


### SYS_TELL




### SYS_CLOSE





# Task 4: Floating Point Operations



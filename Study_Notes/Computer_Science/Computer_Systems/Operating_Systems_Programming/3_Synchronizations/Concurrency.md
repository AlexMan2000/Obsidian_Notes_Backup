# Basic Concepts
## Threads and Processes
> [!concept]
> A _thread_ of execution is the smallest sequence of instructions that can be managed by a scheduler. 
> 
> **A thread is a component of a process**, a recipe of independent execution. 
> 
> Multiple threads can exist within one process, being **executed concurrently** and **sharing the process's resources** such as memory space, executable code, variables, etc. while different processes do not share them. 
> 
> There are a lot of ideas in multiprocessing which lend themselves to _multithreading_, another form of _concurrency programming_, where multiple logical control flow overlap or interleave in time.
> 
> A program does not have to rely on multiprocessing to run multiple functions at the same time. As an alternative, it can create multiple threads with one process.
> 
> **Examples:**
> - An online music application may choose to download multiple songs simultaneously
> - A web browser may choose to load multiple web pages simultaneously using multiple threads.




## Dispatch Loop
> [!concept]
> ![](Concurrency.assets/image-20240306103753955.png)



### Starting a Thread
> [!concept]
> ![](Concurrency.assets/image-20240306110838338.png)![](Concurrency.assets/image-20240306110525188.png)![](Concurrency.assets/image-20240306110519133.png)![](Concurrency.assets/image-20240306110532918.png)![](Concurrency.assets/image-20240306110544795.png)




### Running a Thread
> [!important]
> ![](Concurrency.assets/image-20240306103924493.png)


### Switching between Threads
#### Internal Events: yield()
> [!def]
> ![](Concurrency.assets/image-20240306104000407.png)![](Concurrency.assets/image-20240306104201132.png)
> Each thread has its own kernel stack, each process has its own kernel stack. Threads' kernel stacks are well contained in the same portion of memory of its containing process's kernel stack.
> 
> **Q: What's the relationship between user stack and kernel stack?**
> For each thread or process, there can only be one active stack at the same time. Either the user stack is in use or the kernel stack is in use.
> ![](Concurrency.assets/image-20240306105556263.png)


#### External Events: Interrupts
> [!def]
> ![](Concurrency.assets/image-20240306110315551.png)![](Concurrency.assets/image-20240306110322915.png)![](Concurrency.assets/image-20240306110356378.png)



#### External Events: Timer
> [!def]
> ![](Concurrency.assets/image-20240306110409419.png)








## Context Switching
### Switching Procedures
> [!important]
> ![](Concurrency.assets/image-20240306105857605.png)![](Concurrency.assets/image-20240306105945354.png)


### Efficiency
> [!def]
> ![](Concurrency.assets/image-20240306110205866.png)







## A naïve example
> [!code]
> In psychology, [introversion](https://en.wikipedia.org/wiki/Extraversion_and_introversion) is the state of being predominantly interested in one's own mental self. Introverts are typically perceived as more reserved or reflective, but mistaking introversion for shyness is a common error. They can recharge themselves by spending time alone.
> 
> Introverts prefer solitary to social activities, but do not necessarily fear social encounters.
```c
#include <stdio.h>  
#include <pthread.h>  
​  
/* thread routine: notice the return type and arugument type */  
void *recharge(void *unused) {  
    printf("I recharge by spending time alone.\n");  
    sleep(1);  
    return NULL; /* to statisfy the prototype */  
}  
​  
int main() {  
  pthread_t introverts[6];  
  for (size_t i = 0; i < 6; i++)  
    /* create 6 independent threads */  
    /* All args are pointers */  
    pthread_create(&introverts[i], NULL, recharge, NULL);  
  for (size_t i = 0; i < 6; i++)  
    /* block and wait for the child thread's termination */  
    /* The first arg is a TID, the second is a pointer to pointer */  
    pthread_join(introverts[i], NULL);  
    
  printf("Everyone's recharged!\n");  
  return 0;  
}  
/* takes ~1 sec to run due to multithreading, as opposed to ~6 sec */

```

### pthread_create()
> [!important]
> - `pthread_t` is essentially an integer - the thread's ID (TID). Similar to `pid_t`.
> - The thread routine is a function that **takes in a** `void *` **and returns a** `void *`. In fact, you can pass in a pointer to structure or return a pointer to structure, utilizing pointer's type casting.
> - `pthread_create()`'s takes in 4 arguments, all of which are pointers.
```c
int pthread_create(  
          pthread_t *pTID, /* TID ptr. */  
          const pthread_attr_t *pAttr, /* thread attribute ptr. */  
          void *(*pRoutine) (void *), /* thread routine function ptr. */  
          void *pArg /* argument ptr. */  
        );
```
> [!important]
> - The first argument `pTID` points to the variable to store the TID,
> - The second argument `pAttr` points to the structure whose contents are used at to determine attributes for the new thread, such as priority. It can be `NULL`.
> - The third argument `pRoutine` points to the start function of the thread routine, and that function can call other functions.
> - The fourth argument `pArg` points to the argument that is to be passed to the thread routine. It can be a structure if there are more than one actual arguments to be passed, or a `NULL` if none.
> - It returns `0` on success; on error, it returns an error number, and the content of `pTID` is undefined.


### pthread_join()
> [!important]
> - If the master thread ("the mommy thread"), i.e. the thread of the process itself, exists, the entire virtual memory space of the process will be de-allocated, killing every child threads it gave birth to. So we need to wait for the child threads to terminate before letting the master thread terminates: `int pthread_join(pthread_t TID, void **ppRetval);`
> - The first argument `TID` is the ID of the intended thread. Note that it is not a pointer.
> - The second argument `ppRetval` is a pointer to the pointer to the return value of the thread.
> - If the intended thread has already terminated, then `pthread_join()` returns immediately. Otherwise it **blocks and waits**.
> - The thread specified by `TID` must be **joinable**, i.e. not detached. When a detached thread terminates, its resources are automatically de-allocated without the need for another thread to join with it. `int pthread_detach(pthread_t TID);` can detach a thread. A detached thread cannot be killed nor reaped by another thread, but a joinable thread can.
> - On success, it returns `0`; on error, it returns an error number, among which are:
> 	- `EINVAL`: another thread is already waiting to join with this thread, or the intended child thread is not joinable.
> 	- `ESRCH`: no thread with that TID thread could be found.
> 	- `EDEADLK`: a deadlock was detected (e.g., two threads tried to join with each other), or the first argument `TID` specifies the calling thread itself.
> - Child threads are not obligated to start or finish together or in a predictable order - it is up to the kernel's scheduler (yes, the scheduler can manipulate threads). Once a child thread finishes, `pthread_join()` joins the child thread with the calling thread (in this example, the master thread).
> - Failure to join with a thread that is joinable (i.e. undetached), produces a _zombie thread_. Avoid doing this, since zombie threads consume some system resources.
> 
> An illustration of creating and joining 2 child threads:
```
    ┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐  
                     start             finish       a single process  
                   ▲──●──────────────────●─ ─ ┐   
     master thrd.  │   cr   child thrd. 1     │   jn     
    ───────────────┴───┬──────────────────────▼───▲─────────▶   
                  cr   │      child thrd. 2   jn  │       
                       ▼──────●────────●─ ─ ─ ─ ─ ┘   
                            start     finish  
    └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘  
    cr: pthread_create()     jn: pthread_join()
```
> [!bug] Caveats
> SIDE NOTE: ANSI C doesn't provide native support for threads. But POSIX threads (aka pthread) comes with all standard UNIX and Linux installations of gcc, as concurrency programming requires the cooperation of the kernel.


### The CPU and memory, thread context switch
> [!concept]
> - Each process has a thread manager responsible for interleaving the execution time window within the process's execution time.
> - Note that the threads created in the example above all belong to **the same process**, hence they reside in the **same virtual memory space**.
> - What we are interested in is what happens in the stack and text segments in the virtual memory space.
> 	- **The stack segment:** each thread takes a subsegment in the stack, forming their own call stacks. Inside each thread's call stack, there is a stack space reserved to store the CPU register info when that thread is swapped off from the CPU. There is no overlapping in the stack, so automatic variables cannot be inherited by child threads (unlike multiprocessing). It serves as the "switchframe" of the corresponding thread, the difference from a process's switchframe being that a thread's is stored within the stack segment of the process's virtual memory space, while a process's is stored in the kernel space.
> 	- **The text segment:** the instruction pointer `rip` points to different instructions, jumping among the master's and child threads' routines.
> - All threads share the heap, data, text, .. segments in the virtual memory space. Because of this, **threads within one process can communicate with each other more easily than processes**, who has to turn to pipes and signals.
> - In the same process, a thread's access to another thread's **objects in stack** is provided by pointers/references.
> - _Preemptive multitasking_: the scheduler can switch the task (process/thread) out from CPU and switch another in, at any time it feels like.
> - _Cooperative multitasking_: the task (process/thread) can only be switched out from CPU when it allows - say, a stage completes - and other tasks have to wait. Cooperative multitasking was the primary scheduling scheme for 16-bit applications employed by Microsoft Windows before Windows 95, and by the classic Mac OS. In computer network protocols, similar mechanisms is applied.





# C++ Multithreading
> [!concept]
> The C++ thread interfaces are type-safe and cleaner.

### The old-school C form
```c
#include <stdio.h>  
#include <pthread.h>  
​  
/* thread routine */  
/* Note the return and arg types are all "void *" */  
void *recharge(void *unused) {  
    printf("I recharge by spending time alone.\n");  
    return NULL;  
}  
​  
int main() {  
    pthread_t introverts[6];  
    for (size_t i = 0; i < 6; i++) {  
        pthread_create(&introverts[i], NULL, recharge, NULL);  
    }  
    for (size_t i = 0; i < 6; i++) {  
        pthread_join(introverts[i], NULL);  
    }  
​  
    return 0;  
}
```



## The C++ form
> [!code]
> `using namespace std;` is omitted in C++ code afterwards.
```c++
/* C++11 */  
#include <iostream>  
#include <thread>  
/* CS110 iomanipulators (oslock, osunlock) used to lock down streams */  
#include "ostreamlock.h"  
using namespace std;  
​  
/* Note the return type is "void" */  
void recharge() {  
    cout << oslock   
         << "I recharge by spending time alone." << endl  
         << osunlock;  
    return;  
}  
​  
int main() {  
    /* declare 6 thread objects (handles) */  
    thread introverts[6];  
      
    /* install thread routine to these threads */  
    for (thread &t : introverts) {  
        t = thread(recharge);  
    }  
    /* join: block, wait, reap zombie threads */  
    /* note you need the "&" below, since thread class's  
     * assignment operator is deleted */  
    for (thread &t : introverts) {  
        t.join();  
    }  
​  
    return 0;  
}

```
> [!exp]
> C++ prototypes explained:
> - `oslock` and `osunlock` are implemented by CS110 course and meant to exclusively lock/unlock the output file stream, since `cout` is not thread-safe (unlike `printf()`). Without them, `ostream::operator<<()`'s output by multiple threads may get garbled.
> - In C++, the thread routine can **take in any number of arguments** of any type.
> - In C++, the thread routine **returns nothing**. If it does return something, the return value will be ignored.
> - `thread` is a C++11-provided class, defined in the `std` namespace. These methods are used in the code above:
```c++
 /* default constructor */  
thread();  
/* initialization (the exact prototype is not our focus):  
   takes in a function pointer, followed by arguments (if any)  
   the thread routine's return is ignored */  
thread (pRoutine, args...);  
​  
/* assign operator */  
thread& operator= (thread&& rhs); // rvalue reference  
/* join */  
void join();
```
> [!exp]
> Some other methods that may be frequently use:
```c++
/* check is joinable */  
bool joinable();  
/* detach */  
void detach();  
/* get thread ID */  
thread::id get_id();
```
> [!important]
> The method `thread &operator=(thread &&t)` takes in an rvalue reference. A effect of this design is that, after the `thread` object `t` on right hand side is assigned to the left hand side, **the original** `t` **is gutted**: as if it were a zero-argument constructed, empty, **detached** thread object. Such mechanism is suitable if the right hand size object takes considerable effort to construct or clone. It is unlike normal `a = b` assignment, after which `b` is intact and `a` is a copy of `b`.



## Another C++ example: using variadic arguments
> [!code] 
```c++
/* C++11 */  
#include ...  
​  
/* Note the return type is "void" and we pass in an arg to it*/  
void greet(size_t id) {  
  for (size_t i = 0; i < id; i++) {  
    cout << oslock << "Greeter #" << id << " says 'Hello!'" << endl << osunlock;  
  }      
  cout << oslock   
       << "Greeter #" << id << " has issued all of his hellos, "  
       << "so he goes home!" << endl   
       << osunlock;  
}  
​  
int main(int argc, char *argv[]) {  
  thread greeters[6];  
  for (size_t i = 0; i < 6; i++) {  
      /* Note that the variadic arg is passed in (one arg here):  
         thread (pRoutine, args...); */  
      greeters[i] = thread(greet, i + 1);  
      /* Pay attention to avoid the race condition  
         as discussed before */  
  }  
  for (thread& greeter: greeters) {  
      greeter.join();  
  }  
​  
  return 0;  
}
```



# Java Multithreading
## Starting a Thread
> [!important]
> Why the following line is executed, the following events happen in order:
> 1. A `Runnable` object is created.
> 2. A `Thread` object is created.
> 3. `start()` is called. This function will trap into the kernel of OS and start and schedule a thread.
> 4. `run()` is called, the job associated to the newly started thread is runned.
> 5. `run()` returns.
```java
new Thread(new Runnable() {
	// Job
    public void run() {
        System.out.println("Hello from a thread!");
    }
}).start();


// Equivalent Lambda Expression Form
new Thread(() -> System.out.println("Hello from a thread!")).start();
```
> [!concept]
> **When you run a Java program (for example, using the Run button in Eclipse), how many processors, processes, and threads are created at first?**
> 
> Processors are physical components in the machine. For our purposes, the number of processors is fixed. A better way to say this is we multiplex/schedule a processor for the current program, instead of creating a processor.
> 
> When a program starts, it automatically gets one process to run in, and it gets one thread for its execution.



## start() and run()
> [!bug] Caveat
> The following code is a typical misuse of `start()` and `run()`, in this example, no new threads will be scheduled by CPU. 
> 1. `run()` will call the job that is assigned to the thread object, but is executed by the main thread.
> 2. `start()` will actually trap into the OS and fork new threads for job execution.
```java
public class Parcae {
    public static void main(String[] args) {
        Thread nona = new Thread(new Runnable() {
            public void run() { System.out.println("spinning"); }
        });
        nona.run();
        Runnable decima = new Runnable() {
            public void run() { System.out.println("measuring"); }
        };
        decima.run();
        // ...
    }
}
```
> [!tips]
> **Never** call `run()` on a `Thread`, or on a `Runnable` that you created for a thread. Instead, always make a `new Thread()` with an instance of your `Runnable`, and call `start()` on the thread to start it. `Thread` will take care of calling `run()` on your `Runnable` from the new thread.



## Thread and JUnit
> [!bug] Caveats
> ![](Concurrency.assets/image-20240306115250618.png)





## Thread and Process
> [!code]
> Suppose we run `main` in this program, which contains bugs:
```java
public class Moirai {
    public static void main(String[] args) {
        Thread clotho = new Thread(new Runnable() {
            public void run() { System.out.println("spinning"); }
        });
        clotho.start();
        new Thread(new Runnable() {
            public void run() { System.out.println("measuring"); }
        }).start();
        new Thread(new Runnable() {
            public void run() { System.out.println("cutting"); }
        });
    }
}
```
> [!quiz] 
> 1. **How many new `Thread` objects are created during the execution of `main`?**
> 	3, One is assigned to variable `clotho`. The other two are not assigned to a variable.
> 1. **How many new threads are run?**
> 	2, The code calls `start` on the first two threads. But the third thread is never `start`ed, so it will not run.
> 1. **What is the maximum number of threads that might be running at the same time?**
> 	The **initial thread** running `main` plus the two new threads that were started. The reason we have to say “might” here is because different interleavings may mean that we don’t always reach this maximum; for example, the first new thread might finish running before the second one even starts.








# Race condition: critical region, `mutex` (KOB)
## Problematic Ticket Selling
### Buggy Implementation
> [!concept]
> Consider there are two ticket agents at the [United Airlines](https://en.wikipedia.org/wiki/United_Express_Flight_3411_incident). Their job is to sell 3 tickets in total, and the law prohibits overselling.
    
> [!bug] Buggy Implementations
```c++
/* Buggy */  
#include <iostream>  
#include <thread>  
#include "ostreamlock.h"  
using namespace std;  
static int numTickets = 3; /* threads cannot share automatic variables */  
​void ticketAgent(size_t id) {  
    while (numTickets > 0) {  
       numTickets--;  
        cout << oslock   
             << "Ticket agent " << id << " sold one ticket,"  
             << " there are " << numTickets   
             << " more to sell!" << endl  
             << osunlock;  
     }  
}  
​  
int main() {  
    thread agents[2];  
    for (size_t i = 0; i < 2; i++) {  
        agents[i] = thread(ticketAgent, 101 + i); /* agent 101, 102 */  
    }  
    for (thread &a : agents) { /* block and wait for each thread */  
        a.join();  
    }  
    cout << "End of business day!" << endl;  
​  
    return 0;  
}
```
> [!exp]
> There are two problems caused by the **unpredictability of the scheduler**.
> - **The first problem.**
> 	- Say, (1) agent 101 proceeds to line 8 and discovered that `numTickets` is `1`, and is thus indeed greater than `0`, so it decides to sell one more ticket. (2) immediately after line 8, agent 101's thread is switched out from CPU, and agent 102 comes in. (3) agent 102 comes along and proceeds to line 8, it discovers `numTickets` is `1` and is greater than `0`, so it proceeds to sell the ticket and decrement `numTickets` to `0`. (3) agent 101 is switched back and it proceeds from where it left - it sells one ticket, decrementing `numTickets`.
> 	- In the scenario above, the final `numTickets` is `-1`, and one ticket is oversold.
> 	- The root of this problem is that, the code lacks a mechanism to guarantee line 9 is executed immediately after line 8.
> - **The second problem.**
> 	- Let's assume the first problem is fixed: line 9 is executed immediately after line 8.
> 	- Note that line 9: `numTickets--;` might be translated into at least 3 assembly instructions, not 1 (assume `numTickets` is stored on address `0x1122`) - dependent on the instruction set:
> 		- **mov** $0x1122, %rax   ;move address of `numTickets` to rax (line A)  
> 		- **movq** (%rax), %eax    ; move content of `numTickets` to eax (line B) 
> 		- **leaq** -0x1(%eax), %edx     ;subtract the value in eax by 1 (line C)  
> 		- **mov** $0x1122, %rax           ;move address of `numTickets` to rax (line D)
> 		- **movq** %edx, (%rax)           ;move value from edx to 0x1122  (line E)
> 	- Say (1) agent 101 is switched out from CPU immediately after it completes line A, and the RAX value is stored. (2) agent 102 comes along, sells a ticket, and decrements `numTickets` to `0`. (3) agent 101 is switched back, stored register values loaded back to CPU, and proceeds from where it left: it executes line B,C,D,E.
> 	- Thus, the final `numTickets` is `-1`, and one ticket is oversold. **A C++ statement is not atomic; an assembly instruction is**.
```

    <thrd.1> :                      : <thrd.1>  
    ───●───●─:─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─●──●─●─●─..─●─▶  
       {   A :                      :B  C D E     }    
             ▽                      △                 ──▶ time  
             ▽                      △              
             :  {    A  B  C D  E     } :          
    ─ ─ ─ ─ ─:──●────●──●──●─●──●────●─:─ ─ ─ ─ ──▶  
             :      <thrd.2>        :
    
```
> [!exp]
> 
> A _race condition_ happens when the processes or threads depend on some **shared state** (`numTickets`'s value here). Operations upon shared states are critical code sections (_critical region_s) that must be mutually exclusive. That is, when one steps into the critical region, the others should be prevented to do the same until the first one steps out.



### Solution: `mutex` and locking
> [!success]
> In the example above, C++ code line 8 to 14 should be executed in tandem without the thread being switched halfway. That is, line 8 to 14 should be a transaction.
> 
> "mutex": mutual exlusion. This is a C++ class, and some of its methods are
```c
/* constructor */      mutex();  
/* lock */             void lock();  
/* unlock */           void unlock();  
/* lock if unlocked */ bool try_lock();
```
> [!exp]
> - `lock()`: (1) if the object is unlocked, then lock it, and the following code is in a transaction; (2) if the object is locked by another thread, then **block and wait** until unlocked; (3) if the object is already locked by the same thread, it caused an undefined behavior. 
> 	- Whenever a process or thread is in a blocked state, it will be switched out from CPU, and register values are stored in memory. When more than one thread attempts to lock it, one of them succeeds.
> - `unlock()`: (1) if the object is locked by the same thread, then unlock it, and the following code is not in a transaction; (2) if the object is already unlocked, the behavior is undefined.
> - `try_lock()`: (1) if the object is unlocked, then lock it and return `true`; (2) if the object is locked by another thread, then give up and immediately return `false`; (3) if the object is already locked by the same thread, it caused an undefined behavior.
> 	- Like in a hostel, people go to the bathroom to take shower. The shower-taker locks the door before start and unlocks it after the job is done. While the door is locked, other people just wait outside (or leave and come back later).
> [!success]
> The fixed version:
```c++
/* Problem fixed */  
#include <iostream>  
#include <thread>  
#include "ostreamlock.h"  
#include <mutex>        /* for mutex class */  
using namespace std;  
static int numTickets = 3;  
static mutex ticketLock;   /* global, shared among threads */  
​  
 7 void ticketAgent(size_t id) {  
 8*   while (true) {  
 8+       ticketLock.lock(); /* lock */  
 9        numTickets--;  
10        cout << oslock   
11             << "Ticket agent " << id << " sold one ticket,"  
12             << " there are " << numTickets   
13             << " more to sell!" << endl  
14             << osunlock;  
14+       if (numTickets == 0) break;  
14++      ticketLock.unlock(); /* unlock */  
15    }  
16}  
​  
int main() {  
    thread agents[2];  
    for (size_t i = 0; i < 2; i++) {  
        agents[i] = thread(ticketAgent, 101 + i); /* agent 101, 102 */  
    }  
    for (thread &a : agents) { /* block and wait for each thread */  
        a.join();  
    }  
    cout << "End of business day!" << endl;  
​  
    return 0;  
}
```
> [!exp]
> **Code explained:**
> - **To fix problem 1**: replace `while(numTickets < 0)` with `while (true)` and place the condition checking inside the loop. And...
> - **To fix problem 1 and 2**: use a `mutex` lock object to guard the loop body, which is the _critical region_: the sequence of instructions that **at most one thread** should be in at any time.
> - Note that the `mutex` object should be global, so all threads can agree on this lock.
> 	- You certainly don't want someone else to come into the bathroom **though another door** while you are in it, right?



## Interleaving of Instructions
> [!example] Java Example 1
```java
private static int x = 1;

public static void methodA() {
  x *= 2;
  x *= 3;
}

public static void methodB() {
  x *= 5;
}
```
> [!quiz] 
> 1. Suppose `methodA` and `methodB` run **sequentially**, i.e. first one and then the other. What is the final value of `x`?
> 2. Now suppose `methodA` and `methodB` run **concurrently**, so that their instructions might interleave arbitrarily. Which of the following are possible final values of `x`?
> 
> Suppose the `x*=<n>` involves five instructions:
> - A: mov $0x1102, %rax
> - B: movq (%rax), %eax       ; A and B read the value from `static`, put it in %eax
> - C: leaq (%eax, %eax, n - 1), %edx
> - D: mov $0x1102, %rax
> - E: movq %edx, (%rax)      ; C, D, E,  write the value to `static memory`
> 
> Then the following interleaving may happen:
> 1. Thread B reads the data, then switch to thread A. Thread A update the data and switching to B. Finally B updates the data. In this case, thread B will overwrite the data that thread A has updated to the `int x`, causing the result to be `5`.
> 2. Symmetric to 1, immediately after thread A reads the data, it switches to thread B. Then after thread B finishes, switches to thread A. Thread A will overwrite the modification done by thread B. Setting the result to `6`.
> 3. Thread A execute first `x*=2` and switch to thread B, thread B read the value of `x` and switch to thread A, thread A updates the value to `6` and switch to thread B, thread B then udpates the value to `10`.
> 4. Thread B executes after thread A finishes or vice versa, we get `30`.
> 5. `1` is not possible, because there has to be some modification to `x`.
> 6. `2` is not possible, because it is not the last line to execute in thread A. Since later lines will overwrite the result from previous line.
> 7. `150` is not possible since there are only two threads. The maximum value is `30`.



## Reordering of Instructions
### Buggy Codes
> [!important]
>   It’s even worse than that, in fact. The race condition on the bank account balance can be explained in terms of different interleavings of sequential operations on different processors. But in fact, when you’re using multiple variables and multiple processors, you can’t even count on changes to those variables appearing in the same order.
>   
>   Here’s an example. Note that it uses a loop that continuously checks for a concurrent condition; this is called [busy waiting](https://en.wikipedia.org/wiki/Busy_waiting) and it is not a good pattern. In this case, the code is also broken:
```java
private boolean ready = false;
private int answer = 0;

// computeAnswer runs in one thread
private void computeAnswer() {
    // ... calculate for a long time ...
    answer = 42;
    ready = true;
}

// useAnswer runs in a different thread
private void useAnswer() {
    // busy-wait for computeAnswer to say it's done
    while (!ready) {
        Thread.yield();
    }
    if (answer == 0) throw new RuntimeException("answer wasn't ready!");
}
```
> [!bug] Reordering Issue
> We have two methods that are being run in different threads. `computeAnswer` does a long calculation, finally coming up with the answer 42, which it puts in the `answer` variable. Then it sets the `ready` variable to true, in order to signal to the method running in the other thread, `useAnswer`, that the answer is ready for it to use. Looking at the code, `answer` is set before `ready` is set, so once `useAnswer` sees `ready` as true, then it seems reasonable that it can assume that the `answer` will be 42, right? Not so.
> 
> The problem is that modern compilers and processors do a lot of things to make the code fast. One of those things is making temporary copies of variables like `answer` and `ready` in faster storage (processor registers, or processor caches), and working with them temporarily before eventually storing them back to their official location in memory. The storeback may occur in a different order than the variables were manipulated in your code. Here’s what might be going on under the covers (but expressed in Java syntax to make it clear). The processor is effectively creating two temporary variables, `tmpr` and `tmpa`, to manipulate the fields `ready` and `answer`:
```java
private void computeAnswer() {
    // ... calculate for a long time ...

    boolean tmpr = ready;
    int tmpa = answer;

    tmpa = 42;
    tmpr = true;

	// This is where reordering could happen
	/* The code write answer = 42; ready = true 
		But the compiler would flip the ordering these two as follows
	*/
    ready = tmpr;
                   // <-- what happens if useAnswer() interleaves here?
                   // ready is set, but answer isn't.
    answer = tmpa;
}
```

### Reordering Example
> [!example]
> The code has a race condition that invalidates the invariant that only one simulator object is created.
> 
> Suppose two threads are running `getInstance()`. One thread is about to execute one of the numbered lines above; the other thread is about to execute the other. 
```java
public class PinballSimulator {

    private static PinballSimulator simulator = null;
    // invariant: there should never be more than one PinballSimulator
    //            object created

    public static PinballSimulator getInstance() {
1)      if (simulator == null) {
2)          simulator = new PinballSimulator();
        }
3)      return simulator;
    }

    ...
}
```
> [!quiz]
> **For each pair of possible line numbers, is it possible the invariant will be violated?**
> - **About to execute lines 1 and 3**, normally when line 3 is about to be executed, we must either comes from line 1 or line 2, which means we should have set up the simulator's value to be `new PinballSimulator()` or return the already created one. This means, `simulator != null` and line 1 won't get executed to create a second object. But due to instruction reordering, simulator may not get the value immediately upon request, but instead cached in a temporary registers or memory segment. In which case even if we have already created a new object, 1) still evaluates to true and 3) return null;
> - **About to execute lines 1 and 2**, definitely a violation, if line 1 goes first, then we will create two objects.
> - **About to execute lines 1 and 1**, definitely a violation, two thread execute line 1 at the same time, creating two objects.





## Appendix: the implementation of `oslock` and `osunlock`
> [!code]
```c++
/* ostreamlock.h */  
#include <ostream>  
​  
std::ostream& oslock(std::ostream& os);  
std::ostream& osunlock(std::ostream& os);

/* ostreamlock.cc */  
#include <ostream>  
#include <iostream>  
#include <mutex>  
#include <memory>  
#include <map>  
#include "ostreamlock.h"  
using namespace std;  
​  
static mutex mapLock;  
static map<ostream *, unique_ptr<mutex>> streamLocks;  
​  
ostream& oslock(ostream& os) {  
  ostream *ostreamToLock = &os;  
  if (ostreamToLock == &cerr) ostreamToLock = &cout;  
  mapLock.lock();  
  unique_ptr<mutex>& up = streamLocks[ostreamToLock];  
  if (up == nullptr) {  
    up.reset(new mutex);  
  }  
  mapLock.unlock();  
  up->lock();  
  return os;  
}  
​  
ostream& osunlock(ostream& os) {  
  ostream *ostreamToLock = &os;  
  if (ostreamToLock == &cerr) ostreamToLock = &cout;  
  mapLock.lock();  
  auto found = streamLocks.find(ostreamToLock);  
  mapLock.unlock();  
  if (found == streamLocks.end())  
    throw "unlock inserted into stream that has never been locked.";  
  unique_ptr<mutex>& up = found->second;  
  up->unlock();  
  return os;  
}
```



# Thread Safety
## What is Thread Safety?
> [!def]
> A data type or static method is ==_threadsafe_== if it behaves correctly when used from multiple threads, regardless of how those threads are executed, and without demanding additional coordination from the calling code.


## Achieving Thread Safety
### Strategy 1: Confinement
> [!important]
> Since shared mutable state is the root cause of a race condition, confinement solves it by _not sharing_ the mutable state.
> 
> **Local variables** are always thread confined. A local variable is stored in the stack, and each thread has its own stack. There may be multiple invocations of a method running at a time (in different threads or even at different levels of a single thread’s stack, if the method is recursive), but each of those invocations has its own private copy of the variable, so the variable itself is confined.
> 
> But be careful – the variable is thread confined, but if it’s an object reference(or a pointer address), you also need to check the object it points to. 
> - If the object is mutable, then we want to check that the object is confined as well – there can’t be references to it that are reachable from any other thread.
> 
> In the following code, `n`, `i` and `result` are thread safe since they are local variable on the stack.
```java
public class Factorial {

    /**
     * Computes n! and prints it on standard output.
     * @param n must be >= 0
     */
    private static void computeFact(final int n) {
        BigInteger result = BigInteger.valueOf(1);
        for (int i = 1; i <= n; ++i) {
            System.out.println("working on fact " + n);
            result = result.multiply(BigInteger.valueOf(i));
        }
        System.out.println("fact(" + n + ") = " + result);
    }

    public static void main(String[] args) {
        new Thread(new Runnable() { // create a thread using an
            public void run() {     // anonymous Runnable
                computeFact(99);
            }
        }).start();
        computeFact(100);
    }
}
```


#### Avoid global variables
> [!code]
>   If you have static variables in your program, then you have to make an argument that only one thread will ever use them, and you have to document that fact clearly. Better, you should eliminate the static variables entirely.
>   
>   Here’s an example that follows the [singleton design pattern](https://en.wikipedia.org/wiki/Singleton_pattern), which uses a private static variable:
```java
// This class has a race condition in it.
public class PinballSimulator {

    private static PinballSimulator simulator = null;
    // invariant: there should never be more than one PinballSimulator
    // object created

    private PinballSimulator() {
        System.out.println("created a PinballSimulator object");
    }

    // factory method that returns the sole PinballSimulator object,
    // creating it if it doesn't exist
    public static PinballSimulator getInstance() {
        if (simulator == null) {
            simulator = new PinballSimulator();
        }
        return simulator;
    }
}
```
> [!bug] Caveats
> This class has a race in the `getInstance()` method – two threads could call it at the same time and end up creating two copies of`PinballSimulator` object, which we don’t want.
> 
> To fix this race using the thread confinement approach, you would specify that only a certain thread (maybe the “pinball simulation thread”) is allowed to call `PinballSimulator.getInstance()`. The risk here is that Java won’t help you guarantee this.



#### Local Variables and Global Variables
> [!def]
> The following example shows that **local variables** that don't store reference/address is automatically confined to thread that is running the method call.
> 
> `static` variables in java (global variable in C++)  is not confined to thread.
```java
public class C {
    public static void main(String[] args) {
        new Thread(new Runnable() {
            public void run() {
                threadA();
            }
        }).start();

        new Thread(new Runnable() {
            public void run() {
                threadB();
            }
        }).start();
    }

	/* 
		Global variables, not confined to thread
	*/
    private static String name = "Napoleon Dynamite";
    private static int cashLeft = 150;

    private static void threadA() {
	    
        int amountA = 20; /* Confined to thread */
        cashLeft = spend(amountA);
    }

    private static void threadB() {
        int amountB = 30; /* Confined to thread */
        cashLeft = spend(amountB);
    }

    private static int spend(int amountToSpend) {
	    /* amounToSpend Confined to thread
		   in X86 calling convention, amountToSpend is 
		   either put in %edi register, or on the 
		   calling stack, which are all thread-independent.
		 */
        return cashLeft - amountToSpend;
    }
}
```



#### Instance Variable/Pointer
> [!example]
>   **Instance variables** are **not** automatically thread confined, even if they are declared `private`. If we want to argue that the `PinballSimulator` ADT is threadsafe, we cannot use confinement. We don’t know whether or how clients have created aliases to a `PinballSimulator` instance from multiple threads. If they have, then concurrent calls to methods of this class will make concurrent access to its fields and their values.
> 
```java
public class PinballSimulator {

    private final List<Ball> ballsInPlay;
    private final Flipper leftFlipper;
    private final Flipper rightFlipper;
    // ... other instance fields...

    // ... instance observer and mutator methods ...
}
```


### Confinement and Anonymous Class
> [!concept]
> Two concepts that are commonly encountered in java multithreading:
> 1. final variable
> 2. effectively final variable.
> 
> We will explain these two concepts in the following example:
```java
// Not thread safe
public class PinballSimulator {
    
    private int highScore; /* Instance variable, not thread confined */
    // ...
    
    public void simulate() {
	    /* Local variable of simulate(), not thread confined */
        int numberOfLives = 3; 
        
        new Thread(new Runnable() {
            public void run() {
                numberOfLives -= 1; // ERROR, local variable defined in an enclosing scope must be final or effectively final.
            }
        }).start();
    }
}

// Thread safe
public class PinballSimulator {
    
    private int highScore;
    // ...
    
    public void simulate() {
	    /* Local variable of simulate(), now thread confined */
        final int numberOfLives = 3; /* final*/
        
        new Thread(new Runnable() {
            public void run() {
                /* Only allowed to read */
                System.out.println(numberOfLives);
            }
        }).start();
    }
}



public class PinballSimulator {
    
    private int highScore;
    // ...
    
    public void simulate() {
	    /* Effectively final
		    Effectively final: Without final keyword, thread doesn't reassgin its value
	    */
        List<Ball> ballsInPlay = new ArrayList<>();
        
        new Thread(new Runnable() {
            public void run() {
	            /* ballsInPlay is mutable, but not reassignable
	             If we attempt to write:
	             ballsInPlay = new ArrayList<>(); Compiler error!
				 */
                ballsInPlay.add(new Ball());
            }
        }).start();
    }
}

```



### Strategy 2: Immutability
> [!important]
> So in order to be confident that an immutable data type is threadsafe without locks, we need a stronger definition of immutability. A type is ==_threadsafe immutable_== if it has:
> - No mutator methods
> - All fields declared `private` and `final`
> - No [Representation Exposure](../../../Software_Engineering/MIT_6031/Lecture_Notes/8_Abstract_Data_Type.md#Rep%20Exposure/Independence)
> - No mutation whatsoever of mutable objects in the rep – not even benefit mutation.





### Strategy 3: Using Threadsafe Data Types
> [!important]
> 



## Scheduler's role in thread (un)safety
### Unpredictability of Scheduler
> [!concept]
> - When a child thread calls `malloc()`, it draws memory from the heap segment as the master thread does. Note that two threads may both decide to call `malloc()` at the same time, hence the implementation of `malloc()` is transactional, i.e. if it fails halfway, all changes made by it will be rolled back.
> - Multiple threads may decide to print something to the console. To prevent garbled output in the console, there is an **exclusive lock** (typically implemented as a boolean) within the **file entry** instance in the system-wide file entry table, and if one thread has taken that lock, another thread cannot take it until the former thread finishes printing and release that lock on the file entry. C's `printf()` is thread-safe; that is, it grabs the exclusive lock on the output file entry before printing and release it after it's done. However, C++'s `ostream::operator<<()` is NOT thread-safe.
> - All threads can access the global variables in the data segment. Two threads may both want to alter a global variable's value, so the implementation of the thread routine has to guard against the conflict problem caused by the **unpredictability of the scheduler**. This responsibility falls upon the programmer's shoulder. An example of the conflict problem:
```
scenaio 1:      ┌────────┐┌────────┐                         ──▶ time     
                │write a:││read a, │                                     
     thread 1   │ a = 1  ││& print │                      => print 1  
                └────────┘└────────┘                                     
                                    ┌────────┐┌────────┐  
     thread 2                       │write a:││read a, │  => print 2  
                                    │ a = 2  ││& print │    
                                    └────────┘└────────┘              OK    
───────────────────────────────────────────────────────────────────────   
scenaio 2:      ┌────────┐          ┌────────┐                ERRONEOUS    
                │write a:│          │read a, │    
     thread 1   │ a = 1  │          │& print │            => print 2  
                └────────┘          └────────┘        
                          ┌────────┐          ┌────────┐                  
     thread 2             │write a:│          │read a, │  => print 2  
                          │ a = 2  │          │& print │                  
                          └────────┘          └────────┘                
```
> [!bug] CS186
> Two operations _conflict_ if they are part of different transactions, involve the same variable, and at least one of them is a write. There is a WW conflict between thread 1 & 2, and in scenario 2, that conflict caused a problem. The second scenario is a bad schedule.
> 
> See [CS186:Conflict Operations](../../Database%20Systems/4_Transaction&Concurrency/1_Transactions_Concurrency.md#Conflict%20Operations) for more information.



### An example of problematic multithreading
> [!code]
> Suppose there are 6 extroverts and 1 tag-along introvert in an array. The extroverts need to print their greetings but the introvert needs to remain silent.
```c
/* Problematic multithreading */  
#include ...  
​  
static const char *const names[] = {  
  "Albert Chon",         "John Carlo Buenaflor",  
  "Jessica Guo",         "Lucas Ege",  
  "Sona Allahverdiyeva", "Yun Zhang",  
  "Tagalong Introvert Jerry Cain"  
};  
​  
void *recharge(void *arg) {  
    printf("I'm %s. Empowered to meet you.\n",   
           names[*(size_t *)arg]); /* type cast, don't forget */  
    return NULL;  
}  
​  
int main() {  
    pthread_t extroverts[6];  
    for (size_t i = 0; i < 6; i++) {  
	    /* Here i is allocated on the stack of the current process 
		   Each thread holds a reference to the variable i
		   The conflict operation here is between the main thread's i++
		   and child threads' deference.
	    */
        pthread_create(&extroverts[i], NULL, recharge, &i);  
    }  
    for (size_t i = 0; i < 6; i++) {  
        pthread_join(extroverts[i], NULL);  
    }  
​  
    printf("Everyone's recharged!\n");  
    return 0;  
}
```
> [!exp]
> In this program, the array `names` has 7 pointers to C-strings, and the program should have print the first 6 strings one time each (though not necessarily in order). But the actual output is not deterministic: some strings get printed more than once, some strings is not printed, and sometimes the last string, which should not have been printed, gets printed:
```
$ ./confusing-extroverts  
I'm John Carlo Buenaflor.  Empowered to meet you.  
I'm Jessica Guo.  Empowered to meet you.  
I'm Sona Allahverdiyeva.  Empowered to meet you.  
I'm Sona Allahverdiyeva.  Empowered to meet you.  
I'm Yun Zhang.  Empowered to meet you.  
I'm Tagalong Introvert Jerry Cain.  Empowered to meet you.  
Everyone's recharged!  
​  
$ ./confused-extroverts   
I'm Sona Allahverdiyeva.  Empowered to meet you.  
I'm Tagalong Introvert Jerry Cain.  Empowered to meet you.  
I'm Tagalong Introvert Jerry Cain.  Empowered to meet you.  
I'm Tagalong Introvert Jerry Cain.  Empowered to meet you.  
I'm Tagalong Introvert Jerry Cain.  Empowered to meet you.  
I'm Tagalong Introvert Jerry Cain.  Empowered to meet you.  
Everyone's recharged!  
​  
$ ./confused-extroverts   
I'm Tagalong Introvert Jerry Cain.  Empowered to meet you.  
I'm Tagalong Introvert Jerry Cain.  Empowered to meet you.  
I'm Tagalong Introvert Jerry Cain.  Empowered to meet you.  
I'm Tagalong Introvert Jerry Cain.  Empowered to meet you.  
I'm Tagalong Introvert Jerry Cain.  Empowered to meet you.  
I'm Tagalong Introvert Jerry Cain.  Empowered to meet you.  
Everyone's recharged!
```
> [!bug] Bug: Race Conditions
> **The bug is:**
> - Note that recharge references its incoming parameter this time, and that `pthread_create()` accepts the location of the surrounding loop's index variable via its fourth argument. `pthread_create()`'s 4th argument it always passed verbatim as the single argument to the thread routine.
> - **The problem:** The master thread advances `i` **without regard for the fact that `i`'s address was shared with each of the child threads** in its own stack frame.
> - At first glance, it's easy to assume that `pthread_create()` captures not just the address of `i`, but the value of `i` itself. That assumption would be incorrect, as it copies the address and that's all.
> - The address of `i` (even after it goes out of scope) is constant, but its contents **evolve in parallel with the execution of the child threads**. When dereferencing, `*(size_t *)arg` takes a snapshot of whatever `i` just **happens to be** at the time it's evaluated.
> - This is a simple example of what's called a _race condition_.
> 
> **Q:** Can "Albert Chon" be printed more than once? 
> **A:** No. As the first string, "Albert Chon" can be printed either 0 or 1 time, but not more than that.
> 
> **Q:** How many times can the `k`-th string (`k` = 0, 1, ..., 6) be printed? 
> **A:** The `k`-th string can be printed 0 ~ (`k` + 1) times.
> 
> Illustration:
```
Scenario 1: OK                                   get 5  
                                         ch. 5 ○─●──────────...   t  
○ get &i                                  get 4                   o  
● dereference                   ch. 4  ○──●────────────────...  
                                  get 3                           b  
                       ch. 3  ○───●────────────────────...        e  
                          get 2                     
               ch. 2  ○───●────────────────────────...            j  
                 get 1                                            o  
      ch. 1  ○───●──────────────────────────────...               i  
        get 0                                                     n  
ch.0 ○──●─────────────────────────────────...                     e  
                                                                  d  
 ───●──────●───────●───────●───────●───────●──────●───────......─────────▶  
i = 0      1       2       3       4      5       6(break) master thread

Scenario 2: ERRONEOUS                           get 5  
                                        ch. 5 ○─●──────────...   t  
○ get &i                                 get 4                   o  
● dereference                  ch. 4  ○─●────────────────...  
                                          get 4                  b  
                      ch. 3  ○────────────●────────────...       e  
                                               get 5                     
               ch. 2  ○────────────────────────●───────...       j  
                get 1                                            o   
     ch. 1 ○───●──────────────────────────────...                i  
             get 1                                               n     
ch. 0 ○──────●──────────────────────────...                      e  
                                                                 d  
 ───●───●───────────●───────●───────●──────●──────●───────......────────▶  
i = 0   1           2       3       4      5      6(break) master thread

Scenario 3: ERRONEOUS                get 6  
                    ch. 5 ○──────────●───...                     t  
○ get &i                              get 6                      o  
● dereference  ch. 4  ○───────────────●────...  
                                         get 6                   b  
           ch. 3  ○──────────────────────●────...                e  
                              get 6      
       ch. 2  ○───────────────●──────...                         j  
                                                 get 6           o   
   ch. 1  ○──────────────────────────────────────●──...          i  
                                  get 6                          n   
ch. 0 ○───────────────────────────●──────...                     e  
                                                                 d  
 ───●───●───●───●───●───●───●─────────────────────......────────────────▶  
i = 0   1   2   3   4   5   6(break)                       master thread

```
> [!success] Fix 1
> To fix this, you can pass in the address to the C-strings themselves, instead of the address of the index `i`.
```c
/* Bug fixed */  
#include ...  
​  
static const char *const names[] = {  
  "Albert Chon",         "John Carlo Buenaflor",  
  "Jessica Guo",         "Lucas Ege",  
  "Sona Allahverdiyeva", "Yun Zhang",  
  "Tagalong Introvert Jerry Cain"  
};  
​  
void *recharge(void *arg) {  
    printf("I'm %s. Empowered to meet you.\n",   
           (const char *)arg); /* type cast, don't forget */  
    return NULL;  
}  
​  
int main() {  
    pthread_t extroverts[6];  
    for (size_t i = 0; i < 6; i++) {  
        pthread_create(&extroverts[i], NULL, recharge, (void *)names[i]);  
    }  
    for (size_t i = 0; i < 6; i++) {  
        pthread_join(extroverts[i], NULL);  
    }  
​  
    printf("Everyone's recharged!\n");  
    return 0;  
}
```
> [!success] Fix 2
> Putting `pthread_join()` in the same loop body as the `pthread_create()` also fixes this bug, but this approach essentially does not utilize the power of multithreading - it is just a sequential program in disguise.




# Concurrency Pattern









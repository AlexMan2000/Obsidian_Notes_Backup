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
void ticketAgent(size_t id) {  
    while (true) {  
        ticketLock.lock(); /* lock */  
        numTickets--;  
        cout << oslock   
             << "Ticket agent " << id << " sold one ticket,"  
             << " there are " << numTickets   
             << " more to sell!" << endl  
             << osunlock;  
        if (numTickets == 0) break;  
	    ticketLock.unlock(); /* unlock */  
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







# DeadLock - Dining Philosophy Problem
## Problem Descriptions
> [!motiv]
> `mutex` is not the panacea of all synchronization problems in multithreading. In fact, `mutex` can solve the problem of race conditions (as in 3.4), but not the one we are going to describe below.
> 
> In computer science, the [dining philosophers problem](https://en.wikipedia.org/wiki/Dining_philosophers_problem) is an example problem often used in concurrent algorithm design to illustrate synchronization issues and techniques for resolving them. It was originally formulated in 1965 by [Edsger Dijkstra](https://en.wikipedia.org/wiki/Edsger_W._Dijkstra) as an exam problem.
```
 .─.                THE SETUP:     
                   (   ) Plato            - A circular table,  
                    `─'                   - N philosophers (N >= 2),   
       ┌──────────────────────────┐       - N forks, each placed between  
       │  \       ┌────┐       /  │         two adjacent philosophers,  
       │   \      │bowl│      /   │       - M meals for each philosopher,  
       │          └────┘          │       - Each philosopher needs 2       
       │       ┌──────────┐       │           adjacent forks to eat  
 .─.   │┌────┐ │          │ ┌────┐│   .─.     spaghetti (yeah, weirdos),  
(   )  ││bowl│ │spaghetti │ │bowl││  (   )    otherwise he philosophizes.  
 `─'   │└────┘ │          │ └────┘│   `─'       
Hegel  │       └──────────┘       │ Descartes    
       │          ┌────┐          │              
       │   /      │bowl│      \   │     THE PROBLEM:    
       │  /       └────┘       \  │       How should each philosopher  
       └──────────────────────────┘       behave so no one starves    
                    .─.                   i.e. each one is able to  
 N = 4 here, but   (   ) Rousseau         eat M times?  
 We use N = 5 below `─'                                    
```
> [!note]
> Note that we will assume `N` = 5 and `M` = 3. That is, 5 philosophers, 5 forks, 3 meals for each. 




## Version 1: deadlock happens with nonzero probability
> [!bug]
> The most naïve approach is simply having N forks represented by N locks, and having each philosopher lock the fork before using and unlock it afterwards. There is no race for the fork here, since each fork has a lock on it, but there is another problem.
> 
> Let's look at the code first.
```c++
/* Verion 1: deadlock may happen */  
#include ...  
using namespace std;  
​  
static const unsigned int kNumPhilosophers = 5;  
static const unsigned int kNumForks = kNumPhilosophers;  

// Number of times a philosopher wants to eat
static const unsigned int kNumMeals = 3;  
​  
/* forks modeled as mutexes */  
static mutex forks[kNumForks];  
​  
static void think(unsigned int id) {  
  cout << oslock << id << " starts thinking." << endl << osunlock;  
  sleep_for(getThinkTime()/* random number, not important here */);  
  cout << oslock << id << " all done thinking. " << endl << osunlock;  
}  
​  
static void eat(unsigned int id) {  
  unsigned int left = id;  
  unsigned int right = (id + 1) % kNumForks;  
​  
  forks[left].lock();    /* lock, if already locked, then wait */ 
  // If sleepFor() is here, will increase the probability of deadlock
  forks[right].lock();   /* lock, if already locked, then wait */  
​  
  cout << oslock << id << " starts eating." << endl << osunlock;  
  sleep_for(getEatTime());  
  cout << oslock << id << " done eating." << endl << osunlock;  
​  
  forks[left].unlock();  /* unlock */  
  forks[right].unlock(); /* unlock */  
}  
​  
static void philosopher(unsigned int id) {  
  for (unsigned int i = 0; i < kNumMeals; i++) {  
    think(id);  
    eat(id);  
  }  
}  
​  
int main(int argc, const char *argv[]) {  
  thread philosophers[kNumPhilosophers];  
  for (unsigned int i = 0; i < kNumPhilosophers; i++)   
    philosophers[i] = thread(philosopher, i);  
  for (thread& p: philosophers)  
    p.join();  
​  
  return 0;  
}
```
> [!exp]
> **What's the problem?**
> - **Each** philosopher emerges from his deep thinking, successfully grabs the fork to his left, and then gets pulled off the processor because his time slice is over.
> - If this pathological scheduling pattern presents itself, eventually all each philosopher will be not able to grab the fork on his right, as that fork is already locked by the philosopher on his right.
> - That will leave the program in a state where all threads are entrenched in a state of deadlock, because each philosopher is stuck waiting for the philosopher on his right to let go of his fork.
> - **The probability of this happening increases when there is a sleep between locking the left fork and the right, as a thread switch will most likely happen during this sleep period.**
> 	- If we insert a `sleep` in between left lock and right lock, then very likely every one would hold the left fork before the first thread wakes up to try to pick up the right fork and find that someone else has picked up that lock already.
> 
> A _deadlock_ is a situation in which two or more competing actions are each waiting for the other to finish, and thus neither ever does. If a race condition happens, the program can still proceed (though potentially with erroneous results), but if a deadlock happens, the program falls into a never-ending wait, like an obscure while-true loop.
> 





## Version 2: permission slips, limit the number of bidding threads
> [!def]
> Deadlock can be programmatically prevented by implanting directives to limit the number of threads that try to participate in an action that could otherwise result in deadlock.
> - (1) We could, for instance, recognize that it's impossible for 3 or more philosophers to be eating at the same time, via a simple pigeonhole principle argument (e.g. 3 philosophers can be eating at the same time if and only if there are 6 forks, and there are not). We can, therefore, limit the number of philosophers grabbing forks to 2.
> 	- Multithreading purists may criticize that this approach, by limiting the number of participating threads from 5 to 2, sacrifices the power of multithreading too much.
> - (2) We can also argue that it's okay to let up to 4 (but not all 5) philosophers to transition into the `eat()` function of their think-eat cycle, knowing that at least one will succeed in grabbing both forks. That is, we allow up to 4 philosophers to take part in the bid for forks at the same time.
> 	- We will take this approach, as this approach downsize the number of threads that are allowed to grab fork from 5 to 4, not from 5 to 2, so it lets all threads to make as much progress as possible.
```c++
/* Version 2: no bug, but has busy-waiting */  
#include ...  
using namespace std;  
​  
static const unsigned int kNumPhilosophers = 5;  
static const unsigned int kNumForks = kNumPhilosophers;  
static const unsigned int kNumMeals = 3;  
​  
/* forks modeled as mutexes -- to solve the race condition */  
static mutex forks[kNumForks];   
​  
/* impose limit on # bidding threads -- to solve the deadlock */  
static unsigned int numAllowed = kNumPhilosophers - 1;  
/* the lock partnered with numAllowed */
static mutex numAllowedLock;  
​  
static void think(unsigned int id) {  
  /* same as in version 1 */  
}  
​  
/* wait to get a permission slip to participate in the bid for forks */  
static void waitForPermission() {  
  while (true) {  
    numAllowedLock.lock();  
    if (numAllowed > 0) break;  
    numAllowedLock.unlock();  
    sleep_for(10);  
  }  
  numAllowed--;  
  numAllowedLock.unlock();  
}  
​  
/* give back the permission slip to the pool so others can participate */  
static void grantPermission() {  
  numAllowedLock.lock();  
  numAllowed++;  
  numAllowedLock.unlock();  
}  
​  
static void eat(unsigned int id) {  
  unsigned int left = id;  
  unsigned int right = (id + 1) % kNumForks;  
​  
  waitForPermission(); /* wait for permission until get one */  
​  
  forks[left].lock();  /* may wait here */  
  forks[right].lock(); /* may wait here */  
​  
  cout << oslock << id << " starts eating." << endl << osunlock;  
  sleep_for(getEatTime());  
  cout << oslock << id << " all done eating." << endl << osunlock;  
​  
  grantPermission(); /* give back the permission to the pool */  
​  
  forks[left].unlock();  
  forks[right].unlock();  
}  
​  
static void philosopher(unsigned int id) {  
  /* same as in version 1 */  
}  
​  
int main(int argc, const char *argv[]) {  
  /* same as in version 1 */  
}   
```
> [!exp]
> It solves the problem of deadlock. It does, however, have one design flaw: the solution uses busy waiting in `waitForPermission()`, which is usually a big no-no. In this function:
> - The philosopher thread continually poll the value of `numAllowed` until the value is positive. At that point, decrement it to emulate the consumption of a shared resource — in this case, a permission slip allowing a philosopher to start trying to grab forks.
> - Since there are multiple threads potentially examining and decrementing `numAllowed`, identify the critical region as one that needs to be guarded by a `mutex`. And if the philosopher notices the value of `numAllowed` is 0 (i.e. all permissions slips are out), then release the lock and yield the processor to some other philosopher thread who can actually do some useful work.
> - The above solution uses _busy waiting_, which is a concurrency jargon used when a thread periodically checks to see whether some condition has changed so it can move on to do more meaningful work.
> - The problem with busy waiting, in most situations, is that the busy-waiting thread **occupies the CPU during its time windows, wasting the CPU time**, which would be better spent to ensure other threads — who presumably have meaningful work — to proceed.
> - **A better solution:** if a philosopher doesn't have permission to advance (i.e. `numAllowed` is confirmed to be zero), then that thread should be **put to sleep indefinitely** until some other thread sees a reason to **wake it up**. In this example, another philosopher thread, after it increments `numAllowed` within `grantPermission()`, could notify the indefinitely blocked thread that some permissions slips are now available.



# Condition Variable
## Version 3: Improve the solution - no busy waiting
> [!def]
> We can get rid of the busy-waiting situation by putting the thread into **sleep** and having another thread **wake it up** when some condition is met.
> 
> Implementing this idea requires a more sophisticated concurrency directive that supports a different form of thread communication. Fortunately, C++11 provides a standard, albeit difficult-to-understand, class called the `condition_variable_any`.
```c++
/* Version 3: no bug, no busy-waiting */  
#include ...  
using namespace std;  
​  
static const unsigned int kNumPhilosophers = 5;  
static const unsigned int kNumForks = kNumPhilosophers;  
static const unsigned int kNumMeals = 3;  
​  
/* forks modeled as mutexes -- to solve the race condition */  
static mutex forks[kNumForks];  
​  
/* impose limit on # bidding threads -- to solve the deadlock */  
static unsigned int numAllowed = kNumPhilosophers - 1;  
/* the lock meant to protect numAllowed against ++, -- */  
static mutex numAllowedLock;  
​  
/* to solve the busy-wait introduced in 3.5.2 */  
static condition_variable_any cv;  
​  
static void think(unsigned int id) {  
  /* same as in 3.5.1 */  
}  
​  
/* wait to get a permission slip to participate in the bid for forks */  
static void waitForPermission() {  
  lock_guard<mutex> lg(numAllowedLock);  
​  
  /* test: if condition is met: proceed  
           otherwise: release lock, sleep & wait  
     notified: re-acquire lock, re-test  
   */  
  cv.wait(numAllowedLock, []{ return numAllowed > 0; });  
​  
  numAllowed--;  
}  
​  
/* give back the permission slip to the pool so others can participate */  
static void grantPermission() {  
  lock_guard<mutex> lg(numAllowedLock);  
  numAllowed++;  
  if (numAllowed == 1) { /* if numAllowed goes from 0 to 1 */  
      /* notify cv to re-test the sleeping threads' condition */  
      cv.notify_all();  
  }  
}  
​  
static void eat(unsigned int id) {  
  /* same as in 3.5.2 */  
}  
​  
static void philosopher(unsigned int id) {  
  /* same as in 3.5.1 and 3.5.2 */  
  /* 1. wait for permission until get one,  
     2. lock both forks (may wait here),  
     3. enjoy the spaghetti,  
     4. give back the permission to the pool,  
     5. unlock both forks */  
}  
​  
int main(int argc, const char *argv[]) {  
  /* same as in 3.5.1 and 3.5.2 */  
} 
```
> [!exp]
> - The `condition_variable_any` (abbreviated as "cva" below) is the core concurrency directive that can preempt and block a thread until some condition is met.
> - In this example, the philosopher seeking permission to eat waits indefinitely until some condition is met (unless the condition is met already, in which case it doesn't need to wait), by calling `cva::wait()`.
> - If `numAllowed` is positive at the moment wait is called, then it returns immediately without blocking.
> - If `numAllowed` is zero at the moment `cva::wait()` is called, then the calling thread is **pulled off the CPU, marked as blocked** until the thread manager is informed (by another thread) that the value of `numAllowed` has changed.
> - In this example, the philosopher just finishing up a meal increments `numAllowed`, and if the value of `numAllowed` goes from 0 to 1, the same philosopher signals (via `cva::notify_all()`) all threads blocked by `cva` that a meaningful update has occurred. That prompts the thread manager to reexamine the condition on behalf of all threads blocked by `cva::wait()`, and potentially allow one or more of them to emerge from their long nap and move on to the work they weren't allowed to move on to before.
> - Because `numAllowed` is being examined and potentially changed concurrently by many threads, and because a condition framed in terms of it (that is, `numAllowed > 0`) influences whether a thread blocks or continues uninterrupted, we still need a traditional `mutex` here so that competing threads can lock down **exclusive access** to `numAllowed`.
> - Before `cva::wait()` is called, the the supplied `mutex` lock should have been lock already. If `cva::wait()` notices that the supplied condition isn't met, the `cva` object puts the current thread to **sleep** indefinitely and **automatically release**s the lock. When the `cva` object is notified and a waiting thread is switched back on CPU, it **automatically re-acquire**s the `mutex` lock which it released just prior to sleeping, and **re-evaluate the condition** for that thread. If the condition is met, then the thread proceeds to the following lines; otherwise, it automatically releases the lock again and put the thread back in sleep, and then waits for another notification.
> - This is KOB.
```First call (lock should be locked already)  
          │  
          ▼          ┌───────────────┐  
          ├◀─success─┤re-acquire lock◀────┐  sleep: blocked (off CPU)  
          │          └──┬───────▲────┘    │         & wait for an event  
 ┌────────▼───────┐    fail    lock       │         of interest  
 │   condition?   │     │    available    │  
 └────────┬───────┘   ┌─▼───────┴─┐       │  
          ├──false──┐ │   sleep   │       │  
          │         │ └───────────┘       │  
          │  ┌──────▼─────┐               │  
        true │release lock│               │  
          │  └──────┬─────┘         notification <= notify_all()  
          │  ┌──────▼─────┐               │  
          │  │   sleep    │───────────────┘  
          │  └────────────┘  
┌─────────▼─────────┐  
│ continue to hold  │  
│  lock & proceed   │     FLOWCHART:  
└─────────┬─────────┘     void wait(Lock &lock, Predicate condition);   
          ▼                                     
```


## Condition Variable Any Class


`codition_variable_any` class in summary:
```c++
/* constructor */  
    condition_variable_any();  
    ​  
    /* wait: blocks the current thread   
       until the condition variable is woken up */  
    template<typename Lock, typename Predicate>   
    void wait(Lock &lock, Predicate condition);  
    ​  
    /* notify all threads blocked by cva */  
    void notify_all();  
    ​  
    /* other methods... */
```
> [!exp]
> - Predicate: a function that returns a boolean. You can pass in a function pointer to a predicate, or pass in a [lambda expression](https://msdn.microsoft.com/en-us/library/dd293608.aspx) that is a predicate. If the predicate returns `false`, then `cva::wait()` puts the calling thread into sleep. You should avoid using the one-argument version of `wait()`, which takes the lock as the only argument, because this version of `wait()` sometimes returns without being notified - "[spurious wake](https://www.justsoftwaresolutions.co.uk/threading/condition-variable-spurious-wakes.html)"
> - The `lock_guard` class exists to **automate the locking and unlocking of a** `mutex`.
> - The `lock_guard()` constructor binds an internal reference to the supplied `mutex` object and calls `lock()` on it (if the `mutex` lock is already locked by another thread, the constructor is blocked inside, until the lock is released).
> - The `~lock_guard()` destructor releases the lock on the same `mutex` object.
> - The overall effect: the code section from the constructor being called to the destructor being called (often implicitly at function return or exception throwing) is marked as a `mutex`-protected critical region.
```c++
{                              {  
      ...                        ...  
      m.lock();                  lock_guard<mutex> lg(m); /* lock m */  
      do_something();   <=>      do_something();  
      m.unlock();              } /* the destructor unlocks m */  
      }    
```
> [!exp]
> SIDE NOTE: Java: `lock_guard` is C++ STL's answer to Java keyword `synchronized`.
> SIDE NOTE: The `lock_guard` is a template class, because other than `mutex` class, some other classes like `recursive_mutex` and `timed_mutex` have such `lock()` and `unlock()` methods, too.
> 
> Its prototype is
```c++
/* template declaration */  
    template<typename BasicLockable> lass lock_guard;  
    ​  
    /* constructor (the basic one) */  
    explicit lock_guard(BasicLockable &m);  
    ​  
    /* destructor */  
    ~lock_guard();
```
> [!exp]
> A pedendic note: to let the other threads to proceed as much as they can, in the eat() function, you can place grantPermission(); immediately after successfully locking the left and right forks, since now that the thread succeeded in locking the two forks already, there is no reason to continue to hold the permission slip - it can give the slip back to the pool, knowing that another thread may grab the slip and try to lock forks.
> 
> Placing `grantPermission();` after unlocking the forks is acceptable as well, but it has the opposite effect - it further delays the progress of other threads.
> 
> Another pedendic note: the global variable `numAllowed`, i.e. the number of available permission slips, keeps track of the bidding situation of a resource that is at premium - like the forks, which is fewer than the dining philosopher threads, or network connections, or database access, ...


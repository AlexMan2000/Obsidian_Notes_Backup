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




## Version 1: Problem Diagnostics
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





## Version 2: Semaphore Ideas
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
/* P() operation in semaphore */
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
/* V() operation in semaphore */
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
/* to solve the busy-wait introduced in Version 2 */  
static condition_variable_any cv;  
​  
static void think(unsigned int id) {  
  /* same as in Version 1 */  
}  
​  
/* wait to get a permission slip to participate in the bid for forks */  
static void waitForPermission() {
  // This line of code is equivalent to explcitly calling the lock/unlock pair like the following:
  /*
	numAllowedLock.lock();
	...
	numAllowedLock.unlock();


	lock_guard<> template class has 
	- A constructor that calls numAllowedLock.lock() 
	- A destructor that calls numAllowedLock.unlock()
  */
  lock_guard<mutex> lg(numAllowedLock);  
​  
  /* test: if condition is met: proceed  
           otherwise: release lock, sleep & wait  
     notified: re-acquire lock, re-test  
   */  
  cv.wait(numAllowedLock, []{ return numAllowed > 0; });  
​  
  numAllowed--;  

  // When the object lg goes out of scope, the destructor is called so that the lock on numAllowedLock is freed.
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
  /* same as in Version 2 */  
}  
​  
static void philosopher(unsigned int id) {  
  /* same as in Version 1 and Version 2 */  
  /* 1. wait for permission until get one,  
     2. lock both forks (may wait here),  
     3. enjoy the spaghetti,  
     4. give back the permission to the pool,  
     5. unlock both forks */  
}  
​  
int main(int argc, const char *argv[]) {  
  /* same as in Version 1 and Version 2 */  
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
          ▼           ┌───────────────┐  
          ├◀─success─┤re-acquire lock◀────┐  sleep: blocked (off CPU)  
          │            └──┬───────▲────┘  │         & wait for an event  
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


### Condition Variable Any Class
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



# Producer-Consumer Problem
## Problem Descriptions
> [!def]
> ![](Thread_Synchonization.assets/image-20240404161709132.png)
> **Details:**
> - A producer and consumer thread share a bounded buffer with n slots. 
> - The producer thread repeatedly produces new items and inserts them in the buffer. 
> - The consumer thread repeatedly removes items from the buffer and then consumes (uses) them. 
> - Variants with multiple producers and consumers are also possible.
> - Since inserting and removing items involves updating shared variables, we must guarantee mutually exclusive access to the buffer. **But guaranteeing mutual exclusion is not sufficient. We also need to schedule accesses to the buffer.** 
> - If the buffer is full (there are no empty slots), then the producer must wait until a slot becomes available. Similarly, if the buffer is empty (there are no available items), then the consumer must wait until an item becomes available.
> 
> ![](Thread_Synchonization.assets/image-20240404161806177.png)![](Thread_Synchonization.assets/image-20240404161912320.png)



## Solution 1 - Circular Buffer Data Structure
### Data Structure Definition
> [!def]
> ![](Thread_Synchonization.assets/image-20240407104413505.png)
> Here if `r` catches up with `w` then the queue is empty and vise versa.
> 
> ![](Thread_Synchonization.assets/image-20240407104510152.png)
> Here busy-waiting while loop is wasting CPU resources. Chances are that  `Producer` threads always successfully get the CPU schduling and `Consumer` threads cannot `dequeue()` so that `Producer` is indefinitely spinning and waiting.


### How to use Semapores
> [!important]
> ![](Thread_Synchonization.assets/image-20240407110300903.png)


### Coke Machine
> [!example]
> ![](Thread_Synchonization.assets/image-20240407110324796.png)

> [!bug] Caveats: Order of Semaphores
> ![](Thread_Synchonization.assets/image-20240407110752889.png)
> Here if `Producer` first acquire the mutex and find that `emptySlots = 0` so that it blocks and waits for `Consumer` to increment the `emptySlots`. Meanwhile, since `fullSlots = bufSize`, the `Consumer` acquire the `fullSlots` and then try to grab the mutex but is blocked and waiting for `Producer`.
> 
> So here there is a **deadlock situation.**




## Solution 2 - Semaphores(SBuf)
> [!example]
> This is an encapsulated version of solution 1, the idea is similar.
> ![](Thread_Synchonization.assets/image-20240404161854345.png)



## Solution 3 - Condition Variables
> [!example]
> ![](Thread_Synchonization.assets/image-20240416194450619.png)
> **Several things to note:**
> - `cond_wait(&buf_CV, &buf_lock)` will release the lock when called and will re-acquire the lock before returns.
> - The reason why we need a while loop in the consumer is that 
> 	- During the time a thread is sleeping and woken up by `cond_signal`, the queue maybe modified by other threads, so we need to loop checking the queue to see whether there is things to be consumed.
> 	- Between `cond_signal()`'s attempt to wake up any of the waiting thread and the notified thread re-acquire the lock, there may be other threads that will modified the queue(for example the producer) and release the lock, so an `if` is not enough, causing a spurious wakeup.
> 		- With the perspective of producer thread, I wake up a particular thread by `cond_signal`, hoping that it can consume what I have produced.
> 		- In the perspective of the notified consumer, I was woken up hoping that there is something new in the queue to be consumed, but due to some race condition, there is nothing in the queue, so I am falsely alarmed. (Spurious Wakeup)
> 
> ![](Thread_Synchonization.assets/image-20240416203300847.png)







# Readers and Writers Problem
## Problem Descriptions
> [!def]
> ![](Thread_Synchonization.assets/image-20240404165111345.png)![](Thread_Synchonization.assets/image-20240404165039551.png)![](Thread_Synchonization.assets/image-20240404165049529.png)![](Thread_Synchonization.assets/image-20240404165126740.png)![](Thread_Synchonization.assets/image-20240416205032429.png)


## Solution 1 - Semaphores(读优先)
> [!code]
> ![](Thread_Synchonization.assets/image-20240404164931856.png)
> The w semaphore controls access to the critical sections that access the shared object. The mutex semaphore protects access to the shared readcnt variable, which counts the number of readers currently in the critical section. 
> 
> A writer locks the w mutex each time it enters the critical section and unlocks it each time it leaves. 
> 
> This guarantees that there is at most one writer in the critical section at any point in time. On the other hand, only the first reader to enter the critical section locks w, and only the last reader to leave the critical section unlocks it. The w mutex is ignored by readers who enter and leave while other readers are present. This means that as long as a single reader holds the w mutex, an unbounded number of readers can enter the critical section unimpeded. 
> 
> A correct solution to either of the readers-writers problems can result in starvation, where a thread blocks indefinitely and fails to make progress. For example, in the solution in Figure 12.26, a writer could wait indefinitely while a stream of readers arrived.


## Solution 2 - Monitors(写优先)
> [!important]
> Here we favor writers over readers so readers have to wait for all the waiting writers.
> ![](Thread_Synchonization.assets/image-20240416203952688.png)![](Thread_Synchonization.assets/image-20240416203958856.png)
> The reason why we need to release the lock before `AccessDatabase` is that we just want to check **whether we have the access** to the database and we don't want to lock the database at all. Since the checking logic involves modification to the shared variables, like AW, WW, we need to grab the lock before and release it after.
> 	
> ![](Thread_Synchonization.assets/image-20240416204004771.png)
> **Why we need to prioritize the writer?**
> - Writers update the database far less often than readers read the database.
> - Readers always want to read the most updated value in the database, so it's better for writer to finish updating before reader can read the data.
> - It is a design choice.




## Solution 3 - Single CV(写优先)
> [!example]
> ![](Thread_Synchonization.assets/image-20240417110210558.png)![](Thread_Synchonization.assets/image-20240417110218133.png)








# Concurrent Servers
## Iterative Server
> [!def]
> This kind of server can only handle connection one at a time. 
> ![](Concurrent_Programming.assets/image-20240404135109456.png)![](Concurrent_Programming.assets/image-20240404135120337.png)![](Concurrent_Programming.assets/image-20240404135127398.png)




## Concurrent Server
> [!def]
> ![](Concurrent_Programming.assets/image-20240404135305462.png)



## Process-Based Servers
### Diagram
> [!def]
> ![](Concurrent_Programming.assets/image-20240404135331602.png)![](Concurrent_Programming.assets/image-20240404135633657.png)



### Code Implementations
> [!important]
> ![](Concurrent_Programming.assets/image-20240404134700524.png)![](Concurrent_Programming.assets/image-20240404135600826.png)



### Pros and Cons
> [!bug] Caveats
> ![](Concurrent_Programming.assets/image-20240404135923356.png)![](Concurrent_Programming.assets/image-20240404135747085.png)




## Event-based Servers
### Definition
> [!def]
> ![](Concurrent_Programming.assets/image-20240404135956939.png)



### Select Function
> [!important]
> `select(cardinality, &fd_set, NULL, NULL, NULL)` is the key to the I/O multiplexing of the server without the use of multi processes.
> ![](Concurrent_Programming.assets/image-20240404140424781.png)
> How to use `select()`:
> 1. Declare `fd_set read_set, ready_set`, this will allocate some memory on the stack.  
> 	1. `ready_set` will be used by `select` function to detect which file descriptor is ready to read and write. It will be modified by `select` function. 
> 	2. `read_set` is used as a reference and should not be changed once set.
> 2. Use `FD_ZERO(&read_set)` macro to set `read_set` bits to be all 0's. 
> 3. Use `FD_SET(STDIN_FILENO, &read_set)`, similar to `sigaddset()` will add stdin file descriptor to the bit mask, making the file descriptor 0 from 0 to 1.
> 4. Use `FD_SET(listenfd, &read_set)`. listenfd is opened to be file desciptor 3 of the main process of the server.
> 
> **Before:**
> ![](Concurrent_Programming.assets/image-20240404143953185.png)
> 
> **After:**
> ![](Concurrent_Programming.assets/image-20240404144003824.png)







### I/O Multiplexing
> [!def]
> ![](Concurrent_Programming.assets/image-20240404140201411.png)




### Code Implementations
> [!important]
> ![](Concurrent_Programming.assets/image-20240404140408424.png)



### Pros and Cons
> [!bug] Caveats
> ![](Concurrent_Programming.assets/image-20240404144059489.png)



## Thread-based Servers
### Definition
> [!def]
> ![](Concurrent_Programming.assets/image-20240404144158392.png)![](Concurrent_Programming.assets/image-20240404144417101.png)






### Two Views of Processes in Servers
> [!important]
> ![](Concurrent_Programming.assets/image-20240404144221665.png)![](Concurrent_Programming.assets/image-20240404144227102.png)



### Threads and Processes
> [!important]
> More on [1_Threads_and_Processes](../2_Abstractions/1_Threads_and_Processes.md)
> ![](Concurrent_Programming.assets/image-20240404144303610.png)


### Code Implementations
> [!important]
> ![](Concurrent_Programming.assets/image-20240404144358876.png)
> **Design questions to consider:**
> 1. Why we use `malloc` at all? Prevent Race Conditions!
> 2. Why detaching peer threads?
> 
> To address first question, we must look closely at `pthread_create` function.
> ![](Concurrent_Programming.assets/image-20240404151520050.png)![](Concurrent_Programming.assets/image-20240404151527204.png)
> **Important:**
> - Calling `pthread_join()` on a joinable thread will automatically release all the resources associated with that thread. 
> - When a thread is created with `pthread_create()`, it remains in a joinable state by default. **A joinable thread retains certain resources (such as its stack and thread control block) after it has finished executing, until another thread calls `pthread_join()` to clean up these resources.** If `pthread_join()` is never called, these resources are not released, leading to a resource leak.
> - By detaching a thread using `pthread_detach()`, you inform the system that the thread's resources can be reclaimed immediately when the thread terminates, without waiting for another thread to join it.





 
### Pros and Cons
> [!bug] Caveats
> ![](Concurrent_Programming.assets/image-20240404144444784.png)







# Queues_Message_Passing


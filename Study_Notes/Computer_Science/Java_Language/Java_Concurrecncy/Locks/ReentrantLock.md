# 可打断
> [!important]
> 可用于防止死锁。
> 1. 线程1先获取锁，线程2尝试获取锁失败，从`RUNNABLE -> WAITING`。线程1调用`t1.interrupt()`将线程2从阻塞队列中移除不让其竞争锁。
```java
package cn.itcast.multiple_locks;  
import lombok.extern.slf4j.Slf4j;  
import java.util.concurrent.locks.ReentrantLock;  
  
@Slf4j(topic = "c.test1")  
public class test1 {  
  
    public static ReentrantLock lock = new ReentrantLock();  
    public static void main(String[] args) throws InterruptedException {  
        Thread t1 = new Thread(() -> {  
            try{  
                log.debug("t1 try to acquire the lock");  
                lock.lockInterruptibly();  
            } catch (InterruptedException e) {  
                log.debug("Interrupted by other threads, failed to acquire the lock");  
                // 不能在这里调用lock.unlock(), 因为连锁都没有拿到。
                return;  
            }            


            try {  
                log.debug("Successfully acquire the lock!");  
            } finally {  
                lock.unlock();  
            }        
            }, "t1");  
  
        lock.lock();  
        t1.start();  
        Thread.sleep(1000);  
  
        log.debug("Main Thread interrupted t1");  
        t1.interrupt();  
    }}
```





# 锁超时
> [!important]
> 
```java
package cn.itcast.multiple_locks;

import lombok.extern.slf4j.Slf4j;

import java.util.concurrent.TimeUnit;
import java.util.concurrent.locks.ReentrantLock;

@Slf4j(topic = "c.test2")
public class test2 {

    public static ReentrantLock lock = new ReentrantLock();
    public static void main(String[] args) throws InterruptedException {
        Thread t1 = new Thread(() -> {
            // 如果没有获取到锁, 等待一定时间之后返回false，不再等待，不再参与锁竞争。
            // 如果在等待时间内，主线程释放了锁，那么tryLock()就会马上返回true, 即便等待时间还没有结束。
            try {
                if (!lock.tryLock(3, TimeUnit.SECONDS)) {
                    log.debug("Failed to acquire the lock!");
                    return;
                }
            } catch(InterruptedException e) {
                // tryLock() 也支持可打断的特性。
                e.printStackTrace();
                log.debug("Thread is interrupted from the blocking queue");
                return;
            }
            // 获取到了锁
            try {
                log.debug("Acquired the lock, Logic Execution Flow.");
            } finally {
                lock.unlock();
            }
        }, "t1");

        lock.lock();
        log.debug("Main thread acquired the lock!");
        t1.start();
		// 主线程等待2秒之后释放锁。
        Thread.sleep(2000);

        log.debug("Main thread released the lock!");
        lock.unlock();
    }
}
```



# 条件变量
## 同步模式之顺序控制
### 顺序打印1~10 - await()/signal()
> [!important]
> 假设我需要用10个线程顺序打印`1~10`, 我们可以使用条件变量实现同步控制:
```java
package cn.itcast.self_test;

import lombok.extern.slf4j.Slf4j;
import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.ReentrantLock;

@Slf4j(topic="c.Thread_Sequence")
public class Thread_Sequence {


	// 按顺序打印1 ~ 10
    public static void sychronized_print() {
        Synchronized_Print sp = new Synchronized_Print();
        Thread[] threads = new Thread[10];
        for (int i = 0; i < threads.length; i++) {
            threads[i] =  new Thread(new Sychronized_Print_Runnable(i + 1, sp), "Thread" + i);
        }

        for (int i = 0; i < threads.length; i++) {
            threads[i].start();
        }
    }

    public static void randomized_print() {
        Thread[] threads = new Thread[10];
        for (int i = 0; i < threads.length; i++) {
            int finalJ = i;
            threads[i] =  new Thread(()->{
                System.out.println(finalJ);
            }, "Thread" + (i + 1));
        }

        for (int i = 0; i < threads.length; i++) {
            threads[i].start();
        }
    }

    public static void main(String[] args) {
        sychronized_print();
    }
}

// 对线程传参的方法之一，可以继承一个Runnable类
class Sychronized_Print_Runnable implements Runnable {

    public int num_to_print;
    public Synchronized_Print sp;


    public Sychronized_Print_Runnable(int num_to_print, Synchronized_Print sp) {
        this.num_to_print = num_to_print;
        this.sp = sp;
    }

    @Override
    public void run() {
        sp.print(num_to_print);
    }
}

@Slf4j(topic = "c.Synchronized_Print")
class Synchronized_Print {

    public int numberCounter = 1;
    public ReentrantLock lock = new ReentrantLock();
    public Condition waitingForNext = lock.newCondition();

    public void print(int i) {
        lock.lock();
        try {
            while (i > numberCounter) {
                waitingForNext.await();
            }
            numberCounter++;
            log.debug(String.valueOf(i));
            // waitingForNext.signal() 会有死锁问题, 要注意。
            /**
             死锁产生的原因，假设线程1先抢到锁，然后numberCounter++, 并释放锁。然后线程3抢到了锁，但是条件不满足，于是去waitset中等待，并释放锁，然后线程4, 5, 6, 7, 8, 9, 10均在线程2之前抢到了锁，因为条件不满足于是都去waitset中等待了。最后线程2才抢到了锁，然后numberCounter++, 释放锁，叫醒了线程4，然后线程4没法执行，去waitset并释放锁。但此时blockingSet中已经没有线程等待锁被释放了，也就是说没有线程会去执行signal()方法了，也就是说waitSet中的线程永远不会被唤醒了，也就是死锁问题。
             
         signalAll() 方法保证了所有线程最终都一定会抢到锁并执行numberCounter++。
            */
            waitingForNext.signalAll();
        } catch (InterruptedException e) {
            e.printStackTrace();
            throw new RuntimeException(e);
        } finally {
            lock.unlock();
        }
    }
}
```



### 顺序打印1~10 - park()/unpark()
> [!important]
> 思路如下: 所有线程都`park()`住，然后从`Thread 1` 开始，`Thread i`执行代码并`unpark(i+1)`即可。
```java
package cn.itcast.self_test;

import lombok.extern.slf4j.Slf4j;

import java.util.concurrent.locks.LockSupport;


@Slf4j(topic = "c.Thread_Sequence_Park_Unpark")
public class Thread_Sequence_Park_Unpark {
    public static void main(String[] args) {

        Thread[] threads = new Thread[10];
        for (int i = 0; i < threads.length; i++) {
            final int index = i;
            threads[i] = new Thread(() -> {
                LockSupport.park();
                log.debug(String.valueOf(index + 1));
                if (index + 1 < threads.length) {
                    LockSupport.unpark(threads[index + 1]);
                }
            }, "Thread" + (i + 1));
        }

        for (Thread thread: threads) {
            thread.start();
        }

        LockSupport.unpark(threads[0]);
    }
}
```




## 同步模式之交替输出
> [!important]
> 要求: 三个线程，线程1只负责打印a，线程2只负责打印b，线程3只负责打印c. 要求交替输出abcabcabcabcabc. (5 次 abc)



### 思路1 - cv.wait()/signal()
> [!algo]
> 使用Condition Variable, 维护一个状态和三个条件变量:
> 1. 状态有三种，`a` 和 `b` 和`c`, 如果当前状态为`a`, 则线程1可以打印，线程`b` 和`c` 需要进入各自的休息室。
> 2. 条件变量有三个: `CVA`, `CVB`, `CVC`
> 	1. `CVA` 表示当前状态不是`a`, 需要等待状态变为`a` 的休息室，线程1专属。
> 	2. `CVB` 表示当前状态不是`b`, 需要等待状态变为`b` 的休息室，线程2专属。
> 	3. `CVC` 表示当前状态不是`c`, 需要等待状态变为`c` 的休息室，线程3专属。
> 这种写法不需要使用`signalAll()`也能避免死锁，因为我在`signal()`的时候相当于只通知了下一个可以打印的线程，不存在思路2中的虚假唤醒现象。
```java
package cn.itcast.self_test;


import lombok.extern.slf4j.Slf4j;

import java.util.HashMap;
import java.util.Map;
import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.ReentrantLock;

@Slf4j(topic="c.Interleaving_Print")
public class Interleaving_Print {
    public static void main(String[] args) {

        Sync_Print sp = new Sync_Print("a");

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 5; i++) {
                sp.print("a");
            }
        },"t1");
        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 5; i++) {
                sp.print("b");
            }
        },"t2");
        Thread t3 = new Thread(() -> {
            for (int i = 0; i < 5; i++) {
                sp.print("c");
            }
        },"t3");

        t1.start();
        t2.start();
        t3.start();
    }
}


@Slf4j(topic="c.Sync_Print")
class Sync_Print {

    public String currentState;

    public ReentrantLock lockman = new ReentrantLock();

    public Condition ca = lockman.newCondition();
    public Condition cb = lockman.newCondition();
    public Condition cc = lockman.newCondition();


    public Map<String, Condition> conditionMap = new HashMap<>();

    public Sync_Print(String currentState) {
        this.currentState = currentState;
        initMap();
    }

    public void initMap() {
        this.conditionMap.put("a", ca);
        this.conditionMap.put("b", cb);
        this.conditionMap.put("c", cc);
    }

    public void print(String output) {
        lockman.lock();
        // Critical Section
        try {
            while (!currentState.equals(output)) {
                try {
                    this.conditionMap.get(output).await();
                } catch (InterruptedException e) {
                    throw new RuntimeException(e);
                }
            }

            log.debug(output);
            switch(currentState) {
                case "a":
                    currentState = "b";
                    this.conditionMap.get("b").signal();
                    break;
                case "b":
                    currentState = "c";
                    this.conditionMap.get("c").signal();
                    break;
                case "c":
                    currentState = "a";
                    this.conditionMap.get("a").signal();
                    break;
            }
        } finally {
            lockman.unlock();
        }

    }
}
```


### 思路2 - cv.wait()/signalAll()
> [!algo]
> 维护三个条件变量太多，其实只需要一个即可。
> 
> 注意: 这种写法等价于使用`synchronized(this)`, 因为只有一个条件变量。
```java
package cn.itcast.self_test;


import lombok.extern.slf4j.Slf4j;

import java.util.HashMap;
import java.util.Map;
import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.ReentrantLock;

@Slf4j(topic="c.Interleaving_Print")
public class Interleaving_Print {
    public static void main(String[] args) {

        Sync_Print sp = new Sync_Print("a");

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 5; i++) {
                sp.print("a");
            }
        },"t1");
        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 5; i++) {
                sp.print("b");
            }
        },"t2");
        Thread t3 = new Thread(() -> {
            for (int i = 0; i < 5; i++) {
                sp.print("c");
            }
        },"t3");

        t1.start();
        t2.start();
        t3.start();
    }
}

/**
写法其实和顺序控制很想，所以在通知的时候仍然需要signalAll()而不是signal()，防止死锁。
*/
@Slf4j(topic="c.Sync_Print")
class Sync_Print {
    public String currentState;

    public ReentrantLock lockman = new ReentrantLock();

    public Condition cv = lockman.newCondition();

    public Sync_Print(String currentState) {
        this.currentState = currentState;
    }

    public void print(String output) {
        lockman.lock();
        // Critical Section
        try {
            while (!currentState.equals(output)) {
                try {
                    this.cv.await();
                } catch (InterruptedException e) {
                    throw new RuntimeException(e);
                }
            }

            log.debug(output);
            switch(currentState) {
                case "a":
                    currentState = "b";
                    this.cv.signalAll();
                    break;
                case "b":
                    currentState = "c";
                    this.cv.signalAll();
                    break;
                case "c":
                    currentState = "a";
                    this.cv.signalAll();
                    break;
            }
        } finally {
            lockman.unlock();
        }

    }
}
```






### 思路3 - park()/unpark()
> [!algo]
```java
package cn.itcast.self_test;

import lombok.extern.slf4j.Slf4j;

import java.util.concurrent.locks.LockSupport;

@Slf4j(topic="c.Interleaving_Print_Park")
public class Interleaving_Print_Park {
    public static void main(String[] args) {

        Thread[] threads = new Thread[3];
        threads[0] = new Thread(() -> {
            for (int i = 0; i < 5; i++) {
                LockSupport.park();
                log.debug("a");
                LockSupport.unpark(threads[1]);
            }
        },"t1");
        threads[1] = new Thread(() -> {
            for (int i = 0; i < 5; i++) {
                LockSupport.park();
                log.debug("b");
                LockSupport.unpark(threads[2]);
            }
        },"t2");
        threads[2] = new Thread(() -> {
            for (int i = 0; i < 5; i++) {
                LockSupport.park();
                log.debug("c");
                LockSupport.unpark(threads[0]);
            }
        },"t3");

        threads[0].start();
        threads[1].start();
        threads[2].start();

        LockSupport.unpark(threads[0]);

    }
}
```







# Sleep and Yield
## Thread.sleep()
> [!important]
> 调用`sleep()`会让当前线程从`RUNNING`进入`TIMED WAITING`状态。
```java
package cn.itcast.test;

import lombok.extern.slf4j.Slf4j;


@Slf4j(topic = "c.sleep_yield")
public class sleep_yield {

    public static void main(String[] args) {
        Thread t1 = new Thread(new Runnable() {

            @Override
            public void run() {
                try {
                    Thread.sleep(2000);
                } catch (InterruptedException e) {
                    throw new RuntimeException(e);
                }
            }
        });

        t1.start();


        log.debug("Child Thread State:" + t1.getState());
        try {
            // Make sure that the child process starts sleeping and changes from runnable to timed waiting
            Thread.sleep(500);
            log.debug("Child Thread State:" + t1.getState());
        } catch (InterruptedException e) {
            throw new RuntimeException(e);
        }
    }
}
```
> [!code] Output
> ![](Java_Threads.assets/image-20240402210839940.png)




## Thread.interrupt()
> [!important]
> 其他线程使用`interrupt()`方法可以打断`TIMED WAITING`状态使其变成`RUNNABLE`状态。
```java
package cn.itcast.test;


import lombok.extern.slf4j.Slf4j;

@Slf4j(topic="c.interrupt")
public class interrupt {

    public static void main(String[] args) {
        Thread t1 = new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    log.debug("Ready to sleep!");
                    Thread.sleep(2000);
                } catch (InterruptedException e) {
                    log.debug("waking up...");
                    e.printStackTrace();
                }
            }
        });

        // Before child thread is scheduled by CPU: NEW
        log.debug("Child Thread State:" + t1.getState());
        t1.start();

        try {
            Thread.sleep(500);
            // Check child thread state to become TIMED WAITING
            log.debug("Child Thread State:" + t1.getState());

            // Ready to interrupt
            log.debug("Interrupting...");
            t1.interrupt();

            // Check the child thread state: TIMED WAITING
            log.debug("Child Thread State:" + t1.getState());
        } catch (InterruptedException e) {
            throw new RuntimeException(e);
        }

        try {
            Thread.sleep(500);
        } catch (InterruptedException e) {
            throw new RuntimeException(e);
        }
        
        // TERMINATED
        log.debug("Child Thread State:" + t1.getState());
    }
}
```
> [!code] Output
> ![](Java_Threads.assets/image-20240402214633237.png)



## TimeUnit.sleep()
> [!important]
> `TimeUnit.sleep()`比`Thread.sleep()`拥有更好的可读性，前者在内部调用的就是后者。



## Thread.yield()
> [!important] 
> `Thread.yield()` changes the calling thread from `RUNNING` to `RUNNABLE`.
> 
> The difference between `TIMED WAITING` and `RUNNABLE` is that the former is like setting the priority of the thread to be very low, making it very difficult for scheduler to make it `RUNNABLE`. CPU will not dispatch its resource to a `TIMED WAITING` thread until the timer is over. 
> 
> `yield()` has no parameter, no need to wait.



## 线程优先级
> [!important]
> - 线程优先级会提示（hint）调度器优先调度该线程，但它仅仅是一个提示，调度器可以忽略它
> - 如果 cpu 比较忙，那么优先级高的线程会获得更多的时间片(把有限的钱用在刀刃上)，但 cpu 闲时，优先级几乎没作用
```java
package cn.itcast.test;

public class priority {

    public static void main(String[] args) {
        Runnable task1 = () -> {
            int count = 0;
            for (;;) {
                System.out.println("---->1 " + count++);
            }
        };
        Runnable task2 = () -> {
            int count = 0;
            for (;;) {
// Thread.yield();
                System.out.println(" ---->2 " + count++);
            }
        };
        Thread t1 = new Thread(task1, "t1");
        Thread t2 = new Thread(task2, "t2");
         t1.setPriority(Thread.MIN_PRIORITY);

         /*
            Since we manually create a scenario where CPU is infinitely
            looping, CPU is very busy, so we expect thread 2(which has higher priority)
            to be schduled with higher frequency and count variable increasing
            faster than thread 1.
          */
        t2.setPriority(Thread.MAX_PRIORITY);
        t1.start();
        t2.start();
    }
}
```


## sleep应用 - 防止CPU 100 % 
> [!important]
> 在只有单核的CPU上，我们如果使用`busy-waiting`机制会发现`CPU`占用率非常高，因为一直在跑`while loop`, 此时通过简单的在线程代码中添加`sleep()`即可显著降低占用率。


# Join
> [!important] 
> `t.join()` 可用于等待`t` 线程执行完毕后主线程才能继续执行。
```java
import lombok.extern.slf4j.Slf4j;
import java.util.concurrent.TimeUnit;

@Slf4j(topic="c.join")
public class join {

    static int c = 0;
    public static void main(String[] args) {
        Thread t1 = new Thread(()->{
            log.debug("t1 start...");
            try {
                TimeUnit.SECONDS.sleep(2);
                c = 10;
            } catch (InterruptedException e) {
                throw new RuntimeException(e);
            }
        },"t1");
        t1.start();

        log.debug("Main Thread, c:"  + c); // 0
    }
}
```
> [!code] Output
> ![](Java_Threads.assets/image-20240403084840289.png)




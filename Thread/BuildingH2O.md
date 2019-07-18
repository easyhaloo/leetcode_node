There are two kinds of threads, oxygen and hydrogen. Your goal is to group these threads to form water molecules. There is a barrier where each thread has to wait until a complete molecule can be formed. Hydrogen and oxygen threads will be given a releaseHydrogen and releaseOxygen method respectfully, which will allow them to pass the barrier. These threads should pass the barrier in groups of three, and they must be able to immediately bond with each other to form a water molecule. You must guarantee that all the threads from one molecule bond before any other threads from the next molecule do.

In other words:

- If an oxygen thread arrives at the barrier when no hydrogen threads are present, it has to wait for two hydrogen threads.
- If a hydrogen thread arrives at the barrier when no other threads are present, it has to wait for an oxygen thread and another hydrogen thread.

Write synchronization code for oxygen and hydrogen molecules that enforces these constraints.

**Example 1:**

```pseudocode
Input: "HOH"
Output: "HHO"
Explanation: "HOH" and "OHH" are also valid answers.
```

**Example 2:**

```pseudocode
Input: "OOHHHH"
Output: "HHOHHO"
Explanation: "HOHHHO", "OHHHHO", "HHOHOH", "HOHHOH", "OHHHOH", "HHOOHH", "HOHOHH" and "OHHOHH" are also valid answers.
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/building-h2o
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 解析

> 题意为： 打印水分子，可以很简单的制定一个规则，打印`o`之前必须打印两个`h`即可实现，
>
>我们采用计数的方式，为每次打印`h`给定计数，打印`o`时计数清零。



### 代码

```java
class H2O {

    //    private final CyclicBarrier latch = new CyclicBarrier(2);
    private volatile int count = 0;

    public H2O() {

    }

    public void hydrogen(Runnable releaseHydrogen) throws InterruptedException {

      // releaseHydrogen.run() outputs "H". Do not change or remove this line.
      synchronized (this) {
        while (count == 2) {
          wait();
        }
        releaseHydrogen.run();
        count++;
        notifyAll();
      }
    }

    public void oxygen(Runnable releaseOxygen) throws InterruptedException {

      // releaseOxygen.run() outputs "H". Do not change or remove this line.

      synchronized (this) {
        while (count != 2) {
          wait();
        }
        releaseOxygen.run();
        count = 0;
        notifyAll();
      }
    }
  }
```



### 代码(信号量)

```java
import java.util.concurrent.Semaphore;
class H2O {

    private Semaphore sH = new Semaphore(2); 
    private Semaphore sO = new Semaphore(0); 

    public H2O() {

    }

    public void hydrogen(Runnable releaseHydrogen) throws InterruptedException {

        sH.acquire(); 
        // releaseHydrogen.run() outputs "H". Do not change or remove this line.
        releaseHydrogen.run();
        
        if(sH.availablePermits() == 0) sO.release(); // 如果H资源都用光了，给O补资源
    }

    public void oxygen(Runnable releaseOxygen) throws InterruptedException {

        sO.acquire();
        // releaseOxygen.run() outputs "O". Do not change or remove this line.
        releaseOxygen.run();
        sH.release(2); 
    }
}
```


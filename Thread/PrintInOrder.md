Suppose we have a class:

```java
public class Foo {
  public void one() { print("one"); }
  public void two() { print("two"); }
  public void three() { print("three"); }
}
```


The same instance of Foo will be passed to three different threads. Thread A will call one(), thread B will call two(), and thread C will call three(). Design a mechanism and modify the program to ensure that two() is executed after one(), and three() is executed after two().

**Example 1:**

```java
Input: [1,2,3]
Output: "onetwothree"
Explanation: There are three threads being fired asynchronously. The input [1,2,3] means thread A calls one(), thread B calls two(), and thread C calls three(). "onetwothree" is the correct output.
```



**Example 2:**

```java
Input: [1,3,2]
Output: "onetwothree"
Explanation: The input [1,3,2] means thread A calls one(), thread B calls three(), and thread C calls two(). "onetwothree" is the correct output.
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/print-in-order
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。





### 解析

> 多线程顺按顺序输出1,2,3。
>
> 两种方式：  
>
> - 采用信号量，线程1 线程2 执行完分别释放自己的信号量。
> - 采用计数形式，每个线程执行完毕计数器自增一，每个线程必须拿到跟自己线程对应的序号才可以正常执行。





### 代码

```java
import java.util.concurrent.Semaphore;
class Foo {
  private int flag = 1;
  public Foo() {

  }
  
  private Semaphore semaphore = new Semaphore(0);
  private Semaphore semaphore2 = new Semaphore(0);

  public void first(Runnable printFirst) throws InterruptedException {

//    synchronized (this) {
//      while (flag != 1) {
//        this.wait();
//      }
//
//      printFirst.run();
//      flag = 2;
//      this.notifyAll();
//    }
    // printFirst.run() outputs "first". Do not change or remove this line.
      printFirst.run();
      semaphore.release();
  }

  public void second(Runnable printSecond) throws InterruptedException {

    // printSecond.run() outputs "second". Do not change or remove this line.
//    synchronized (this) {
//      while (flag != 2) {
//        this.wait();
//      }
//
//      printSecond.run();
//      flag = 3;
//      this.notifyAll();
//    }
    semaphore.acquire();
    printSecond.run();
    semaphore2.release();

  }

  public void third(Runnable printThird) throws InterruptedException {

//    synchronized (this) {
//      while (flag != 3) {
//        this.wait();
//      }
//      printThird.run();
//      flag = 1;
//      this.notifyAll();
//    }
    semaphore2.acquire();
    printThird.run();
  }
}
```


Suppose you are given the following code:

```java
class FooBar {
  public void foo() {
    for (int i = 0; i < n; i++) {
      print("foo");
    }
  }

  public void bar() {
    for (int i = 0; i < n; i++) {
      print("bar");
    }
  }
}

```

The same instance of FooBar will be passed to two different threads. Thread A will call foo() while thread B will call bar(). Modify the given program to output "foobar" n times.

**Example 1:**

```cassandra
Input: n = 1
Output: "foobar"
Explanation: There are two threads being fired asynchronously. One of them calls foo(), while the other calls bar(). "foobar" is being output 1 time.

```

**Example 2:**

```cobol
Input: n = 2
Output: "foobarfoobar"
Explanation: "foobar" is being output 2 times.

```



来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/print-foobar-alternately
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。





### 解析

> 该题目要求，多线程交替输出`foobar`。
>
> 可以使用信号量，需要注意的是我们需要让`foo`先获取信号量，所以一个信号量初始值为1，另外一个为0



### 代码

```java
import java.util.concurrent.Semaphore;
class FooBar {
    private int n;
    private Semaphore semaphoreFoo = new Semaphore(0);
    private Semaphore semaphoreBar = new Semaphore(1);
    public FooBar(int n) {
        this.n = n;
    }

    public void foo(Runnable printFoo) throws InterruptedException {
        
         for (int i = 0; i < n; i++) {
              semaphoreBar.acquire();
              printFoo.run();
              semaphoreFoo.release();
          }
    }

    public void bar(Runnable printBar) throws InterruptedException {
        
      for (int i = 0; i < n; i++) {
          semaphoreFoo.acquire();
          printBar.run();
          semaphoreBar.release();
        }
    }
}
```


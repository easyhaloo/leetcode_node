Given a char array representing tasks CPU need to do. It contains capital letters A to Z where different letters represent different tasks. Tasks could be done without original order. Each task could be done in one interval. For each interval, CPU could finish one task or just be idle.

However, there is a non-negative cooling interval n that means between two same tasks, there must be at least n intervals that CPU are doing different tasks or just be idle.

You need to return the least number of intervals the CPU will take to finish all the given tasks.



**Example:**

```verilog
Input: tasks = ["A","A","A","B","B","B"], n = 2
Output: 8
Explanation: A -> B -> idle -> A -> B -> idle -> A -> B.
```



来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/task-scheduler
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。





### 解析

> 计算所有任务完成的最短时间。由于题目中要求所有相同的任务类型，它的间隔必须为n，所以这题可以使用贪心求解。
>
> 首先遍历数组，求出任务出现次数最多那个任务(max_count_task)。因为任意相同的两个任务之间的间隔必须为n，那么此时我们可以使用(max_count_task-1)*(n+1)来表示所耗费的时间。
>
> (max_count_task-1)不包括最后一次出现的任务。因为最后一次执行后面还可能包含其他的任务，所以我们需要单独考虑。
>
> 如果说只有一个max_count_task，那么就直接+1，如果有多个则需要+x(x代表有多个出现max_count_task次数的字任务)





### 代码

```java
 public int leastInterval(char[] tasks, int n) {
    if (tasks == null || tasks.length == 0) return 0;
    int[] counts = new int[26];
    for (char task : tasks) {
      counts[task - 'A']++;
    }

    int max = Integer.MIN_VALUE;
    for (int count : counts) {
      max = Math.max(max, count);
    }

    int ret = 0;
    for (int count : counts) {
      if (count == max) ++ret;
    }
    return Math.max(tasks.length, (n + 1) * (max - 1) + ret);
  }
```


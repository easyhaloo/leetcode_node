You are given a circular array nums of positive and negative integers. If a number k at an index is positive, then move forward k steps. Conversely, if it's negative (-k), move backward k steps. Since the array is circular, you may assume that the last element's next element is the first element, and the first element's previous element is the last element.

Determine if there is a loop (or a cycle) in nums. A cycle must start and end at the same index and the cycle's length > 1. Furthermore, movements in a cycle must all follow a single direction. In other words, a cycle must not consist of both forward and backward movements.



Example 1:

Input: [2,-1,1,2,2]
Output: true
Explanation: There is a cycle, from index 0 -> 2 -> 3 -> 0. The cycle's length is 3.



来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/circular-array-loop
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。





### 解析

>  题意为求数组是否为环，有点类似缓行链表，因此同样可以使用双指针来做。
>
> -  首先我们需要计算下一个所谓的位置，由于数组元素存在正负，所以我们需要设定一个通用的下一个节点的索引，` ((nums[index] + index) % nums.length + nums.length) % nums.length`，我们需要对len取两次余数，因为数组中的负数可能存在大于`len`的情况。所以我们先要取一次余让其在len范围内，然后加上len,再取一次余。 如果`nums[index] + index`是整数后面的操作将不影响前面的计算，如果是负数我们可以使用`+ nums.length`来取长度的补集。 例如：nums[index] = -7.  Len = 5.   那么nextIndex = 3
> - 设置快慢指针，slow，fast。slow，fast需要满足两个条件才可以前进，第一两者索引的元素必须同向才可以，第二slow的下一个索引不能是自己，如果是这样，则不满足环形的特性。所以直接跳过。当slow == fast 时，即代表存在环
> - 如果这一轮循环不存在环，需要将这一轮中经过的点设置为0（题意中说明索引不存在0）。当遇见0时直接跳过。



### 代码

```java
 public static boolean circularArrayLoop(int[] nums) {
    int len = nums.length;
    for (int i = 0; i < len; i++) {
      if (nums[i] == 0) continue;
      int slow = i, fast = getNext(nums, i), val = nums[i];
      while (val * nums[fast] > 0 && val * nums[getNext(nums, fast)] > 0) {
        if (slow == fast) {
          if (slow == getNext(nums, slow)) break;
          return true;
        }
        slow = getNext(nums, slow);
        fast = getNext(nums, getNext(nums, fast));
      }
      slow = i;
      while (val * nums[slow] > 0) {
        int next = getNext(nums, slow);
        nums[slow] = 0;
        slow = next;
      }
    }
    return false;
  }

  public static int getNext(int[] nums, int index) {
    return ((nums[index] + index) % nums.length + nums.length) % nums.length;
  }
```




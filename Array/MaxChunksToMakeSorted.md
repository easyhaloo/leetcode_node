Given an array arr that is a permutation of [0, 1, ..., arr.length - 1], we split the array into some number of "chunks" (partitions), and individually sort each chunk.  After concatenating them, the result equals the sorted array.

What is the most number of chunks we could have made?

**Example 1:**

```verilog
Input: arr = [4,3,2,1,0]
Output: 1
Explanation:
Splitting into two or more chunks will not return the required result.
For example, splitting into [4, 3], [2, 1, 0] will result in [3, 4, 0, 1, 2], which isn't sorted.
```

**Example 2:**

```verilog
Input: arr = [1,0,2,3,4]
Output: 4
Explanation:
We can split into two chunks, such as [1, 0], [2, 3, 4].
However, splitting into [1, 0], [2], [3], [4] is the highest number of chunks possible.
```



来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/max-chunks-to-make-sorted
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 解析

> 根据题意所给出的要求，数组是有规律的，arr[i] 在[0,1,…arr.length-1]之间，而且一定没有重复的元素，如果想要拆分区间，那么一段区间中的最大值max 应该是大于等于这段区间的最大索引值。这是由于分段区间的降序排列所致。



### 代码

```java
  public int maxChunksToSorted(int[] arr) {
    if (arr == null || arr.length == 0) return 0;

    int ret = 0;
    int max = 0;

    for (int i = 0; i < arr.length; i++) {
      max = Math.max(max, arr[i]);
      // max == i 则表示这是一段最大区间了，因为如果i继续加则超过了这个区间，因为分段的区间总是降序
      if (max == i) ret++;
    }
    return ret;
  }
```


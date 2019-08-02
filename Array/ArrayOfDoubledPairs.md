Given an array of integers A with even length, return true if and only if it is possible to reorder it such that A[2 * i + 1] = 2 * A[2 * i] for every 0 <= i < len(A) / 2.

 

**Example 1:**

```verilog
Input: [3,1,3,6]
Output: false
```

**Example 2:**

```verilog
Input: [2,1,2,6]
Output: false
```

**Example 3:**

```verilog
Input: [4,-2,2,-4]
Output: true
Explanation: We can take two groups, [-2,-4] and [2,4] to form [-2,-4,2,4] or [2,4,-2,-4].
```

**Example 4:**

```verilog
Input: [1,2,4,16,8,4]
Output: false
```



来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/array-of-doubled-pairs
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 解析

> 使用两个数组，同时记录正数，负数。使用数组中的值作为下标索引。 
>
> 因为数组长度固定为【-100000，100000】，所以正数负数各占100000,负数数组将负数变为正数存储。
>
>  同时遍历新的数组，先遍历低位(原始数组中最大值/2)，将出现的索引（也就是新数组的值大于0）和当前索引的两倍同时减去，当发现索引下标（<0)返回false。 然后遍历高位,如果索引位置的值不为0，返回false. 其实就是要保证新开辟的两个数组，遍历完毕后，所有索引位置的值都为0



### 代码

```java
public boolean canReorderDoubled(int[] A) {
    // 记录负数
    short[] negative = new short[100000];
    // 记录正数
    short[] positive = new short[100000];

    // 负数必须是2的整数倍，最小的正数必须是2的倍数
    int maxPositive = 0, minNegative = 0, actualNegativeCount = 0;
    for (int i : A) {
      if (i > 0) {
        positive[i]++;
        maxPositive = Math.max(maxPositive, i);
      } else {
        i = -i;
        negative[i]++;
        actualNegativeCount++;
        minNegative = Math.max(minNegative, i);
      }
    }

    if ((actualNegativeCount & 1) != 0
        || (positive[0] & 1) != 0) return false;

    return search(positive, maxPositive) && search(negative, minNegative);
  }

  private boolean search(short[] arr, int max) {
    int mid = max >> 1;
    for (int i = 1; i <= mid; i++) {
      if (arr[i] > 0) {
        arr[i * 2] -= arr[i];
      } else if (arr[i] < 0) return false;
    }

    for (int i = mid + 1; i <= max; i++) {
      if (arr[i] != 0) return false;
    }
    return true;
  }
```


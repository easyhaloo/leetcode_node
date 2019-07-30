Given two integers n and k, you need to construct a list which contains n different positive integers ranging from 1 to n and obeys the following requirement: 
Suppose this list is [a1, a2, a3, ... , an], then the list [|a1 - a2|, |a2 - a3|, |a3 - a4|, ... , |an-1 - an|] has exactly k distinct integers.

If there are multiple answers, print any of them.

**Example 1:**

```verilog
Input: n = 3, k = 1
Output: [1, 2, 3]
Explanation: The [1, 2, 3] has three different positive integers ranging from 1 to 3, and the [1, 1] has exactly 1 distinct integer: 1.
```

**Example 2:**

```verilog
Input: n = 3, k = 2
Output: [1, 3, 2]
Explanation: The [1, 3, 2] has three different positive integers ranging from 1 to 3, and the [2, 1] has exactly 2 distinct integers: 1 and 2.
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/beautiful-arrangement-ii
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 解析

> 这题可以使用双指针。
>
> 每次取值时，都会同时从数组头部或者是尾部获取数据。由于题目中给定数组元素的值都不一样，谷可以直接用1~n来代替。
>
> 有点类似摆动排序一样，每次从顺序列表中一次取首部一次取尾部。
>
> 例如： [1,n] [2,n-1] 这样每次取得得差值都不一样。
>
> 我们最后根据k的奇偶来确定，是逆序输出还是顺序输出。



### 代码

```java
class Solution {
    public int[] constructArray(int n, int k) {
     int[] ret = new int[n];

    int start = 1, end = n, i = 0;

    while (start <= end) {
      if (i < k && i % 2 == 0 || (i >= k && (k - 1) % 2 == 0)) ret[i++] = start++;
      else ret[i++] = end--;
    }
    return ret;
    }
}
```


A zero-indexed array A of length N contains all integers from 0 to N-1. Find and return the longest length of set S, where S[i] = {A[i], A[A[i]], A[A[A[i]]], ... } subjected to the rule below.

Suppose the first element in S starts with the selection of element A[i] of index = i, the next element in S should be A[A[i]], and then A[A[A[i]]]… By that analogy, we stop adding right before a duplicate element occurs in S.



**Example 1:**

```verilog
Input: A = [5,4,0,3,1,6,2]
Output: 4
Explanation: 
A[0] = 5, A[1] = 4, A[2] = 0, A[3] = 3, A[4] = 1, A[5] = 6, A[6] = 2.

One of the longest S[K]:
S[0] = {A[0], A[5], A[6], A[2]} = {5, 6, 2, 0}
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/array-nesting
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 解析

> 设置一个visited数组，用来记录当前访问过的数组索引，当索引位置已经访问过，代表结果已经计算过不需要重复计算。
>
> 这里题意给出的数组中元素的值不会超过数组元素，可以开一个数组长度大小的visited
>
> 从每个位置开始循环往后找，并且记录一个长度，就行了。
>
> 这里还可以剪枝，我们可以记录当前数组中已经遍历多少个，如果发现 nums.length-cnt < ret也就是说剩下的全部连在一起都不会超过当前已经知道的最大的 。



### 代码

```java
class Solution {
    public int arrayNesting(int[] nums) {
     int ret = 0, cnt = 0;
        int[] visited = new int[nums.length];
        for (int i = 0; i<nums.length&&(nums.length-cnt)>ret; i++) {
            int len = 0;
            int c = i;
            while (visited[c] == 0) {
                len++;
                visited[c] = 1;
                cnt++;
                c = nums[c];
            }
            ret = Math.max(ret, len);
        }
        return ret;    
    }
}
```


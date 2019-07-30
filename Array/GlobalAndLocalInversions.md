We have some permutation A of [0, 1, ..., N - 1], where N is the length of A.

The number of (global) inversions is the number of i < j with 0 <= i < j < N and A[i] > A[j].

The number of local inversions is the number of i with 0 <= i < N and A[i] > A[i+1].

Return true if and only if the number of global inversions is equal to the number of local inversions.

**Example 1:**

```verilog
Input: A = [1,0,2]
Output: true
Explanation: There is 1 global inversion, and 1 local inversion.
```

**Example 2:**

```log
Input: A = [1,2,0]
Output: false
Explanation: There are 2 global inversions, and 1 local inversion.
```



来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/global-and-local-inversions
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 解析

> 根据题意可知：
>
> 局部转置一定是全局转置,。即全部是局部转置，则不会出现A[i] > A[i+2]
>
> 只要用一个max表示前i-2项的最大值，这个最大值是否大于第i项，大于的话则为false



### 代码

```java
    public boolean isIdealPermutation(int[] A) {
        if(A.length <= 2) return true;
        int max = A[0];
        for(int i = 2; i < A.length;i++){
            if(A[i] < max) return false;
            if(A[i-1] > max) max = A[i-1];
        }
        return true;
    }
```


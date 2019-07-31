Given an array A of non-negative integers, return the maximum sum of elements in two non-overlapping (contiguous) subarrays, which have lengths L and M.  (For clarification, the L-length subarray could occur before or after the M-length subarray.)

Formally, return the largest V for which V = (A[i] + A[i+1] + ... + A[i+L-1]) + (A[j] + A[j+1] + ... + A[j+M-1]) and either:

- 0 <= i < i + L - 1 < j < j + M - 1 < A.length, or
- 0 <= j < j + M - 1 < i < i + L - 1 < A.length.

**Example 1:**

```verilog
Input: A = [0,6,5,2,2,5,1,9,4], L = 1, M = 2
Output: 20
Explanation: One choice of subarrays is [9] with length 1, and [6,5] with length 2.
```

**Example 2:**

```verilog
Input: A = [3,8,1,3,2,1,8,9,0], L = 3, M = 2
Output: 29
Explanation: One choice of subarrays is [3,8,1] with length 3, and [8,9] with length 2.
```

**Example 3:**

```verilog
Input: A = [2,1,5,6,0,9,5,0,3,8], L = 4, M = 3
Output: 31
Explanation: One choice of subarrays is [5,6,0,9] with length 4, and [3,8] with length 3.
```



来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/maximum-sum-of-two-non-overlapping-subarrays
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 解析

> 这题，我们可以先求出前缀的的总和即A[i] = A[0,i]的和。由于两个数组不能重叠，
>
> 分别求出maxL，maxM，即maxL代表L的最大值，maxM代表M的最大值。
>
> 我们可以设定初始值的时候，前M+L个元素的和为最大值。前L个元素的为L的最大值，前M个元素为M的最大值。
>
> 然后通过max(maxL+A[i] - A[i-M],maxM+A[i] - A[i-L])来判断到底是L在M前，还是M在L前
>
> 这样可以避免两次for循环，来分别讨论L在M前，还是M在L前两种情况。



### 代码

```java
class Solution {
    public int maxSumTwoNoOverlap(int[] A, int L, int M) {
        for (int i = 1; i < A.length; ++i)
            A[i] += A[i - 1];
        int res = A[L + M - 1], Lmax = A[L - 1], Mmax = A[M - 1];
        for (int i = L + M; i < A.length; ++i) {
            Lmax = Math.max(Lmax, A[i - M] - A[i - L - M]);
            Mmax = Math.max(Mmax, A[i - L] - A[i - L - M]);
            res = Math.max(res, Math.max(Lmax + A[i] - A[i - M], Mmax + A[i] - A[i - L]));
        }
        return res;
    }
}
```





```java
public int maxSumTwoNoOverlap(int[] A, int L, int M) {
    int max = 0, maxL = 0, maxM = 0;
    for (int i = L; i < A.length - M + 1; i++) {
      maxL = Math.max(maxL, sum(A, i - L, i - 1));
      max = Math.max(max, maxL + sum(A, i, i + M - 1));
    }
    for (int i = M; i < A.length - L + 1; i++) {
      maxM = Math.max(maxM, sum(A, i - M, i - 1));
      max = Math.max(max, sum(A, i, i + L - 1) + maxM);
    }
    return max;
  }

  private int sum(int[] arr, int l, int r) {
    int sum = 0;
    while (l <= r) {
      sum += arr[l++];
    }
    return sum;
  }
```


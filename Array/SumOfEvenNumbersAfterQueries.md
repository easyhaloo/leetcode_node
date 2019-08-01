We have an array A of integers, and an array queries of queries.

For the i-th query val = queries[i][0], index = queries[i][1], we add val to A[index].  Then, the answer to the i-th query is the sum of the even values of A.

(Here, the given index = queries[i][1] is a 0-based index, and each query permanently modifies the array A.)

Return the answer to all queries.  Your answer array should have answer[i] as the answer to the i-th query.

 

**Example 1:**

```verilog
Input: A = [1,2,3,4], queries = [[1,0],[-3,1],[-4,0],[2,3]]
Output: [8,6,2,4]
Explanation: 
At the beginning, the array is [1,2,3,4].
After adding 1 to A[0], the array is [2,2,3,4], and the sum of even values is 2 + 2 + 4 = 8.
After adding -3 to A[1], the array is [2,-1,3,4], and the sum of even values is 2 + 4 = 6.
After adding -4 to A[0], the array is [-2,-1,3,4], and the sum of even values is -2 + 4 = 2.
After adding 2 to A[3], the array is [-2,-1,3,6], and the sum of even values is -2 + 6 = 4.
```



来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/sum-of-even-numbers-after-queries
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。





### 解析

> 这题不能使用双重for循环来做，必定超时，必须想办法变成一个for循环。
>
> 题意是求解偶数值的和，我们可以在初始化时，计算原数组中所有的偶数值。
>
> Queries数组中包含value和index，我们可以通过原数组中的index位置的元素加上value来判断是否时偶数，如果是偶数则加上这个value。
>
> 这里注意的是，每次我们还需要对index的位置进行判断一下，如果之前就是偶数那么我们只是加上这个value，如果原来是奇数加上这个value后变为偶数，则需要加上改变之后的值。



### 代码

```java
public static int[] sumEvenAfterQueries(int[] A, int[][] queries) {
    int[] ret = new int[A.length];
    // 计算所有偶数和
    int sum = 0;
    for (int i : A) {
      if (i % 2 == 0) sum += i;
    }
    for (int i = 0; i < queries.length; i++) {
      int value = queries[i][0], index = queries[i][1];
      if (A[index] % 2 == 0) sum -= A[index];
      A[index] += value;
      if (A[index] % 2 == 0) sum += A[index];
      ret[i] = sum;
    }
    return ret;
  }
```


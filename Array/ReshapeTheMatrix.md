In MATLAB, there is a very useful function called 'reshape', which can reshape a matrix into a new one with different size but keep its original data.

You're given a matrix represented by a two-dimensional array, and two positive integers r and c representing the row number and column number of the wanted reshaped matrix, respectively.

The reshaped matrix need to be filled with all the elements of the original matrix in the same row-traversing order as they were.

If the 'reshape' operation with given parameters is possible and legal, output the new reshaped matrix; Otherwise, output the original matrix.



**Example 1:**

```java
Input: 
nums = 
[[1,2],
 [3,4]]
r = 1, c = 4
Output: 
[[1,2,3,4]]
Explanation:
The row-traversing of nums is [1,2,3,4]. The new reshaped matrix is a 1 * 4 matrix, fill it row by row by using the previous list.
```



来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/reshape-the-matrix
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 解析

> 该题可以直接先将所有的元素取出来保存，然后按照题目给定的矩阵顺序挨个存储。
>
> 还可以使用节省存储空间的做法，使用取余数的做法。
>
> **`nnums[i][j] = nums[(i * c + j) / nums[0].length][(i * c + j) % nums[0].length];`**





### 代码

```java
public int[][] matrixReshape(int[][] nums, int r, int c) {
         if (nums[0].length * nums.length != r * c) {
            return nums;
        }

        int[][] nnums = new int[r][c];

        for (int i = 0; i < r; i++) {
            for (int j = 0; j < c; j++) {
                 nnums[i][j] = nums[(i * c + j) / nums[0].length][(i * c + j) % nums[0].length];
            }
        }
        return nnums;
    }
```


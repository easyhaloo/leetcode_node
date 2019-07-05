In a 2 dimensional array grid, each value grid[i][j] represents the height of a building located there. We are allowed to increase the height of any number of buildings, by any amount (the amounts can be different for different buildings). Height 0 is considered to be a building as well. 

At the end, the "skyline" when viewed from all four directions of the grid, i.e. top, bottom, left, and right, must be the same as the skyline of the original grid. A city's skyline is the outer contour of the rectangles formed by all the buildings when viewed from a distance. See the following example.

What is the maximum total sum that the height of the buildings can be increased?



What is the maximum total sum that the height of the buildings can be increased?

Example:
Input: grid = [[3,0,8,4],[2,4,5,7],[9,2,6,3],[0,3,1,0]]
Output: 35
Explanation: 
The grid is:
[ [3, 0, 8, 4], 
  [2, 4, 5, 7],
  [9, 2, 6, 3],
  [0, 3, 1, 0] ]

The skyline viewed from top or bottom is: [9, 4, 8, 7]
The skyline viewed from left or right is: [8, 7, 9, 3]

The grid after increasing the height of buildings without affecting skylines is:

gridNew = [ [8, 4, 8, 7],
            [7, 4, 7, 7],
            [9, 4, 8, 7],
            [3, 3, 3, 3] ]



来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/max-increase-to-keep-city-skyline
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 解析

>  求天际线，也就是求当前位置的建筑物在其横向与纵向位置中，取最高中的最小值。
>
> 首先需要求出横向中的最大值，纵向中的最大值。
>
> 然后遍历数组，取当前位置下，横向与纵向位置的最小值，然后减去本身。



### 代码

```java
 public static int maxIncreaseKeepingSkyline(int[][] grid) {
    if (grid == null || grid.length == 0) return 0;
    if (grid.length == 1) {
      int sum = 0;
      int max = 0;
      for (int ints : grid[0]) {
        max = Math.max(max, ints);
        sum += ints;
      }
      return max * grid[0].length - sum;
    }
    // 竖直方向
    int[] bottomLine = new int[grid.length];
    // 水平方向
    int[] leftLine = new int[grid[0].length];

    for (int i = 0; i < grid.length; i++) {
      for (int j = 0; j < grid[i].length; j++) {
        bottomLine[j] = Math.max(bottomLine[j], grid[i][j]);
        leftLine[i] = Math.max(leftLine[i], grid[i][j]);
      }
    }

    int increment = 0;
    for (int i = 0; i < grid.length; i++) {
      for (int j = 0; j < grid[i].length; j++) {
        int line = Math.min(bottomLine[i], leftLine[j]);
        increment += line - grid[i][j];
      }
    }

    return increment;
  }
```


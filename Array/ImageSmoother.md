Given a 2D integer matrix M representing the gray scale of an image, you need to design a smoother to make the gray scale of each cell becomes the average gray scale (rounding down) of all the 8 surrounding cells and itself. If a cell has less than 8 surrounding cells, then use as many as you can.



**Example 1:**

```verilog
Input:
[[1,1,1],
 [1,0,1],
 [1,1,1]]
Output:
[[0, 0, 0],
 [0, 0, 0],
 [0, 0, 0]]
Explanation:
For the point (0,0), (0,2), (2,0), (2,2): floor(3/4) = floor(0.75) = 0
For the point (0,1), (1,0), (1,2), (2,1): floor(5/6) = floor(0.83333333) = 0
For the point (1,1): floor(8/9) = floor(0.88888889) = 0
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/image-smoother
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 解析

> 直接暴力破解



### 代码

```java
public class ImageSmoother {
  int row;
  int col;

  public int[][] imageSmoother(int[][] M) {
    if (M == null || M.length < 1 || M[0] == null || M[0].length < 1) {
      return null;
    }

    row = M.length;
    col = M[row - 1].length;

    int ret[][] = new int[row][col];
    for (int i = 0;i < row;i++) {
      for (int j = 0;j < col;j++) {
        ret[i][j] = cal(M,i,j);
      }
    }
    return ret;

  }

  private int[] y = {-1, 1, 0, 0, -1, -1, 1, 1};
  private int[] x = {0, 0, 1, -1, -1, 1, -1, 1};

  private int cal(int[][] M, int r, int c) {
    int count = 1;
    int sum = M[r][c];
    for (int i = 0; i < 8; i++) {
      int nc = c + x[i];
      int nr = r + y[i];
      if (nr >= 0 && nr < row && nc >= 0 && nc < col) {
        count++;
        sum += M[nr][nc];
      }
    }
    return sum / count;
  }
}
```


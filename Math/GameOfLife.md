According to the Wikipedia's article: "The Game of Life, also known simply as Life, is a cellular automaton devised by the British mathematician John Horton Conway in 1970."

Given a board with m by n cells, each cell has an initial state live (1) or dead (0). Each cell interacts with its eight neighbors (horizontal, vertical, diagonal) using the following four rules (taken from the above Wikipedia article):



1. Any live cell with fewer than two live neighbors dies, as if caused by under-population.
2. Any live cell with two or three live neighbors lives on to the next generation.
3. Any live cell with more than three live neighbors dies, as if by over-population..
4. Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.

Write a function to compute the next state (after one update) of the board given its current state. The next state is created by applying the above rules simultaneously to every cell in the current state, where births and deaths occur simultaneously.

```java
Example:
Input: 
[
  [0,1,0],
  [0,0,1],
  [1,1,1],
  [0,0,0]
]
Output: 
[
  [0,0,0],
  [1,0,1],
  [0,1,1],
  [0,1,0]
]
```

**Follow up:**

1. Could you solve it in-place? Remember that the board needs to be updated at the same time: You cannot update some cells first and then use their updated values to update other cells.
2. In this question, we represent the board using a 2D array. In principle, the board is infinite, which would cause problems when the active area encroaches the border of the array. How would you address these problems?



来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/game-of-life
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 解析

>  此题是需要计算细胞的一次存活后的状态面板。它有比较重要的三条规则：
>
> 1. 八个临近位置活细胞少于两个则  活->死
> 2. 八个临近位置活细胞有两个或三个则  活->活
> 3. 八个临近位置活细胞超过三个则 活->死
> 4. 八个临近位置活细胞等于三个则 死->活
>
>  总共有这四种状态，且题目让我们使用原地算法，则表示不能先改变某个细胞状态，再拿来下一次计算。所以我们需要用四个状态来表示细胞的存活状态：
>
> - -1 死->活 
> -  0 死->死
> - 1  活->活
> - 2  活->死
>
> 使用一个live变量来表示临近细胞存活数量，依次遍历，注意边界的处理。
>
> 遍历完毕之后重置状态，-1 置为1，2 置为0.
>
> 这里需要注意的是，必须要让 **-1 死->活 和2  活->死**这两个状态不能随意改变，因为我们的判断条件是
>
> `board[x - 1][y + 1]>0`来表示细胞存活，为了不影响临近节点的判断，我们需要将其置为< 0.





### 代码

```java
public class GameOfLife {

  public void gameOfLife(int[][] board) {
    for (int i = 0; i < board.length; i++) {
      for (int j = 0; j < board[0].length; j++) {
        neighbor(board, i, j);
      }
    }

    for (int i = 0; i < board.length; i++) {
      for (int j = 0; j < board[0].length; j++) {
        if (board[i][j] == -1) {
          board[i][j] = 1;
        }
        if (board[i][j] == 2) {
          board[i][j] = 0;
        }
      }
    }
  }

  private void neighbor(int[][] board, int x, int y) {
    // -1  dead->live
    // 0  dead
    // 1  live
    // 2 live-dead
    int live = 0;
    if (x > 0) {
      if (board[x - 1][y] > 0) {
        live++;
      }
      if (y > 0 && board[x - 1][y - 1] > 0) {
        live++;
      }
      if (y < board[0].length - 1 && board[x - 1][y + 1] > 0) {
        live++;
      }
    }


    if (x < board.length - 1) {
      if (board[x + 1][y] > 0) {
        live++;
      }
      if (y > 0 && board[x + 1][y - 1] > 0) {
        live++;
      }
      if (y < board[0].length - 1 && board[x + 1][y + 1] > 0) {
        live++;
      }
    }

    if (y > 0 && board[x][y - 1] > 0) {
      live++;
    }

    if (y < board[0].length - 1 && board[x][y + 1] > 0) {
      live++;
    }
    if (board[x][y] == 1) {
      if (live < 2 || live > 3) {
        board[x][y] = 2;
      }
    } else if (live == 3) {
      board[x][y] = -1;
    }
  }
}
```



### 解法2

>  跟解法1有点类似的是，我们同样采取四个值来表示四种状态：
>
> 利用一个 two bits 的状态机来记录细胞状态, 第一位表示 下一状态, 第二位表示当前状态:
>
> **00: dead (next state) <- dead (current state)**
> **01: dead (next state) <- live (current state)** 
> **10: live (next state) <- dead (current state)**
> **11: live (next state) <- live (current state)** 
>
> 计算完毕之后，只需要向右移动一位即可表示细胞的真正存活状态。





### 代码

```java
class Solution {
    public void gameOfLife(int[][] board) {
        /**
        利用一个 two bits 的状态机来记录细胞状态, 第一位表示
        下一状态, 第二位表示当前状态:
        00: dead (next state) <- dead (current state)
        01: dead (next state) <- live (current state) 
        10: live (next state) <- dead (current state)
        11: live (next state) <- live (current state) 
        初始情况对应就是 00 和 01 (默认下一状态是 dead state)
        统计每个位置周围的 live 细胞数决定高位置 1 (live)还是 
        0 (dead), 最后右移一位即为最终状态, 注意不需要考虑 01
        以及 00 的情况, 因为已经默认下一状态为 dead.
        **/
        if(board.length < 1) return;
        // 更新矩阵
        for(int i = 0; i < board.length; ++i) {
            for(int j = 0; j < board[0].length; ++j) {
                int lives = countLives(board, i, j);
                // live -> live
                if((board[i][j] & 1) == 1) {
                    if(lives >= 2 && lives <= 3)
                        board[i][j] = 3;
                }
                // dead -> live
                else {
                    if(lives == 3)
                        board[i][j] = 2;
                }
            }
        }
        // 重置矩阵
        for(int i = 0; i < board.length; ++i) {
            for(int j = 0; j < board[0].length; ++j) 
                board[i][j] >>= 1;
        }
    }
    
    private int countLives(int[][] b, int i, int j) {
        int count = 0;
        int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1},{1,1},{1,-1},{-1,1},{-1,-1}};   
        for(int[] dir : dirs) {
            int x = i + dir[0];
            int y = j + dir[1];
            if(x < 0 || x > b.length-1 || y < 0 || y > b[0].length-1)
                continue;
            count += (b[x][y] & 1);
        }
        return count;
    }
}
```




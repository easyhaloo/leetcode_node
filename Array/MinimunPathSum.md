
- ### 代码

```java

package interview.array;
	
	public class MinimunPathSum {
	
	
	
	    public int minPathSum(int[][] grid){
	        int row = grid.length;
	        int col = grid[0].length;
	        for(int i = 0;i<row;i++){
	            for(int j = 0;j<col;j++){
	                if(i == 0 && j!= 0) {
	                    grid[i][j] += grid[i][j-1];
	                }else if( i != 0 && j == 0){
	                    grid[i][j] += grid[i-1][j];
	                }else if( i == 0 && j == 0){
	                    grid[i][j] = grid[i][j];
	                }else {
	                    grid[i][j] += Math.min(grid[i][j-1],grid[i-1][j]);
	                }
	            }
	        }
	
	        return grid[row-1][col-1];
	    }
	
	
	
	    public int minPathSumDp(int[][] grid){
	        int m = grid.length;
	        int n = grid[0].length;
	        int[][] memo =new int[m][n];
	        return dfs(grid,m-1,n-1,memo);
	    }
	
	    private int dfs(int[][] grid,int x , int y,int[][] memo){
	        if(x < 0 || y< 0){
	            return Integer.MAX_VALUE;
	        }
	        if(memo[x][y] > 0){
	            return memo[x][y];
	        }
	
	        if(x==0 && y==0){
	            return grid[0][0];
	        }
	
	        int res = grid[x][y] + Math.min(dfs(grid,x-1,y,memo),dfs(grid,x,y-1,memo));
	
	        memo[x][y] = res;
	
	        return res;
	    }
	}
	

```

- ### 代码

```java

package interview.array;
	
	public class UniquePaths2 {
	
	    public static void main(String[] args){
	        int[][]  obstacles = new int[][]{
	                {1}
	        };
	        UniquePaths2 uniquePaths2 = new UniquePaths2();
	        System.out.println(  uniquePaths2.uniquePathsWithObstacles2(obstacles));
	    }
	    static int count = 0;
	    public int uniquePathsWithObstacles(int[][] obstacles){
	        int count = helper(obstacles,0,0);
	        System.out.println(count);
	        return 0;
	    }
	
	
	//    public int helper(int[][] obstackes,int x,int y){
	//        if( y >= obstackes[0].length || x>=obstackes.length){
	//            return count;
	//        }
	//        if(x == obstackes.length-1 && y == obstackes[0].length-1){
	//            count++;
	//            return count;
	//        }
	//        if(obstackes[x][y] != 1){
	//            helper(obstackes,x+1,y);
	//            helper(obstackes,x,y+1);
	//        }
	//        return count;
	//    }
	
	
	    public int uniquePathsWithObstacles2(int[][] obstacleGrid) {
	        int c = helper(obstacleGrid,0,0);
	        return c;
	    }
	
	    public int helper(int[][] obstackes,int x , int y){
	        if( y >= obstackes[0].length || x>=obstackes.length){
	            return count;
	        }
	        if(x == obstackes.length-1 && y == obstackes[0].length-1 && obstackes[x][y] != 1){
	            count++;
	            return count;
	        }
	        if(obstackes[x][y] != 1){
	            helper(obstackes,x+1,y);
	            helper(obstackes,x,y+1);
	        }
	        return count;
	    }
	
	
	
	    public int dp(int[][] nums){
	        int width  = nums.length-1;
	        int[] dp = new int[width];
	        dp[0] = 1;
	        for(int[] row:nums){
	            for(int i = 0 ; i < width ; i++){
	                if(row[i] == 1) {
	                    dp[i] = 0;
	                }else if( i>0){
	                    dp[i] += dp[i-1];
	                }
	            }
	        }
	        return dp[width-1];
	    }
	}
	

```
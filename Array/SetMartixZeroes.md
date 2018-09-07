
- ### 代码

```java

package interview.array;
	
	public class SetMartixZeroes {
	
	
	    public static void main(String[] args){
	        int[][] matrix = new  int[][]{
	            {0,1,2,0},
	            {3,4,5,2},
	            {1,3,1,5}
	        };
	        setZeroes(matrix);
	        for(int[] row:matrix){
	           for(int i : row){
	               System.out.print(i);
	           }
	            System.out.println();
	        }
	    }
	
	    public static void setZeroes(int[][] maxtrix){
	        int m  = maxtrix.length;
	        int n = maxtrix[0].length;
	        for(int i=0;i<m;i++){
	            for(int j=i+1;j<n;j++){
	                if(maxtrix[i][j] == 0){
	                    for(int k = 0;k< m ;k++){
	                        maxtrix[k][j] = 0;
	                    }
	                    for(int l = 0;l< n ;l++){
	                        maxtrix[i][l] = 0;
	                    }
	                    break;
	                }
	            }
	        }
	    }
	}
	

```
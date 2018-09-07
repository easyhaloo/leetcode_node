
- ### 代码

```java

package interview.array;
	
	import java.util.Arrays;
	
	public class SpiralMatrix2 {
	
	
	    public static void main(String[] args){
	        int[][] ints = generateMatrix(3);
	       for(int i = 0;i< 3;i++){
	           for(int j= 0 ;j < 3;j++){
	               System.out.print(ints[i][j]+" ");
	           }
	           System.out.println();
	       }
	    }
	
	    public static int[][] generateMatrix(int n){
	        int [][] matrix = new int[n][n];
	
	        int left = 0;
	        int right = matrix[0].length-1;
	        int top = 0;
	        int buttom = matrix.length-1;
	        int idx= 1;
	
	        while(true){
	            for(int i=left;i<=right;i++){
	                matrix[top][i] = idx++;
	            }
	            top++;
	
	            if(left > right || top > buttom) break;
	
	            for(int j=top;j<=buttom;j++){
	                matrix[j][right] = idx++;
	            }
	            right--;
	            if(left > right || top > buttom) break;
	
	            for(int k = right;k>=left;k--){
	                matrix[buttom][k] = idx++;
	            }
	            buttom--;
	            if(left > right || top > buttom) break;
	
	            for(int m= buttom;m>=top;m--){
	                matrix[m][left] = idx++;
	            }
	            left++;
	            if(left > right || top > buttom) break;
	        }
	        return matrix;
	    }
	}
	

```
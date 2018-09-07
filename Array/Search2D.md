
- ### 代码

```java

package interview.array;
	
	public class Search2D {
	
	    public static void main(String[] args){
	        int[][] matrix = new int[][]{
	                {1,   3,  5,  7},
	        {10, 11, 16, 20},
	            {23, 30, 34, 50}
	        };
	        System.out.println(searchMatrix(matrix,5));
	    }
	
	    public static boolean searchMatrix(int[][] matrix,int target){
	
	        int col = matrix[0].length;
	        int left = 0 ;
	        int right = matrix[0].length*matrix.length-1;
	
	        while(left <= right){
	            int mid = left + (right - left) / 2;
	
	            if(matrix[mid/col][mid%col] == target){
	                return true;
	            }else if(matrix[mid/col][mid%col] < target){
	                left = mid + 1;
	            }else{
	                right = mid -1;
	            }
	        }
	        return false;
	    }
	}
	

```
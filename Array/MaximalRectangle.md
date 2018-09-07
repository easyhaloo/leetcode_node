
- ### 代码

```java

package interview.array;
	
	import java.util.Stack;
	
	public class MaximalRectangle {
	
	
	    public static void main(String[] args){
	        char[][] matrix = new char[][]{
	                {'1','0','1','0','0'},
	                {'1','0','1','1','1'},
	                {'1','0','1','1','1'},
	                {'1','0','0','1','0'}
	        };
	        System.out.println(maximalRectangle(matrix));
	
	    }
	
	    public static int maximalRectangle(char[][] matrix){
	
	        int res = 0;
	        int[] height = new int[matrix[0].length];
	        for(int i = 0 ; i< matrix.length ; i++){
	            for(int j = 0; j < matrix[i].length;j++){
	                height[j] = matrix[i][j] == '0' ? 0 : (1 + height[j]);
	                System.out.print(height[j]+" ");
	            }
	            System.out.println();
	            res = Math.max(res,largestRectangeleArea(res,height));
	        }
	        return res;
	    }
	
	
	    private  static  int largestRectangeleArea(int res,int[] height){
	        Stack<Integer> stack = new Stack<>();
	        for(int i = 0 ;  i<height.length;i++){
	            if(stack.isEmpty() || height[stack.peek()] < height[i] ) stack.push(i);
	            else {
	                int temp = stack.pop();
	                res = Math.max(res,height[temp]*(stack.isEmpty() ? i : (i - stack.peek() - 1)));
	                i--;
	            }
	        }
	        return res;
	    }
	}
	

```
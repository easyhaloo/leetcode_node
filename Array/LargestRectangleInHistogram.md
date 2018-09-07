
- ### 代码

```java

package interview.array;
	
	import java.util.Arrays;
	import java.util.Stack;
	
	public class LargestRectangleInHistogram {
	
	
	    public static void main(String[] args){
	        int[] nums = new int[]{2,1,5,6,2,3};
	        System.out.println(stack(nums));
	    }
	    public static int largestRectangleArea(int[] heights) {
	        int res = 0;
	        for(int i=0;i<heights.length;i++){
	            if(i+1 < heights.length && heights[i] <= heights[i+1]) continue;
	
	            int minH = heights[i];
	            for(int j = i ; j >= 0 ;j--){
	                minH = Math.min(heights[j],minH);
	                int maxArea = minH*(i-j+1);
	                res = Math.max(maxArea,res);
	            }
	        }
	        return res;
	    }
	
	
	
	    public static int stack(int[] heights){
	        Stack<Integer> indexStack =  new Stack<>();
	
	        int maxArea = 0;
	
	        int i = 0;
	        int[] h = Arrays.copyOf(heights,heights.length+1);
	
	        while(i< h.length){
	            if(indexStack.isEmpty() || h[indexStack.peek()] <= h[i]){
	                indexStack.push(i++);
	            }else {
	                int width = indexStack.pop();
	                maxArea = Math.max(maxArea,h[width]*(indexStack.isEmpty() ? i : (i-indexStack.peek()-1)));
	            }
	        }
	        return maxArea;
	    }
	}
	

```
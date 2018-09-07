
- ### 代码

```java

package interview.array;
	
	import java.util.Arrays;
	
	public class MissingNumber {
	
	
	    public static void main(String[] args){
	        int[] nums = new int[]{1};
	        System.out.println(method2(nums));
	    }
	    public static int missingNumber(int[] nums) {
	      int res = 0;
	      for(int i = 0 ; i< nums.length;i++){
	          res ^=(i+1)^nums[i];
	      }
	      return res;
	    }
	
	
	    public static int method2(int[] nums){
	        int sum =0;
	        for(int num : nums){
	            sum+=num;
	        }
	        int len = nums.length;
	        return len*(len+1)/2- sum;
	    }
	}
	

```
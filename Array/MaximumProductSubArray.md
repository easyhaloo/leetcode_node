
- ### 代码

```java

package interview.array;
	
	public class MaximumProductSubArray {
	
	
	
	
	    public static void main(String[] args){
	        int nums[] = new int[]{2,3,-2,4};
	        System.out.println(three(nums));
	    }
	
	
	    public static int one(int[] nums){
	        int max  = nums[0], min = nums[0],res = nums[0];
	        for(int i = 1;i<nums.length;i++){
	            int mx = max,mn = min;
	            max = Math.max(Math.max(nums[i],mx*nums[i]),mn*nums[i]);
	            min = Math.min(Math.min(nums[i],mn*nums[i]),mx*nums[i]);
	            res = Math.max(res,max);
	        }
	        return res;
	    }
	
	
	
	    public static int two(int[] nums){
	        int max = nums[0], min = nums[0],res = nums[0];
	        for(int i = 1;i<nums.length ;i++){
	            if(nums[i] > 0){
	                max = Math.max(max*nums[i],nums[i]);
	                min = Math.min(min*nums[i],nums[i]);
	            }else{
	                int t = max;
	                max = Math.max(min*nums[i],nums[i]);
	                min =Math.min(t*nums[i],nums[i]);
	            }
	            res = Math.max(max,res);
	        }
	        return res;
	    }
	
	
	    public static int three(int[] nums){
	        int res = nums[0],prod =1 , len = nums.length;
	        for(int i = 0;i<len;i++){
	            res = Math.max(res,prod*=nums[i]);
	            if(nums[i] == 0) prod = 1;
	        }
	
	        prod = 1;
	        for(int i = len-1 ; i >= 0 ;i--){
	            res = Math.max(res,prod*=nums[i]);
	            if(nums[i] == 0) prod = 1;
	        }
	        return res;
	    }
	}
	

```
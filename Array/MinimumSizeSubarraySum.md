
- ### 代码

```java

package interview.array;
	
	public class MinimumSizeSubarraySum {
	
	
	
	    public static void main(String[] args){
	        int[] nums=  new int[]{2,3,1,2,4,3};
	        System.out.println(minSubArrayLen(7,nums));
	    }
	    public static int minSubArrayLen(int s,int[] nums){
	       int res = Integer.MAX_VALUE,left = 0,sum = 0;
	
	       for(int i = 0 ; i <  nums.length;i++){
	           sum += nums[i];
	           while(sum >=s && left <= i){
	                res = Math.min(res,i-left+1);
	                sum-=nums[left++];
	           }
	       }
	       return res == Integer.MAX_VALUE ? 0 : res;
	    }
	
	
	
	}
	

```
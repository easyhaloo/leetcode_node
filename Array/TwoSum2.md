
- ### 代码

```java

package interview.array;
	
	public class TwoSum2 {
	
	
	    public static void main(String[] args){
	        int[] nums = new int[]{2,3,4};
	        int[] res = twoSum(nums,6);
	        System.out.println(res[0]+res[1]);
	    }
	
	
	    public static int[] twoSum(int[] nums,int target){
	        int[] res = new int[]{0,0};
	        int left = 0 , right = nums.length-1;
	        while(left < right){
	            if(target == nums[right] + nums[left]) {
	                return new int[]{left+1,right+1};
	            }else if(target < nums[right] + nums[left]){
	                right--;
	            }else{
	                left++;
	            }
	
	        }
	        return res;
	    }
	 }
	

```
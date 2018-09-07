
- ### 代码

```java

package interview.array;
	
	public class JumpGame {
	
	
	    public boolean canJump(int[] nums){
	        int max = 0;
	        for(int i= 0;i<nums.length;i++){
	            if(i > max) return false;
	            max = Math.max(max,nums[i]+i);
	        }
	        return true;
	    }
	
	
	    public boolean canJumpRevers(int[] nums){
	        int last = nums.length-1;
	        for(int i = nums.length-2;i>=0;i--){
	            if(nums[i]+i >= last) last = i;
	        }
	        return last <= 0 ;
	    }
	}
	

```
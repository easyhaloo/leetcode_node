
- ### 代码

```java

package interview.array;
	
	public class RemoveDuplicatesArray2 {
	
	    public int removeDuplicates(int[] nums){
	
	        int count = 1;
	        int len = nums.length;
	        int cur = 1,prev=  0;
	        while(cur < len){
	            if(nums[prev] == nums[cur] && count == 0) cur++;
	            else{
	                if(nums[prev] ==nums[cur]) count--;
	                else count =1;
	                nums[++prev] = nums[++cur];
	            }
	        }
	        return prev+1;
	    }
	
	
	    public int sovle2(int[] nums){
	        int idx = 0;
	        for(int n : nums){
	            if( idx <2 || n > nums[idx-2]){
	                nums[idx++] = n;
	            }
	        }
	        return idx;
	    }
	}
	

```
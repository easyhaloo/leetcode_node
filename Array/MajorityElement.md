
- ### 代码

```java

package interview.array;
	
	public class MajorityElement {
	
	
	
	    public static void main(String[] args){
	        int[] nums = new int[]{2,2,1,1,1,2,2};
	        System.out.println(majorityElementByBit(nums));
	    }
	    public static int majorityElement(int[] nums){
	        int major = nums[0] , count = 1;
	        for(int i = 1;i<nums.length;i++){
	            if(count == 0){
	                count++;
	                major = nums[i];
	            }else if(major == nums[i]){
	                count++;
	            }else{
	                count--;
	            }
	        }
	        return major;
	    }
	
	
	    public static int majorityElementByBit(int[] nums){
	        int res = 0;
	        int bit[] = new int[32];
	        for(int num:nums){
	            for(int i = 0; i< 32;i++){
	                if((num>>(32-i)&1) == 1){
	                    bit[i] ++;
	                }
	            }
	        }
	        for(int i = 0 ; i < 32 ; i++){
	            bit[i] = bit[i] > nums.length/2 ? 1:0;
	            res+=bit[i]*(1<<(32-i));
	        }
	        return res;
	    }
	}
	

```

- ### 代码

```java

package interview.array;
	
	import java.util.ArrayList;
	import java.util.List;
	
	public class SummaryRanges {
	
	    public static void main(String[] args){
	        int [] nums = new int[]{0,1,2,4,5,7};
	        System.out.println(summaryRanges(nums));
	    }
	
	
	    public static List<String> summaryRanges(int[] nums){
	        List<String> res = new ArrayList<>();
	        if(nums.length == 0) return res;
	        if(nums.length == 1) {
	            res.add(nums[0]+"");
	            return res;
	        }
	
	        int left = 0 , right = 1;
	        while(right < nums.length){
	            if(nums[right] - nums[right-1] != 1){
	                if(right-1-left == 0) res.add(nums[right-1]+"");
	                else if(right-1-left > 0){
	                    res.add(nums[left]+"->"+nums[right-1]);
	                }
	
	                left = right;
	                if(right == nums.length-1){
	                    res.add(nums[right]+"");
	                }
	            }else{
	                if(right == nums.length-1){
	                    res.add(nums[left]+"->"+nums[right]);
	                }
	            }
	            right++;
	        }
	        return res;
	    }
	}
	

```

- ### 代码

```java

package interview.array;
	
	import java.util.ArrayList;
	import java.util.Arrays;
	import java.util.List;
	
	public class ThreeSum {
	
	    public static void main(String[] args){
	        int nums[] = new int[]{-2,0,1,1,2};
	         System.out.println(threeSum(nums));
	    }
	
	    public static  List<List<Integer>> threeSum(int[] nums){
	        Arrays.sort(nums);
	        List<List<Integer> > res = new ArrayList<>();
	        for(int i = 0;i<nums.length-2;i++){
	            if(i >0 && nums[i] == nums[i-1]) continue;
	            else {
	                int target = -nums[i];
	                int left = i+1,right = nums.length-1;
	                while(left < right){
	                    if(nums[left] + nums[right] == target){
	                        res.add(Arrays.asList(nums[i],nums[left],nums[right]));
	                        left++;right--;
	
	                        while (left < right && nums[left] == nums[left-1]){
	                            left++;
	                        }
	                        while (left < right && nums[right] == nums[right+1]){
	                            right--;
	                        }
	                    }else if(nums[left] + nums[right] < target){
	                        left++;
	                    }else{
	                        right--;
	                    }
	
	                }
	            }
	        }
	
	        return res;
	
	     }
	
	
	
	
	}
	

```
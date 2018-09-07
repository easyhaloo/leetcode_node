
- ### 代码

```java

package interview.array;
	
	import java.util.Arrays;
	
	public class MaxumumGap {
	
	     public int maximumGap(int[] nums){
	         if(nums.length < 3) return 0;
	
	         int max = nums[0],min = nums[0];
	         for(int i : nums){
	             max = Math.max(max,i);
	             min = Math.min(min,i);
	         }
	
	         int len = (max -min)/ nums.length+1;
	         int buckets = (max - min) / len+1;
	
	         int[] bMin = new int[nums.length];
	         int[] bMax = new int[nums.length];
	         Arrays.fill(bMin,Integer.MIN_VALUE);
	         Arrays.fill(bMax,Integer.MAX_VALUE);
	
	         for(int i:nums){
	             if(i == min || i == max) continue;
	             int idx = (i-min)/len;
	             bMin[idx] = Math.min(i,bMin[idx]);
	             bMax[idx] = Math.max(i,bMax[idx]);
	         }
	
	         int maxGap = Integer.MIN_VALUE;
	         int pre = min;
	         for(int i = 0 ; i< nums.length-1;i++){
	             if(bMin[i] == Integer.MAX_VALUE && bMax[i] == Integer.MIN_VALUE) continue;
	             maxGap  = Math.max(maxGap,bMin[i] - pre);
	             pre = bMax[i];
	         }
	         maxGap = Math.max(maxGap,max-pre);
	         return maxGap;
	     }
	}
	

```
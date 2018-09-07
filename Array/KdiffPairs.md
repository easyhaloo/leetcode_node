
- ### 代码

```java

package interview.array;
	
	import java.util.Arrays;
	import java.util.HashMap;
	import java.util.Map;
	
	
	public class KdiffPairs {
		
		public static void main(String[] args) {
	//		System.out.println(findPairs2(new int[] {3, 1, 4, 1, 5},2));
		}
		
		public static int findPairs(int[] nums,int k) {
			int ans = 0;
			Arrays.sort(nums);
			for(int i=0,j=0;i<nums.length;i++) {
				for(j = Math.max(j, i+1);j<nums.length&&nums[j]-nums[i]<k;j++); 
				if(j<nums.length&&nums[j]-nums[i] == k)ans++;
				while(i+1<nums.length&&nums[i] == nums[i+1])i++;
			}
			return ans;
		}
		
		
	//	public static int findPairs2(int[] nums,int k) {
	//		if(nums ==null || nums.length < 2|| k< 0)
	//			return 0;
	//
	//		Map<Integer, Integer> map = new HashMap<Integer,Integer>();
	//		int count = 0;
	//		for(int  i:nums) {
	//			map.put(i, map.getOrDefault(i, 0)+1);
	//		}
	//
	//		for(Map.Entry<Integer,Integer> entry:map.entrySet()) {
	//			if(k == 0) {
	//				if(entry.getValue() >= 2) {
	//					count++;
	//				}
	//			}else {
	//				if(map.containsKey(entry.getKey()+k)) {
	//					count++;
	//				}
	//			}
	//		}
	//		return count;
	//	}
	}
	

```
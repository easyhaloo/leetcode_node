
- ### 代码

```java

package interview.array;
	
	import java.util.ArrayList;
	import java.util.Arrays;
	import java.util.List;
	
	public class Subsets2 {
	
	    public static void main(String[] args){
	        int[] nums=  new int[]{1,2,2};
	        System.out.println(method(nums));
	    }
	
	    public static List<List<Integer>> subsetsWithDup(int[] nums){
	         List<List<Integer>> res = new ArrayList<>();
	         Arrays.sort(nums);
	         dfs(nums,new ArrayList<Integer>(),res,0);
	        return res;
	    }
	
	    private static void dfs(int[] nums,List<Integer> temp , List<List<Integer>>  res,int start){
	        res.add(new ArrayList<>(temp));
	        for(int i = start;i<nums.length;i++){
	            temp.add(nums[i]);
	            dfs(nums,temp,res,i+1);
	            temp.remove(temp.size()-1);
	            while( i+1 < nums.length && nums[i] == nums[i+1]) i++;
	        }
	    }
	
	
	    public static List<List<Integer>> method(int[] nums){
	        List<List<Integer>> res = new ArrayList<>();
	        if(nums.length <= 0) return res;
	        res.add(new ArrayList<Integer>());
	        Arrays.sort(nums);
	
	        int begin = 0;
	        for(int i = 0 ; i< nums.length;i++){
	            if(i == 0 || nums[i] != nums[i-1]) begin = 0;
	            int size = res.size();
	            for(int j = begin ; j <size;j++){
	                List<Integer> a = new ArrayList<>(res.get(j));
	                a.add(nums[i]);
	                res.add(a);
	            }
	            begin = size;
	        }
	        return res;
	    }
	}
	

```
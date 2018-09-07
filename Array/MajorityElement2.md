
- ### 代码

```java

package interview.array;
	
	import java.util.ArrayList;
	import java.util.List;
	
	public class MajorityElement2 {
	
	    public static void main(String[] args){
	        int [] nums = new int[]{1,1,1,3,3,2,2,2};
	        System.out.println(majorityElement(nums));
	    }
	
	    /**
	     * 鎽╁皵鎶曠エ娉� Moore Voting
	     * 浠绘剰涓�涓暟缁勫嚭鐜版鏁板ぇ浜巒/3鐨勪紬鏁版渶澶氭湁涓や釜
	     * @param nums
	     * @return
	     */
	    public static List<Integer> majorityElement(int[] nums){
	        int m = 0 , n = 0 , cm = 0 , cn = 0;
	        List<Integer> res = new ArrayList<>();
	        for(int num : nums){
	            if(m == num) cm++;
	            else if(n == num) cn++;
	            else if(cm == 0) {m = num;cm = 1;}
	            else if(cn == 0) {n = num;cn = 1;}
	            else {cm--;cn--;}
	        }
	        cm = cn = 0;
	        for(int num : nums){
	            if(num == m ) cm++;
	            else if(num == n) cn++;
	        }
	        if(cm > nums.length/3) res.add(m);
	        if(cn > nums.length/3) res.add(n);
	        return res;
	    }
	}
	

```
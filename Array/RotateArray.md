
- ### 代码

```java

package interview.array;
	
	public class RotateArray {
	
	
	    public static void main(String[] args){
	
	        int[] nums1=  new int[]{1,2,3,4,5,6,7,8,9};
	        rotate2(nums1,2);
	        for(int i:nums1){
	           System.out.print(i+"  ");
	       }
	    }
	    public  static void rotate(int[] nums,int k){
	        k %= nums.length;
	        reverse(nums,0,nums.length-1);
	        reverse(nums,0,k-1);
	            reverse(nums,k,nums.length-1);
	
	    }
	
	    private static void reverse(int nums[],int left,int right){
	        while(left < right){
	            int temp = nums[left];
	            nums[left] = nums[right];
	            nums[right] =temp;
	            left++;
	            right--;
	        }
	    }
	
	
	    public static void rotate2(int nums[] ,int k){
	        if(nums == null || nums.length < 0 ) return ;
	        int start = 0;
	        for(int n = nums.length; (k%=n) > 0; n-=k){
	            for(int j = 0 ; j< k ;j++){
	                swap(nums,start+j,start+j+n-k);
	            }
	            start+=k;
	        }
	    }
	
	    private static void swap(int[] nums,int start,int end){
	        int temp = nums[start];
	        nums[start] = nums[end];
	        nums[end] =temp;
	    }
	}
	

```
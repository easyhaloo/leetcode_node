
- ### 代码

```java

package interview.array;
	
	public class MoveZeroes {
	
	
	    public static void main(String[] args){
	        int[] nums = new int[]{0,0,0,1,1};
	        moveZero(nums);
	        for(int num : nums){
	            System.out.println(num);
	        }
	    }
	
	
	    public static void moveZero(int nums[]){
	      for(int i = 0 , j = 0 ; i < nums.length;i++){
	          if(nums[i] != 0 ){
	                swap(nums,i,j++);
	          }
	      }
	    }
	    private static void swap(int nums[],int start,int end){
	        int temp = nums[start];
	        nums[start] = nums[end];
	        nums[end]  = temp;
	    }
	}
	

```
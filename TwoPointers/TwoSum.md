Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

`Example:`
```java
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
- - -

### 解析：
> 这道题目是求解从数组中获取两个值，使得两个值的和与目标值相等.这道题可是使用双指针的方式来解答，不过此方法比较麻烦。

>我们需要维护两个数组，第一个是原数组，目的是保证索引，还要clone一个原数组，对clone的数组排序，然后开始建立双指针，一个从前往后扫描，一个从后往前扫描，将两者相加，小于目标值Left指针右移，大于目标值right指针左移，遇见相等的情况，需要记录下这两个值，然后两者同时移动，或者break掉。

> 然后从原来的数组中循环比较，获取原始数组中的索引下标。最后对结果数组排序即可。
### 代码：
```java
public  static int[] towSum2(int[] nums,int target) {
		 int[] temp = nums.clone();
		 Arrays.sort(nums);
		 int[] result = {-1,-1};
		 int left = 0,
			 right = nums.length-1;
		 int tempA = 0,tempB = 0;
		 while(left < right) {
			if(nums[left] + nums[right] == target) {
				tempA = nums[left];
				tempB = nums[right];
				left++;
				right--;
			}else if(nums[left] + nums[right] < target) {
				left++;
			}else {
				right--;
			}
		}

		 for(int i=0;i<nums.length;i++) {
			 if(temp[i] == tempA) {
				 result[0] = i;
				 break;
			 }
		 }

		 if(tempA!=tempB) {
			 for(int i=0;i<nums.length;i++) {
				 if(temp[i] == tempB) {
					 result[1] = i;
					 break;
				 }
			 }
		 }else {
			 for(int i=0;i<nums.length;i++) {
				 if(temp[i] == tempB && i!=result[0]) {
					 result[1] = i;
					 break;
				 }
			 }
		 }

		Arrays.sort(result);
		return result;
	 }
```

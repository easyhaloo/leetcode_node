Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

`Example:`
```java
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
- - -

- ### 解析：
> 这道题目是求解从数组中获取两个值，使得两个值的和与目标值相等.最直接的方式是采用暴力法，循环遍历两次数组，先锁定一个值，然后从数组中选取目标值与已选中值的差。如何匹配直接返回结果，不匹配则重选锁定新值，依次循环。
- ### 代码：
```java
public int[] twoSum(int[] nums, int target) {
    for (int i = 0; i < nums.length; i++) {
        for (int j = i + 1; j < nums.length; j++) {
            if (nums[j] == target - nums[i]) {
                return new int[] { i, j };
            }
        }
    }
    return new int[]{};
}
```

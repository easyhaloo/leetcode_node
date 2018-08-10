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
> 这道题目是求解从数组中获取两个值，使得两个值的和与目标值相等.采用HashMap，使用一个HashMap来建立一种映射关系：K 存储的是第二个需要匹配的数,V 第一个值的下标索引。循环检测Map中是否包含这个数，如果包含证明找到了结果，直接返回。
### 代码：
```java
public static int[] twoSum(int[] nums, int target) {
     Map<Integer,Integer> map = new HashMap<>();
     for(int i=0 ; i<nums.length;i++) {
       int sub = target - nums[i];
       if(map.containsKey(nums[i])) {
         return new int[] {i,map.get(nums[i])};
       }
       map.put(sub, i);
     }
     return new int[]{0,0};
}
```

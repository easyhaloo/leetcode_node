Given an array of integers, 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements that appear twice in this array.

Could you do it without extra space and in O(n) runtime?



**Example:**

```java
Input:
[4,3,2,7,8,2,3,1]

Output:
[2,3]
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/find-all-duplicates-in-an-array
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 解析

> 此题是需要将数组中出现过两次的数纪录下来。必须在o(n)，且没有额外空间的情况下。
>
> 但是题目中给出了一个关键的信息 **1 ≤ a[i] ≤ n**，数组中的元素必定是在数组长度之内的，所以我们可以使用数组中的元素值来代替原数组索引。
>
> - 每次遍历当遇见nums[nums[i]-1] > 0  我们需要对其*-1
> - 每次遇见nums[nums[i]-1] < 0 ，则添加到结果集中
>
> 注意**nums[i]-1**需要对其取绝对值。





### 代码

```java
class Solution {
    public List<Integer> findDuplicates(int[] nums) {
    List<Integer> ret = new ArrayList<>();
    for (int num : nums) {
      if (nums[Math.abs(num) - 1] > 0) {
        nums[Math.abs(num) - 1] *= -1;
      } else {
        ret.add(Math.abs(num));
      }
    }
    return ret;
    }
}
```


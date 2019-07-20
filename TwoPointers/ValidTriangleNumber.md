  

Given an array consists of non-negative integers, your task is to count the number of triplets chosen from the array that can make triangles if we take them as side lengths of a triangle.



**Example 1:**

```verilog
Input: [2,2,3,4]
Output: 3
Explanation:
Valid combinations are: 
2,3,4 (using the first 2)
2,3,4 (using the second 2)
2,2,3
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/valid-triangle-number
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 解析

> 此题大意是求数组元素中，能够组成三角形的个数。
>
> 根据三角形定理可得： 两边之和大于第三边 ，两边之差小于第三边
>
> 有数组的特性，我们可以选择对数组进行排序，这样 a1+a2> a3。只要保证满足此条件，即可保证能正确组织三角形。
>
> 这里暴力破解肯定超时，所以我们选择优化，采用双指针。每次固定一个边，然后再选取其他边，
>
> 针对排序后的数组，我们可以选择数组的最后一列，然后遍历前面的元素，保证 a[i] + a[j] > a[last]。
>
> 这样可以保证有 j-i种，然后我们移动last，向前推进。

### 代码

```java
    public int triangleNumber(int[] nums) {
         if (nums == null || nums.length < 3) return 0;
        Arrays.sort(nums);
        int ret = 0;
        int n = nums.length;
        for (int i = n - 1; i >= 2; i--) {
            int l = 0, r = i - 1;
            while (l < r) {
                if (nums[l] + nums[r] > nums[i]) {
                    ret += r - l;
                    --r;
                } else {
                    l++;
                }
            }
        }
        return ret;
    }
```


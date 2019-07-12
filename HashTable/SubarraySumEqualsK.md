**Example 1:**

```
Input:nums = [1,1,1], k = 2
Output: 2
```

**Note:**

1. The length of the array is in range [1, 20,000].
2. The range of numbers in the array is [-1000, 1000] and the range of the integer k is [-1e7, 1e7].

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/subarray-sum-equals-k
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。







### 解析

>  求数组中连续的子数组和为k，求这样子数组的个数。这题有点类似`TwoSum`，同样是求和，不过方式变了，一个是求个数，一个是求内容。
>
> 此时，我们可以借助一个HashMap来辅助。
>
> 由于其连续的特性，我们可以知道sum[i,j] = sum[0,j] - sum[0,i]。因此，我们可以使用HashMap来存储已经求解过的sum。例如sum[0,i]。
>
> 每次计算完sum后，然后使用sum-k ，sum-k就是我们所需要的补集。可以去查询map获取对应的计算结果集。





### 代码

```java
public int subarraySum(int[] nums, int k) {
    int cnt = 0;
    Map<Integer, Integer> map = new HashMap<>();
    int sum = 0;
  	// 下面的可以换成map.put(0,1) 0也要进行计算的，防止数组元素中就存在等于k的情况。
    map.put(sum, map.getOrDefault(sum, 0) + 1);
    for (int num : nums) {
      sum += num;
      int pSum = sum - k;
      if (map.containsKey(pSum)) {
        cnt += map.get(pSum);
      }
      map.put(sum, map.getOrDefault(sum, 0) + 1);
    }
    return cnt;
  }
```


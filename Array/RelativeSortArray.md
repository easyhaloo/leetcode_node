Given two arrays arr1 and arr2, the elements of arr2 are distinct, and all elements in arr2 are also in arr1.

Sort the elements of arr1 such that the relative ordering of items in arr1 are the same as in arr2.  Elements that don't appear in arr2 should be placed at the end of arr1 in ascending order.

 

**Example 1:**

```verilog
Input: arr1 = [2,3,1,3,2,4,6,7,9,2,19], arr2 = [2,1,4,3,9,6]
Output: [2,2,2,1,4,3,3,9,6,7,19]
```


Constraints:

arr1.length, arr2.length <= 1000
0 <= arr1[i], arr2[i] <= 1000
Each arr2[i] is distinct.
Each arr2[i] is in arr1.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/relative-sort-array
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。





### 解析

> 首先可以使用TreeMap对arr1中的元素按Key进行排序，然后统计key的出现次数。
>
> 由于arr2中的元素都会在arr1中，所以我们可以按照map中维护的每个元素个数来进行填充，
>
> 当遍历完arr2后，剩下对treemap的元素遍历输出追加到结果数组中



### 代码

```java
 public int[] relativeSortArray(int[] arr1, int[] arr2) {
        if (arr1.length == 0) return arr1;

        Map<Integer, Integer> countMap = new TreeMap<>();

        for (int arr : arr1) {
            countMap.put(arr, countMap.getOrDefault(arr, 0) + 1);
        }

        int[] ret = new int[arr1.length];
        int index = 0;
        for (int i = 0; i < arr2.length; i++) {
            Integer count = countMap.remove(arr1[i]);
            while (count-- >= 0) {
                ret[index] = arr1[i];
                index++;
            }
        }

        for (Map.Entry<Integer, Integer> entry : countMap.entrySet()) {
            Integer value = entry.getKey();
            Integer count = entry.getValue();
            while (count-- >= 0) {
                ret[index] = value;
                index++;
            }
        }

        return ret;
    }
```


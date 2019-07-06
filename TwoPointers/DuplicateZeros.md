Given a fixed length array arr of integers, duplicate each occurrence of zero, shifting the remaining elements to the right.

Note that elements beyond the length of the original array are not written.

Do the above modifications to the input array in place, do not return anything from your function.



Example 1:

Input: [1,0,2,3,0,4,5,0]
Output: null
Explanation: After calling your function, the input array is modified to: [1,0,0,2,3,0,0,4]

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/duplicate-zeros
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。





### 解析

>  复制数组中的0，但是必须保证数组的长度不变。 
>
> 可以使用双指针来做
>
> 1. 建立fast，slow指针。 slow指针的位置就是操作完毕后数组的尾部边界，fast指针的位置就是原数组 的长度 
> 2. 从后向前遍历，将slow指针指向的元素赋值给fast指针，slow指针指向0时，fast写两次
> 3. 同时移动fast,slow指针 





### 代码 

```java
 public void duplicateZeros(int[] arr) {
                int len = arr.length;
        int slow = 0, fast = 0;
        while (fast < len) {
            if (arr[slow] == 0) fast++;
            slow++;
            fast++;
        }

        slow--;
        fast--;
        while (slow >= 0) {
            if (fast < len) arr[fast] = arr[slow];
            if (arr[slow] == 0) arr[--fast] = arr[slow];
            slow--;
            fast--;
        }
    }
```


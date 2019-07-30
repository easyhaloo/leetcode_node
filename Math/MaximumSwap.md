Given a non-negative integer, you could swap two digits at most once to get the maximum valued number. Return the maximum valued number you could get.

**Example 1:**

```java
Input: 2736
Output: 7236
Explanation: Swap the number 2 and the number 7.
```

**Example 2:**

```java
Input: 9973
Output: 9973
Explanation: No swap.
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/maximum-swap
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 解析

> 可以先对给定的数字转换为字符串，然后对其进行排序(升序)。
>
> 然后和原数字序列进行比较，从高位开始以此比较，如果两个序列当前位置不一样，则需要进行替换。
>
> 例如：
>
> 2736 
>
> 7632
>
> 此时第一位不一样，所以我们需要交换两个序列的第一位。



### 代码

```java
class Solution {
    public int maximumSwap(int num) {
    char[] orderNum = Integer.toString(num).toCharArray();
    Arrays.sort(orderNum);
    char[] oldNum = Integer.toString(num).toCharArray();
    int diff = -1;
    for (int i = 0; i < orderNum.length; i++) {
      if (oldNum[i] != orderNum[orderNum.length - 1 - i]) {
        diff = i;
        break;
      }
    }

    if (diff == -1) return num;

    for (int i = oldNum.length - 1; i >= diff; i--) {
      if (oldNum[i] == orderNum[orderNum.length - 1 - diff]) {
        char tmp = oldNum[diff];
        oldNum[diff] = oldNum[i];
        oldNum[i] = tmp;
        break;
      }
    }
    return Integer.parseInt(new String(oldNum));
    }
}
```


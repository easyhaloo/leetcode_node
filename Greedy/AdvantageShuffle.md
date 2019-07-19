Given two arrays A and B of equal size, the advantage of A with respect to B is the number of indices i for which A[i] > B[i].

Return any permutation of A that maximizes its advantage with respect to B.



**Example 1:**

```verilog
Input: A = [2,7,11,15], B = [1,10,4,11]
Output: [2,11,7,15]
```



**Example 2:**

```verilog
Input: A = [12,24,8,32], B = [13,25,32,11]
Output: [24,32,8,12]
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/advantage-shuffle
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。





### 解析

> 1. 我们可以首先对两个数组进行排序。对B数组进行排序的同时，我们需要记录下原始的索引。
> 2. 当对排序后对数组进行比较时，我们可以取出原始的索引进行填充。
> 3. 比较时，使用贪心算法。 由于题目中求的A[i]>B[i]。 那么排序完毕后,A[maxIndex] > B[maxIndex]。如果不满足，此时开启贪心策略，需要将A[minIndex] 放在结果集中，这样就保证A[maxIndex]还能对后续对B[maxIndex]保持统治地位。典型对田忌赛马。





### 代码

```java
public int[] advantageCount(int[] A, int[] B) {
    if (A == null || B == null) return A;
    // 排序集合A
    Arrays.sort(A);
    // 索引排序
    int[] indexs = quickSort(B);
    int[] ret = new int[A.length];
    int index = B.length - 1;
    int maxIndex = A.length - 1;
    int minIndex = 0;
    while (index >= 0) {
      if (B[index] < A[maxIndex]) {
        ret[indexs[index]] = A[maxIndex];
        maxIndex--;
        index--;
      } else {
        ret[indexs[index]] = A[minIndex];
        index--;
        minIndex++;
      }
    }

    return ret;
  }


  private int[] quickSort(int[] b) {
    int[] indexs = new int[b.length];
    int i = 0;
    while (i < b.length) {
      indexs[i++] = i;
    }
    partition(indexs, b, 0, b.length - 1);
    return indexs;
  }

  private void partition(int[] indexs, int[] arr, int start, int end) {

    if (end <= start) return;

    int r = end;
    int l = start + 1;
    int flag = arr[start];
    while (true) {
      while (r >= start && arr[r] >= flag) {
        r--;
      }
      while (l <= end && arr[l] <= flag) {
        l++;
      }
      if (r <= l) break;
      swap(indexs, l, r);
      swap(arr, l, r);
    }
    swap(indexs, start, l - 1);
    swap(arr, start, l - 1);
    partition(indexs, arr, start, l - 2);
    partition(indexs, arr, l, end);
  }


  private void swap(int[] arr, int l, int r) {
    int temp;
    temp = arr[l];
    arr[l] = arr[r];
    arr[r] = temp;
  }

```





### 解析2

>  可以使用hashmap+linklist。
>
> 首先建立b中数组元素于list中的对应关心，list中保存的是a数组中大于b的元素。
>
> 还需要建立一个补充队列list，用于存放小于b的元素。





### 代码

```java
class Solution {
    public int[] advantageCount(int[] A, int[] B) {
        if (A == null || B == null) return A;
    int[] aClone = A.clone();
    int[] bClone = B.clone();
    Arrays.sort(aClone);
    Arrays.sort(bClone);

    Map<Integer, Deque<Integer>> map = new HashMap<>();
    for (int b : B) {
      map.put(b, new LinkedList<>());
    }

    Deque<Integer> remaining = new LinkedList<>();
    int j = 0;
    for (int a : aClone) {
      if (a > bClone[j]) {
        map.get(bClone[j++]).add(a);
      } else {
        remaining.add(a);
      }
    }

    int[] ret = new int[A.length];

    for (int i = 0; i < B.length; i++) {
      if (map.get(B[i]).size() > 0) {
        ret[i] = map.get(B[i]).pop();
      } else {
        ret[i] = remaining.pop();
      }
    }

    return ret;
    }
}
```


Given a non-empty array of integers, return the **k** most frequent elements.



**Example 1:**

```java
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

**Example 2:**

```java
Input: nums = [1], k = 1
Output: [1]
```



### 解析

> 题目大意： 给定一个非空数组，需要求出,出现频率大于等于K次数的元素
>
> 这道题简单解法可以直接使用`排序+slice`这种做法，但是这样一来肯定会超时。
>
> 下面我们将使用两种不同的解法：
>
> -  HashMap + Heap
> - HashMap + 桶排序



#### HashMap + Heap

​	在这里我们使用HashMap记录每个元素出现的次数，Heap使用来排序的，这里使用小顶堆，通过固定堆的大小，我们使用维护一个K大小的堆，将多余的元数依次与堆顶进行比较，如果比堆顶大，此时我们将选择替换堆顶，依次类推，将后面`nums.length-k`个元素比较完。剩下的堆即为所求。



**代码**

```java
 public List<Integer> topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
     // hash表记录出现次数
        for (Integer num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
     // 构建最小堆
        Queue<Integer> queue = new PriorityQueue<>((o1, o2) -> map.get(o2) - map.get(o1));
        map.forEach((key, value) -> queue.add(key));
        List<Integer> ret = new ArrayList<>();
        int i = 0;
        int endpos = Math.min(k, map.size());
        while (i++ < endpos) {
            ret.add(queue.poll());
        }
        return ret;
    }
```



#### HahsMap + 桶排序

​		HashMap同样是为了记录元素出现次数，而比较方式由堆替换位桶排序的方式。桶排序的的优势在于入桶操作为O(1)时间复杂度。

​		这里桶使用的是一个ArrayList数组，我们以元素出现的次数作为数组的下标索引，然后以实际出现的元素表示为List中的真正元素，相当于一种逆向的存储方式，key为value，value为索引。

​		这里需要使用的ArrayList是由于可能出现不同元素出现相同的次数，为了防止索引相同，key会存在被覆盖的危险。

​		最后，我们逆向取ArrayList数组中的元素，由于是桶排序，下标为元素出现的次数，所以需要逆向遍历。当遍历完或者取完k个元素即可结束。



```java
 public  List<Integer> topKFrequentV(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        for (Integer num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }

        List<Integer>[] peers = new ArrayList[nums.length + 1];

        for (Integer key : map.keySet()) {
            int index = map.get(key);
            if (peers[index] == null) {
                peers[index] = new ArrayList<>();
            }
            peers[index].add(key);

        }

        List<Integer> ret = new ArrayList<>();
        for (int i = peers.length - 1; i >= 0 && ret.size() < k; i--) {
            if (peers[i] == null) continue;
            ret.addAll(peers[i]);
        }
        return ret;
    }
```






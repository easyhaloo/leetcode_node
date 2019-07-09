#### [Insert Delete GetRandom O(1)](https://leetcode-cn.com/problems/insert-delete-getrandom-o1/)

Design a data structure that supports all following operations in average O(1) time.

1. insert(val): Inserts an item val to the set if not already present.
2. remove(val): Removes an item val from the set if present.
3. getRandom: Returns a random element from current set of elements. Each element must have the same probability of being returned.



**Example:**

```java
// Init an empty set.
RandomizedSet randomSet = new RandomizedSet();

// Inserts 1 to the set. Returns true as 1 was inserted successfully.
randomSet.insert(1);

// Returns false as 2 does not exist in the set.
randomSet.remove(2);

// Inserts 2 to the set, returns true. Set now contains [1,2].
randomSet.insert(2);

// getRandom should return either 1 or 2 randomly.
randomSet.getRandom();

// Removes 1 from the set, returns true. Set now contains [2].
randomSet.remove(1);

// 2 was already in the set, so return false.
randomSet.insert(2);

// Since 2 is the only number in the set, getRandom always return 2.
randomSet.getRandom();
```



来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/insert-delete-getrandom-o1
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 解析

>  该题是设计题，设计一个随机的set集合。而且保证所有操作都必须为O(1)复杂度。
>
> 我们需要借助两个Map来实现，一个Map装value->index,另外一个是index->value的映射关系。
>
> add操作很容易做到这一点，但是，我们需要remove就不是那么方便了，此时我们需要使用一个tick，讲尾部的元素替换到被删除的节点上，然后移除尾部节点。





### 代码

```java
class RandomizedSet {

   private final Map<Integer, Integer> valueMap;
  private final Map<Integer, Integer> indexMap;

  private int index = 0;

  /**
   * Initialize your data structure here.
   */
  public RandomizedSet() {
    valueMap = new HashMap<>();
    indexMap = new HashMap<>();
  }

  /**
   * Inserts a value to the set. Returns true if the set did not already contain the specified element.
   */
  public boolean insert(int val) {
    if (!valueMap.containsKey(val)) {
      valueMap.put(val, index);
      indexMap.put(index, val);
      index++;
      return true;
    }
    return false;
  }

  /**
   * Removes a value from the set. Returns true if the set contained the specified element.
   */
  public boolean remove(int val) {
    if (valueMap.size() == 0) return false;
    Integer oldIndex = valueMap.get(val);
    if (oldIndex == null) return false;

    if (oldIndex != valueMap.size() - 1) {
      Integer last = indexMap.get(valueMap.size() - 1);
      valueMap.put(last, oldIndex);
      indexMap.put(oldIndex, last);
    }

    valueMap.remove(val);
    index--;
    return true;
  }

  /**
   * Get a random element from the set.
   */
  public int getRandom() {
    Random random = new Random();
    int index = random.nextInt(valueMap.size());
    System.out.println(index + ":" + indexMap.get(index));
    return indexMap.get(index);
  }
}
```



### 代码

```java
// 使用list+map实现
class RandomizedSet {
private final Map<Integer, Integer> valueMap;
  private final List<Integer> keys;
  private final Random random = new Random();
  private int index = 0;

  /**
   * Initialize your data structure here.
   */
  public RandomizedSet() {
    valueMap = new HashMap<>();
    keys = new ArrayList<>();
  }

  /**
   * Inserts a value to the set. Returns true if the set did not already contain the specified element.
   */
  public boolean insert(int val) {
    if (!valueMap.containsKey(val)) {
      valueMap.put(val, index);
      keys.add(val);
      index++;
      return true;
    }
    return false;
  }

  /**
   * Removes a value from the set. Returns true if the set contained the specified element.
   */
  public boolean remove(int val) {
    if(!valueMap.containsKey(val)){   return false;}
        int i = valueMap.get(val);
        int last = index-1;
        if(index != last){
            keys.set(i, keys.get(last));   
            valueMap.put(keys.get(last), i);     
        }
        keys.remove(last);
        valueMap.remove(val);
        index--;
        return true;
  }

  /**
   * Get a random element from the set.
   */
  public int getRandom() {
    return keys.get(random.nextInt(index));
  }
}
```


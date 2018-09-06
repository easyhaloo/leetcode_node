



- ### 解析：

> 将罗马数字转化成数字，可以先定义一个Map存放罗马字符与数字的映射关系。

> 然后从左向右遍历，我们规定右边的数字比左边的要大，遇见这样的组合直接用大数减去小数。

> 例如：MCM  可以表示
  >  - M
  >  - MC  (M>C) 直接➕
  >  - CM  (M>C) 需要M-C
  >
  > 最后一步我们需要减去两次C，因为之前加过一次C，这个C不能单独存在，应该与CM组成一个数的，所以减去两次

- ### 代码：

```java
public int romanToInt(String s) {
    Map<Character,Integer> map = new HashMap<>();
    //将罗马数字对应的整数存入MAP
    map.put('I', 1);
    map.put('V', 5);
    map.put('X', 10);
    map.put('L', 50);
    map.put('C', 100);
    map.put('D', 500);
    map.put('M', 1000);
    int value = map.get(s.charAt(0));
    for(int i=1;i<s.length();i++){
        //规定右边的数比左边大 用大数减去小数
        if(map.get(s.charAt(i))>map.get(s.charAt(i-1))){
            //此处减两次 是因为 之前多加了一次  MCM  先m+c  在cm m-c 此处多加一次C
            value += map.get(s.charAt(i))-2*map.get(s.charAt(i-1));
        }else{
            value +=map.get(s.charAt(i));
        }
    }
    return value;
 }
```

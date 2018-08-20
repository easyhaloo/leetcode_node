Given a 32-bit signed integer, reverse digits of an integer.

`Example 1:`
```java
Input: 123
Output: 321
```
`Example 2:`
```java
Input: -123
Output: -321
```
`Example 3:`
```java
Input: 120
Output: 21
```
`Note:`
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [$-2^31$,  $2^31 − 1$]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.



- ### 解析
> 题目大意是，给定一个数字，要求将数字转置，如果遇见转置后的结果大于$2^31−1$，或者小于$-2^31$，即反转后的整数溢出，直接返回0。

- 可以采用一个trick,题目所给的限制整数的范围，我们直接可以将结果转换为长整型long来进行计算，这样当我们遇见`Integer.MIN_VALUE`或者`Integer.MAX_VALUE`就不会导致溢出，程序就不会报错，我们可以对结果进行判断当出现小于`Integer.MIN_VALUE`，或是大于`Integer.MAX_VALUE`，直接返回0，最后对结果进行强转成int类型即可。
- ### 代码
```java
public int reverse(int x){
    long res = 0 ;
    while(x != 0){
        res  =  res*10+x%10;
        x/=10;
        if(res < Integer.MIN_VALUE || res > Integer.MAX_VALUE) return 0;

    }
    return (int)res;
}
```

---
- 还有另外一种解法，当使用一个临时变量temp存储要翻转的那一位，然后对结果进行判断，当结果大于`Integer.MAX_VALUE/10`，或者是小于`Integer.MIN_VALUE/10`,直接返回0，因为这样可以避免溢出，当然我们还要注意，MIN是-2147483648，MAX是2147483647,当我们截取到整数的最后一位时，如果`res= Integer.MAX_VALUE/10&&temp>8`,此时会发生溢出，同理`res == Integer.MIN_VALUE/10 && temp < -7` ,也会发生溢出此时直接返回0即可。如果通过前面的校验，直接`res = res*10+temp;`
- ### 代码
```java
public int reverse(int x){
  int res = 0 ;
while(x != 0){
    int temp = x%10;
    x/=10;
    // MIN: -2147483648
    if(res > Integer.MAX_VALUE/10 || res == Integer.MAX_VALUE/10 && temp > 8 ) return 0;
    // MAX:  2147483647
    if(res < Integer.MIN_VALUE/10 || res == Integer.MIN_VALUE/10 && temp < -7 ) return 0;
    res = res*10+temp;
}
return res;
}
```

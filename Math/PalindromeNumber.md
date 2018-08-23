Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

`Example 1:`
```java
Input: 121
Output: true
```

`Example 2:`
```java
Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```

`Example 3:`
```java
Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

- ### 解析：
> 该题的大意就是判断一个数字，从左往右，从右往左都一样，说明此数字就是回文数字。这样一来很好判读了，遇见负数直接返回false,如果是整数则将每一位翻转，然后再同原来的数值进行比较。

- ### 代码：
```java
 public static  boolean isPalindrome(int x) {
    if(x < 0) return false;

    int temp = 0 ;
    int src = x;
    while(x != 0){
        temp = temp*10+x%10;
        x /=10;
    }
    System.out.println(temp);
    return temp == src;
}
```

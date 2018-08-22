Implement `atoi` which converts a string to an integer.

The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned.

`Note:`
Only the space character ' ' is considered as whitespace character.
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−2^31,  2^31 − 1]. If the numerical value is out of the range of representable values, INT_MAX (2^31 − 1) or INT_MIN (−2^31) is returned.

`Example 1:`
```java
Input: "42"
Output: 42
```
`Example 2:`
```java
Input: "   -42"
Output: -42
Explanation: The first non-whitespace character is '-', which is the minus sign.
             Then take as many numerical digits as possible, which gets 42.
```

- ### 解析
> 实现C++中的内置函数，atoi的功能，遇见非数字直接返回前面的数字结果。

这道题比较简单，直接进行处理，先对字符串去掉空格，然后判断首位是否包涵正负，设置一个标志位positive，记录正负。设置结果为double类型，遍历字符串，依次叠加，当超过限定值，直接返回。


- ### 代码

```java
public int myAtoi(String str){

    double res = 0;
    boolean positive = true;
    int index = 0;
    while(index < str.length() && str.charAt(index) == ' '){
        index++;
    }

    if(str.length() > index && str.charAt(index) == '-'){
        positive = false;
        index++;
    }else if(str.length() > index && str.charAt(index) == '+'){
        index++;
    }


    while(index < str.length() && Character.isDigit(str.charAt(index))){
        res = res*10+ str.charAt(index)-'0';
        if(res > Integer.MAX_VALUE){
            return positive ? Integer.MAX_VALUE :Integer.MIN_VALUE;
        }
        index++;
    }

    return positive ? (int)res : -(int)res;
}
```

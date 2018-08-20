The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```java
P   A   H   N
A P L S I I G
Y   I   R
```
And then read line by line: ``"PAHNAPLSIIGYIR"``

Write the code that will take a string and make this conversion given a number of rows:
```java
string convert(string s, int numRows);
```
`Example 1:`
```java
Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"
```
`Example 2:`
```java
Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"
Explanation:

P     I    N
A   L S  I G
Y A   H R
P     I
```


- ### 解析：
> 此题的意思是将给定的字符串按照rowNum行的形式呈Z形状进行排列，那么我们可以从两方面入手，第一种是直接安装Z形状建立rowNum个String对象，从上到下然后从下到上依次往String中填充字符串，或者直接通过层序遍历的方式扫描填充。
- - -
- ### 解法一（行排序）：
>建立rowNum个StringBuilder,然后遍历字符串，将对应的字符加入到对应行所属的StringBuilder中,就如同下面一样
> P加入StringBuilder1，A加入StringBuilder2，依次类推，当到达P的时候需要逆转，A加入StringBuilder3，L加入StringBuilder2，当到达I的时候继续逆转，往返下去直到遍历完毕。
```
StringBuilder1            P     I    N
StringBuilder2            A   L S  I G
StringBuilder3            Y A   H R
StringBuilder4            P     I
```

- ### 代码：
```java
public String convert(String s, int numRows) {

    if(numRows == 1) return s;

    char[] chs = s.toCharArray();
    int len = chs.length;
    StringBuilder[] sb = new StringBuilder[numRows];
    for (int i = 0; i < sb.length; i++) sb[i] = new StringBuilder();

    int j = 0 ;
    while(j < len){
        for(int idx = 0 ; idx< numRows&& j< len;idx++){
            sb[idx].append(chs[j++]);
        }
        for(int idx = numRows-2 ; idx>=1&&j< len;idx--){
            sb[idx].append(chs[j++]);
        }
    }

    for(int i = 1 ; i< numRows;i++){
        sb[0].append(sb[i]);
    }
    return sb[0].toString();
}
```
- - -
- ### 解法二（行扫描）：
>直接扫描每行一次添加进去即可，这里需要确定是每个字符的定位公式。通过观察，我们可以发现一些规律：
>  - 第一行跟最后一行相邻的两个字符相差`2*rownum-2`个位置。
>  - 中间的行比较难以发现规律，不过还是有规律可言，拿第二行来说，L-A的距离为4，I-P的距离为6，刚好在上一行的基础上少2，正好P与A之间的行索引差值为1，所有我们可以确定中间的规律，`2*rownum-2*i`,总体来说，除了最后一行，这个规则都适用。
```
            P     I    N
            A   L S  I G  
            Y A   H R
            P     I
```

- ### 代码：
```java
public String convert(String s, int numRows) {
  if(numRows == 1) return s;

         int step = 2*numRows-2;
         StringBuilder sb = new StringBuilder();
         for(int i = 0;i< numRows;i++){
             for(int j = i;j < s.length();j+=step){
                 sb.append(s.charAt(j));
                 int temp = j+step-2*i;
                 if(i!= 0 && i!= numRows-1 &&temp < s.length())
                     sb.append(s.charAt(temp));
             }
         }
         return sb.toString();
}
```

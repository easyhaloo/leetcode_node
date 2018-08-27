
- #### 解析：
> 该题目的意思比较明显，就是将整数按照罗马数字的规则进行展示。可以很直观的将所有可能的罗马数字先进行组合，然后从中选取合适的组合即可。


- #### 代码：

```java
public String intToRoman(int num) {
        int[] values = {1000,900,500,400,100,90,50,40,10,9,5,4,1};
        String[] strs = {"M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"};

    StringBuffer res = new StringBuffer();
    for(int i=0,len=values.length;i<len;i++){
        while(num>=values[i]){
              num -= values[i];
        res.append(strs[i]);
        }

    }
    return res.toString();
}
```

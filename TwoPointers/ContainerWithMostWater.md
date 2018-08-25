
- #### 解析：
> 题目的意思是：求两条垂直线与X组成的梯形最多能容纳多少体积是水，求这个最大值。该题可以直接暴力破解，两次for循环计算两个索引的位置所组成的面积，再跟原来保留的最大值比较即可得出结果。这里我们将使用双指针的方式来遍历，从两端同时遍历，一次扫描，可以提升复杂度。
> ###### 双指针
> 定义两个变量，一个left=0，一个right 为数组的右边界
>
> 开始扫描，每次以left,right为边界计算面积，如之前保存的最大值比较，大则更新。

> 然后比较left,right边界的长度，将短的边界向中心移动

- #### 代码：

```java
public int maxArea(int[] height) {
       if(height.length<2){
           return 0;
       }
   int maxArea = 0;
   int l =0,r = height.length-1;

   while(l<r){
       //取水量的大小  由短边跟底决定。
       maxArea = Math.max(maxArea,Math.min(height[l],height[r])*(r-l));
       if(height[l]<height[r]){
           l++;
       }else{
           r--;
       }
   }
   return maxArea;
}
```

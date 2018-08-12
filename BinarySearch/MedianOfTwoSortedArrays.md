There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

You may assume nums1 and nums2 cannot be both empty.


`Example 1:`
```java
nums1 = [1, 3]
nums2 = [2]

The median is 2.0
```

```java
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```


- ### 分析：
> 题目意思是求解两个数组中的中位数，要在log(m+N)的时间内求解，所以只能使用二分搜索。该题的难点在于如何在两个未合并的数组中同时进行二分查找，为了打到目的，我们需要定义一个寻找`kth`第k个元素的函数做辅助。
>
> 由于数组是排序的，所有中位数存在的可能性只有有三种
> 出现在nums1中，或者出现在nums2中，或者两者中都存在。所以我们可以进行分类讨论，定义`findKth(int[] arr1,int start1,int[] arr2,int start2,int k)`函数，求解从num1中的start1开始，从num2中的start2开始寻找Kth.当start1超出num1的范围，那么kth就在nums2中，同理亦然。比较nums1,nums2中中位数的大小，不断截去小的部分，并使得k减少2/k.





- ### 代码：
```java
public double findMedianSortedArrays(int[] nums1, int[] nums2) {
      int m = nums1.length, n = nums2.length;
	    int l = (m + n + 1) / 2;
	    int r = (m + n + 2) / 2;

        return (findKth(nums1, 0, nums2, 0, l) + findKth(nums1, 0, nums2, 0, r)) / 2.0;
    }
    //寻找第K小的数

    public double findKth(int[] arr1,int start1,int[] arr2,int start2,int k){
        //arr1用尽 直接取第K小的数在arr2中
        if(start1>arr1.length-1){
            return arr2[start2+k-1];
        }
        if(start2>arr2.length-1){
            return arr1[start1+k-1];
        }

        if(k==1){
            return Math.min(arr1[start1],arr2[start2]);
        }

        int mid1 = Integer.MAX_VALUE,mid2=Integer.MAX_VALUE;

        if(start1+k/2-1<arr1.length) mid1 = arr1[start1+k/2-1];
        if(start2+k/2-1<arr2.length) mid2 = arr2[start2+k/2-1];

        //二分
        //当K在左边
        if(mid1<mid2){ //截取左边
            return findKth(arr1,start1+k/2,arr2,start2,k-k/2);
        }else{
            return findKth(arr1,start1,arr2,start2+k/2,k-k/2);
        }
}
```

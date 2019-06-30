You are given a series of video clips from a sporting event that lasted T seconds.  These video clips can be overlapping with each other and have varied lengths.

Each video clip clips[i] is an interval: it starts at time clips[i][0] and ends at time clips[i][1].  We can cut these clips into segments freely: for example, a clip [0, 7] can be cut into segments [0, 1] + [1, 3] + [3, 7].

Return the minimum number of clips needed so that we can cut the clips into segments that cover the entire sporting event ([0, T]).  If the task is impossible, return -1.



Example 1:

Input: clips = [[0,2],[4,6],[8,10],[1,9],[1,5],[5,9]], T = 10
Output: 3
Explanation: 
We take the clips [0,2], [8,10], [1,9]; a total of 3 clips.
Then, we can reconstruct the sporting event as follows:
We cut [1,9] into segments [1,2] + [2,8] + [8,9].
Now we have segments [0,2] + [2,8] + [8,10] which cover the sporting event [0, 10].



[题目地址](https://leetcode-cn.com/problems/video-stitching/)



### 题解

>  题目大意：给定一组数组，代表电影中的某个剪辑点，类似[0,1]，左边代表开始，右边代表结束时间。 给定的时间可以通过重合叠加的形式来覆盖。
>
> 此题可以使用贪心的做法：
>
> 首先我们需要将各个剪辑点的结束时间clips[i] [1] ，按从大到小的顺序进行排序。
>
> 然后依次遍历，用给定的时间` T`来与剪辑点的结束时间比较。寻找到`T`所在的区间段。保证clips[0] < T <= clip[1]
>
> 如果上述clip找到了，我们需要借助一个cur变量来保存clip[0]，此时我们需要判断上一次的T 是否大于 clip，这样为了将T分解，通过不断缩小T来寻找答案。
>
> 如果没有T 大于clip则说明无法拼凑子片段。



### 代码

```java
public static int videoStitching(int[][] clips, int T) {
        // 排序
        Arrays.sort(clips, ((o1, o2) -> o2[1] - o1[1]));
        // [8,10] [5,9],[1,9],[4,6],[1,5],[0,2]
        int cur = T, cnt = 0, i = 0;
        while (T != 0) {
            if (i < clips.length && clips[i][1] >= T) {
                cur = Math.min(cur, clips[i][0]);
                i++;
            } else {
                if (cur < T) {
                    T = cur;
                    cnt++;
                } else {
                    return -1;
                }
            }
        }
        return cnt;
    }

```



#### 非排序版本

> 上述算法可以改为非排序，以0位起始位，迭代寻找0所在区间，将0所在的区间的结束位作为下一次迭代的起始位，依次迭代，直至寻找到当前的区间的结束位>=T。

```java
 public static int videoStitchingv2(int[][] clips, int T) {
        // 排序
        int currentMin = 0, currentMax = 0;
        int step = 0;
        while (currentMax < T) {
            boolean hit = false;
            for (int[] clip : clips) {
                int start = clip[0];
                int end = clip[1];
                if (start <= currentMin && end > currentMax) {
                    currentMax = end;
                    hit = true;
                }
            }
            currentMin = currentMax;

            step++;
            if (!hit) return -1;
        }
        return step;
    }
```








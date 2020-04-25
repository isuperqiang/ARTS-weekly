## 1. Algorithm

#### 22. 递增的三元子序列（中等）

##### 描述：

> 给定一个未排序的数组，判断这个数组中是否存在长度为 3 的递增子序列。
>
> 数学表达式如下:
>
> 如果存在这样的 i, j, k,  且满足 0 ≤ i < j < k ≤ n-1，
> 使得 arr[i] < arr[j] < arr[k] ，返回 true ; 否则返回 false 。

##### 示例：

```
输入: [1,2,3,4,5]
输出: true
输入: [5,4,3,2,1]
输出: false
```

##### 思路：

**双指针**

定义 min 为序列中的较小值，mid 为中间值，看是否能找到较大值。

```java
class Sulution {
    public boolean increasingTriplet(int[] nums) {
        if (nums == null || nums.length < 3) {
            return false;
        }

        int min = Integer.MAX_VALUE;
        int mid = Integer.MAX_VALUE;
        for (int num : nums) {
            if (num <= min) {
                min = num;
            } else if (num <= mid) {
                mid = num;
            } else {
                return true;
            }
        }
        return false;    
    }
}
```

##### 分析：

- 时间复杂度：O(n)
- 空间复杂度：O(1)

## 2. Review

[The Greatest Developer Fallacy Or The Wisest Words You’ll Ever Hear?](https://skorks.com/2011/02/the-greatest-developer-fallacy-or-the-wisest-words-youll-ever-hear/) 你听过最伟大开发者的谬误还是最明智的话？

作者从 “I will learn it when I need it” 开始谈起，列举了一些自己的观点。

- 投资你的未来，而不是需要的时候才学习，渴望比知识更重要。
- 你不知道你不知道的知识，你不去学习它，是因为你根本不知道它的存在。
- 广度是深度的副作用，在一个领域成为专家，其他领域也顺便了解。
- 和大牛交朋友，从他们那里学到东西。

## 3. Tip

分享一个搜索引擎 —— [多吉搜索](https://www.dogedoge.com/)，它的宗旨是不追踪，不误导，称得上是国内的 duckduckgo。界面清爽，简单纯粹，搜索质量比百度高 100 倍。如果你不能愉快地访问谷歌，那么多吉搜索是不错的选择。:)

## 4. Share

最近由于国庆，SS 服务被阻隔了，无法访问谷歌，对开发很不方便。互联网本该自由，何必构筑高墙，遮蔽众人耳目，自欺欺人呢？
## 1. Algorithm

#### 35. 搜索插入位置（简单）

##### 描述：

> 给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。你可以假设数组中无重复元素。

##### 示例：

```properties
输入: [1,3,5,6], 5
输出: 2
输入: [1,3,5,6], 7
输出: 4
```

##### 思路：

>  - 解法一：因为是排序的数组，直接从头遍历，然后找到大于或者等于目标值的下标，就是结果。
>  - 解法二：使用二分法查找，然后找到目标值或者左边界（low）。

##### 解法：

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] >= target) {
                return i;
            }
        }
        return nums.length;
    }

    public int searchInsertByBinary(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int min = 0;
        int max = nums.length - 1;
        while (min <= max) {
            int mid = (max + min) / 2;
            if (nums[mid] > target) {
                max = mid - 1;
            } else if (nums[mid] < target) {
                min = mid + 1;
            } else {
                return mid;
            }
        }
        return min;
    }
}
```

##### 分析：

- 时间复杂度：解法一 O(n)，解法二 O(logn)
- 空间复杂度：O(1)

-----

#### 69. X 的平方根（简单）

##### 描述：

> 实现 `int sqrt(int x)` 函数。计算并返回 *x* 的平方根，其中 *x* 是非负整数。
>
> 由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

##### 示例：

```properties
输入: 4
输出: 2
输入: 8
输出: 2
```

##### 思路：

> 
> 牛顿法 https://en.wikipedia.org/wiki/Integer_square_root
> 注意防止整形越界。
> 

##### 解法：

```java
class Solution {
    public int mySqrt(int x) {
        if (x <= 1) {
            return x;
        }
        int r = x / 2;
        while (r > x / r) {
            r = (r + x / r) / 2;
        }
        return r;
    }
}
```

##### 分析：

- 时间复杂度：O(logn)
- 空间复杂度：O(1)

## 2. Review

[What is readable code?](https://medium.com/s/story/readability-as-usability-78c5a2a373cc)  什么是可读的代码？

代码创建了接口，但是代码本身也是一种接口。就像生活中的门可以打开、关闭一样，开发者写代码可以添加新功能、修复错误。忘记代码的位置很容易，所以代码应该是可搜索的，简短通用的名称可以作为默认值表示。

可读的代码应当容易安全地编辑，前提是要理解代码的逻辑。当变量名称具有表现力时，代码更容易编辑。可读的代码一定可用，另外看起来也漂亮。

作者从 UI 层面举了几个例子，View 的状态和代码层面的变量产生对应关系，如果让用户清晰理解操作意图，那么代码也要保证逻辑是一致的。

## 3. Tip

读《码出高效：Java 开发手册》集合篇看到 fail-fast 有感，[Java集合的fail-fast机制](https://isuperqiang.cn/post/java-ji-he-de-fail-fast-ji-zhi/)


## 4. Share

[马蜂窝张矗：我对技术团队绩效考核管理的几点思考](<https://mp.weixin.qq.com/s/FkrrBLoB2YZ45fIQed0dsw>)

技术人员绩效考核一般难以量化，不好的衡量标准有代码行数、Bug 数量等。要关注目标，而不是任务，目标可量化。不同级别的人员，考核的重点不同。按月或按季度进行评估，周期不宜太长。
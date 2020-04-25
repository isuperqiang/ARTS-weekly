## 1. Algorithm

#### [搜索二维矩阵 II](https://leetcode-cn.com/problems/search-a-2d-matrix-ii/)（中等）

##### 描述：

> 编写一个高效的算法来搜索 m x n 矩阵 matrix 中的一个目标值 target。该矩阵具有以下特性：
> 每行的元素从左到右升序排列。
> 每列的元素从上到下升序排列。

##### 示例：

```
现有矩阵 matrix 如下：
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
给定 target = 5，返回 true。
给定 target = 20，返回 false。
```

##### 思路：

从左下角出发，把 target 和当前值比较。如果 target 大于当前值，就往右走；如果小于，就往上走。如果等于，就返回 true。

```java
class Sulution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return false;
        }
        int row = matrix.length - 1;
        int column = 0;
        int columnLength = matrix[0].length;
        while (row >= 0 && column < columnLength) {
            if (matrix[row][column] > target) {
                row--;
            } else if (matrix[row][column] < target) {
                column++;
            } else {
                return true;
            }
        }
        return false;
    }
}
```

##### 分析：

- 时间复杂度：O(M+N)
- 空间复杂度：O(1)

## 2. Review

[My guiding principles after 20 years of programming](https://medium.com/@alexewerlof/my-guiding-principles-after-20-years-of-programming-a087dc55596c)  [20 年老程序员告诉你的 20 条编码原则](https://www.infoq.cn/article/VEgR7xkNIYUsSWP9Ohc3)

软件开发的历史没多久，20年经验的程序员也比较稀缺。作者总结了编程的经验和原则，对刚入门不久的新人有很大启发。比如第一条不要纠结于开发工具，不管是库、编程语言或平台。总是有人争吵什么是最好的语言，其实抛开具体业务场景谈是没有意义的。

## 3. Tip

断点调试是排查问题的好方法，其效率比打印 log 要高。不管是 Native 库还是 Java 库，都可以用断点调试，一步步执行代码，查看变量值和函数跳转。

## 4. Share

**为什么需要软件架构?**

早在 1986 年的时候，人月神话的作者在讨论软件的复杂性时，谈到：软件的本质复杂性存在于复杂的业务需求中。

而管理复杂性，最根本的手段就是职责分离。为了实现职责分离，代码重用，架构慢慢地复现出来。架构的本质是管理复杂性。

没有架构，我们所有的代码都耦合在一起，人类的心智模型不擅长处理这种复杂性，架构的设立，和图书馆的图书分类，公司的组织划分等，本质都是一样的。是为了管理复杂性，以取得更高的生产力。
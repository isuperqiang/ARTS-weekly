## 1. Algorithm

#### [路径总和](https://leetcode-cn.com/problems/path-sum/)（简单）

#### 描述：

> 给定一个二叉树和一个目标和，判断该树中是否存在根节点到叶子节点的路径，这条路径上所有节点值相加等于目标和。
> 叶子节点是指没有子节点的节点。

#### 示例：

```
给定如下二叉树，以及目标和 sum = 22，
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1
```

#### 思路：

从根节点开始遍历，每次遍历时从目标和减去当前节点值，当作子节点要凑的和，在叶子节点判断是否刚好凑齐。

```java
class Sulution {
    pbulic boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) {
            return false;
        }
        if (root.left == null && root.right == null) {
            return sum == root.val;
        }
        int csum = sum - root.val;
        return hasPathSum(root.left, csum) || hasPathSum(root.right, csum);
    }
}
```

#### 分析：

- 时间复杂度：O(N)
- 空间复杂度：O(log(N)) or O(N)

## 2. Review

[A 3-Minute Hack for Focus You’ve Probably Never Heard Of](https://medium.com/mind-cafe/a-3-minute-hack-for-focus-youve-probably-never-heard-of-40708b788a0f) 你从未听说过的 3 分钟聚焦大法

作者一直无法专注工作，同事分享了一个方法给他——双耳节拍。本质上，双耳节拍是重复播放的音乐。它没有实际的节拍，而是在大脑中产生的同时播放两个不同频率的音调。

我一直在用的产品叫「小睡眠」，它主要功能是助眠，但是也有聚焦和放松模式。配合降噪耳机，很快便进入高效工作中。

## 3. Tip

接手维护老项目，开发者代码设计得烂，不知道怎么代码怎么调用，也无处安放 debug 点。这时只要创建一个异常，打印它的 stack track，就能够对调用时序一目了然。查看源码时也可以通过这种办法确定调用流程。

## 4. Share

[CS-Notes](https://cyc2018.github.io/CS-Notes/#/) GitHub 100k+ star 的项目，技术面试必备基础知识、Leetcode、计算机操作系统、计算机网络、系统设计、Java 等。

面试前可以刷一刷，主要是增加知识面的广度。
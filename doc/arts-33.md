## 1. Algorithm

#### [路径总和 III](https://leetcode-cn.com/problems/path-sum-iii/)（简单）

#### 描述：

> 给定一个二叉树，它的每个结点都存放着一个整数值。找出路径和等于给定数值的路径总数。
> 路径不需要从根节点开始，也不需要在叶子节点结束，但是路径方向必须是向下的（只能从父节点到子节点）。
> 二叉树不超过1000个节点，且节点数值范围是 [-1000000,1000000] 的整数。

#### 示例：

```
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

返回 3。和等于 8 的路径有:

1.  5 -> 3
2.  5 -> 2 -> 1
3.  -3 -> 11
```

#### 思路：

两次递归。pathSum 返回以当前节点为根的树中，路径和为目标值的路径总数；count 返回以当前节点为根的树中，有多少以该节点为开头，路径和为目标值的路径总数。

```java
class Sulution {
    public int pathSum(TreeNode root, int sum) {
        if (root == null) {
            return 0;
        }
        return count(root, sum) + pathSum(root.left, sum) + pathSum(root.right, sum);
    }

    private int count(TreeNode root, int sum) {
        if (root == null) {
            return 0;
        }
        int count = 0;
        if (sum == root.val) {
            count += 1;
        }
        int diff = sum - root.val;
        return count + count(root.left, diff) + count(root.right, diff);
    }
}
```

## 2. Review

[The most important skill a programmer can learn](https://medium.com/free-code-camp/the-most-important-skill-a-programmer-can-learn-9d410c786baf) 程序员该学到的最重要技能

知道什么时候不写代码，该拒绝的需求就坚定拒绝。代码增多会带来很多问题，面对各种需求，我们不该被动接受，不合理的需求就不做。

## 3. Tip

程序员不喜欢做重复的事情，写脚本成了偷懒的方法，shell 是最常用的脚本，可完成许多自动化的操作。[Bash脚本教程](https://wangdoc.com/bash/index.html) 是不错的参考资料。

## 4. Share

[caoz 的职场系列](https://mp.weixin.qq.com/s/TIxWo9LMI3tFrz5612JWFw) 写得很受用，职场人可以多读读。
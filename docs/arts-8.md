## 1. Algorithm

#### 101. 对称二叉树（简单）

##### 描述：

> 给定一个二叉树，检查它是否是镜像对称的。

##### 示例：

```
例如，二叉树 [1,2,2,3,4,4,3] 是对称的。
         1
       /   \
      2     2
     / \   /  \
    3   4 4    3
```

##### 思路：

> - 递归法：如果同时满足下面的条件，两个树互为镜像：它们的两个根结点具有相同的值；每个树的右子树都与另一个树的左子树镜像对称。
> - 迭代法：类似广度优先遍历，但要把队列存的值 Double 一下。每次提取两个结点并比较它们的值。然后将两个结点的左右子结点按相反的顺序插入队列中。当队列为空时，或者我们检测到树不对称（即从队列中取出两个不相等的连续结点）时，算法结束。

##### 解法：

```java
class Solution {
      // 迭代法
    public boolean isSymmetric2(TreeNode root) {
        if (root == null) {
            return true;
        }

        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        q.add(root);
        while (q.size() > 0) {
            TreeNode left = q.poll();
            TreeNode right = q.poll();
            if (left == null && right == null) {
                continue;
            }
            if (left == null || right == null) {
                return false;
            }
            if (left.val != right.val) {
                return false;
            }
            q.add(left.left);
            q.add(right.right);
            q.add(left.right);
            q.add(right.left);
        }
        return true;
    }

    // 递归法
    public boolean isSymmetric(TreeNode root) {
        if (root == null) {
            return true;
        }
        return isMirror(root.left, root.right);
    }

    private boolean isMirror(TreeNode left, TreeNode right) {
        if (left == null && right == null) {
            return true;
        }

        if (left == null || right == null) {
            return false;
        }

        if (left.val == right.val) {
            return isMirror(left.left, right.right) && isMirror(left.right, right.left);
        }
        return false;
    }
}
```

##### 分析：

- 递归法：时间复杂度：O(n)，空间复杂度：O(n)
- 迭代法：时间复杂度：O(n)，空间复杂度：O(n)

-----

#### 107. 二叉树的层次遍历 II（简单）

##### 描述：

> 给定一个二叉树，返回其节点值自底向上的层次遍历。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

##### 示例：

```
例如，给定二叉树 [3,9,20,null,null,15,7],
     3
   /   \
  9    20
 / \
15  7
返回其自底向上的层次遍历为：
[
  [15,7],
  [9,20],
  [3]
]
```

##### 思路：

> 广度优先，逐层遍历。首先构建数据列表和下层结点列表，遍历当前层的结点列表，把数据添加到数据列表，并把每个结点的子结点添加到下层结点列表。遍历完成后，把数据列表放到结果列表的首部，然后把下层结点列表变成当前结点列表，继续遍历。

##### 解法：

```java
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        if (root == null) {
            return Collections.emptyList();
        }

        List<List<Integer>> result = new LinkedList<>();
        List<TreeNode> currRowList = new LinkedList<>();
        currRowList.add(root);
        List<TreeNode> nextRowList;
        List<Integer> valueList;
        while (currRowList.size() > 0) {
            valueList = new LinkedList<>();
            nextRowList = new LinkedList<>();
            for (TreeNode treeNode : currRowList) {
                valueList.add(treeNode.val);
                if (treeNode.left != null) {
                    nextRowList.add(treeNode.left);
                }
                if (treeNode.right != null) {
                    nextRowList.add(treeNode.right);
                }
            }
            result.add(0, valueList);
            currRowList = nextRowList;
        }
        return result;
    }
}
```

##### 分析：

- 时间复杂度：O(n)
- 空间复杂度：O(n)

## 2. Review

[How to write a killer Software Engineering résumé](https://medium.freecodecamp.org/writing-a-killer-software-engineering-resume-b11c91ef699d) 软件工程师如何写出杀手级的简历

作者是位面霸，他凭简历获得了 Google、Facebook、Amazon 等公司的面试机会。文章讲述了杀手级简历的特征，以及如何写出更好更高效的简历。

如何写出杀手级的简历？这里有几点建议：

- 一眼就要看到的信息：你是谁，联系方式，教育经历，工作经历，项目经历，专业技能。
- 内容一两页就够了，排版格式简单明了。
- 让 HR 省事、舒心，自然就给你机会。
- 个人经历要和职位相关，按照最近时间排列。
- 简历不是通用的，每个职位都要有不同的版本。
- 描述工作成果：Accomplished [X] as measured by [Y] by doing [Z]。
- 个人项目很重要，体现了对编程的热爱和追求。
- 专业技能，精通、熟悉、了解 XXX。

## 3. Tip

每个开发者都该有一套自己的代码工具箱，用来收集日常开发用到的工具类，为的是能够在项目中快速集成和使用， 从而缩短开发周期，提高编码效率，节约时间成本。我自己就整理了一套 Android 开发的常用代码库，有需要时直接拿来使用，简单省事。

## 4. Share

[努力成为一名‘‘值得跟’’的Leader](https://mp.weixin.qq.com/s/9ZU8aovjazSPdrQoNhIkqg)

什么样的人才是一个好的 Leader？“**值得跟**”绝对是对一个 Leader 最高的赞扬。

## 1. Algorithm

#### 226. 翻转二叉树（简单）

##### 描述：

> 翻转一棵二叉树

##### 示例：

```
示例：
输入:
    4
  2    7
1  3  6  9
输出:
    4
  7    2
9  6  3  1
```

##### 思路：

- 递归法：翻转一个二叉树，就是把根节点的左子树翻转一下，同样的把右子树翻转一下，再交换左右子树就可以了。
- 迭代法：类似广度优先遍历的方式，使用队列存储尚未交换的节点，每次从队列取出一个结点，交互其左右子结点，直到队列为空。

```java
class Solution {
    public TreeNode invertTreeRecursively(TreeNode root) {
        if (root == null) {
            return null;
        }

        TreeNode temp = root.left;
        root.left = root.right;
        root.right = temp;
        invertTreeRecursively(root.left);
        invertTreeRecursively(root.right);
        return root;
    }

    public TreeNode invertTreeIteratively(TreeNode root) {
        if (root == null) {
            return null;
        }

        LinkedList<TreeNode> list = new LinkedList<>();
        list.add(root);
        while (list.isEmpty()) {
            TreeNode current = list.poll();
            TreeNode temp = current.left;
            current.left = current.right;
            current.right = temp;

            if (current.left != null) {
                list.add(current.left);
            }
            if (current.right != null) {
                list.add(current.right);
            }
        }
        return root;
    }
}
```

##### 分析：

递归和迭代法一样：

- 时间复杂度：O(n)
- 空间复杂度：O(n)

-----

#### 326. 3 的幂（简单）

##### 描述：

> 给定一个整数，写一个函数来判断它是否是 3 的幂次方。

##### 示例：

```
输入: 27
输出: true
```

##### 思路：

- 解法一：累乘法
- 解法二：3的幂次质因子只有3，而整数范围内的3的幂次最大是1162261467

##### 解法：

```java
class Solution {
    public boolean isPowerOfThree(int n) {
        if (n <= 0) {
            return false;
        }
        if (n == 1) {
            return true;
        }
        long m = 1;
        while (m < n) {
            m *= 3;
            if (m == n) {
                return true;
            }
        }
        return false;
    }

    public boolean isPowerOfThree2(int n) {
        return n > 0 && 1162261467 % n == 0;
    }
}
```

##### 分析：

解法一：

- 时间复杂度：O(n)
- 空间复杂度：O(1)

解法二：

- 时间复杂度：O(1)
- 空间复杂度：O(1)

## 2. Review

[Goodbye, Object Oriented Programming](https://medium.com/@cscalfani/goodbye-object-oriented-programming-a59cda4c0e53) 再见，面向对象编程

作者是个有着多年经验的老程序员，他毫不留情地指出了面向对象编程的问题，分别从封装、继承和多态这三大支柱来阐述。

- 继承最大的好处就是复用。但是出现了「猴子香蕉丛林」问题，我只想要一根香蕉，得到的却是香蕉丛林。钻石问题，继承关系的结构图就像钻石一样，这样容易造成调用混乱。还有基类问题，子类不知道基类的实现，从而引发操作错误。解决办法就是用组合替代继承，原意是包含和委托。
- 封装使得对象保证内部的变量受保护，然而它却带来了一下问题。引用问题，给构造方法传参时，对象存在多个应用，这样对象就不安全了。解决办法是对象深拷贝，但不是所有对象都支持克隆。
- 面向对象编程不需要多态，它完全可以基于接口来实现。

最后作者告别了面向对象编程，转向函数式编程。

虽然作者举出这么多 OOP 的问题，但是面向对象的思想依然非常流行。软件开发没有银弹，能够实现功能、解决问题的思想都是值得采用的。

## 3. Tip

日常的琐事都用软件记录，比如有道云笔记、滴答清单、LastPass。大脑是用来思考的，不是用来记东西的，它充当的更多是 CPU 的角色，而不是硬盘。所以，让大脑轻松一下，用工具记录吧。

## 4. Share

[关于线程和I/O模型的极简知识](https://mp.weixin.qq.com/s/qodCngOPXGSaaBy2ULAgqg) 主要讲述了线程和 I/O 模型的演化历史，问题驱动模型的演化，每种模型都有各自的使用场景。
## 1. Algorithm

#### 110. 平衡二叉树（简单）

##### 描述：

> 给定一个二叉树，判断它是否是高度平衡的二叉树。
> 本题中，一棵高度平衡二叉树定义为：
> 一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过1。

##### 示例：

```
给定二叉树 [3,9,20,null,null,15,7]
    3
   / \
  9  20
    /  \
   15   7
 返回 true
```

##### 思路：

平衡二叉树的条件：
 - 左子树是平衡二叉树
 - 右子树是平衡二叉树
 - 左右子树的高度差的绝对值不超过 1

深度优先遍历，递归求解树的高度。终止条件是不满足上述三个条件之一，二叉树的最大深度可以参考第 114 题。

```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        return height(root) != -1;
    }
    
    private int height(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int leftHeight = height(root.left);
        int rightHeight = height(root.right);
        if (leftHeight == -1 || rightHeight == -1 
                || Math.abs(leftHeight - rightHeight) > 1) {
            return -1;
        }
        return Math.max(leftHeight, rightHeight) + 1;
    }
}
```

##### 分析：

- 时间复杂度：O(n)
- 空间复杂度：O(1)

## 2. Review

[Basic Linux Commands for Beginners](https://maker.pro/linux/tutorial/basic-linux-commands-for-beginners) 为新手准备的 Linux 命令

Linux 是免费、开源的操作系统内核，你可以修改 Linux 上的任何东西，并用自己的名字重新发布，比如 Ubuntu、Debian、Red Hat 等版本。

Linux 主要应用于服务器上，世界上 90% 的服务器都运行 Linux 系统，因为它安全、快速并且免费。Android 手机占据智能机的 80%，它也是基于 Linux 内核。大多数的病毒出现在 Windows 上，而不是 Linux。

shell 是一个程序，它接收用户的命令，并传递给系统执行，然后显示结果。Linux 有个命令行界面，是 shell 的主要交互部分。

接下来，作者列举了一些基本的命令：cd/ls/pwd/mkdir/rm/touch/man/cp/mv/cat/sudo/echo/df/vi/tar/apt-get/chmod/ping 等。

## 3. Tip

[oh my zsh](https://github.com/robbyrussell/oh-my-zsh) 非常强大的 shell，拥有丰富的插件和主题，只支持 macOS 和 Linux。不愧是终极 Shell，提高 10x 效率没问题。有时候一成不变挺悲哀的，尝试折腾一下才有乐趣。Have a try, you will enjoy it.

## 4. Share

程序员应该学习 Linux，理解设计理想，熟悉常用命令。对于高手来说，一个 Terminal 就够了。在 macOs 或 Linux 下开发，比 Windows 省心多了。首先没有字符编码的问题，其次 Unix-like 平台上有非常多的开发工具，程序员用了绝对爱不释手。另外，Unix-like 平台上的软件不像 Windows 系统上那样流氓，而且不容易感染病毒。值得庆幸的是，Windows 10 内置了 Linux，我们可以下载 Ubuntu 体验。虽然是阉割版，但用来学习够用了。
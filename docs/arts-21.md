## 1. Algorithm

#### 24. 两两交换链表中的节点（中等）

##### 描述：

> 给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。
> 你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

##### 示例：

```
给定 1->2->3->4, 你应该返回 2->1->4->3.
```

##### 思路：

- 迭代法：从 head 开始遍历，改变相邻节点和它们前后节点之间的关系。

```java
class Sulution {
    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode curr = head;
        ListNode result = head.next;
        ListNode next;
        ListNode prev = null;
        while (curr != null && (next = curr.next) != null) {
            ListNode temp = next.next;
            next.next = curr;
            curr.next = temp;
            if (prev != null) {
                prev.next = next;
            }
            prev = curr;
            curr = temp;
        }
        return result;
    }
}
```

- 递归法：先处理最后两个或一个节点，然后再从后往前处理每一对节点。

```java
class Sulution {
    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode next = head.next;
        head.next = swapPairs(next.next);
        next.next = head;
        return next;
    }
}
```

## 2. Review

[How to use Git efficiently](https://medium.com/free-code-camp/how-to-use-git-efficiently-54320a236369) 如何高效地使用 Git

作者通过一个开发场景，讲解了 Git workflow 的使用技巧。在多人协作的开发过程中，分支是重要的代码管理手段。

分支主要分为三种：master、release/、feature/xxx。master 是主分支，它存放的是生产代码的拷贝，任何人都不允许在 master 分支提交代码。release 是发布分支，它从 master 分支创建，可以存在多个并行分支 release/xxx，多个项目在同一个 code base 中时，release 分支可以保证项目并行。feature 是需求分支，它通常从 release 分支创建。每个需求都可以创建新的分支，每个开发者在不同的分支上进行功能开发。然后通过 PR 把代码合并到 release 分支。

通过 pull request，feature 分支的代码合并到 release 分支，主管可以在合并前进行 code review。如果发生合并冲突，解决办法有两种：处理 PR 的主管解决；开发者从 release 分支 pull 最新代码合并到 feature 分支并解决冲突。

项目完成后，release 分支的代码合并到 master 分支，然后发布产品。

## 3. Tip

最近在维护代码的过程中，发现很多地方写得不够好，重复的代码太多，代码结构有些混乱。有时间我就重构，每个点都仔细推敲，引入经典的设计模式，本着可读性和可维护性好的原则，其他人接手也容易，clean code 原则一定要牢记心间呐。

## 4. Share

[高效工作](https://www.yuque.com/zenany/up/high_productivity_work) 来自语雀精选

作者从两方面列举了高效工作的做法。

- 增加有效工作时间
- 提高单位时间的产能

高效能的三个要素：**时间、能量和注意力**。
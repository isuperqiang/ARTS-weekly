## 1. Algorithm

#### [环形链表 II](https://leetcode-cn.com/problems/linked-list-cycle-ii/)（中等）

#### 描述：

>  给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。
>  为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。
>  说明：不允许修改给定的链表。

#### 示例：

```
输入：head = [3,2,0,-4,2], pos = 1
输出：tail connects to node index 1
解释：链表中有一个环，其尾部连接到第二个节点。
```

#### 思路：

快慢指针：使用快慢指针从头遍历链表，如果两个指针相遇则表示链表有环。然后让慢指针从头开始，快指针继续向前，两者再次相遇点就是环的入口。这个地方用图解释更清晰，推荐阅读 [双指针技巧总结](https://labuladong.gitbook.io/algo/di-ling-zhang-bi-du-xi-lie/shuang-zhi-zhen-ji-qiao)。

```java
class Sulution {
    public ListNode detectCycle(ListNode head) {
       if (head == null || head.next == null) {
            return null;
        }
        ListNode fast = head;
        ListNode slow = head;
        boolean hasCycle = false;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
            if (fast == slow) {
                hasCycle = true;
                break;
            }
        }
        if (!hasCycle) {
            return null;
        }
        slow = head;
        while (fast != slow) {
            fast = fast.next;
            slow = slow.next;
        }
        return slow;
    }
}
```

#### 分析：

- 时间复杂度：O(N)
- 空间复杂度：O(1)

## 2. Review

[The S.O.L.I.D Principles in Pictures](https://medium.com/backticks-tildes/the-s-o-l-i-d-principles-in-pictures-b34ce2f1e898) 图画讲解 SOLID 原则

本文介绍了面向对象编程的 SOLID 原则，每个原则下面都有漫画说明，挺有趣的。

- 单一职责原则：每个类应该只有一个职责，包含一组强相关的行为。
- 开闭原则：类应该对扩展开放，对修改关闭。扩展功能要增加行为而不是修改它。
- 里氏替换原则：如果 S 是 T 的子类，那么 T 出现的地方就该被 S 替换并不需要改动代码。
- 接口隔离原则：类不应该依赖不需要的行为，需要把行为拆分成更小的粒度。
- 依赖反转原则：高层模块不该依赖低层模块，他们都该依赖抽象；抽象不该依赖细节，细节该依赖抽象。

## 3. Tip

重构项目代码的过程中，遇到不美观的地方，用新技术方案完美解决。[使用Android架构组件Lifecycle优化代码](https://isuperqiang.cn/post/shi-yong-android-jia-gou-zu-jian-lifecycle-you-hua-dai-ma/)

## 4. Share

B站有个不错的视频 [计算机科学速成课](https://www.bilibili.com/video/BV1EW411u7th)，从计算机历史、硬件、软件、编程等方面介绍，是计算机科学的基础知识，当作科普也不错，推荐大家看看。

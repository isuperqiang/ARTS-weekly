## 1. Algorithm

#### 160. 相交链表（简单）

##### 描述：

> 编写一个程序，找到两个单链表相交的起始节点。

##### 示例：

```properties
输入: 9->1->2->4, 3->2->4
输出: 2
```

##### 思路：

> 定义两个指针, 第一轮让到达末尾的节点指向另一个链表的头部, 最后如果两个指针相遇则为交点。两个指针移动了相同的距离, 有交点就结束, 无交点就各走了两条指针的长度。

##### 解法：

```java
class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) {
            return null;
        }

        ListNode pointA = headA;
        ListNode pointB = headB;
        while (pointA != pointB) {
            pointA = pointA == null ? headB : pointA.next;
            pointB = pointB == null ? headA : pointB.next;
            if (pointA != null && pointB != null && pointA.val == pointB.val) {
                break;
            }
        }
        return pointA;
    }
}
```

##### 分析：

- 时间复杂度：O(n)
- 空间复杂度：O(1)

-----

#### 169. 求众数（简单）

##### 描述：

> 给定一个大小为 n 的数组，找到其中的众数。众数是指在数组中出现次数大于 n/2 的元素。你可以假设数组是非空的，并且给定的数组总是存在众数。

##### 示例：

```properties
输入: [2,2,1,1,1,2,2]
输出: 2
```

##### 思路：

> 从第一个数开始 count=1，遇到相同的就加 1，遇到不同的就减 1。如果减到 0，就换个数开始计数，总能找到最多的那个。

##### 解法：

```java
class Solution {
    public int majorityElement(int[] nums) {
        if (nums == null) {
            return 0;
        }

        int count = 1;
        int major = nums[0];
        for (int i = 1; i < nums.length; i++) {
            if (major == nums[i]) {
                count++;
            } else {
                if (--count == 0) {
                    major = nums[i + 1];
                }
            }
        }
        return major;
    }
}
```

##### 分析：

- 时间复杂度：O(n)
- 空间复杂度：O(1)

## 2. Review

[A Software Engineering survival guide](https://medium.freecodecamp.org/a-software-engineering-survival-guide-fe3eafb47166) 软件工程师生存指南

作者总结了软件工程师职业生涯前几年的经验：

- 怎样充分准备面试
- 工作中如何成长
- 持续进步需要什么资源

准备面试的几条意见：

- 简历上列举的编程语言，至少能够完成 `FizzBuzz` 测试。
- 基本的数据结构和算法，像链表、数组、树和排序。
- 你选择的语言的特点，比如字符串为什么不可变，内存是如何管理的。
- 面向对象编程的概念，比如类、对象和继承。
- 学会总结你的经验，在简历上记叙下来。
- 在 GitHub 上展示代码，或者参与开源项目。
- 面试是双向的过程，也要面试你的面试官，比如提问几个问题：
  - 你们是如何进行软件测试的
  - 你们用什么版本控制系统
  - 你们是如何处理技术债的
  - ...

工作中的几条建议：

- 优秀的工业级代码是可读的、具有防御性的、经过优化的。
- 大多数时间不是用来写新代码，而是 debug、读代码。
- debug 和读代码，熟悉基础代码和产品。
- 组织你的想法，比如使用 TODO 列表、笔记、图表。
- 好的库具备的特征：开源、宽松的许可（MIT、BSD等）、成熟、一直维护、其他公司或项目在用。

持续提升的几条建议：在线课程、在线硕士学位、博客、大会。

## 3. Tip

最近在读《软技能：代码之外的生存指南》，看到营销的章节。对于有才华的人来说，营销就是一个「乘数效应」。你的营销越好，你的才华才能表现得淋漓尽致。自我营销的正确的方式是为别人提供价值，塑造好自己的形象，打造引人注目的品牌。对于软件开发人员，推荐的是博客。

## 4. Share

[Git Commit 日志风格指南](https://open.leancloud.cn/git-commit-message/)

这是 LeanCloud 技术团队的文章，主要讲了几点 Git 提交日志的规范。
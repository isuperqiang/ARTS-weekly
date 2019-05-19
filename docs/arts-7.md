## 1. Algorithm

#### 141. 环形链表（简单）

##### 描述：

> 给定一个链表，判断链表中是否有环。

##### 示例：

```properties
输入: [3,2,0,4,2]
输出: true
```

##### 思路：

> 使用快慢指针，慢指针每次移动一步，而快指针每次移动两步。如果存在环，那么两指针必定相遇。

##### 解法：

```java
class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null) {
            return false;
        }

        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {
                return true;
            }
        }
        return false;
    }
}
```

##### 分析：

- 时间复杂度：O(n)
- 空间复杂度：O(1)

-----

#### 172. 阶乘后的零（简单）

##### 描述：

> 给定一个整数 *n*，返回 *n*! 结果尾数中零的数量。

##### 示例：

```properties
输入: 5
输出: 1
解释: 5! = 120, 尾数中有 1 个
```

##### 思路：

> 只有 2 * 5 末尾才有零，乘数中 2 的个数肯定比 5 多。n! 为递减阶乘，只要统计乘数里因子 5 的个数就行了。

##### 解法：

```java
class Solution {
    // 递归法
    public int trailingZeroes1(int n) {
        if (n < 5) {
            return 0;
        } else {
            return n / 5 + trailingZeroes1(n / 5);
        }
    }

    // 迭代法
    public int trailingZeroes2(int n) {
        int count = 0;
        while (n >= 5) {
            count += n / 5;
            n /= 5;
        }
        return count;
    }
}
```

##### 分析：

- 时间复杂度：O(n)
- 空间复杂度：O(1)

## 2. Review

[Ace your first year as a junior developer with this advice](https://medium.freecodecamp.org/ace-your-first-year-as-a-junior-developer-with-this-advice-bbc68b6fe2d9) 初级开发者赢得首年的建议

文章主要从以下几个方面展开论述：

- 知识有缺口不可怕，软件开发者就要不断学习。
- 有问题是好事，要积极寻求帮助。
- 代码审查是你的朋友，从中可以学到很多。
- 把大任务拆解成小任务，写下步骤会更加清晰。
- 保持简洁。三个步骤：走通、重构、优化。测试驱动开发（TDD）
- 学习如何写整洁代码。平庸的程序员写出机器理解的代码，优秀的程序员写出人类可读的代码。
- 你遇到的问题大部分都有答案，所以先去寻找答案吧。比如到 GitHub、StackOverflow 上。
- 学会如何读代码。关注设计模式、方法类变量的命名、注释的使用、测试的使用。

## 3. Tip

这周末学习了 Dagger2 依赖注入框架，在 Android 开发中经常被使用。原理是这样的，它在编译阶段通过注解处理器扫描代码中的注解，然后自动生成辅助代码，简化了依赖注入的步骤，而且不会对性能产生任何影响，

## 4. Share

[从程序员到架构师 - 技能篇](https://mp.weixin.qq.com/s/M1E_UrkCQ3PNnGsyqpKc1A)

架构师只是功底深厚的程序员。程序员从初级、中级、高级再到架构师，是一个不断经验积累的过程。在程序员生涯中，除了技术实力以外，其它软实力也不容忽视。如：主动学习、积累经验、控制注意力、超越自我。

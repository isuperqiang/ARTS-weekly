## 1. Algorithm

#### 268. 缺失数字（简单）

##### 描述：

> 给定一个包含 0, 1, 2, ..., n 中 n 个数的序列，找出 0 .. n 中没有出现在序列中的那个数。

##### 示例：

```
输入: [3,0,1]
输出: 2
```

##### 思路：

- 解法一：用完整数组的元素之和减去当前数组的元素之和就可以了。
- 解法二：异或操作，eg: b^a^b=a; 相同的数字互相抵消，剩下的数值就是结果

##### 解法：

```java
class Solution {
    public int missingNumber1(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int numSum = 0;
        int allSum = nums.length;
        for (int i = 0; i < nums.length; i++) {
            numSum += nums[i];
            allSum += i;
        }
        return allSum - numSum;
    }

    public int missingNumber2(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int result = nums.length;
        for (int i = 0; i < nums.length; i++) {
            result ^= nums[i];
            result ^= i;
        }
        return result;
    }
}
```

##### 分析：

解法一和解法二一样。

- 时间复杂度：O(n)
- 空间复杂度：O(1)

#### 203. 移除链表元素（简单）

##### 描述：

> 删除链表中等于给定值 val 的所有节点。 

##### 示例：

```
输入: 1->2->6->3->4->5->6, val = 6
输出: 1->2->3->4->5
```

##### 思路：

- 解法一：首先检查头结点，如果结点值与val相等，那么把头指针后移；然后遍历链表，如果当前结点值与val相等，那么将前一个结点的指针指向后一个结点。
- 解法二：递归。

##### 解法：

```java
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        if (head == null) {
            return null;
        }
        while (head != null && head.val == val) {
            head = head.next;
        }
        ListNode curr = head;
        ListNode prev = curr;
        while (curr != null) {
            if (curr.val == val) {
                prev.next = curr.next;
            } else {
                prev = curr;
            }
            curr = curr.next;
        }
        return head;
    }

    public ListNode removeElementsRecursive(ListNode head, int val) {
        if (head == null) {
            return null;
        }
        head.next = removeElementsRecursive(head.next, val);
        return head.val == val ? head.next : head;
    }
}
```

##### 分析：

- 时间复杂度：O(n)
- 空间复杂度：O(1)

## 2. Review

[50+ Data Structure and Algorithms Interview Questions for Programmers](https://hackernoon.com/50-data-structure-and-algorithms-interview-questions-for-programmers-b4b1ac61f5b0) 50个数据结构和算法面试题

作者主要介绍了面试中常见的算法题，大多关于数组、链表、字符串、二叉树，还有其他等。

- 数组是最基本的线性数据结构，使用连续的存储空间。随机访问元素的时间复杂度 O(1)，添加和移除元素的时间复杂度是 O(n)。常见的题目有：数组反转、数据排序等。
- 链表也是一种线性数据结构，通过结点的指针连接，存储空间不连续。添加和移除元素的时间复杂度是 O(1)，查找元素的时间复杂度是 O(n)。解决链表问题不要忘记递归的思想。
- 字符串的问题也很常见，String 本质上就是字符数组，可以采用基于数组的解法。
- 树是一种有层次的数据结构，解决二叉树问题的关键是树的理论知识。比如：树的深度、大小、叶子结点，还有前序遍历、中序遍历、后序遍历。
- 其他的问题，比如算法、设计、位运算、逻辑题等，

## 3. Tip

重新复习了 Gradle 构建的知识。Gradle 构建就是围绕 Project 和 Task 展开的，Project 可以理解要构建的模块，Task 则是要执行的任务。Gradle 构建要经历初始化、配置和执行的过程，Task 之间存在依赖关系，开发者可以自由配置 Task，灵活性非常好。另外，Groovy 是基于 JVM 的语言，可以和 Java 兼容，语法和 Python 类似，封装了很多常用的 API，特别适合写脚本。

## 4. Share

[作为 IT 行业的过来人，你有什么话想对后辈说的？](https://www.zhihu.com/question/312019918)

从老一代 IT 人的经历中，得到一些发展和行为的启示。


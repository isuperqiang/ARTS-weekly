## 1. Algorithm

#### 83. 删除排序链表中的重复元素（简单）

##### 描述：

> 给定一个排序链表，删除所有重复的元素，使得每个元素只出现一次。

##### 示例：

```properties
输入: 1->1->2->3->3
输出: 1->2->3
```

##### 思路：

> 从头开始遍历链表，比较前后两个节点元素的值。如果相等就修改前置指针，不想等就继续往后移动。

##### 解法：

```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null) {
            return null;
        }
        ListNode lastNose = head;
        ListNode currentNode = head;
        while ((currentNode = currentNode.next) != null){
            if(lastNose.val == currentNode.val){
                lastNose.next = currentNode.next;
            } else {
                lastNose = currentNode;
            }
        }
        return head;
    }
}
```

##### 分析：

- 时间复杂度：O(n)
- 空间复杂度：O(1)

#### 231. 2 的幂（简单）

##### 描述：

> 给定一个整数，编写一个函数来判断它是否是 2 的幂次方。

##### 示例：

```properties
输入: 16
输出: true
解释: 24 = 16
```

##### 思路：

> 如果一个数是2的幂次，那么它的二进制表示一定只有一个1。比如8的二进制 00001000，现在把这个数减1，得到 00000111。发现低4位是按位取反，这时候（n&n-1）的结果就一定是0。如果一个数不是2的幂次，那么它的二进制数里1的个数就大于1（0除外）。n 和 n-1 就不会出现左边都是0的现象了，n&(n-1) 一定不是0。

##### 解法：

```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        if (n <= 0) {
            return false;
        }
        return (n & (n - 1)) == 0;
    }
}
```

##### 分析：

- 时间复杂度：O(1)
- 空间复杂度：O(1)

## 2. Review

[Why you are never too old to learn Java (or any programming language)](https://medium.freecodecamp.org/why-you-are-never-too-old-to-learn-java-or-any-programming-language-a62603e89448) 为什么任何时候学习 Java 都不算晚

作者是位 Java 课程的讲师，文章的主旨是任何时候学习一项新技能都不算晚，比如 30 多岁学习编程。职业不是终身不变的，只要你愿意，就可以不断学习。学到老，学到老。

作者阐述了学习 Java 的 5 个原因：

- 学习新东西，可以活跃你的大脑，大脑总是越用越灵活。
- 现在有许多在线课程和资料，没有人在乎你的年龄。
- 年龄无关，想学新东西什么时候都不晚。
- 学习 Java 就像学习其他技能一样。
- 现在就是最好的时间，开始学习吧。

这是作者针对国外的情况写的，从国内的环境来看，30多岁再学习编程，进入企业的优势非常小。明明是一门靠手艺吃饭的职业，非要变成靠体力消耗，程序员年轻化已经成为常态。

## 3. Tip

最近在学习音视频编解码。简单来讲，编码就是压缩，解码就是解压。编码的目的是减小数据的体积，方便网络传输和本地存储。编码后的数据是不能直接使用的，必须先解码成原来的样子。就像 zip 压缩文件里面有张图片，我们用图片查看器是无法打开的，必须先解压文件，恢复图片原来的数据，这样才能查看。音视频编解码也是同样的道理。

## 4. Share

[写代码这条路，能走多远？工程师能力模型告诉你](https://mp.weixin.qq.com/s/qGC08VgXc66t0WT7mgZxhA)

从能力习得速度和技能演进速度两个维度分析，程序员发生职业危机的可能性非常高。解决问题的三条出路：技术专家、管理岗、产品运营等。适合于走哪个路线，需要结合自己的性格来定。

技术专家的能力模型，处于中心的是行为处事的准则，也就是正确的思想观念。其中最核心的观念就是要把职业生涯当作自己的事业，为自己而工作，把提升自身能力作为事业的目标。围绕着这一核心的还包括以结果导向、主动承担责任的观念和既精又专的技术、团队协作能力等。
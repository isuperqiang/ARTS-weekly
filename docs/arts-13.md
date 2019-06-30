## 1. Algorithm

#### 242. 有效的字母异位词（简单）

##### 描述：

> 给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。

##### 示例：

```
输入: s = "anagram", t = "nagaram"
输出: true
```

##### 思路：

统计 s 中每个字母出现的次数，遍历 t 中的字母减去相应的次数。如果次数小于 0，那么认为是 false。

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s == null || t == null || s.length() != t.length()) {
            return false;
        }

        int[] counter = new int[26];
        for (int i = 0, size = s.length(); i < size; i++) {
            counter[s.charAt(i) - 'a']++;
        }
        for (int i = 0, size = t.length(); i < size; i++) {
            char c = t.charAt(i);
            counter[c - 'a']--;
            if (counter[c - 'a'] < 0) {
                return false;
            }
        }
        return true;
    }
}
```

##### 分析：

- 时间复杂度：O(n)
- 空间复杂度：O(1)

-----

## 2. Review

[How to Become a Better Software Developer](https://medium.com/devtrailsio/how-to-become-a-better-software-developer-dd16072c974e) 如何成为更好的软件开发者

作者分享了一些提升技能和高效工作的方法，这里简单列举几条：

- 从端到端理解流程。程序员不要低头写代码，应该关注软件开发的其他方面，比如产品、设计、测试等。
- 理解客户的需求。客户不懂技术，我们要赢得客户的信任，多站在客户的角度考虑。
- 为工作选择正确的工具。不要限制自己思维，要提出不同的方案。尝试新事物时，要注意到安全性。
- 站在巨人的肩膀上。不要重复造轮子，但是可以通过重新实现来学习。
- 关心自己如何工作。提升个人和团队的研发效能，比如完善的工作流程、项目计划等。
- 专注于基础。IT 行业瞬息万变，新框架层出不穷，唯有基础知识是一成不变的。
- 其他的经验：积极分享知识，不要指责自己和他人，不要做刺头。

## 3. Tip

最近在读《Java并发编程实战》，里面讲了一些线程安全的技巧和概念，比如原子性、可见性、不可变对象。线程安全的核心在于对共享和可变的对象进行访问控制，采用同步机制（synchronized），同步的代码块保持精细。不可变对象一定是线程安全的，比如 String。加锁机制可以确保可见性和原子性，而 volatile 只能保证可见性。

## 4. Share

19 年过半，我发现有些目标做到一半就停止了，执行力还需要提高。计划-执行-坚持。
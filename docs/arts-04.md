## 1. Algorithm

#### 20. 有效的括号

##### 描述：

> 给定一个只包括 `'('`，`')'`，`'{'`，`'}'`，`'['`，`']'` 的字符串，判断字符串是否有效。
>
> 有效字符串需满足：
>
> 1. 左括号必须用相同类型的右括号闭合。
> 2. 左括号必须以正确的顺序闭合。
>
> 注意空字符串可被认为是有效字符串。

##### 示例：

```properties
输入: "()[]{}"
输出: true
输入: "([)]"
输出: false
```

##### 思路：

> 利用栈的「后进先出」的特点，将左括号压栈，然后和最近的右括号匹配。匹配成功则出栈，继续匹配下一个，否则算作失败。完全匹配时，最后的栈为空，即为有效的括号。

##### 解法：

```java
class Solution {
    public boolean isValid(String s) {
        if (s == null) {
            return false;
        }
        char[] chars = s.toCharArray();
        LinkedList<Character> stack = new LinkedList<>();
        for (char aChar : chars) {
            if (aChar == '(' || aChar == '[' || aChar == '{') {
                stack.push(aChar);
            } else {
                Character peek = stack.peek();
                if (peek != null && isMatch(peek, aChar)) {
                    stack.pop();
                } else {
                    return false;
                }
            }
        }
        return stack.isEmpty();
    }

    private boolean isMatch(char left, char right) {
        if (left == '(' && right == ')') {
            return true;
        }
        if (left == '{' && right == '}') {
            return true;
        }
        if (left == '[' && right == ']') {
            return true;
        }
        return false;
    }
}
```

##### 分析：

- 时间复杂度：O(n)
- 空间复杂度：O(n)

#### 155. 最小栈（简单）

##### 描述：

> 设计一个支持 push，pop，top 操作，并能在常数时间内检索到最小元素的栈。
> - push(x) -- 将元素 x 推入栈中。
> - pop() -- 删除栈顶的元素。
> - top() -- 获取栈顶元素。
> - getMin() -- 检索栈中的最小元素。

##### 示例：

```properties
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.getMin();   --> 返回 -2.
```

##### 思路：

>   每次入栈 2 个元素，一个是要入栈的元素本身，一个是当前栈内元素的最小值。
>   如：入栈序列为 2-3-1，则入栈后元素序列为：2-2-3-2-1-1。用空间代价来换取时间代价

##### 解法：

```java
class MinStack {
    private Stack<Integer> stack = new Stack<>();
    
 		public void push(int x) {
        if (stack.isEmpty()) {
            stack.push(x);
            stack.push(x);
        } else {
            Integer currMin = stack.peek();
            stack.push(x);
            stack.push(x < currMin ? x : currMin);
        }
    }

    public void pop() {
        stack.pop();
        stack.pop();
    }

    public int top() {
        return stack.get(stack.size() - 2);
    }

    public int getMin() {
        return stack.peek();
    }

}
```

## 2. Review

[The junior developer’s guide to writing super clean and readable code](https://medium.freecodecamp.org/the-junior-developers-guide-to-writing-super-clean-and-readable-code-cd2568e08aae) 初级开发者如何写出整洁可读的代码

作者主要讲述了整洁代码的特征，以及如何写出整洁的代码。clean code 就该像文章一样段落清晰、层次分明、结构严谨。clean code 有这么几个特征：

- 它是专注的，只做一件事
- 它是优雅的，会让你微笑
- 它是易维护的
- 它是通过测试的

下面给出了几个建议：

- 使用一致的格式和缩进
- 使用清晰的变量和方法名
- 如有必要，请使用注释
- 遵循 DRY (Don't repeat yourself) 原则

另外，推荐阅读[《代码整洁之道》](https://book.douban.com/subject/4199741/)，英文名《Clean Code: A Handbook of Agile Software Craftsmanship》。

## 3. Tip

[GitHub](https://github.com) 上有许多好玩的东西， 比如 [BaiduPSC-Go](https://github.com/iikira/BaiduPCS-Go) 一个使用命令行的百度客户端，不限速，非常极客。[Dress](https://github.com/komeiji-satori/Dress) 男孩子的女装照。[libpku](https://github.com/lib-pku/libpku) 贵校课程资料民间整理，大学的课程资料等。

经常去 [Explore](https://github.com/explore) 一下项目，就可以发现热门，GitHub 真是个神奇的地方。

## 4. Share

最近在重新学王争的《数据结构与算法之美》专栏，理解理论知识，动手写代码，输出[学习笔记](https://isuperqiang.cn/tag/datastruct-algorithm/)。算法是编程的内功，可以通过刻意练习来修炼，每天一道 LeetCode 题目就够了。
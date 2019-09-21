## 1. Algorithm

#### 22. 生成括号（中等）

##### 描述：

> 给出 n 代表生成括号的对数，请你写出一个函数，使其能够生成所有可能的并且有效的括号组合。

##### 示例：

```
例如，给出 n = 3，生成结果为：
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

##### 思路：

**动态规划**

生成 N 对括号，必然有 N 个左括号和 N 个右括号，左括号的数量大于等于右括号。要确定 N 对，首先确定 N-1 对，利用递归求解。

left 记录左括号的数量，right 记录右括号的数量，当左右括号的数量相等时，记录结果，结束递归。

```java
class Sulution {
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];
        for (int i = 0; i < m; i++) {
            dp[i][0] = 1;
        }
        for (int i = 0; i < n; i++) {
            dp[0][i] = 1;
        }
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
        return dp[m - 1][n - 1];
    }
}
```

##### 分析：

- 时间复杂度：O(n)
- 空间复杂度：O(n)

## 2. Review

[The Two Types of Programmers](https://blog.codinghorror.com/the-two-types-of-programmers/) 两种程序员

在软件开发领域，有两种程序员：20% 的开拓者，他们对技术痴迷，紧跟最新趋势。还有 80% 的普通人，编程对于他们只是工作，工作之外不关心代码。这两类人群有着巨大的鸿沟，如果要改变软件开发的现状，就要在这两类人群之间建立连接。

## 3. Tip

[花椒移动端基础框架架构](https://mp.weixin.qq.com/s/QMhMSJ95Kl0tdE-jb1Jvgw) 这篇文章总结了移动端的架构，对移动应用架构设计有参考价值。

## 4. Share

[总结几点“上不得台面”的技术领导经验](https://mp.weixin.qq.com/s/XXSkDygqm2RY8YqmJCyJWw)

在我看来，身为技术领导，对技术的敬畏、诚实谦和、尊重客观、力求平等，应当是始终不变的坚持。但是，在坚韧的骨骼之外，让身段变柔软一点，总不是坏事。
## 1. Algorithm

#### [零钱兑换](https://leetcode-cn.com/problems/coin-change/)（中等）

##### 描述：

>  给定不同面额的硬币 coins 和一个总金额 amount。编写一个函数来计算可以凑成总金额所需的最少的硬币个数。如果没有任何一种硬币组合能组成总金额，返回 -1。
>  你可以认为每种硬币的数量是无限的。

##### 示例：

```
输入: coins = [1, 2, 5], amount = 11
输出: 3 
解释: 11 = 5 + 5 + 1
```

##### 思路：

动态规划：dp[i] 表示总金额为 i 时至少需要的硬币个数，初始赋值 amount+1 表示不可能取到的值。注意总金额要不小于硬币面值，而且保证总金额可以被硬币凑出来。

```java
class Sulution {
    public int coinChange(int[] coins, int amount) {
        if (coins == null || coins.length == 0) {
            return -1;
        }
        int length = amount + 1;
        int[] dp = new int[length];
        Arrays.fill(dp, length);
        dp[0] = 0;
        for (int i = 0; i < dp.length; i++) {
            for (int coin : coins) {
                if (i >= coin) {
                    dp[i] = Math.min(dp[i], dp[i - coin] + 1);
                }
            }
        }
        return dp[amount] == length ? -1 : dp[amount];
    }
}
```

##### 分析：

- 时间复杂度：O(N * k)，k 为硬币个数
- 空间复杂度：O(N)

## 2. Review

[Why you should totally switch to Kotlin](https://medium.com/@magnus.chatt/why-you-should-totally-switch-to-kotlin-c7bbde9e10d5) 为什么你该完全切换到 Kotlin

介绍了 Kotlin 的特性，与 Java 互操作、类型推断、空安全、数据类等，Kotlin 是现代化的语言，其特性会令开发者喜欢。

## 3. Tip

遇到 crash 如何解决呢？分享一下我的经验。

首先查看 stack trace，找到报错的类型、信息、代码文件和行数，常见的异常有 NullPointerException、ClassCastException、IndexOutOfBoundException 等，根据信息就大概可以知道报错原因。如果之前没见过这种异常，把信息复制粘贴到谷歌搜索，排名靠前的搜索结果都来自 Stack Overflow，说不定前人也碰到了类似的错误，从问题回复中就能找到答案，这就要求英文阅读能力要过关。最后如果实在搜不到，那只能请教大佬了。

## 4. Share

分享两个网站，收录了 Windows 和 Mac 平台上的优质软件。

- [Awesome-Windows](https://github.com/Awesome-Windows/Awesome/blob/master/README-cn.md)
- [Awesome-Mac](https://github.com/jaywcjlove/awesome-mac/blob/master/README-zh.md)
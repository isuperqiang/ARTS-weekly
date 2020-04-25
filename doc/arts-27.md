## 1. Algorithm

#### [判定字符是否唯一](https://leetcode-cn.com/problems/is-unique-lcci/)（简单）

##### 描述：

> 实现一个算法，确定一个字符串 s 的所有字符是否全都不同。
>

##### 示例：

```
输入: s = "leetcode"
输出: false 
输入: s = "abc"
输出: true
```

##### 思路：

- 统计次数：使用一个额外的 int 数组，统计每个字符出现的次数。
- 位运算：int 类型有 32 位，取其中的低 26 位，作为每个字符的标志位，通过左移、与、或运算，记录每个字符的对应位置。真是高级解法！

```java
class Sulution {
    public boolean isUnique1(String astr) {
        if (astr == null || astr.length() == 0) {
            return true;
        }
        int[] counts = new int[26];
        for (int i = 0, length = astr.length(); i < length; i++) {
            int pos = astr.charAt(i) - 'a';
            if (counts[pos] >= 1) {
                return false;
            }
            counts[pos] += 1;
        }
        return true;
    }

    public boolean isUnique2(String astr) {
        if (astr == null || astr.length() == 0) {
            return true;
        }
        int mark = 0;
        for (int i = 0, length = astr.length(); i < length; i++) {
            int flag = 1 << (astr.charAt(i) - 'a');
            if ((mark & flag) != 0) {
                return false;
            } else {
                mark |= flag;
            }
        }
        return true;
    }
}
```

##### 分析：

统计次数：
- 时间复杂度：O(N)
- 空间复杂度：O(N)

位运算：
- 时间复杂度：O(N)
- 空间复杂度：O(1)

## 2. Review

[How to Go from Junior to Senior Programmer](https://levelup.gitconnected.com/how-to-go-from-junior-to-senior-programmer-29d53f3edd27)  [如何从初级程序员变成高级程序员？](https://www.infoq.cn/article/6gagslvv3x5oQLpaVpv8)

从 InfoQ 看到的一篇译文，算是经验之谈。高工不是根据经验判定，而是分析的技能。深有同感，我总是把代码放在第一位，有时候忽略了业务场景，考虑问题的出发点不同，导致任务处理方式也不同。代码只是一部分，真正的目的是解决问题。

> 一名程序员不会因为他会写代码而成为一名合格的程序员，而是因为在开始做任何事情之前先做分析，然后再来开展工作，这才是真正的程序员。

## 3. Tip

最近某 BAT 之一坑害了 pandownload，真的是令人发指！自己的产品做得烂不去反思，却耍小伎俩坑无辜的开发者。天下苦 B 久矣，作为程序员，从抵制 B 开始。推荐一个好用的木弟子 [AgentNeo](https://neoproxy.org/?rc=r1gv64bl)，线路非常稳定，价格也实惠。通过我的链接注册，可以享受 5 元优惠 https://neoproxy.org/?rc=r1gv64bl。 （结算时选择团购下单，团购代码 21853G0V，享受 8 折优惠，活动截止 2020-04-25）

## 4. Share

在 GitHub 上搜了一些 Android 面试资料 http://note.youdao.com/noteshare?id=a04ac812925b23f6dc112eda70079c53 愿步步高升。

**题外话：**

由于个人原因，ARTS 暂停了将近半年，后续恢复打卡，请见谅。
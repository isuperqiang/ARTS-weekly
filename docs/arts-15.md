## 1. Algorithm

#### 287. 寻找重复数（中等）

##### 描述：

> 给定一个包含 n + 1 个整数的数组 nums，其数字都在 1 到 n 之间（包括 1 和 n），可知至少存在一个重复的整数。假设只有一个重复的整数，找出这个重复的数。

##### 示例：

```
输入: [1,3,4,2,2]
输出: 2
```

##### 说明：
- 不能更改原数组（假设数组是只读的）。
- 只能使用额外的 O(1) 的空间。
- 时间复杂度小于 O(n2) 。
- 数组中只有一个重复的数字，但它可能不止重复出现一次。

##### 思路：

数组元素在 [0, n] 之间，可以作为数组索引使用。先通过快慢指针找到相交点，然后两个指针分别从零位置和相交点一起向前遍历，直到找出相同的值。

```java
class Solution {
    public int findDuplicate(int[] nums) {
        if (nums == null || nums.length == 0) {
            return -1;
        }

        int fast = nums[0];
        int slow = nums[0];
        do {
            slow = nums[slow];
            fast = nums[nums[fast]];
        } while (fast != slow);

        slow = nums[0];
        while (fast != slow) {
            slow = nums[slow];
            fast = nums[fast];
        }
        return fast;
    }
}
```

##### 分析：

- 时间复杂度：O(n)
- 空间复杂度：O(1)

-----

## 2. Review

[Key habits and things I wish I knew earlier as a developer](https://medium.com/@rhamedy/key-habits-and-things-i-wish-i-knew-earlier-as-a-developer-43c9466a0407) 作为开发者，我希望尽早知道的习惯和事情

作者总结了开发者应该尽早熟知的东西，比如习惯、技能、观念等。

- 有效地使用搜索引擎
- 使用现代化的 IDE 提高生产力
- 学习 Linux
- 学习 Git
- 自我学习，跟随技术潮流
- 至少精通一门编程语言
- 聚焦简约
- 加入团体或者论坛
- 建立你的个人档案
- 提问，提问，提问
- 写代码前先在纸上比划
- 遵守技术规范，先写测试用例
- 在日常中解决难题和挑战
- 开始白板编程
- 高效地管理时间
- 保护个人隐私
- 跟随激励你的个人和组织
- 参加技术活动
- 拥抱错误消息
- 选择正确类型的公司作为事业
- 建立一套工作方案，不断迭代使其完美
- 对自己 SEO

下面几点需要注意：

- 不轻言放弃
- 不拷贝工程代码
- 不要推迟
- 不要忽略其他学科
- 不要沉迷社交网络
- 不是失去希望

## 3. Tip

[Homebrew](https://brew.sh/) 真是 Mac 上的神器，软件开发包都可以通过命令安装，自动配置环境变量，brew cask 还可以安装 GUI 应用程序。brew 在手，软件我有。

## 4. Share

公司 Q2 季度考核，根据实际情况，自评打了高分，我觉得是对的。caoz 有篇文章：[你矜持，你活该](https://mp.weixin.qq.com/s?src=11&timestamp=1563019087&ver=1726&signature=9fQ4ZX*rEFkwGbhmEqH4Q4-cRmJ2hjBIU8yPq85eD-OesZsWf*n85fixDcGv*hq9aAgqwCiQh0XnA*UiH9S6m9ECXXcIVCvm6eep1MgZFSPRG5IflvDrl5F3206kzQRg&new=1) 讲过。

职场不要太矜持，合作沟通的时候姿态低一些，争取权益的时候胆子大一些。

创业不能太矜持， 宣传营销的时候，该吹牛的时候敢吹牛，不要怕丢脸。业务合作的时候，该低姿态的时候低姿态，不要老端着。

有些技术人才我知道的，在企业不是很顺心，有些权益期待但没有落实，又觉得老板一直对自己不错，总觉得不好意思提要求，其实该争取的要争取，人家稍微温情两句，自己就开始自责了，哪那么多戏。

你矜持，你端着，你失去好机会，你权益无保障，你自废武功，你男/女神被人追跑了，你活该。
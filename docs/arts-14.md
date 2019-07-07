## 1. Algorithm

#### 78. 子集（中等）

##### 描述：

> 给定一组不含重复元素的整数数组 nums，返回该数组所有可能的子集（幂集）。解集不能包含重复的子集。

##### 示例：

```
输入: nums = [1,2,3]
输出:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

##### 思路：

利用二进制与位运算：
数组中的每个元素，都有两个状态：在子数组中和不在子数组中。所有状态的组合就是所有的子数组。
遍历 000 到 111，也就是 0 到 7，判断每个比特位是否为 1，如果是 1，那么将对应数字加入子数组。

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        if (nums == null || nums.length == 0) {
            return Collections.emptyList();
        }

        List<Integer> subList;
        int resultLength = 1 << nums.length;
        List<List<Integer>> resultList = new ArrayList<>(resultLength);
        for (int i = 0, numsLength = nums.length; i < resultLength; i++) {
            subList = new ArrayList<>(numsLength);
            for (int j = 0; j < numsLength; j++) {
                if ((i >> j & 1) == 1) {
                    subList.add(nums[j]);
                }
            }
            resultList.add(subList);
        }
        return resultList;
    }
}
```

##### 分析：

- 时间复杂度：O(n^2)
- 空间复杂度：O(n)

-----

## 2. Review

[What I Learned in My First Two Years as a Software Engineer](https://blog.usejournal.com/what-i-learned-in-my-first-two-years-as-a-software-engineer-4e374fdcf0fd) 在我做软件工程师的前两年里学到了什么

作者讲了两个故事。

第一个故事，读大学时导师布置任务，完成好的学生会被分到一组，完成差的学生要么努力挤进好学生队伍，要么放弃，好学生不会帮助差学生，导师奖励做得好的学生。然而进入公司后，如果再采用这种原则，同事之间不免发生矛盾。完成任务不是唯一的事情，与同事的关系和硬技能同样重要。

第二个故事，作者在结对编程时遇到了 Bob，Bob 经常对项目提出问题，帮助作者解决潜在的 bug，此时无招胜有招，因此作者非常佩服 Bob。优秀的问题解决者在给出方案之前，会提出很多问题，用论证影响团队的成员，表现出领导力。

最后，作者总结了一些教训。处理好与同事的关系，编程不比家庭、友谊、健康重要，尽可能做最好的工程师。

## 3. Tip

《Java并发编程实战》中讲到单例设计模式的几种线程安全的实现方式：延迟初始化、提前初始化、延迟初始化占位类和双重检查锁。其中，双重检查锁的实例变量要声明为 volatile 才有效，作者称其为糟糕的实现，不如静态的占位类优雅。

## 4. Share

近期在优化项目代码，发现在渲染每帧图像的时候，存在大量无用的对象创建。这么来看，Android 屏幕的刷新速率是 60 FPS，高密集地创建对象导致堆空间占满，造成频繁的垃圾回收，不利于程序的性能。我们要避免这种操作，做一个环保的程序员。
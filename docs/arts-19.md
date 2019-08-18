## 1. Algorithm

#### 46. 全排列（中等）

##### 描述：

> 给定一个没有重复数字的序列，返回其所有可能的全排列。

##### 示例：

```
输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

##### 思路：

回溯法。深度优先搜索（DFS）和交换元素

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        if (nums == null || nums.length == 0) {
            return null;
        }
        List<List<Integer>> result = new ArrayList<>();
        dfs(0, nums, result);
        return result;
    }

    private void dfs(int curr, int[] nums, List<List<Integer>> result) {
        if (curr == nums.length - 1) {
            List<Integer> res = new ArrayList<>();
            for (int num : nums) {
                res.add(num);
            }
            result.add(res);
            return;
        }
        for (int i = curr; i < nums.length; i++) {
            swap(nums, i, curr);
            dfs(curr + 1, nums, result);
            swap(nums, i, curr);
        }
    }

    private void swap(int[] nums, int i, int j) {
        int t = nums[i];
        nums[i] = nums[j];
        nums[j] = t;
    }
}
```

## 2. Review

[These four “clean code” tips will dramatically improve your engineering team’s productivity](https://engineering.videoblocks.com/these-four-clean-code-tips-will-dramatically-improve-your-engineering-teams-productivity-b5bd121dd150) 这四个「整洁代码」的技巧将极大地提高工程团队的生产力

作者列举了整洁代码的四个技巧：

- 如果没有经过测试，代码就是不合格的

    要写大量的测试，特别是单元测试，否则你会后悔的。

- 选择有意义的名字

    为变量、类和函数，起一个短小准确的名字。

- 类和函数应该短小，遵循单一职责法则

    函数不该超过 4 行，类代码不该超过 100 行。它们做并且只做一件事。

    （点评：这里阈值太低，可以适量放大。《阿里巴巴 Java 开发手册》里讲到：方法一般不超过 80 行）

- 函数不该产生副作用

    副作用（比如修改输入参数）是魔鬼，代码里面千万不要有，尽可能在函数契约中明确指定这一点。

## 3. Tip

有时候觉得 IDE 太重量级了，打开个工程都要十几秒。相比之下，Sublime 是轻量级的编辑器，每次几乎秒开，代码显示友好，有丰富的插件。每个程序员都该熟练使用一种 IDE 之外的编辑器，IDE 不总是可靠的，或许也尝试白板编程。

## 4. Share

前些天，有个头条的同行和我聊，说他们面试非常看重基础。基础是什么？我觉得包括这几项：算法和数据结构、操作系统、计算机网络、数据库原理、设计模式等。这些是经久不衰的、不依赖具体语言的基础原理。想要在编程路上走得长远，静下心来研究基础非常必要。
## 1. Algorithm

#### 15. 三数之和（中等）

##### 描述：

> 给定一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？找出所有满足条件且不重复的三元组。

##### 示例：

```
例如, 给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

##### 思路：

**双指针法**

首先对数组进行排序，然后固定一个数 nums[i]，使用左右指针分别指向 nums[i] 后面的两端。计算三个数的和 sum，判断 sum 是否满足为 0。如果满足则添加进结果集，否则左右指针交替向中间移动。同时注意去重。

```java
class Sulution {
    public List<List<Integer>> threeSum(int[] nums) {
        if (nums == null || nums.length < 3) {
            return Collections.emptyList();
        }
        Arrays.sort(nums);
        List<List<Integer>> result = new ArrayList<>();
        int length = nums.length;
        for (int i = 0; i < length; i++) {
            if (nums[i] > 0) {
                break;
            }
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            int l = i + 1, r = length - 1;
            while (l < r) {
                int s = nums[i] + nums[l] + nums[r];
                if (s == 0) {
                    while (l < r && nums[l] == nums[l + 1]) {
                        l++;
                    }
                    while (l < r && nums[r] == nums[r - 1]) {
                        r--;
                    }
                    result.add(Arrays.asList(nums[i], nums[l], nums[r]));
                    l++;
                    r--;
                } else if (s > 0) {
                    r--;
                } else {
                    l++;
                }
            }
        }
        return result;
    }

}
```
##### 分析：

- 时间复杂度：O(n^2)
- 空间复杂度：O(1)

## 2. Review

[Advanced Coding Skills, Techniques, and Ideas](https://medium.com/@maladdinsayed/advanced-techniques-and-ideas-for-better-coding-skills-d632e9f9675)

作者列举了一些编程的技巧。

- 重构可以帮助我们写出整洁的代码，可读可维护可重用。
- 不要重构生产环境中没有经过单元测试的代码，要想重构，先单元测试。
- 从代码的最深处开始重构，最深处只关注单一的逻辑，这使得重构更加容易。
- 使你的方法变得短小，通过把它们拆分成更小的方法。
- if 语句后面总是跟着 {}，即使只有一行。
- 不要使用魔法值，因为它的可读性太差了，可以抽取出变量或者常量。
- 如果没有必要，不要使用 else 语句，比如 if 语句中有 return 时，语句块外不需要 else。
- 为你的方法、变量和测试选择有意义的命名。
- 使用你的编程语言的最大能力，这样会省力，增强代码的健壮性。
- ……

代码经验都要靠积累，推荐阿里巴巴的[代码规约](https://github.com/alibaba/p3c)。

## 3. Tip

最近在读[《深入理解计算机系统》](https://book.douban.com/subject/1230413/)，又称 CSAPP，真是神书！读完第一章，对计算机系统有了新的认识——[深入理解计算机系统之计算机系统漫游](https://isuperqiang.cn/post/shen-ru-li-jie-ji-suan-ji-xi-tong-zhi-ji-suan-ji-xi-tong-man-you/)。

## 4. Share

说一说如何选书。写书是一件正式的活动，作者都会认真对待。但是作者的经验水平不一样，产出的内容质量也参差不齐。对于追热点的、空洞无物的、作者资历尚浅的图书，一般不值得阅读。辨别的方式是看豆瓣评分，经过时间筛选过的经典，最值得阅读。
## 1. Algorithm

#### 108. 将有序数组转换为二叉搜索树（简单）

##### 描述：

> 将一个按照升序排列的有序数组，转换为一棵高度平衡二叉搜索树。本题中，一个高度平衡二叉树是指一个二叉树每个节点的左右两个子树的高度差的绝对值不超过 1。

##### 示例：

```
给定有序数组: [-10,-3,0,5,9],
一个可能的答案是：[0,-3,9,-10,null,5]，它可以表示下面这个高度平衡二叉搜索树：

      0
     / \
   -3   9
   /   /
 -10  5
```

##### 思路：

以数组的中间元素为根节点，将数组分为左右两部分，用递归的方法对两个子数组分别构建左右子树。

```java
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        if (nums == null || nums.length == 0) {
            return null;
        }
        return toBst(nums, 0, nums.length - 1);
    }

    private TreeNode toBst(int[] nums, int l, int r) {
        if (l > r) {
            return null;
        }
        int mid = l + (r - l) / 2;
        TreeNode root = new TreeNode(nums[mid]);
        root.left = toBst(nums, l, mid - 1);
        root.right = toBst(nums, mid + 1, r);
        return root;
    }
}
```

##### 分析：

- 时间复杂度：O(logn)
- 空间复杂度：O(1)

-----

## 2. Review

[TDD Changed My Life](https://medium.com/javascript-scene/tdd-changed-my-life-5af0ce099f80) TDD 改变了我的人生

TDD 是测试驱动开发，先写测试用例，再写实现代码。作者讲了一个切身的经历，debug 到奔溃也没有发现问题。如果提前写好单元测试，就能及早发现这个 bug。软件开发就是模块的组装，单元测试针对某个功能，每个部件都通过验证，那么整个系统也得到保证。

## 3. Tip

[Java 比较浮点数的正确方式](https://isuperqiang.cn/post/java-bi-jiao-fu-dian-shu-de-zheng-que-fang-shi/) 重新认识了浮点数，彻底解决了以前踩过的坑。

## 4. Share

一本书不读完，坚决不碰下一本。最近读书一直虎头蛇尾，看到一半就停下来看其他的。碎片化的生活，耐心越来越稀缺，我想静下心来，踏踏实实做下去。
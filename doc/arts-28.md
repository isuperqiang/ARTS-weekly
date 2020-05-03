## 1. Algorithm

#### [旋转数组](https://leetcode-cn.com/problems/rotate-array/)（简单）

##### 描述：

> 给定一个数组，将数组中的元素向右移动 k 个位置，其中 k 是非负数。
> 尽可能想出更多的解决方案，至少有三种不同的方法可以解决这个问题。
> 要求使用空间复杂度为 O(1) 的原地算法。 

##### 示例：

```
输入: [1,2,3,4,5,6,7] 和 k = 3
输出: [5,6,7,1,2,3,4]
```

##### 思路：

- 暴力解法：循环 K 次，每次移动一个元素。时间复杂度：O(k*N)，空间复杂度：O(1)。

```java
class Sulution {
    public void rotate(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return;
        }
        int length = nums.length;
        int temp;
        for (int i = 0; i < k; i++) {
            temp = nums[length - 1];
            for (int j = length - 1; j > 0; j--) {
                nums[j] = nums[j - 1];
            }
            nums[0] = temp;
        }
    }
}
```

- 额外空间：使用额外数组保存旋转后的元素，把原数组下标是 i 的元素放到临时数组 (i+k)%nums.length 的位置，然后写回原数组。时间复杂度：O(N)，空间复杂度：O(N)。

```java
class Sulution {
    public void rotate(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return;
        }
        int[] temp = new int[nums.length];
        for (int i = 0; i < nums.length; i++) {
            temp[(i + k) % nums.length] = nums[i];
        }
        System.arraycopy(temp, 0, nums, 0, nums.length);
    }
}
```

- 环状替换：计算每个元素的最终位置，每次迭代时替换到正确位置并保存被替换的值，计算被替换值的正确位置。以 K 为步长跳跃，如果跳跃回原地，就从下一个位置继续。时间复杂度：O(N)，空间复杂度：O(1)。

```java
class Sulution {
    public void rotate(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return;
        }
        k = k % nums.length;
        int count = 0;
        for (int start = 0; count < nums.length; start++) {
            int currentI = start;
            int currentE = nums[start];
            do {
                int nextI = (currentI + k) % nums.length;
                int temp = nums[nextI];
                nums[nextI] = currentE;
                currentE = temp;
                currentI = nextI;
                count++;
            } while (start != currentI);
        }
    }
}
```

- 三次反转：当我们旋转数组 k 次， k%n 个尾部元素会被移动到头部，剩下的元素会被向后移动。时间复杂度：O(N)，空间复杂度：O(1)。

```java
class Sulution {
  // 原始数组                  : 1 2 3 4 5 6 7
  // 反转所有数字后             : 7 6 5 4 3 2 1
  // 反转前 k 个数字后          : 5 6 7 4 3 2 1
  // 反转后 n-k 个数字后        : 5 6 7 1 2 3 4 --> 结果
    public void rotate(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return;
        }
        k = k % nums.length;
        reverse(nums, 0, nums.length - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, nums.length - 1);
    }
    
    private void reverse(int[] arr, int start, int end) {
        while (start < end) {
            int temp = arr[start];
            arr[start] = arr[end];
            arr[end] = temp;
            start++;
            end--;
        }
    }
}
```

## 2. Review

[Programming Habits You Should Adopt](https://levelup.gitconnected.com/programming-habits-you-should-adopt-8ab75419fb09) 你应该养成的编程习惯

作者列举了 7 个编程习惯：

- 不要写重复代码。遇到重复代码，就该考虑重构了。
- 一旦认为自己完成了，开始重构吧。实现需求并不代表完成，接下来就该重构。
- 聚焦业务逻辑。不要总是专注于业务之外的技术栈，做好工作内容更重要。
- 短小精简的提交。便于回滚排查问题和代码审查。
- 一致性很关键。坚持标准的代码规范，提升代码的可维护性。
- 多做一步。完成任务意味着解决 todo，单元测试，编写文档。
- 不要停止学习。一直做自己熟练的事情，是不会得到成长的。

## 3. Tip

近期看了 Kotlin 语言，感觉是增强型的 Java，简洁灵活安全省心。同样基于 JVM，弥补 Java 的不足，编程语言总是在进化，Google 力推 Kotlin 作为 Android 开发语言是正确的。建议新项目尝试 Kotlin，老项目继续用 Java，两者还可以混编。Have a try :)

## 4. Share

在 Twitter 上看到陈皓发的推文，从程序员职业发展的角度评论编程语言，有生命力、有市场需求的语言值得投入。原帖在这里：https://twitter.com/haoel/status/1254974994964086785

![有生命力语言的特征](https://richie-storage.oss-cn-hangzhou.aliyuncs.com/img/EWqQTnKU4AES4-K.png)

![陈皓评论语言](https://richie-storage.oss-cn-hangzhou.aliyuncs.com/img/EWqQRcGUcAAKt6z.png)
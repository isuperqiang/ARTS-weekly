## 1. Algorithm

#### 152. 乘积最大子序列（中等）

##### 描述：

> 给定一个整数数组 nums ，找出一个序列中乘积最大的连续子序列（该序列至少包含一个数）。

##### 示例：

```
输入: [2,3,-2,4]
输出: 6
解释: 子数组 [2,3] 有最大乘积 6。
```

##### 思路：

- 解法一：暴力解法，遍历数组，逐个求出连续子序列的乘积，和当前最大值比较，找到最大值。
- 解法二：动态规划，遍历数组，计算当前最大值，并不断更新。当前最大乘积 max，当前最小乘积 min。由于存在负数，会导致最大的变成最小的，最小的变成最大的。所以分两种情况讨论：
    - nums[i] > 0 时，max = Max(max * nums[i], nums[i]); min = Min(min * num[i], num[i]);
    - nums[i] < 0 时，max = Max(min * nums[i], nums[i]); min = Min(max * num[i], num[i]);

```java
class Solution {
    public int maxProduct1(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int max = nums[0];
        int temp;
        for (int i = 0; i < nums.length; i++) {
            temp = nums[i];
            if (temp > max) {
                max = temp;
            }
            for (int j = i + 1; j < nums.length; j++) {
                temp *= nums[j];
                if (temp > max) {
                    max = temp;
                }
            }
        }
        return max;
    }

    public int maxProduct2(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int ret = nums[0];
        int min = nums[0];
        int max = nums[0];
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] < 0) {
                int temp = min;
                min = max;
                max = temp;
            }
            max = Math.max(max * nums[i], nums[i]);
            min = Math.min(min * nums[i], nums[i]);
            ret = Math.max(ret, max);
        }
        return ret;
    }
}
```

##### 分析：

- 时间复杂度：
  - 解法一：O(n^2)
  - 解法二：O(n)
- 空间复杂度都是 O(1)

-----

## 2. Review

[Java Memory  Model](http://tutorials.jenkov.com/java-concurrency/java-memory-model.html) 主要讲述了 Java 内存模型、硬件内存架构和两者之间的差异。

Java 内存模型把内存分为线程栈和堆。每个线程都有各自的线程栈，线程栈内部包含方法调用信息和方法内局部变量，它不能被其他线程访问。线程栈存储的局部变量，包括「基本数据类型和引用变量」的拷贝，而引用的对象存储在堆中。堆用来存储应用创建的对象，不管是局部对象还是成员对象，不论是哪个线程创建的。

硬件内存架构包含 CPU 寄存器、高速缓存和 RAM 主存，按照前面的顺序，读写速度越来越慢，容量越来越大。当 CPU 读取数据时，会把数据缓存在寄存器和高速缓存中。当 CPU 写回数据时，会把数据从寄存器和高速缓存刷新到 RAM。

Java 内存模型和硬件模型架构不同，通常线程栈和堆在 RAM 中，但有时也会在寄存器和高速缓存中。当变量存储在计算机的不同位置时，就会引发两个主要问题：多线程读写变量的可见性和竞态条件。使用 volatile 可以解决可见性问题，synchronized 可以解决竞态条件。

## 3. Tip

刷题的时候看到了 override 和 overload，结合前段时间读过的《码出高效：Java开发手册》中的内容，重新梳理了一下知识点：[深入理解 Java 中的 override 和 overload](https://isuperqiang.cn/post/shen-ru-li-jie-java-zhong-de-override-he-overload/)。

## 4. Share

多学一些东西总没有错，所谓「技多不压身」。别人不懂的你能做，别人现学现查，你信手拈来，别人浮于表面，你深入原理。这都是机会，是优势，机会总是留给有准备的人。

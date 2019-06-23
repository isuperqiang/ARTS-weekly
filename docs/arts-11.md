## 1. Algorithm

#### 263. 丑数（简单）

##### 描述：

> 编写一个程序判断给定的数是否为丑数。丑数就是只包含质因数 2, 3, 5 的正整数。

##### 示例：

```
示例：
输入: 6
输出: true
解释: 6 = 2 × 3
```

##### 思路：

- 循环实现：循环去除 2、3、5，直到不能整除，如果余数是 1，那么就是丑数。
- 递归实现：和循环一样，也是不停地除2、3、5。

```java
class Solution {
    public boolean isUgly(int num) {
        if (num <= 0) {
            return false;
        } else if (num == 1) {
            return true;
        }
        while (num % 2 == 0) {
            num /= 2;
        }
        while (num % 3 == 0) {
            num /= 3;
        }
        while (num % 5 == 0) {
            num /= 5;
        }
        return num == 1;
    }
  
   private static boolean isUgly2(int num) {
        if (num <= 0) {
            return false;
        } else if (num == 1) {
            return true;
        }
        if (num % 2 == 0) {
            return isUgly2(num / 2);
        }
        if (num % 3 == 0) {
            return isUgly2(num / 3);
        }
        if (num % 5 == 0) {
            return isUgly2(num / 5);
        }
        return false;
    }
}
```

##### 分析：

循环和递归实现一样：

- 时间复杂度：O(logn)
- 空间复杂度：O(1)

-----

#### 349.  两个数组的交集（简单）

##### 描述：

> 给定两个数组，编写一个函数来计算它们的交集。

##### 示例：

```
输入: nums1 = [1,2,2,1], nums2 = [2,2]
输出: [2]
```

##### 说明：

- 输出结果中的每个元素一定是唯一的。
- 我们可以不考虑输出结果的顺序。

##### 思路：

使用一个 Set 去除数组一重复元素，另一个 Set 保存两个数组的交集

##### 解法：

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        if (nums1 == null || nums2 == null) {
            return new int[]{};
        }

        Set<Integer> set1 = new HashSet<>(nums1.length);
        for (int i : nums1) {
            set1.add(i);
        }
        Set<Integer> set2 = new HashSet<>(nums1.length);
        for (int i : nums2) {
            if (set1.contains(i)) {
                set2.add(i);
            }
        }
        int size = set2.size();
        int[] ret = new int[size];
        Iterator<Integer> iterator = set2.iterator();
        for (int i = 0; i < size; i++) {
            ret[i] = iterator.next();
        }
        return ret;
    }
}
```

##### 分析：

- 时间复杂度：O(n)
- 空间复杂度：O(n)

## 2. Review

[What is an API? In English, please.](https://medium.com/free-code-camp/what-is-an-api-in-english-please-b880a3214a82) 什么是 API？

开发者都知道 API 是应用程序接口，作者对它有更广泛的认识。API 是服务方的一部分，它接收请求并发出响应。API 是向客户提供服务的一种方式，客户端访问 API 获取消息，比如 GitHub 的 API。在面向对象编程中，对象的 public 方法也可以看作是一种 API，用来与其他对象进行交互。

## 3. Tip

[Android I/O 那些事儿](https://isuperqiang.cn/post/android-io-na-xie-shi-er/) 总结了 Android 系统的 I/O 知识，对它有了更深层次的了解。

## 4. Share

经典是经过时间筛选的，在这个浮躁的社会，多读经典是最省时间的选择。
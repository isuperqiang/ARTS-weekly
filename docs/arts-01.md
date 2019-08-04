## 1. Algorithm

#### 13. 罗马数字转整数（简单）

##### 描述：

> 罗马数字包含以下七种字符: `I`， `V`， `X`， `L`，`C`，`D` 和 `M`。
>
> ```properties
> 字符          数值
> I             1
> V             5
> X             10
> L             50
> C             100
> D             500
> M             1000
> ```
>
> 例如， 罗马数字 2 写做 `II` ，即为两个并列的 1。12 写做 `XII` ，即为 `X` + `II` 。 27 写做  `XXVII`, 即为 `XX` + `V` + `II` 。
>
> 通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做 `IIII`，而是 `IV`。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。同样地，数字 9 表示为 `IX`。这个特殊的规则只适用于以下六种情况：
>
> - `I` 可以放在 `V` (5) 和 `X` (10) 的左边，来表示 4 和 9。
> - `X` 可以放在 `L` (50) 和 `C` (100) 的左边，来表示 40 和 90。 
> - `C` 可以放在 `D` (500) 和 `M` (1000) 的左边，来表示 400 和 900。
>
> 给定一个罗马数字，将其转换成整数。输入确保在 1 到 3999 的范围内。

##### 示例：

```properties
输入: "III"
输出: 3
输入: "IV"
输出: 4
```

##### 思路：

>
> 把罗马数字和整数建立映射，然后从左到右遍历字符串，对比前后的两个值。因为正常的罗马数字是位上的值递减的，当出现左值大于右值，就使用两者的差作为结果。
> 

##### 解法：

```java
class Solution {
    public int romanToInt(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }

        Map<Character, Integer> romanIntMap = new HashMap<>(8);
        romanIntMap.put('I', 1);
        romanIntMap.put('V', 5);
        romanIntMap.put('X', 10);
        romanIntMap.put('L', 50);
        romanIntMap.put('C', 100);
        romanIntMap.put('D', 500);
        romanIntMap.put('M', 1000);
        int result = 0;
        char[] chars = s.toCharArray();
        int preValue = 0;
        for (int i = 0; i < chars.length; i++) {
            int value = romanIntMap.get(chars[i]);
            if(value > preValue){
                result -= preValue;
                result += value - preValue;
            } else {
                result += value;
            }
            preValue = value;
        }
        return result;
    }
}
```

##### 分析：

- 时间复杂度：O(n)
- 空间复杂度：O(n)

#### 27. 移除元素（简单）

##### 描述：

> 给定一个数组 *nums* 和一个值 *val*，你需要**原地**移除所有数值等于 *val* 的元素，返回移除后数组的新长度。
> 不要使用额外的数组空间，你必须在**原地修改输入数组**并在使用 O(1) 额外空间的条件下完成。
> 元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

##### 示例：

```
给定 nums = [3,2,2,3], val = 3,
函数应该返回新的长度 2, 并且 nums 中的前两个元素均为 2。
你不需要考虑数组中超出新长度后面的元素。
```

##### 思路：

> - 解法一：题目要求原地修改，我想到的是在遍历数组的时候，如果当前元素和 val 相等，那么交换到后面的位置，最后的结果是
> 要移除的元素都在数组右端，然后就得到新数组的长度和移除后的数组。
> - 解法二：使用快慢指针，在遍历数组（快指针）的时候，如果当前元素和 val 不等，那么把元素赋值给慢指针，慢指针向后移动，最后根据慢指针的位置，就可以得到新的长度和移除后的数组。

##### 解法：

```java
class Solution {
    public int removeElement2(int[] nums, int val) {
        if (nums == null) {
            return 0;
        }
        int slowPointer = 0;
        for (int i = 0; i < nums.length; i++) {
            if(nums[i] != val){
                nums[slowPointer++] = nums[i];
            }
        }
        return slowPointer;
    }
  
    public int removeElement1(int[] nums, int val) {
        if (nums == null) {
            return 0;
        }
        int valIndex = nums.length - 1;
        int i = 0;
        while (i < nums.length) {
            if (nums[i] == val & i <= valIndex) {
                int temp = nums[i];
                nums[i] = nums[valIndex];
                nums[valIndex--] = temp;
            } else {
                i++;
            }
        }
        return valIndex + 1;
    }
}
```

##### 分析：

- 时间复杂度：O(n)
- 空间复杂度：O(1)

## 2. Review

从 [Medium](https://medium.com/) 上读到一篇文章：[Learning To Code By Writing Code Poems](<https://medium.com/@smashingmag/learning-to-code-by-writing-code-poems-cd29cd3ba320>) 从写代码诗开始学习编程。

作者编造了一个故事——相爱的两个比特，用人类可以理解的 JavaScript 代码写出来，其语法和人类语言有差异，让浏览器去执行。


```javascript
// Love at first sight
const me = new Bit('blue');
const you = new Bit('purple');

if (me.getDistanceTo(you.position) < 200) {
  me.setFeelings({
    inLove: true,
  })
}
```

一旦你把代码看作人类语言，而不是外星人发明的东西，学习编程就会变得容易。

作者是个浪漫的程序员，写代码就像写诗一样，编程本来就该这么有趣，哈哈。

## 3. Tip

本周学习了 Java 线程间通信，简单总结了一下。[Java线程间通信和协作的两种方式](https://isuperqiang.cn/post/java-xian-cheng-jian-tong-xin-he-xie-zuo-de-liang-chong-fang-shi/)


## 4. Share

有些事情因为难做而不想做，但是真正做起来的时候，却发现它没有预想的那么难，比如这个 ARTS 挑战。学习是逆人性的，成长的道路是不舒服的。要想成为大牛，必须得苦练呐。

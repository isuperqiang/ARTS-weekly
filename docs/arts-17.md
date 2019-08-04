## 1. Algorithm

#### 1114. 按序打印（简单）

##### 描述：

> 三个不同的线程将会共用一个 Foo 实例，它们会被异步启动。
>   * 线程 A 将会调用 one() 方法
>
>   * 线程 B 将会调用 two() 方法
>
>   * 线程 C 将会调用 three() 方法
>    
>     请设计修改程序，以确保 two() 方法在 one() 方法之后被执行，three() 方法在 two() 方法之后被执行。

##### 示例：

```
输入: [1,2,3]
输出: "onetwothree"
解释: 
有三个线程会被异步启动。
输入 [1,2,3] 表示线程 A 将会调用 one() 方法，线程 B 将会调用 two() 方法，线程 C 将会调用 three() 方法。
正确的输出是 "onetwothree"。
```

##### 思路：

排序的思路就是 线程 C 等待线程 B 执行完毕，线程 B 等待线程 A 执行完毕，通过线程阻塞的方式实现，JUC 提供了许多的多线程工具类。

- 解法一：CountDownLoatch

```java
  /**
     * 通过 CountDownLatch
     */
    public static class Foo1 {
        private CountDownLatch countDownLatchSecond = new CountDownLatch(1);
        private CountDownLatch countDownLatchThird = new CountDownLatch(1);

        public void first(Runnable printFirst) throws InterruptedException {
            printFirst.run();
            countDownLatchSecond.countDown();
        }

        public void second(Runnable printSecond) throws InterruptedException {
            countDownLatchSecond.await();
            printSecond.run();
            countDownLatchThird.countDown();
        }

        public void third(Runnable printThird) throws InterruptedException {
            countDownLatchThird.await();
            printThird.run();
        }
    }
```
- 解法二：Object 内置锁

```java
    /**
     * 通过 Object 内置锁
     */
    public static class Foo2 {
        private final Object lock = new Object();
        private int state = 1;

        public void first(Runnable printFirst) throws InterruptedException {
            synchronized (lock) {
                printFirst.run();
                state = 2;
                lock.notifyAll();
            }
        }

        public void second(Runnable printSecond) throws InterruptedException {
            synchronized (lock) {
                while (state != 2) {
                    lock.wait();
                }
                printSecond.run();
                state = 3;
                lock.notifyAll();
            }
        }

        public void third(Runnable printThird) throws InterruptedException {
            synchronized (lock) {
                while (state != 3) {
                    lock.wait();
                }
                printThird.run();
            }
        }
    }
```

- 解法三：Lock 和 Condition

```java
    /**
     * 通过 Lock 和 Condition
     */
    public static class Foo3 {
        private Lock lock = new ReentrantLock();
        private Condition condition = lock.newCondition();
        private int state = 1;

        public void first(Runnable printFirst) throws InterruptedException {
            lock.lock();
            try {
                printFirst.run();
                state = 2;
                condition.signalAll();
            } finally {
                lock.unlock();
            }
        }

        public void second(Runnable printSecond) throws InterruptedException {
            lock.lock();
            try {
                while (state != 2) {
                    condition.await();
                }
                printSecond.run();
                state = 3;
                condition.signalAll();
            } finally {
                lock.unlock();
            }
        }

        public void third(Runnable printThird) throws InterruptedException {
            lock.lock();
            try {
                while (state != 3) {
                    condition.await();
                }
                printThird.run();
            } finally {
                lock.unlock();
            }
        }
    }
```

- 解法四：Semaphore

```java
    /**
     * 通过 Semaphore
     */
    public static class Foo4 {
        private Semaphore semaphoreSecond = new Semaphore(0);
        private Semaphore semaphoreThird = new Semaphore(0);

        public void first(Runnable printFirst) throws InterruptedException {
            printFirst.run();
            semaphoreSecond.release();
        }

        public void second(Runnable printSecond) throws InterruptedException {
            semaphoreSecond.acquire();
            printSecond.run();
            semaphoreThird.release();
        }

        public void third(Runnable printThird) throws InterruptedException {
            semaphoreThird.acquire();
            printThird.run();
        }
    }
```

## 2. Review

[20 Google Search Tips to Use Google More Efficiently](https://www.lifehack.org/articles/technology/20-tips-use-google-search-efficiently.html) 用好谷歌搜索的 20 条技巧

1. 使用 Tab 分类，比如图片、新闻、视频等
2. 使用双引号，精确匹配关键词，比如： “浪潮之巅 吴军”
3. 使用连字符 `-` 排除词语，比如：见识 -吴军
4. 使用冒号 `site:url` 搜索指定网站，比如：吴军 site:dangdang.com
5. 查找链接到另一个页面的页面 `link:url`，比如：link:qq.com
6. 使用星号 `*` 通配符，比如：生活不止 * 苟且
7. 查找与其他网站相似的网站 `related:url`，比如：related:amazon.com
8. 用谷歌搜索做数学，比如：8 * 5 + 5
9. 一个搜索多个关键词 `OR`，比如：巧克力 OR 白巧克力
10. 搜索一系列数字 `..`，比如：41..43
11. 保持简单，比如：附近的披萨店
12. 逐渐添加搜索词，比如：
    - 首先尝试：工作面试
    - 其次尝试：准备工作面试
    - 再次尝试：如何准备工作面试
13. 使用网站会用的词汇，比如：“我头疼”可以换成“头痛缓解”
14. 只用重要的词汇，比如：
    - 不要用：我从哪儿可以找到提供配送的餐馆？
    - 而要用：附近的餐馆
15. 谷歌搜索有快捷方式，就像上面的计算器一样。比如：北京时间、杭州天气
16. 拼写不那么重要，谷歌搜索会帮你纠正语法和词汇。
17. 使用描述性词语，比如：如何安装 Ubuntu 的驱动？
18. 查找特定文件 `filetype:pdf`，比如：文明之光 filetype:pdf
19. 货币和单位换算，
20. 追踪你的包裹

谷歌搜索是最棒的搜索工具，比某度好一万倍，善用谷歌是一种高效的方式。

## 3. Tip

推荐一个静态博客写作客户端 [Gridea](https://github.com/getgridea/gridea)，使用它可以方便地管理文章，进行分类、打标签等，一键同步到 GitHub，提供了多套主题，支持配置域名和评论功能，Windows、Mac 、Linux 全平台支持。我的[博客](https://isuperqiang.cn/)托管在 GitHub 上，以前使用 [Hexo](https://hexo.io/zh-cn/) 发布，但是没有本地管理功能，想修改文章非常麻烦。现在用 Gridea 发布，果然优雅了不少啊。

## 4. Share

程序员一般不喜欢写文档，遇到问题时又骂别人不写文档。在我看来，文档和代码一样重要，开源库的 API 文档写得清晰明了，开发者使用时也省心。最怕的是，过了一段时间，自己的代码都捋不清了。所以，尽可能多些文档吧，为了自己也为了接盘侠 :)

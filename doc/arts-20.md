## 1. Algorithm

#### 1116. 打印零与奇偶数（中等）

##### 描述：

> 有这样一个类 ZeroEvenOdd，相同的一个 ZeroEvenOdd 类实例将会传递给三个不同的线程：
> - 线程 A 将调用 zero()，它只输出 0 。
>
> - 线程 B 将调用 even()，它只输出偶数。
>
> - 线程 C 将调用 odd()，它只输出奇数。
>
> 每个线程都有一个 printNumber 方法来输出一个整数。请修改给出的代码以输出整数序列 010203040506... ，其中序列的长度必须为 2n。

##### 示例：

```
输入：n = 2
输出："0102"
说明：三条线程异步执行，其中一个调用 zero()，另一个线程调用 even()，最后一个线程调用odd()。正确的输出为 "0102"。
```

##### 思路：

线程同步问题，可以使用锁或者信号量解决。
- 解法一：Lock 和 Condition

```java
    private static class ZeroEvenOdd1 {
        private final Lock lock = new ReentrantLock();
        private final Condition evenCondition = lock.newCondition();
        private final Condition oddCondition = lock.newCondition();
        private final Condition zeroCondition = lock.newCondition();
        private int n;
        private int current = 1;
        // 0 refers zero, 1 refers odd, 2 refers even
        private int state = 0;

        public ZeroEvenOdd1(int n) {
            this.n = n;
        }

        // printNumber.accept(x) outputs "x", where x is an integer.
        public void zero(IntConsumer printNumber) throws InterruptedException {
            lock.lock();
            try {
                while (current <= n) {
                    if (state != 0) {
                        zeroCondition.await();
                    }
                    printNumber.accept(0);
                    if ((current & 1) == 0) {
                        state = 2;
                        evenCondition.signal();
                    } else {
                        state = 1;
                        oddCondition.signal();
                    }
                    zeroCondition.await();
                }
                oddCondition.signal();
                evenCondition.signal();
            } finally {
                lock.unlock();
            }
        }

        // 偶数
        public void even(IntConsumer printNumber) throws InterruptedException {
            lock.lock();
            try {
                while (current <= n) {
                    if (state != 2) {
                        evenCondition.await();
                    } else {
                        printNumber.accept(current++);
                        state = 0;
                        zeroCondition.signal();
                    }
                }
            } finally {
                lock.unlock();
            }
        }

        // 奇数
        public void odd(IntConsumer printNumber) throws InterruptedException {
            lock.lock();
            try {
                while (current <= n) {
                    if (state != 1) {
                        oddCondition.await();
                    } else {
                        printNumber.accept(current++);
                        state = 0;
                        zeroCondition.signal();
                    }
                }
            } finally {
                lock.unlock();
            }
        }
    }
```

- 解法二：Semaphore

```java
    private static class ZeroEvenOdd2 {
        private final Semaphore zeroSemaphore = new Semaphore(1);
        private final Semaphore evenSemaphore = new Semaphore(0);
        private final Semaphore oddSemaphore = new Semaphore(0);
        private int n;

        public ZeroEvenOdd2(int n) {
            this.n = n;
        }

        // printNumber.accept(x) outputs "x", where x is an integer.
        public void zero(IntConsumer printNumber) throws InterruptedException {
            for (int i = 1; i <= n; i++) {
                zeroSemaphore.acquire();
                printNumber.accept(0);
                if ((i & 1) == 0) {
                    evenSemaphore.release();
                } else {
                    oddSemaphore.release();
                }
            }
        }

        public void even(IntConsumer printNumber) throws InterruptedException {
            for (int i = 2; i <= n; i += 2) {
                evenSemaphore.acquire();
                printNumber.accept(i);
                zeroSemaphore.release();
            }
        }

        public void odd(IntConsumer printNumber) throws InterruptedException {
            for (int i = 1; i <= n; i += 2) {
                oddSemaphore.acquire();
                printNumber.accept(i);
                zeroSemaphore.release();
            }
        }
    }
```

## 2. Review

[Follow these simple rules and you’ll become a Git and GitHub master](https://medium.com/free-code-camp/follow-these-simple-rules-and-youll-become-a-git-and-github-master-e1045057468f) 遵循这些规范，你就会成为 Git 大师。

作者提出了三条建议：

- 为每个新项目创建 Git 仓库
- 为每个新需求创建新分支
- 使用 pull request 合并代码到 master 分支

点评：Git 是非常强大的版本控制工具，每个程序员都该熟练掌握。

## 3. Tip

《高效阅读法》（levarage reading）讲了许多不一样的读书方法。读书不一定要从头开始完整读一遍，只读对自己有用的、感兴趣的地方，无关紧要的内容一律跳过，设定读书的时间限制，比如两小时读完，这样读书速度就提升了一大截。仅仅读了还不够，要运用到生活中，读以致用。 最有效的投资就是自我投资，读书是最好的自我投资。

## 4. Share

[技术人如何通过了解业务，获取晋升机会？](https://mp.weixin.qq.com/s/o4CfgIcPibG_QxrsZ4x7sA)

阿里技术专家的一篇分享，对于技术和业务讲得非常中肯。下面是作者的几个观点：

- 业务先赢是技术第一要务。技术人员首要任务是先把业务支持好，在这个前提下，再来讲技术沉淀和技术红利。
- 理解业务有助于你做技术决策去驱动业务，有助于你对资源的优先级做判断，而且还有助于提升你的研发效能。
- 理解业务更多是理解了运营决策背后的原因，理解了网站各个角色的诉求和痛点，理解了自己做的产品和项目对业务的价值和影响。
- 技术人的三大支柱：业务理解、项目管理和专业技术。一个不理解业务的研发，和流水线的工人是没有很大的区别的。
- 技术人员不一定要去这么深入理解业务或者成果出在业务上，对技术很感兴趣的同学而且有抓手的同学，就安心地去专研技术并取得结果就好，注意要取得结果，不能是说不清楚的东西。
- 对于技术上没有鲜明特色的同学，或者有技术深度但是暂时想不到什么技术挖掘点的同学，不妨去多看看业务，寻找技术驱动业务的机会。
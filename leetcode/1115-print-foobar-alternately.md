# [交替打印FooBar](https://leetcode-cn.com/problems/print-foobar-alternately/)

### 方法一

```java
class FooBar {
    private int n;
    private Semaphore foo;
    private Semaphore bar;

    public FooBar(int n) {
        this.n = n;
        foo = new Semaphore(1);
        bar = new Semaphore(0);
    }

    public void foo(Runnable printFoo) throws InterruptedException {
        for (int i = 0; i < n; i++) {
            foo.acquire();
        	printFoo.run();
            bar.release();
        }
    }

    public void bar(Runnable printBar) throws InterruptedException {
        
        for (int i = 0; i < n; i++) {
            bar.acquire();
        	printBar.run();
            foo.release();
        }
    }
}
```

### 方法二

```java
class FooBar {

    private int n;
    private CountDownLatch cdl;
    private CyclicBarrier cb;


    public FooBar(int n) {
        this.n = n;
        cdl = new CountDownLatch(1);
        cb  = new CyclicBarrier(2);
    }

    public void foo(Runnable printFoo) throws InterruptedException {
        try {
            for (int i = 0; i < n; i++) {
                printFoo.run();
                cdl.countDown();
                cb.await();
            }
        } catch (Exception e) {

        }
    }

    public void bar(Runnable printBar) throws InterruptedException {
        try {
            for (int i = 0; i < n; i++) {
                cdl.await();
                printBar.run();
                cdl = new CountDownLatch(1);
                cb.await();
            }
        } catch (Exception e) {
        }
    }
}
```


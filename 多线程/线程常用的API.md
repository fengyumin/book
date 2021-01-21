
### 线程常用的API

#### Thread.sleep()
> Thread.sleep()可以把当前线程暂停一段时间。

```
public class Main {
    public static void main(String[] args) {
        System.out.println("main start...");
        Thread t = new Thread() {
            public void run() {
                System.out.println("thread run...");
                try {
                    Thread.sleep(10);
                } catch (InterruptedException e) {}
                System.out.println("thread end.");
            }
        };
        t.start();
        try {
            Thread.sleep(20);
        } catch (InterruptedException e) {}
        System.out.println("main end...");
    }
}
```

#### Thread.join()
> Thread.join() 通过对另一个线程对象调用join()方法可以等待其执行结束；
> - 可以指定等待时间，超过等待时间线程仍然没有结束就不再等待；
> - 对已经运行结束的线程调用join()方法会立刻返回。

```
public class Main {
    public static void main(String[] args) throws InterruptedException {
        Thread t = new Thread(() -> {
            System.out.println("hello");
        });
        System.out.println("start");
        t.start();
        t.join();//main线程在启动t线程后，可以通过t.join()等待t线程结束后再继续运行
        System.out.println("end");
    }
}

```



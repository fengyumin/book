说一下runnable和callable有什么区别.md

### 说一下runnable和callable有什么区别?

1. Callable接口与Runnable相似，两者均适用于其实例可能由另一个线程执行的情况。
2. 但是，**Runnable不会返回结果，也无法抛出已知的异常。**
3. Callable需要实现call()方法而Runnable需要实现run()的方法
> The Callable interface is similar to Runnable, in that both are designed for classes whose instances are potentially executed by another thread. A Runnable, however, does not return a result and cannot throw a checked exception.

```
public interface Runnable {
    void run();
}

public interface Callable<V> { //Callable接口是一个泛型接口，可以返回指定类型的结果。
    V call() throws Exception;
}
```


4. 一个Callable可以与`ExecutorService#invokeXXX(Collection<? extends Callable<T>> tasks)`方法一起使用，但Runnable不能。

```
ExecutorService executor = Executors.newFixedThreadPool(4); 
// 定义任务:
Callable<String> task = new Task();
// 提交任务并获得Future:
Future<String> future = executor.submit(task);
// 从Future获取异步执行返回的结果:
String result = future.get(); // 可能阻塞
```

- 当我们提交一个Callable任务后，我们会同时获得一个Future对象，
- 然后，我们在主线程某个时刻调用Future对象的get()方法，就可以获得异步执行的结果。
- 在调用get()时，如果异步任务已经完成，我们就直接获得结果。如果异步任务还没有完成，那么get()会阻塞，直到任务完成后才返回结果。

一个Future<V>接口表示一个未来可能会返回的结果，它定义的方法有：
- get()：获取结果（可能会等待）
- get(long timeout, TimeUnit unit)：获取结果，但只等待指定的时间；
- cancel(boolean mayInterruptIfRunning)：取消当前任务；
- isDone()：判断任务是否已完成。


***

Runnable自Java 1.0以来一直存在，但Callable仅在Java 1.5中引入用来来处理Runnable不支持的用例。从理论上讲，Java团队可以更改该Runnable.run()方法的签名，但是这会破坏与1.5版之前的代码的兼容性，因此在将旧的Java代码迁移到更新的JVM时需要重新编码。这样行不通,Java致力于向后兼容...这一直是Java商业计算的最大卖点之一。

而且，很明显，在某些用例中，**任务不需要返回结果或抛出检查到的异常**。对于这些用例，使用Runnable比使用Callable<Void>并从call()中返回null值更为简洁。

>Runnable has been around since Java 1.0, but Callable was only introduced in Java 1.5 ... to handle use-cases that Runnable does not support. In theory, the Java team could have changed the signature of the Runnable.run() method, but this would have broken binary compatiblity with pre-1.5 code, requiring recoding when migrating old Java code to newer JVMs. That is a BIG NO-NO. Java strives to be backwards compatible ... and that's been one of Java's biggest selling points for business computing.
And, obviously, there are use-cases where a task doesn't need to return a result or throw a checked exception. For those use-cases, using Runnable is more concise than using Callable<Void> and returning a dummy (null) value from the call() method.

> 参考: https://stackoverflow.com/questions/141284/the-difference-between-the-runnable-and-callable-interfaces-in-java
# Java 中 volatile 关键字的作用是什么？

## 回答重点*

volatile 它的主要作用是保证变量的**可见性**和**禁止指令重排优化**。

1）可见性（Visibility）

* `volatile` 关键字确保变量的可见性。当一个线程修改了 `volatile` 变量的值，新值会立即被刷新到主内存中，其他线程在读取该变量时可以立即获得最新的值。这样可以避免线程间由于缓存一致性问题导致的“看见”旧值的现象。

2）**禁止指令重排序（Ordering）**：

* `volatile` 还通过内存屏障来禁止特定情况下的指令重排序，从而保证程序的执行顺序符合预期。对 `volatile` 变量的写操作会在其前面插入一个 StoreStore 屏障，而对 `volatile` 变量的读操作则会在其后插入一个 LoadLoad 屏障。这确保了在多线程环境下，某些代码块执行顺序的可预测性。

## 注意 volatile 不能保证操作的原子性

虽然 `volatile` 保证了可见性和有序性，但它不能保证操作的原子性。原子性意味着一个操作不可分割，不能被中断。典型的例子是 `i++` 操作，这实际上分为读取 `i` 的值、递增、写回三个步骤。如果多个线程同时执行 `i++`，最终结果可能不正确，因为每个线程都可能读取到相同的初始值。

**示例**：

```java
private static volatile int count = 0;

public static void main(String[] args) {
  for (int i = 0; i < 1000; i++) {
      new Thread(() -> count++).start();
  }
  System.out.println(count); // 结果可能不为 1000
}
```

解决这个问题的方法是使用 `AtomicInteger` 或者 `synchronized` 块。

### volatile 与 synchronized 的对比

* **性能**：`volatile` 是一种轻量级的同步机制，开销较小，但它只能用于变量的可见性和禁止重排序，无法实现复杂的同步逻辑。`synchronized` 则是重量级的同步机制，可以保证代码块的原子性和可见性，但开销较大。
* **使用场景**：`volatile` 适用于简单的状态标志、标记等场景，而 `synchronized` 更适合复杂的临界区保护，需要确保多个操作的原子性时。

### Java 内存模型（JMM）与 volatile

Java 内存模型（Java Memory Model, JMM）定义了多线程环境下共享变量的可见性和指令重排序规则。`volatile` 是 JMM 的关键组成部分，提供了一种简化的方式来实现线程间的内存可见性。

JMM 中规定了以下规则：

* 对一个 `volatile` 变量的写操作，happens-before 于每一个后续对这个 `volatile` 变量的读操作。
* `volatile` 变量的操作不会与其他内存操作进行重排序。

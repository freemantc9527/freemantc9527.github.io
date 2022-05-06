# 单例模式

## 优点
单例模式在内存中只有一个对象，节省内存空间； 避免频繁的创建销毁对象，可以提高性能；避免对共享资源的多重占用，简化访问；为整个系统提供一个全局访问点。

## 缺点
单例模式不适用于变化频繁的对象；如果实例化的对象长时间不被利用，系统会认为该对象是垃圾而被回收，这可能会导致对象状态的丢失。

## 适用场景
一般常用在工具类的实现或创建对象需要消耗大量系统资源时使用单例模式。
- 需要生成唯一序列的环境
- 需要频繁实例化然后销毁的对象
- 创建对象时耗时过多或者耗资源过多，但又经常用到的对象
- 方便资源相互通信的环境
- 频繁访问数据库或文件的对象
- 工具类对象（推荐静态类，静态方法）

## 实现方式

### 饿汉模式
```java
// 静态常量方式
public class Singleton {
    // 指向自己实例的私有静态引用，主动创建
    private static Singleton singleton = new Singleton();

    // 私有的构造方法，使外界不能创建该类实例
    private Singleton() {}

    // 获取单例的实例
    public static Singleton GetInstance() {
        return singleton;
    }
}

// java 静态代码块（c# 静态构造函数）
public class Singleton {
    private static Singleton singleton;
    private Singleton() {}

    static {
        // 还可以干些别的事情，比如读取一些配置
        singleton = new Singleton();
    }

    public static Singleton GetInstance() {
        return singleton;
    }
}
```

### 饱汉模式
为保证线程安全，统一使用双重检查单例（DCL）
```java
public class Singleton {
    private static volatile Singleton singleton;
    private Singleton() {}

    public static Singleton GetInstance() {
        if(null==singleton) {
            synchronized(Singleton.class) {
                if(null==singleton) {
                    singleton = new Singleton();
                }
            }
        }
        return singleton;
    }
}
```

```csharp
public class Singleton
{
    // 定义一个标识确保线程同步
    private static readonly object locker = new object();

    private static Singleton uniqueInstance;
    private Singleton() {}

    public static Singleton GetInstance()
    {
        if (null == uniqueInstance) 
        {
            lock (locker)
            {
                if (null == uniqueInstance)
                {
                    uniqueInstance = new Singleton();
                }
            }
        }
        return uniqueInstance;
    }
}
```

## 关于单例模式常见的面试题

- ***知道单例模式吗? 那说说单例模式的特点和作用吧。***
> 正确回答： 知道的。单例模式是设计模式中非常重要的一种设计模式。在日常开发中我们使用到场景也是很多的。比如 需要频繁实例化，然后销毁的对象创建对象时耗时过多或者耗资源过多，但又经常用到的对象 。以及频繁访问数据库或文件的对象，工具类对象等。
特点： 全局仅提供一个实例、提供公有的方法获取实例、私有的构造方法、私有的成员变量等
作用：1.  在要求线程安全的情况下，保证了类实例的唯一性。
​            2.  在不需要多实例的情况下，保证了 类实例的单一性。

- ***不使用synchronized和lock，如何实现一个线程安全的单例？***
> 错误回答：实现单例模式的方式多种多样，通过上面咱们的总结，这里可以使用饿汉模式、饿汉模式变种、静态内部类、枚举、以及通过容器等方式来实现单例模式。但这里有个误区，需要区分隐形锁和显示锁的使用。
以上几种答案，其实现原理都是利用借助了类加载的时候初始化单例。即借助了ClassLoader的线程安全机制。所谓ClassLoader的线程安全机制，就是ClassLoader的loadClass方法在加载类的时候使用了synchronized关键字。也正是因为这样， 除非被重写，这个方法默认在整个装载过程中都是同步的，也就是保证了线程安全。
所以，以上各种方法，虽然并没有显示的使用synchronized，但是还是其底层实现原理还是用到了synchronized，即隐形使用。
终极答案： 那就是使用CAS。
CAS是项乐观锁技术，当多个线程尝试使用CAS同时更新同一个临界资源时，只有其中一个线程能更新变量的值，而其它线程都失败，失败的线程并不会被挂起，而是被告知这次竞争中失败，并可以再次尝试。
用CAS的好处在于不需要使用传统的锁机制来保证线程安全,CAS是一种基于忙等待的算法,依赖底层硬件的实现,相对于锁它没有线程切换和阻塞的额外消耗,可以支持较大的并行度。
CAS的一个重要缺点在于如果忙等待一直执行不成功(一直在死循环中),会对CPU造成较大的执行开销。

- ***DCL实现单例模式中，Volatitle 关键字的作用？***
> - volatile 变量提供执行顺序和内存可见性保证，例如，JVM 或者 JIT为了获得更好的性能会对语句重排序，但是 volatile 类型变量即使在没有同步块的情况下赋值也不会与其他语句重排序。
> - volatile 提供 happens-before 的保证，确保一个线程的修改能对其他线程是可见的。某些情况下，volatile 还能提供原子性。volatile 本质是在告诉jvm当前变量在寄存器中的值是不确定的,需要从主存中读取。
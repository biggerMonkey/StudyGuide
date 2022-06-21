## 1.java字符串不可变原因

1. 保存字符串的数组被 final 修饰且为私有的，并且String 类没有提供/暴露修改这个字符串的方法。
2. String 类被 final 修饰导致其不能被继承，进而避免了子类破坏 String 不可变。

## 2.java只有值传递

只有值传递，没有应用传递，就算传递的是对象，也是对象的应用地址的值，在子方法内交换后，不会影响外部

## 3.cglib 和 jdk 动态代理有什么区别

1. jdk只能基于接口，利用拦截器加反射，cglib可以基于类，利用ASM修改字节码
2. jdk生成的代理类实现了被代理类的接口，cglib生成的代理类继承了被代理类
3. 大多数jdk动态代理性能更好

[cglib源码分析](https://cloud.tencent.com/developer/article/1898468)

[jdk动态代理源码分析](https://blog.csdn.net/CarryBest/article/details/112857330)

### 4.Java堆外内存

对外内存指**机器内存**，区别于java堆内内存，当进行IO操作时，能够节省堆内存到堆外内存的数据拷贝，如果用堆内内存，需要先将数据拷贝到机器内存，再发送，用堆外内存就少了这一步，可以提高性能。如netty零拷贝技术

DirectByteBuffer 这个类是 JDK 提供使用堆外内存的一种途径

堆外内存分配：unsafe.allocateMemory

堆外内存释放（手动）：手动调用 DirectByteBuffer 的 cleaner 的 clean 方法来释放空间，最后使用，unsafe.freeMemory

堆外内存释放（自动）：Cleaner 继承了 PhantomReference（虚引用），当 GC 某个对象时，如果有此对象上还有虚引用对其引用，会将 PhantomReference 对象插入 ReferenceQueue 队列。Reference 类内部 static 静态块会启动 ReferenceHandler 线程，线程优先级很高，这个线程是用来处理 JVM 在 GC 过程中交接过来的 reference，run方法中调用Cleaner的 clean方法


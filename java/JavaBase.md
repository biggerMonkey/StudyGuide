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

### SpringBean是单例的吗

​	SpringBean是单例的，类的成员变量会受到多线程的影响,可以使用ThreadLocal来保证线程安全。
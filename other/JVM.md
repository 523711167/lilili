## JVM

### Jvm的内存模型

​	jvm的内存分为 方法区 、堆区、虚拟机栈、本地方法栈、程序计数器五个部分。

#### 1.本地方法栈

#### 2.栈(stack)

​	伴随线程创建而创建，当线程进入一个方法，就会生成一个栈针，保存执行方法过程需要的信息然后压入栈中，执行完毕再从栈中弹出，线程执行完毕，栈也结束。

##### 栈保存的数据

​	本地变量

​	栈操作

​	栈针数据	

#### 3.程序计数器

#### 4.方法区

#### 5.堆

```
设置元空间大小
-XX:MetaspaceSize=128m
设置最大元空间大小 
-XX:MaxMetaspaceSize=256m
-XX:MetaspaceSize=128m -XX:MaxMetaspaceSize=256m
```

​	

### JDK自带的命令行调优工具

#### 1.JPS

​	查看正在运行的 Java 进程

```
# -q：仅仅显示 LVMID（local virtual machine id），即本地虚拟机唯一 id。不显示主类的名称等
# -l：输出应用程序主类的全类名或如果进程执行的是 jar 包，则输出 jar 完整路径
# -m：输出虚拟机进程启动时传递给主类 main() 的参数
# -v：列出虚拟机进程启动时的 JVM 参数。比如：-Xms20m -Xmx50m 是启动程序指定的 jvm 参数
# jps [option] [hostid]
# jps可以通过hostid访问远程服务器上的java应用
```

> [!CAUTION]
>
> 💡 如果某 Java 进程关闭了默认开启的 UsePerfData 参数（即使用参数 -XX:-UsePerfData），那么 jps 命令（以及下面介绍的 jstat）将**无法探知**该 Java 进程。



### 2.jstat

​	查看JVM的统计信息

```
<option>: 指定要显示的统计信息的类型，例如 gc（垃圾收集）、class（类加载）等。
-t: 可选，显示输出中包含时间戳。
-h<lines>: 可选，通过指定 lines 的值来控制输出是多少行后显示一次标题（即列名）。
<vmid>: 目标 Java 虚拟机的进程 ID。
<interval>: 可选，刷新数据的时间间隔（以毫秒为单位）。
<count>: 可选，数据刷新的总次数。
#统计48872 PID java进程的的堆内存信息，间隔1000毫秒输出一次，输出2000次，并且每输出10行打印表头信息
jstat -gc -h 10  48872  1000 2000  
#YGC: Young Generation Collection Count - 年轻代垃圾收集次数
#YGCT: Young Generation Collection Time - 年轻代垃圾收集总耗时(秒)
#FGC: Full Garbage Collection Count - 完全垃圾收集次数
#FGCT: Full Garbage Collection Time - 完全垃圾收集总耗时(秒)
#CGC: Concurrent Garbage Collection Count - 并发垃圾收集次数
#CGCT: Concurrent Garbage Collection Time - 并发垃圾收集总耗时(秒)
#GCT: Garbage Collection Time - 垃圾收集总耗时(秒)

```

### 3.jstack

​	用于生成虚拟机指定进程当前时刻的线程快照（虚拟机堆栈跟踪）。

```
-F	当正常输出的请求不被响应时，强制输出线程堆栈
-l	除堆栈外，显示关于锁的附加信息
-m	如果调用本地方法的话，可以显示 C/C++ 的堆栈
```

### 4.jconsole

​	JVM自带的可视化观察虚拟机参数的工具

### 5.DUMP文件

​	它还可以获取目标 Java 进程的内存相关信息，包括 Java 堆各区域的使用情况、堆中对象的统计信息、类加载信息等。

#### 获取方式

1.通过Jmap命令导出dump文件

       2. Visual VM导出dump文件
       2. 通过设置java启动参数到处dump文件

```
// 开启在出现 OOM 错误时生成堆转储文件
-Xmx1024m
-XX:+HeapDumpOnOutOfMemoryError
// 将生成的堆转储文件保存到 /tmp 目录下，并以进程 ID 和时间戳作为文件名
-XX:HeapDumpPath=/tmp/java_%p_%t.hprof
 
// 在进行 Full GC 前生成堆转储文件
// 注：如果没有开启自动 GC，则此参数无效。JDK 9 之后该参数已被删除。
-XX:+HeapDumpBeforeFullGC    
```

### 6.JVM调优

###### jvm虚拟机垃圾回收过程

 1. 新创建的对象都保存在新生代的eden区，eden区储存满后触发GC（Young Gc），清空eden区，删除未引用的对象。

 2. 存活的对象移动到幸存1区(S1)，并标记年龄为1，每经历一次GC，年龄+1

 3. eden如果再次存储满，再次触发GC（young GC），删除eden区和幸存1区（S1）未引用数据，存活对象移动到幸存0区，

 4. 往复GC（young GC）次数到达阈值，年龄达到阈值的对象写入老年代中。

 5. 老年代区域存储满后，触发Full GC，清理老年代未引用对象。

    > [!CAUTION]
    >
    > 💡 老年代存储满触发Full GC
    >
    > ​	方法区空间不足触发Full GC
    >
    > ​	当年龄到达阈值的对象写入老年代，老年代内存不足，触发Full GC

#### 调优核心参数

 1. 调整堆内存的空间大小

 2. 调整eden区、幸存1区、幸存0区、和老年代之前的比例关系

 4. 调整吞吐量的比率，吞吐量=运行时长/运行时长+GC时长

    ```shell
    -XX:GCTimeRatio=99
    ```

 5. 调整存活对象写入老年代的年龄阈值。

 6. 调整GC中断应用程序的执行时间。

    ```shell
    //GC停顿时间，垃圾收集器会尝试用各种手段达到这个时间
     -XX:MaxGCPauseMillis=10
    ```

    

[1]: https://blog.csdn.net/qq_40991313/article/details/132382094

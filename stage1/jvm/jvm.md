[黑马程序员JVM教程](https://www.bilibili.com/video/BV1yE411Z7AP?spm_id_from=333.999.0.0)
1. 内存结构
- 程序计数器
jvm中的程序计数器用来存储下一条指令的地址，jvm使用cpu中的寄存器作为程序计数器。
jdk1.8版本之后，方法区内存改为MetaSpace,默认是使用机器内存，可以通过`-XX:MaxMetaspaceSize=8m`设置 

堆内存的默认垃圾回收机制：
jdk8 CMS 
jdk9 G1
jdk11 ZGC 

https://docs.oracle.com/en/java/javase/11/index.html


[java命令参数手册](https://docs.oracle.com/en/java/javase/11/tools/java.html#GUID-BE93ABDC-999C-4CB5-A88B-1994AAAC74D5)
编译期优化：



2. 线上问题排查
- 内存溢出
    - 堆内存
    - 栈内存
        - 递归方法调用导致栈内存耗尽
        - 单个对象过大导致栈内存耗尽，常见的map，string，list中保存1-2个对象。
    - 方法区
- CPU过高解决步骤

    - 死循环
    - 网络I/O阻塞
    - 本地I/O阻塞
    - 
- 接口返回特别慢



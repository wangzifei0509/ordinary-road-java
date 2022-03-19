1. 并发（concurrent），同一时间应对不同的事情。并行（parallel），同一时间处理不同的事情。大多数情况下，我们的程序是即有并发又有并行。
2. 多核多线程才有意义，如果是单核那么CPU由于还是串行，还要切换线程上下文，那么单核下，多线程反而比单线程慢。这个结果也解释了为什么线程池的core thread num 一般设置为核数，而max thread num 设置为核数*2.  
IO并不占用CPU，但是会阻塞CPU，所以之后才出现了非阻塞IO和异步IO。IO主要分为网络IO和磁盘IO，一个是本机的数据操作，一个是网络socket之间的数据交换。
3. 初始化线程的三种方法
- 直接使用Thread
- 使用Runnable配合Thread
- 使用Future配合Thread
  ```java
   // 1 不建议使用Thread本身
        Thread t1 = new Thread("t1"){
            @Override
            public void run() {
                log.info("running");
            }
        };
        t1.start();

        //2 建议使用这种方式，具体异步执行的代码和Thread分开
        Thread t2 = new Thread(()->{
           log.info("running");
        },"t2");
        t2.start();
        //3 获取结果的阻塞异步，
        FutureTask<Integer> ft = new FutureTask<>(()->{
            log.info("calling");
            return 100;
        });

        Thread t3 = new Thread(ft,"t3");
        t3.start();
        ft.get();
  ```
4. java 查看线程的命令
  - jps //查看所有java进程
  - jstack pid //查看指定java进程的线程情况
  - jconsole  //图形化方式查看java各项指标
5. 线程的状态
6. 线程锁升级
   - 偏向锁
   - 轻量级锁
   - 重量级锁
   - 自旋
   - 锁升级
   - 锁消除
7. sleep vs wait 
8. 使用wait-notify的正确方式
```java
synchorinzed (lock){
    while(!condition){
    lock.wait();
    }

    //do something
}
synchorinzed(lock){
    condition = true
    lock.notifyAll();
}
```
9. 同步保护暂停模式
10. 异步生产这消费者模式
11. wait-notify
12. park-unpark
13. 



- 阻塞
- 同步
- 释放CPU
- 释放lock
- 

原子性：操作一次完成，不会被打断，就算时间片用完了，下一次还是只能该线程执行。
可见性：线程内的缓存和主存的同步
排序性：取消CPU指令重排，CPU指令重排是为了提高CPU的吞吐量。
synchronize 能保证保护的 代码块的原子性、可见性和排序性。
volatile 能保证可见性和排序性，不能保证原子性。能保证在被volatile修饰的变量，赋值前的代码都从主存中获取并且代码取消重排，取值后的代码都从主存中获取并且代码取消重排。










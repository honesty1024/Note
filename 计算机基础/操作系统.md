# 操作系统

## 一、进程（Process）：进程是正在运行的程序。

​    1.进程的状态：

​        New：进程正在被创建

​        Running：指令正在被执行

​        Waiting：进程等待某个事件的发生（如I/O完成或收到信号）

​        Ready：进程等待分配处理器

​        Terminated：进程完成执行

​        ![img](https://img-blog.csdnimg.cn/20190514211654722.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hvbmVzdHkxMDI0,size_16,color_FFFFFF,t_70)

​        重要：一次只有一个进程可在一个处理器上运行，但是多个进程可处于就绪或等待状态。

​    2.进程调度：多道程序设计的目的就是无论何时都有进程在运行，从而使CPU利用率达到最大。选择一个可用的进程到CPU上执行。

​        当进程分配到CPU并执行时，可能发生的情形：

​            ①进程可能发出一个I/O请求，并被放到I/O队列中。

​            ②进程可能创建一个新的子进程，并等待期结束。

​            ③进程可能会由于中断而强制释放CPU，并被放回到就绪队列中。

​    3.进程调度程序：

​        ①长期调度程序（long-term scheduler) 或作业调度程序（job shceduler)：从进程池中选择进程，并装入内存/ready queue以准备执行。

​        ②短期调度程序（short-term scheduler)或CPU调度程序：从准备执行的进程中选择进程并为之分配CPU.

​        ③中期调度程序（medium-term scheduler)：将进程从内存中删除，之后该进程可以重新引入内存，并可以在中断的位置继续执行。有利降低多道程序设计的程度。![img](https://img-blog.csdnimg.cn/20190514211736813.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hvbmVzdHkxMDI0,size_16,color_FFFFFF,t_70)

​        并发Concurrent和并行Parallelism的区别：![img](https://img-blog.csdnimg.cn/2019051421181727.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hvbmVzdHkxMDI0,size_16,color_FFFFFF,t_70)

​    4.进程间通信(interprocess communication,IPC)：

​        ①共享内存系统（Shared-Memory Systems）

​            采用共享内存的进程间通信需要通信进程建立共享内存区域。通常，一块共享内存区域驻留在生成共享内存段进程的地址空间。其他希望使用这个共享内存段进行通信的进程必须将此放到他们自己的地址空间上。

​        ②消息传递系统（Message-Passing Systems）

​            消息传递工具：发送消息，接收消息，通信线路

​            ⅰ.命名：直接通信，间接通信（邮箱）

​            ⅱ.同步synchronization：消息传递可以是阻塞或非阻塞（也称为同步或异步）

​            ⅲ.缓冲buffering：不管通信是直接还是间接的，通信进程所交换的信息都驻留在临时队列中，简单的讲，队列实现有三种方法：

​            ⅳ.零容量 Zero capacity：队列的最大长度为0；因此，线路中不能有任何消息处于等待。即必须阻塞发送，直到接收者接收到消息。

​            ⅴ.有限容量Bounded capacity：队列长度为有限的n；因此，最多只能有n个消息驻留在队列中，如果发送新消息是队列未满，那么该消息可以放在队列中（或者复制消息或者保存消息的指针），其发送者可以继续执行而不必等待。不过线路容量有限。如果线路满，则必须阻塞发送者直到队列中的空间可用为止。

​            ⅵ.无限容量Unbounded capacity：队列长度可以无限，因此不管多少消息都可在其中等待，从不阻塞发送者。

## 二、线程（Thread）：

​    1.概述

​        ①线程：是CPU使用的基本单元，它由线程ID,程序计数器，寄存器集合和栈组成。它与属于统一进程的其他线程共享代码段、数据段和其他操作系统资源。

​        ②多线程的优点：

​            ⅰ.响应度高

​            ⅱ.共享资源：默认共享他们所属进程的内存和资源。

​            ⅲ.经济：线程可以共享资源，创建和替换速度比进程块。

​            ⅳ.多处理体系结构的利用：能充分利用多处理器体系结构，以便每个进程能并行运行在不同的处理器上。

## 三、CPU调度（CPU Scheduling）：

CPU调度是多道程序操作系统的基础。通过在进程之间切换CPU,操作系统可以提高计算机的吞吐率。

​    1.CPU调度程序：抢占调度（Preemptive scheduler）

​        CPU调度决策发生的四种环境：

​            ①当一个CPU从运行状态切换到等待状态（I/O请求或调用wait)

​            ②当一个进程从运行状态切换到就绪状态（当出现中断）

​            ③当一个进程从等待状态切换到就绪状态（I/O完成）（根据优先级抢占）

​            ④当一个进程终止时。

​    2.调度算法：

​        ①First-Come,First-Served(FCFS) Scheduling

​        ②Shortest-Job-First(SJF) Scheduling:分抢占式和非抢占式

​        ③Priority Scheduling

​        ④Round-Robin,RR Scheduling时间片转轮算法

​        ⑤多级队列调度(Multilevel Queue Scheduling )

## 四、进程同步（Process Synchronization）：

多个进程并发访问和操作同一数据且执行结果与访问发生的特定顺序有关，称为竞争条件（race condition)。为了避免竞争条件，需要确保一段时间内只有一个进程能操作变量，其必须进行一定形式的同步。

​    1.互斥（mutual exclusion):如果进程P在其临界区执行，其他进程都不能在其临界区执行。

​    2.信号量（semaphore)：一种同步工具，信号量S是个整数变量，除了初始化外，他只能通过两个标准原子操作：wait()和signal()来访问。

​    3.经典案例：

​        ①生产者/消费者问题（The Bounded-Buffer Problem）：先申请资源，再申请互斥；先释放互斥，再释放资源。

​        ②读写者问题（The Readers-Writers Problem）：只能有一个在写。有人在写时不可读。

​        ③哲学家吃饭问题（The Dining-Philosophers Problem）：第一轮奇数座位抢左边筷子，偶数抢右边筷子；第二轮，没抢到筷子的不能抢，奇数座位抢右边筷子，偶数抢左边筷子。

## 五、死锁（Deadlock）：

死锁是指两个或两个以上的进程在执行过程中，由于竞争资源或者由于彼此通信而造成的一种阻塞的现象，若无外力作用，它们都将无法推进下去。此时称系统处于死锁状态或系统产生了死锁，这些永远在互相等待的进程称为死锁进程。（两个事务永远不能结束，形成死锁）

​    1.死锁的四个特征：互斥Mutual exclusion，占有且等待Hold and wait，不可抢占 no preemption，循环等待Circular wait。

死锁产生的4个必要条件

​        ①互斥：某种资源一次只允许一个进程访问，即该资源一旦分配给某个进程， 其他进程就不能再访问，直到该进程访问结束。

​        ②占有且等待：一个进程本身占有资源（一种或多种），同时还有资源未得到满足，正在等待其他进程释放该资源。

​        ③不可抢占：别人已经占有了某项资源，你不能因为自己也需要该资源，就去把别人的资源抢过来。

​        ④循环等待：存在一个进程链，使得每个进程都占有下一个进程所需的至少 一种资源。

​    2.死锁处理方法：

​        可使用协议以预防或避免死锁；

​        可允许系统进入死锁状态，然后检测它，并加以恢复；

​        ①死锁预防（deadlock prevention)：

​            1.一次封锁法：要求每个事务必须一次将所有要用的数据全部加锁，否则不能继续执行。

​            2.顺序封锁法：预先对数据对象规定一个封锁顺序，所有事务都按这个顺序实施封锁。

​          两段锁协议：指所有事务必须分两个阶段对数据项进行加锁和解锁。1.在对任何数据进行读、写操作前，首先要申请并获得对该数据的封锁。2.在释放一个封锁后，事务不得再申请和获得任何其他封锁。

​        ②死锁避免（deadlock avoidance):要求操作系统事先得到有关进程申请资源和使用资源的额外信息。

​        ③死锁恢复

​            ⅰ.进程终止:（1）终止所有死锁进程；（2）一次只终止一个进程知道取消死锁循环为止；

​            ⅱ.资源抢占：（1）选择一个牺牲品；（2） 回滚

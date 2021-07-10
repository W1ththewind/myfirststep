# Embedded OS 
- 操作系统功能  
> 用户、系统角度
- ***☆嵌入式操作系统的特点***
> 针对性；界面简单；资源有限；待机时间长；内置应用；与外部设备连接
- RTOS
> 实时操作系统
- 常见嵌入式操作系统
- ***☆Linux作为嵌入式操作系统的优势***
> 跨平台；性能稳定，裁剪性好；内核的网络方面结构完整；大小很适合嵌入式操作系统；源码实用性强，使用Linux的程序员很多
- ***☆嵌入式Linux和桌面Linux的异同***
> 处理器；内存；应用场景；硬件；电源；内核；界面；
- ***计算机体系架构***
> 冯·诺依曼结构：程序存储和数据存储使用同一个内存设备  
> 哈佛结构：程序存储与数据存储分开，地址隔离
> 改良：地址共享/地址隔离但可以从程序地址空间读取数据
- CPU架构与指令集
- ***☆处理器两种工作模式***
> 1. 特权模式（root）：对存储和设备无限制访问，可以执行特权指令
> 2. 普通模式：指令受限，不能直接使用硬件，需要通过系统调用
- 字节端序
- 嵌入式处理器的分类和典型微处理器
- ***☆MMU概念***
> 存储器管理单元，也称分页内存管理单元，负责处理CPU的**内存访问请求**的硬件  
> 功能包括：虚拟地址到物理地址的转换，内存保护，CPUcache的控制
- ***☆指针***
- 数组
- 结构体
- 链表概念
- ***☆Linux启动流程***
> BIOS引导->MBR引导->bootloader->内核阶段->初始化阶段
- sysinit运行级别概念
- 命令基本作用：***dd***，***ln***，fdisk，mount
> - dd：用指定大小的块copy文件，并进行指定的转换  
> dd创建64MB全0文件：dd if=/dev/zero of=zero.file bs=4096 count=16K
> - ln：用于创建文件的链接文件，格式-： ln -s target link_name 
- ***☆ls -l 显示文件权限，属性***
> ls：列出当前文件目录  
> ls -l：-rw-------.  1 root root 1.3K Dec 14 01:38 anaconda-ks.cfg  
> 第一列1位表示文件类型，后面9位对应owner、group、others的权限,第二列表示链接数，第三列拥有者，第四列群组，第五列文件大小，第六列最后修改时间，第七列名称（以.开头为隐藏文件
- 根文件系统目录结构与源代码目录结构
- - 根文件：***/dev /sys /proc*** /etc /bin /lib /var
> /dev：设备文件存储目录；  
> /sys：记录系统硬件相关信息；  
> /proc：存放进程信息和内核信息
- - 源代码：***/arch /include /kernel /driver /mm*** /modules /fs /net
> /arch：包含和硬件体系结构相关代码；  
> /include：头文件；  
> /kernel：内核最核心部分，包含进程调度、定时器等；  
> /drivers：设备驱动程序，不同驱动占用一个子目录；  
> /mm：内存管理代码
- ***☆进程概念***
> 一个程序对数据的执行过程，是操作系统对资源分配、保护和调度的基本单位，程序执行时的一个实体（包括 代码、数据和更多的**控制信息**。
- ***☆进程与程序的区别和联系***
> 一个程序可以运行多个进程，一个进程可以执行多个程序
> 程序位于磁盘，而进程位于内存上
- ***☆PCB***
> 进程描述符，用于记录进程相关信息（可用在进程中断和系统调用过程   
> 信息：状态；编号id；程序计数器；寄存器；I/O信息；
- ***☆进程基本三态模型与转换***
> 1. 运行态：占用CPU,执行指令，每时只有一个进程可在一个处理器上执行(被高优先抢占或超出运行时间时进入ready态)
> 2. 就绪态：具备了除CPU外的所有执行条件（因调度获得CPU）
> 3. 等待态：缺少某些资源，等待某事件的发生(只能 获得资源转 向就绪态)
- 进程生命周期：***fork()***,exec(),waitpid(),exit()
> 系统调用创建一个与原进程几乎完全相同的进程
- ***☆进程与线程的联系与区别***
> 线程常称为 轻量级进程 ，进程之间资源隔离，需要通过进程通信机制进行资源共享，而同一进程的线程之间，共享地址空间，因此能够共享资源
- ***☆IPC的概念与作用，Linux IPC包含的方式***
> 进程间通信（不同进程间传播或交换信息），方式：
> - 将信息从一个地址空间复制到另一个地址空间（需要传递，利用套接字、管道。POSIX消息队列）
> - 创建内存并同时映射到多个进程地址空间（需要同步访问机制，如信号或互斥）
- 管道与FIFO的概念
- ***☆信号概念，信号的安装、发送、接收***
> 信号用于通知进程有某种事情发生，是软件层次上对中断机制的模拟  
> 安装：确定信号值以及进程对于该信号应执行的操作  
> 发送：kill、raise、sigqueue、alarm、setitimer、abort
> 接收：
- 进程竞争条件的概念
- ***☆LinuxIPC的方式***
> System V：信号量、共享内存、消息队列  
> Socket  
> POSIX：信号、管道
- ***☆信号量***
> 代表进程目前的状态，可类比为交通灯，实际是一个与队列有关的整型变量
- ***☆共享内存***
> 在内核中开辟一块内存区域，分别被映射到进程A、B各自的进程地址空间
- VMM
- ***☆Linux进程虚拟地址空间***
> MMU提供虚拟空间运行程序，地址从0开始，以最高地址结束，被划分为多个4KB大小的页面，分为用户空间（给应用），内核空间
- 堆内存的分配与释放
- ***☆mmap内存映射***
> 常用于 内存共享 或者 应用程序控制硬件设备 文件的直接访问   
> 提供了不同于一般对普通文件的访问方式，进程可以像读写内存一样对普通文件操作  
> 进程之间通过映射同一个普通文件实现共享内存
- ***☆VFS概念***
> 虚拟文件系统 是一个软件层，让上层的软件可以用单一的方式与底层不同的实体文件系统沟通  
> 用户应用程序与文件系统实现之间的抽象层；为各种文件系统提供通用接口
- ***☆文件的基本操作：open(),read(),write(),close()***

- ***☆SCI与API概念***
> SCI：系统调用接口，是内核与应用程序进行交互通信的接口
> API：应用程序接口，是一些预先定义的函数，提供访问例程的能力
- ***☆文件描述符与标准文件描述符***
> 文件描述符：用于表述指向文件的引用，是0~1023的正数，实际是进程打开文件结构体数组的下标
- 设备驱动概念
- Linux设备驱动工作层次
- ***☆Linux设备的3个分类***
> 字符设备，数据流、顺序读取  
> 块设备，随机访问，程序可以自行确定读取数据的位置  
> 网络设备，通过接口进行网络事务（接口也有可能是软件设备
- ***☆Linux设备控制的3种方式***
> 查询方式：CPU不停查询外设状态，硬件开销小，但效率低  
> 中断方式：中断源向CPU发出中断请求，优先级高则中断当前程序的运行，转而执行新的程序段  
> 直接访问内存方式：硬件直接读写系统内存
- ***☆嵌入式Linux开发四要素***
> 工具链toolchain；引导加载程序bootloader；内核；根文件系统
- ***☆交叉编译概念***
> 在一个平台上生成另一个平台上的可执行代码，如在Windows系统上开发linux程序
- ***☆bootloader概念***
> 在操作系统内核运行之前运行的一小段程序，可以初始化硬件设备、建立内存空间的映射图，从而将系统的软硬件环境带到一个合适状态
- ***☆uboot是啥***
> 是sourceforge网站上的一个开放源代码的项目，对许多处理器提供支持，用于开发嵌入式系统初始化代码bootloader
- ***☆busybox是啥***
> 将许多常见应用程序的微缩版组合到一个单独小巧的可执行程序中
- Android 与 Liunx关系
> Android采用Linux作为内核，做了修改以适应移动设备，曾作为Linux的分支，后被内核小组从开发树上剔除
- Android 驱动闭源与GPLv2
- ***☆Android 框架***
> 操作系统->中间件（库和运行环境）层->应用程序框架->应用程序
- ***☆Android 软件系统层次结构***
> Linux Kernel，Userspace drivers，Native libaries，API Framework，App
- ***☆Android 虚拟机概念***
> Dalvik：运行dex文件的虚拟计算机系统，使用java编写的android程序实际运行在DVM上，DVM针对手机程序做了优化，占用的资源小，可同时运行多个实例
- ***☆Android NDK概念***
> 是开发工具，允许程序开发人员在Android应用中嵌入C/C++等语言编写的非托管代码
- Android Binder概念
- ***☆Android 四大组件***
> Activities：界面，处理用户交互  
> Services：处理应用有关的后台进程  
> Broadcast Receivers：处理系统与应用的通信  
> Content Providers：处理数据和数据库管理，访问接口
- ***☆Android Activity 生命周期***
> 活动（焦点）生命周期：Activity在最上层可交互的阶段  
> 可视生命周期：从可见到不可见的过程  
> 完全生命周期：从建立到销毁的全过程  
- Android APK，adb
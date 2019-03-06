# lec 3 SPOC Discussion

## **提前准备**
（请在上课前完成）


 - 完成lec3的视频学习和提交对应的在线练习
 - git pull ucore_os_lab, v9_cpu, os_course_spoc_exercises  　in github repos。这样可以在本机上完成课堂练习。
 - 仔细观察自己使用的计算机的启动过程和linux/ucore操作系统运行后的情况。搜索“80386　开机　启动”
 - 了解控制流，异常控制流，函数调用,中断，异常(故障)，系统调用（陷阱）,切换，用户态（用户模式），内核态（内核模式）等基本概念。思考一下这些基本概念在linux, ucore, v9-cpu中的os*.c中是如何具体体现的。
 - 思考为什么操作系统需要处理中断，异常，系统调用。这些是必须要有的吗？有哪些好处？有哪些不好的地方？
 - 了解在PC机上有啥中断和异常。搜索“80386　中断　异常”
 - 安装好ucore实验环境，能够编译运行lab8的answer
 - 了解Linux和ucore有哪些系统调用。搜索“linux 系统调用", 搜索lab8中的syscall关键字相关内容。在linux下执行命令: ```man syscalls```
 - 会使用linux中的命令:objdump，nm，file, strace，man, 了解这些命令的用途。
 - 了解如何OS是如何实现中断，异常，或系统调用的。会使用v9-cpu的dis,xc, xem命令（包括启动参数），分析v9-cpu中的os0.c, os2.c，了解与异常，中断，系统调用相关的os设计实现。阅读v9-cpu中的cpu.md文档，了解汇编指令的类型和含义等，了解v9-cpu的细节。
 - 在piazza上就lec3学习中不理解问题进行提问。

## 第三讲 启动、中断、异常和系统调用-思考题

## 3.1 BIOS
-  x86中BIOS从磁盘读入的第一个扇区是是什么内容？为什么没有直接读入操作系统内核映像？

**主引导扇区MBR**

**因为操作系统内核映像不只有一个扇区，无法决定从哪个开始读，没有建立文件系统，只能固定读一个扇区**

-  比较UEFI和BIOS的区别。

**UEFI为统一可扩展固件接口，是BIOS的替代方案。UEFI安全性更好，可以保护系统，配置更加灵活，引导所支持的容量更大。**

-  理解rcore中的Berkeley BootLoader (BBL)的功能。

**BBL将整个操作系统通过payload.S进行包装并装载到内存中。**

## 3.2 系统启动流程

- x86中分区引导扇区的结束标志是什么？

**0x66AA**

- x86中在UEFI中的可信启动有什么作用？

**确定启动盘的安全性**

- RV中BBL的启动过程大致包括哪些内容？

**BBL将整个操作系统通过payload.S进行包装并装载到内存中。**

## 3.3 中断、异常和系统调用比较
- 什么是中断、异常和系统调用？

**中断 外部设备引起的响应**

**异常 内部指令执行异常引起的响应**

**系统调用 系用指令引起的响应**

- 中断、异常和系统调用的处理流程有什么异同？

**同： 都进入内核态开始处理**

**异： * 原因不同**

​	*** 响应方式不同 中断为异步，异常为同步，系统调用为同步**

- 以ucore/rcore lab8的answer为例，ucore的系统调用有哪些？大致的功能分类有哪些？

```
static int (*syscalls[])(uint32_t arg[]) = {
    [SYS_exit]              sys_exit,
    [SYS_fork]              sys_fork,
    [SYS_wait]              sys_wait,
    [SYS_exec]              sys_exec,
    [SYS_yield]             sys_yield,
    [SYS_kill]              sys_kill,
    [SYS_getpid]            sys_getpid,
    [SYS_putc]              sys_putc,
    [SYS_pgdir]             sys_pgdir,
    [SYS_gettime]           sys_gettime,
    [SYS_lab6_set_priority] sys_lab6_set_priority,
    [SYS_sleep]             sys_sleep,
    [SYS_open]              sys_open,
    [SYS_close]             sys_close,
    [SYS_read]              sys_read,
    [SYS_write]             sys_write,
    [SYS_seek]              sys_seek,
    [SYS_fstat]             sys_fstat,
    [SYS_fsync]             sys_fsync,
    [SYS_getcwd]            sys_getcwd,
    [SYS_getdirentry]       sys_getdirentry,
    [SYS_dup]               sys_dup,
};
```

**进程管理类(exit, wait, fork, exec, kill)，文件操作类(write, read, close, open)，系统信息类(getcwd getdirentry)，输出类(putc)**

## 3.4 linux系统调用分析

- 通过分析[lab1_ex0](https://github.com/chyyuu/ucore_lab/blob/master/related_info/lab1/lab1-ex0.md)了解Linux应用的系统调用编写和含义。(仅实践，不用回答)
- 通过调试[lab1_ex1](https://github.com/chyyuu/ucore_lab/blob/master/related_info/lab1/lab1-ex1.md)了解Linux应用的系统调用执行过程。(仅实践，不用回答)


## 3.5 ucore/rcore系统调用分析 （扩展练习，可选）
-  基于实验八的代码分析ucore的系统调用实现，说明指定系统调用的参数和返回值的传递方式和存放位置信息，以及内核中的系统调用功能实现函数。
- 以ucore/rcore lab8的answer为例，分析ucore 应用的系统调用编写和含义。
- 以ucore/rcore lab8的answer为例，尝试修改并运行ucore OS kernel代码，使其具有类似Linux应用工具`strace`的功能，即能够显示出应用程序发出的系统调用，从而可以分析ucore应用的系统调用执行过程。


## 3.6 请分析函数调用和系统调用的区别
- 系统调用与函数调用的区别是什么？	
  - **系统调用进入内核态，权限更高**
  - **系统调用涉及堆栈转换**
- 通过分析x86中函数调用规范以及`int`、`iret`、`call`和`ret`的指令准确功能和调用代码，比较x86中函数调用与系统调用的堆栈操作有什么不同？

  - **系统调用中，涉及到堆栈的转换，所以int、iret指令前后的栈顶指针esp不在一个堆栈上；int指令后，处理者handler栈会存储相关的信息；iret指令后，栈顶指针esp会恢复到引发系统调用的栈上。**
  - **函数调用中，不涉及堆栈的转换，故在call和ret调用的前后，栈顶指针在同一个堆栈上；call指令后，esp会增加，并在栈新增的空间中存储参数；而ret指令后，esp会恢复到调用前的位置，并恢复栈。**


- 通过分析RV中函数调用规范以及`ecall`、`eret`、`jal`和`jalr`的指令准确功能和调用代码，比较x86中函数调用与系统调用的堆栈操作有什么不同？


**RV通过ABI来实现系统调用，用ecall和eret实现堆栈和特权级的切换，保存寄存器的值到堆栈**

## 课堂实践 （在课堂上根据老师安排完成，课后不用做）
### 练习一
通过静态代码分析，举例描述ucore/rcore键盘输入中断的响应过程。

### 练习二
通过静态代码分析，举例描述ucore/rcore系统调用过程，及调用参数和返回值的传递方法。

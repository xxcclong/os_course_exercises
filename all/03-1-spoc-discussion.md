# lec5: SPOC思考题

##**提前准备**
（请在上课前完成）

- 完成lec５的视频学习和提交对应的在线练习
- git pull ucore_os_lab, v9_cpu, os_course_spoc_exercises in github repos。这样可以在本机上完成课堂练习。
- 理解连续内存动态分配算法的实现（主要自学和网上查找）

NOTICE
- 有"hard"标记的题有一定难度，鼓励实现。
- 有"easy"标记的题很容易实现，鼓励实现。
- 有"midd"标记的题是一般水平，鼓励实现。


## 思考题
---

## “连续内存分配”与视频相关的课堂练习

### 5.1 计算机体系结构和内存层次

1.操作系统中存储管理的目标是什么？

**因为各个层级的存储设备成本，容量，速度都不同，所以需要使用层级的管理模式来同时保证容量和速度，但是需要给上层一个简单的接口，同时为了保证效率需要统一管理，所以需要存储管理。**


### 5.2 地址空间和地址生成
1.描述编译、汇编、链接和加载的过程是什么？

**先将每个代码文件编译为汇编代码，之后将其汇编为机器代码，之后将所有机器码链接为可执行程序**

2.动态链接如何使用？尝试在Linux平台上使用LD_DEBUG查看一个C语言Hello world的启动流程。  (optional)

>  18749:	find library=libc.so.6 [0]; searching
>
>      18749:	 search path=/home/huangkz/nccl_2.1.15-1+cuda8.0_x86_64/lib/tls/x86_64:/home/huangkz/nccl_2.1.15-1+cuda8.0_x86_64/lib/tls:/home/huangkz/nccl_2.1.15-1+cuda8.0_x86_64/lib/x86_64:/home/huangkz/nccl_2.1.15-1+cuda8.0_x86_64/lib:/usr/lib/x86_64-linux-gnu/slurm/tls/x86_64:/usr/lib/x86_64-linux-gnu/slurm/tls:/usr/lib/x86_64-linux-gnu/slurm/x86_64:/usr/lib/x86_64-linux-gnu/slurm:/home/huangkz/Test/GTEst/googletest/mybuild/tls/x86_64:/home/huangkz/Test/GTEst/googletest/mybuild/tls:/home/huangkz/Test/GTEst/googletest/mybuild/x86_64:/home/huangkz/Test/GTEst/googletest/mybuild:/home/huangkz/usr/lib/tls/x86_64:/home/huangkz/usr/lib/tls:/home/huangkz/usr/lib/x86_64:/home/huangkz/usr/lib:/home/huangkz/mpich-install/lib/tls/x86_64:/home/huangkz/mpich-install/lib/tls:/home/huangkz/mpich-install/lib/x86_64:/home/huangkz/mpich-install/lib:/home/huangkz/ngraph_dist/lib/tls/x86_64:/home/huangkz/ngraph_dist/lib/tls:/home/huangkz/ngraph_dist/lib/x86_64:/home/huangkz/ngraph_dist/lib:/opt/intel/mkl/lib/intel64/tls/x86_64:/opt/intel/mkl/lib/intel64/tls:/opt/intel/mkl/lib/intel64/x86_64:/opt/intel/mkl/lib/intel64:/home/huangkz/Repos/TensorRT/TensorRT-4.0.1.6/lib/tls/x86_64:/home/huangkz/Repos/TensorRT/TensorRT-4.0.1.6/lib/tls:/home/huangkz/Repos/TensorRT/TensorRT-4.0.1.6/lib/x86_64:/home/huangkz/Repos/TensorRT/TensorRT-4.0.1.6/lib:/home/huangkz/Repos/TensorRT/TensorRT-4.0.1.6/targets/x86_64-linux-gnu/lib/tls/x86_64:/home/huangkz/Repos/TensorRT/TensorRT-4.0.1.6/targets/x86_64-linux-gnu/lib/tls:/home/huangkz/Repos/TensorRT/TensorRT-4.0.1.6/targets/x86_64-linux-gnu/lib/x86_64:/home/huangkz/Repos/TensorRT/TensorRT-4.0.1.6/targets/x86_64-linux-gnu/lib:/usr/local/cuda-10.0/lib64/tls/x86_64:/usr/local/cuda-10.0/lib64/tls:/usr/local/cuda-10.0/lib64/x86_64:/usr/local/cuda-10.0/lib64:/home/huangkz/usr/cuda-9.0/extras/CUPTI/lib64/tls/x86_64:/home/huangkz/usr/cuda-9.0/extras/CUPTI/lib64/tls:/home/huangkz/usr/cuda-9.0/extras/CUPTI/lib64/x86_64:/home/huangkz/usr/cuda-9.0/extras/CUPTI/lib64:tls/x86_64:tls:x86_64:		(LD_LIBRARY_PATH)
>      18749:	  trying file=/home/huangkz/nccl_2.1.15-1+cuda8.0_x86_64/lib/tls/x86_64/libc.so.6
>      18749:	  trying file=/home/huangkz/nccl_2.1.15-1+cuda8.0_x86_64/lib/tls/libc.so.6
>      18749:	  trying file=/home/huangkz/nccl_2.1.15-1+cuda8.0_x86_64/lib/x86_64/libc.so.6
>      18749:	  trying file=/home/huangkz/nccl_2.1.15-1+cuda8.0_x86_64/lib/libc.so.6
>      18749:	  trying file=/usr/lib/x86_64-linux-gnu/slurm/tls/x86_64/libc.so.6
>      18749:	  trying file=/usr/lib/x86_64-linux-gnu/slurm/tls/libc.so.6
>      18749:	  trying file=/usr/lib/x86_64-linux-gnu/slurm/x86_64/libc.so.6
>      18749:	  trying file=/usr/lib/x86_64-linux-gnu/slurm/libc.so.6
>      18749:	  trying file=/home/huangkz/Test/GTEst/googletest/mybuild/tls/x86_64/libc.so.6
>      18749:	  trying file=/home/huangkz/Test/GTEst/googletest/mybuild/tls/libc.so.6
>      18749:	  trying file=/home/huangkz/Test/GTEst/googletest/mybuild/x86_64/libc.so.6
>      18749:	  trying file=/home/huangkz/Test/GTEst/googletest/mybuild/libc.so.6
>      18749:	  trying file=/home/huangkz/usr/lib/tls/x86_64/libc.so.6
>      18749:	  trying file=/home/huangkz/usr/lib/tls/libc.so.6
>      18749:	  trying file=/home/huangkz/usr/lib/x86_64/libc.so.6
>      18749:	  trying file=/home/huangkz/usr/lib/libc.so.6
>      18749:	  trying file=/home/huangkz/mpich-install/lib/tls/x86_64/libc.so.6
>      18749:	  trying file=/home/huangkz/mpich-install/lib/tls/libc.so.6
>      18749:	  trying file=/home/huangkz/mpich-install/lib/x86_64/libc.so.6
>      18749:	  trying file=/home/huangkz/mpich-install/lib/libc.so.6
>      18749:	  trying file=/home/huangkz/ngraph_dist/lib/tls/x86_64/libc.so.6
>      18749:	  trying file=/home/huangkz/ngraph_dist/lib/tls/libc.so.6
>      18749:	  trying file=/home/huangkz/ngraph_dist/lib/x86_64/libc.so.6
>      18749:	  trying file=/home/huangkz/ngraph_dist/lib/libc.so.6
>      18749:	  trying file=/opt/intel/mkl/lib/intel64/tls/x86_64/libc.so.6
>      18749:	  trying file=/opt/intel/mkl/lib/intel64/tls/libc.so.6
>      18749:	  trying file=/opt/intel/mkl/lib/intel64/x86_64/libc.so.6
>      18749:	  trying file=/opt/intel/mkl/lib/intel64/libc.so.6
>      18749:	  trying file=/home/huangkz/Repos/TensorRT/TensorRT-4.0.1.6/lib/tls/x86_64/libc.so.6
>      18749:	  trying file=/home/huangkz/Repos/TensorRT/TensorRT-4.0.1.6/lib/tls/libc.so.6
>      18749:	  trying file=/home/huangkz/Repos/TensorRT/TensorRT-4.0.1.6/lib/x86_64/libc.so.6
>      18749:	  trying file=/home/huangkz/Repos/TensorRT/TensorRT-4.0.1.6/lib/libc.so.6
>      18749:	  trying file=/home/huangkz/Repos/TensorRT/TensorRT-4.0.1.6/targets/x86_64-linux-gnu/lib/tls/x86_64/libc.so.6
>      18749:	  trying file=/home/huangkz/Repos/TensorRT/TensorRT-4.0.1.6/targets/x86_64-linux-gnu/lib/tls/libc.so.6
>      18749:	  trying file=/home/huangkz/Repos/TensorRT/TensorRT-4.0.1.6/targets/x86_64-linux-gnu/lib/x86_64/libc.so.6
>      18749:	  trying file=/home/huangkz/Repos/TensorRT/TensorRT-4.0.1.6/targets/x86_64-linux-gnu/lib/libc.so.6
>      18749:	  trying file=/usr/local/cuda-10.0/lib64/tls/x86_64/libc.so.6
>      18749:	  trying file=/usr/local/cuda-10.0/lib64/tls/libc.so.6
>      18749:	  trying file=/usr/local/cuda-10.0/lib64/x86_64/libc.so.6
>      18749:	  trying file=/usr/local/cuda-10.0/lib64/libc.so.6
>      18749:	  trying file=/home/huangkz/usr/cuda-9.0/extras/CUPTI/lib64/tls/x86_64/libc.so.6
>      18749:	  trying file=/home/huangkz/usr/cuda-9.0/extras/CUPTI/lib64/tls/libc.so.6
>      18749:	  trying file=/home/huangkz/usr/cuda-9.0/extras/CUPTI/lib64/x86_64/libc.so.6
>      18749:	  trying file=/home/huangkz/usr/cuda-9.0/extras/CUPTI/lib64/libc.so.6
>      18749:	  trying file=tls/x86_64/libc.so.6
>      18749:	  trying file=tls/libc.so.6
>      18749:	  trying file=x86_64/libc.so.6
>      18749:	  trying file=libc.so.6
>      18749:	 search cache=/etc/ld.so.cache
>      18749:	  trying file=/lib/x86_64-linux-gnu/libc.so.6
>      18749:
>      18749:
>      18749:	calling init: /lib/x86_64-linux-gnu/libc.so.6
>      18749:
>      18749:
>      18749:	initialize program: ./a.out
>      18749:
>      18749:
>      18749:	transferring control: ./a.out
>      18749:
>      18749:
>      18749:	calling fini: ./a.out [0]
>      18749:

### 5.3 连续内存分配
1.什么是内碎片、外碎片？

**内碎片是操作系统分配给进程时，因为进程申请空间时可能不是2的幂次，而操作系统分配的又一定是2的幂次，所以会出现操作系统分配给进程的空间有一部分不会被使用到**

**外碎片是未被分配的内存，但是由于其太小而无法被分配出去**

2.最先匹配会越用越慢吗？请说明理由（可来源于猜想或具体的实验）？

会，因为最先匹配，一旦在中间的内存释放掉之后，就难以找到合适的大小放入，所以会很快产生大量碎片，需要经常move内存

3.最差匹配的外碎片会比最优适配算法少吗？请说明理由（可来源于猜想或具体的实验）？

会，因为最差匹配每次都取最大的空闲空间，所以切割之后剩下的空间会更大，而最优匹配是取最接近的空间，所以剩下的空间更少，更容易形成外碎片

4.理解0:最优匹配，1:最差匹配，2:最先匹配，3:buddy systemm算法中分区释放后的合并处理过程？ (optional)


### 5.4 碎片整理
1.对换和紧凑都是碎片整理技术，它们的主要区别是什么？为什么在早期的操作系统中采用对换技术？  

紧凑是搬移内存中已经申请了的块，合并外碎片；对换是将内存中的已申请空间搬出到外存，获得足够空间。

因为早期内存空间小，即使紧凑也不够要使用的，而且对换实现简单

2.一个处于等待状态的进程被对换到外存（对换等待状态）后，等待事件出现了。操作系统需要如何响应？

将该进程从外存对换到内存，并这个进程标记为等待

### 5.5 伙伴系统
1.伙伴系统的空闲块如何组织？

通过多个链表组织，对于$2^N$大小的内存，链表记录其地址

2.伙伴系统的内存分配流程？伙伴系统的内存回收流程？

分配：对于需求为R的，首先找最小的i使得$2^i > S > 2^{i -1}$，如果不存在，就依次找更大的i，并将其切分

回收：回收后需要查看两侧是否有相同大小的块可以合并，直到合并到不能合并

## 课堂实践

观察最先匹配、最佳匹配和最差匹配这几种动态分区分配算法的工作过程，并选择一个例子进行分析分析整个工作过程中的分配和释放操作对维护数据结构的影响和原因。

  * [算法演示脚本的使用说明](https://github.com/chyyuu/os_tutorial_lab/blob/master/ostep/ostep3-malloc.md)
  * [算法演示脚本](https://github.com/chyyuu/os_tutorial_lab/blob/master/ostep/ostep3-malloc.py)

例如：
```
python ./ostep3-malloc.py -S 100 -b 1000 -H 4 -a 4 -l ADDRSORT -p BEST -n 5 -c
python ./ostep3-malloc.py -S 100 -b 1000 -H 4 -a 4 -l ADDRSORT -p FIRST -n 5 -c
python ./ostep3-malloc.py -S 100 -b 1000 -H 4 -a 4 -l ADDRSORT -p WORST -n 5 -c
```

### 扩展思考题 (optional)

1. 请参考xv6（umalloc.c），ucore lab2代码，选择四种（0:最优匹配，1:最差匹配，2:最先匹配，3:buddy systemm）分配算法中的一种或多种，在Linux应用程序/库层面，用C、C++或python来实现malloc/free，给出你的设计思路，并给出可以在Linux上运行的malloc/free实现和测试用例。


2. 阅读[slab分配算法](http://en.wikipedia.org/wiki/Slab_allocation)，尝试在应用程序中实现slab分配算法，给出设计方案和测试用例。

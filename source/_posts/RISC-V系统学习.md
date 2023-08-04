---
title: RISC-V系统学习
comments: true
date: 2023-08-03 12:42:09
layout:
updated:
categories:
tags:
lang:
---
# 坑

##### 1. riscv64-unknown-elf-gcc 找不到头文件

解决方法：[howto-run-with-ubuntu1804_zh.md · unicornx/riscv-operating-system-mooc - Gitee.com](https://gitee.com/unicornx/riscv-operating-system-mooc/blob/main/howto-run-with-ubuntu1804_zh.md)



##### 2. qemu-system-riscv32: error while loading shared libraries: libncursesw.so.6: cannot open shared object file: No such file or directory

解决方法：[环境配置问题 :qemu-system-riscv32: error while loading shared libraries: libncursesw.so.6: cannot open shared object file: No such file or directory · Issue #I477IX · unicornx/riscv-operating-system-mooc - Gitee.com](https://gitee.com/unicornx/riscv-operating-system-mooc/issues/I477IX)










# 第一章 计算机系统漫游

##### 计算机硬件组成

![1691037758995](image/RISC-V系统学习/1691037758995.png)

cpu:

* 控制单元：把指令解析处理运行再交给控制单元和计算逻辑单元
* 计算逻辑单元：负责数字运算和逻辑运算
* 寄存器：

IOBridge（IO桥）：负责cpu和外界的桥梁，连接主存和总线

总线下面的是一些外设：鼠标、键盘、硬盘、显示器

![1691039406849](image/RISC-V系统学习/1691039406849.png)

##### 计算机架构

* 冯·诺依曼架构
  指令和数据不加以区分的存储的存储器中，执行效率较低，总线开销更小，控制逻辑更简单
* 哈佛架构
  指令和数据分开存储，执行效率高，总线开销更大，控制逻辑更难实现

##### 一个c语言文件到执行的过程

1. 编译和链接 -> a.out 存在硬盘
2. 运行 -> 把可执行程序a.out里的指令加载到内存
3. cpu的控制单元会一条一条把内存里的指令取出来（不断地 **取址** 、**译码**、**执行**）

谁会驱动cpu做这个事情？

晶振：通电后会不断一下一下发出脉冲信号，驱动cpu不断地 **取址** 、**译码**、**执行** ,这个频率叫**cpu的主频**

![1691040923895](image/RISC-V系统学习/1691040923895.png)

##### 一个mini的计算机（8位计算机，仅支持加法）

8位划分：8个比特bit

* 2位表示操作：支持最多4种操作	 01（LOAD）	 10（STORE）	 11（ADD）
* 2位表示寄存器：支持最多4个寄存器
* 4位表示地址：支持最多16个地址

![1691041407923](image/RISC-V系统学习/1691041407923.png)

OPCODE：操作码

```html
1. xxxx-00-01
2. xxxx-01-01
3. xx01-00-11
4. xxxx-00-10
```

![1691041621872](image/RISC-V系统学习/1691041621872.png)

![1691042787094](image/RISC-V系统学习/1691042787094.png)

![1691043024470](image/RISC-V系统学习/1691043024470.png)

1. 取址

![1691043327256](image/RISC-V系统学习/1691043327256.png)

2.译码

![1691043390109](image/RISC-V系统学习/1691043390109.png)

![1691043468471](image/RISC-V系统学习/1691043468471.png)

![1691043788518](image/RISC-V系统学习/1691043788518.png)

![1691043940905](image/RISC-V系统学习/1691043940905.png)

![1691044010216](image/RISC-V系统学习/1691044010216.png)

##### 存储设备的层次结构

![1691044119886](image/RISC-V系统学习/1691044119886.png)

![1691044138575](image/RISC-V系统学习/1691044138575.png)

##### 操作系统

* 系统调用（System Call）
* 指令集架构（ISA）

1. 保护硬件不被失控的软件应用程序滥用
2. 为软件提供简单一致的抽象接口，来控制复杂的多个外设硬件

![1691044343598](image/RISC-V系统学习/1691044343598.png)

---

# 第二章 RISC-V ISA介绍

[第2章(上)-RISC-V ISA 介绍_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Q5411w7z5/?p=3&spm_id_from=pageDriver&vd_source=f30dd07ede5a1255c0b1aaf0d2788938)

ISA是一个接口规范，微架构是一种实现

* 基本数据类型：byte（8）halfword（16）word（32）

![1691046983069](image/RISC-V系统学习/1691046983069.png)

![1691047540034](image/RISC-V系统学习/1691047540034.png)

![1691047582312](image/RISC-V系统学习/1691047582312.png)

ISA的宽度代表 寻址范围的大小

注意：ISA的宽度与指令长度无关

![1691049421045](image/RISC-V系统学习/1691049421045.png)

![1691050118090](image/RISC-V系统学习/1691050118090.png)

![1691050327719](image/RISC-V系统学习/1691050327719.png)

RV[字宽][模块集合]

![1691051144823](image/RISC-V系统学习/1691051144823.png)

![1691051434914](image/RISC-V系统学习/1691051434914.png)

##### 模块化

1. I	整数模块
2. E	嵌入式
3. M	乘法、除法
4. A	储存器原子指令集
5. F	单浮点精度
6. D	双浮点精度
7. C	压缩指令集
8. **G	IMAFD模块的组合**

![1691051779162](image/RISC-V系统学习/1691051779162.png)

##### 通用寄存器

非特权模式中定义了32个通用寄存器和一个PC寄存器（在RISC-V中PC没有暴露出来，与x86不一样）

![1691052494542](image/RISC-V系统学习/1691052494542.png)

##### Hart

翻译：硬件线程

指令执行流：在早期的cpu，一个核心只有一个指令执行流，也就是只有一个控制单元不停地取址、译码、执行

![1691052771942](image/RISC-V系统学习/1691052771942.png)

##### 特权级别

1. User/Application	U	（用户地址）
2. Supervisor		S	（类似保护模式，开启虚拟地址）
3. Reserved
4. Machine			M	(类似x86的实模式，此时，虚拟地址不生效，全部运行在物理地址，)

开了虚拟地址之后才有进程的概念

![1691053114697](image/RISC-V系统学习/1691053114697.png)

##### Control and Status Registers（CSR）

- 在不同的级别下，有对应各自一套寄存器（CSR）
- 高级别可以访问低级别的寄存器
- 有专门操作CSR的指令
- 有特定的指令可以在不同特权级别之间切换

![1691053590126](image/RISC-V系统学习/1691053590126.png)

##### 内存管理与保护

虚拟内存需要硬件MMU（内存管理单元）

Locker表示这段内存不可使用

RWX表示能读、写、执行

X-only只能执行

![1691054105766](image/RISC-V系统学习/1691054105766.png)

##### 异常和中断

异常：自身的问题，给你一个改过自新的机会

中断：外部的

![1691054568999](image/RISC-V系统学习/1691054568999.png)

# 第三章 编译和链接

##### gcc

- -E：预处理 -> hello.i	cc1
- -S：编译成汇编		cc1
- -c：编译成机器语言		as
- 无参数：链接，链接一些标准库成为最终可执行文件		ld

![1691073312723](image/RISC-V系统学习/1691073312723.png)

![1691073997611](image/RISC-V系统学习/1691073997611.png)

![1691074104045](image/RISC-V系统学习/1691074104045.png)

##### ELF文件格式

![1691074405644](image/RISC-V系统学习/1691074405644.png)

![1691074279668](image/RISC-V系统学习/1691074279668.png)

- ELF Header:文件的基本信息，文件运行在哪个体系架构上的，版本号信息
- Program Header Table：运行视图

  最终程序放入内存中时，会4k对齐，把几个节（Section）放在一起形成段（Segment），比如都是指令的节。
- 一个一个节
- .text：放指令
- .init：初始化指令
- .data：数组，全局变量
- Section Header Table：链接视图，知道有哪些节，有多大，在什么位置

![1691076015849](image/RISC-V系统学习/1691076015849.png)

##### Binutils

![1691076077763](image/RISC-V系统学习/1691076077763.png)

![1691076736930](image/RISC-V系统学习/1691076736930.png)

##### objdump反汇编

要加 -g 调试信息！！

![1691076975455](image/RISC-V系统学习/1691076975455.png)



# 第四章 嵌入式开发



![1691131745673](image/RISC-V系统学习/1691131745673.png)


![1691131883738](image/RISC-V系统学习/1691131883738.png)


##### 交叉编译

- 构建系统
- 主机系统
- 目标系统

本地编译：都在一台机器上

交叉编译：目标系统不是同一台

![1691132020876](image/RISC-V系统学习/1691132020876.png)


1. 用x86_64gcc做一个RISCV64的gcc编译器
2. 让然后用这个编译器编译源代码

![1691132463113](image/RISC-V系统学习/1691132463113.png)



##### GDB

> gdb  a.out

gdb会fork一个子进程跑我们的程序，当进程跑到我们的断点时，gdb会挂起这个进程，此时就可以读寄存器，看相关的值

远程调试时，目标系统会跑一个gdb-server来代理我们的操作。

![1691132831141](image/RISC-V系统学习/1691132831141.png)



![1691133041787](image/RISC-V系统学习/1691133041787.png)





```shell
snow@snow$ riscv64-unknown-elf-gcc -march=rv32ima -mabi=ilp32 hello.c
snow@snow$ gcc hello.c -o a_x86.out
snow@snow$ file a.out
a.out:     ELF 32-bit LSB executable, UCB RISC-V, soft-float ABI, version 1 (SYSV), statically linked, with debug_info, not stripped
snow@snow$ file a_x86.out
a_x86.out: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=e374fe264738f54f3249dae124c2308601f46db3, for GNU/Linux 3.2.0, not stripped
```



![1691140538175](image/RISC-V系统学习/1691140538175.png)





##### MakeFile

![1691156348163](image/RISC-V系统学习/1691156348163.png)



![1691156433714](image/RISC-V系统学习/1691156433714.png)




第五章 汇编语言编程

![1691158572630](image/RISC-V系统学习/1691158572630.png)



![1691158861213](image/RISC-V系统学习/1691158861213.png)



![1691159239603](image/RISC-V系统学习/1691159239603.png)



- label		标志
  ：结尾
- operation	操作
  1. instruction：对应二进制指令
  2. pseudo-instruction：伪指令 ，实际上是多条指令
  3. directive：伪操作， “.”开头，类似自定义函数
  4. macro:   .macro和.endm 的 自定义宏
- comment		注释  #开头

![1691159739525](image/RISC-V系统学习/1691159739525.png)



##### 汇编指令操作对象

![1691161113352](image/RISC-V系统学习/1691161113352.png)

寄存器

1. 可以操作的有32个通用寄存器
2. 执行算数运算、逻辑运算时，只能对寄存器上的数据运算
3. hart是运算的最小单元，也就是一个执行流，以前的cpu一个核只有一个hart

内存

1. hart可以在内存与寄存器之间读写
2. 读写操作时，字节是最小单位，一个字节一个字节寻址，每个字节都有一个地址
3. RV最大可以访问2^32给字节

![1691161278779](image/RISC-V系统学习/1691161278779.png)



![1691162233550](image/RISC-V系统学习/1691162233550.png)



![1691162305051](image/RISC-V系统学习/1691162305051.png)



![1691162446183](image/RISC-V系统学习/1691162446183.png)



##### 小端序

- 主机字节序
- 大端序
- 小端序

![1691162537665](image/RISC-V系统学习/1691162537665.png)



RISC-V是小端序

![1691162761566](image/RISC-V系统学习/1691162761566.png)



![1691163080444](image/RISC-V系统学习/1691163080444.png)

##### 汇编指令分类

![1691163187563](image/RISC-V系统学习/1691163187563.png)



![1691163262986](image/RISC-V系统学习/1691163262986.png)



![1691163422923](image/RISC-V系统学习/1691163422923.png)

a

# 一、什么是设备树
&emsp;&emsp;1、前段时间在 u-boot 移植的时候，接触过设备树，但是当时只知道设备树文件 .dtb 是移植 zImage 文件之外另外一个重要文件，但是具体是什么并不是很了解。

&emsp;&emsp;2、设备树：设备和树。描述设备树的文件叫做 DTS（Device Tree Source），采用树形结构描述板级设备，也就是开发版上的设备信息，比如 CPU 数量、内存基地址、IIC 接口上接了哪些设备等。

&emsp;&emsp;3、在单片机中是将这些设备文件（板级信息）直接写死在 .c 文件中的，若·一些无用、冗余的信息也存放在 Linux 中，会使得 Linux 内核特别“臃肿”，所以将开发版信息（板级信息）做成独立的格式，存放在 .dts 文件中，一个机器或者平台对应一个 .dts。

# 二、DTS、DTB和DTC的关系
&emsp;&emsp;设备树源文件扩展名为 .dts，但是我们在前面移植 Linux 的时候却一直在使 用 .dtb 文件，那么 DTS 和 DTB 这两个文件是什么关系呢？ DTS 是设备树源码文件， DTB 是将 DTS 编译以后得到的二进制文件。将 .c 文件编译为 .o 需要用到 gcc 编译器，那么将 .dts 编译为 .dtb  需要什么工具呢？




**1、加载头文件**
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY4NTQ3MTY3LDE5NjA3MTUzNDgsMTQ0Mj
Q1Mzc0M119
-->
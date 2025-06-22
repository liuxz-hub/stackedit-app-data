# 一、什么是设备树
&emsp;&emsp;1、前段时间在 u-boot 移植的时候，接触过设备树，但是当时只知道设备树文件 .dtb 是移植 zImage 文件之外另外一个重要文件，但是具体是什么并不是很了解。

&emsp;&emsp;2、设备树：设备和树。描述设备树的文件叫做 DTS（Device Tree Source），采用树形结构描述板级设备，也就是开发版上的设备信息，比如 CPU 数量、内存基地址、IIC 接口上接了哪些设备等。

&emsp;&emsp;3、在单片机中是将这些设备文件（板级信息）直接写死在 .c 文件中的，若·一些无用、冗余的信息也存放在 Linux 中，会使得 Linux 内核特别“臃肿”，所以将开发版信息（板级信息）做成独立的格式，存放在 .dts 文件中，一个机器或者平台对应一个 .dts。

# 二、DTS、DTB和DTC的关系
&emsp;&emsp;设备树源文件扩展名为 .dts，但是我们在前面移植 Linux 的时候却一直在使 用 .dtb 文件，那么 DTS 和 DTB 这两个文件是什么关系呢？ DTS 是设备树源码文件， DTB 是将 DTS 编译以后得到的二进制文件。

&emsp;&emsp;形象比喻：  .dts 好比是 .c 文件，.dtb 好比是 .o 文件，DTC 编译工具好比是  gcc 编译器。

&emsp;&emsp;命令： 
`make all`命令是编译 Linux 源码中的所有东西，包括 zImage， .ko 驱动模块以及设备树；
 `make dtbs` 命令是编译设备树。

# 三、DTS 基本语法
1、设备树也有头文件，扩展名为 `.dtsi`。可以将一款 SOC 他的其他所有设备/平台的共有的信息提出来，作为一个通用的 `.dtsi `文件。

1、DTS 也是从 `/` 开始

2、从`/` 根节点开始描述设备信息

3、在`/`根节点外有一些 `& cpu0` 这样的语句是"追加"，其中`&`后面跟的是节点名字对应的标签`Lable`。

4、节点名字，完整的要求：`node-name@unit-address`，有时候在节点名字前面还会出现标签 `Lable : Node-name @ Unit-address`。

一般都是外设寄存器的起始地址，例如：`i2c4:i2c@021f8000`、`uart6:serial@021fc000` 等；
有时候是 I2C 的设备地址，例如：`mag3110@0e` 、`fxls8471@1ed` 等，或者其他含义，具体节点具体分析。
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTI5MDA4NDQ2LC03MDY1NTU0OTAsMjA2MT
k1MDgzMiw5MzIwNzExOTAsMTY4NTQ3MTY3LDE5NjA3MTUzNDgs
MTQ0MjQ1Mzc0M119
-->
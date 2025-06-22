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
&emsp;&emsp;1、设备树也有头文件，扩展名为 `.dtsi`。可以将一款 SOC 他的其他所有设备/平台的共有的信息提出来，作为一个通用的 `.dtsi `文件。

&emsp;&emsp;2、DTS 也是从 `/` 开始；

&emsp;&emsp;从`/` 根节点开始描述设备信息；

&emsp;&emsp;在`/`根节点外有一些 `& cpu0` 这样的语句是"（覆盖性）追加"，其中`&`后面跟的是节点名字对应的标签`Lable`。

&emsp;&emsp;3、节点名字，完整的要求：`node-name@unit-address`，有时候在节点名字前面还会出现标签 `Lable : Node-name @ Unit-address`。

&emsp;&emsp;一般都是外设寄存器的起始地址，例如：`i2c4:i2c@021f8000`、`uart6:serial@021fc000` 等；
&emsp;&emsp;有时候是 I2C 的设备地址，例如：`mag3110@0e` 、`fxls8471@1ed` 等，或者其他含义，具体节点具体分析。

# 四、设备树在系统中的体现
&emsp;&emsp;系统启动以后可以在根文件系统里面看到设备树的节点信息。在`/proc/device-tree/`目下存放着设备树信息。

&emsp;&emsp;内核启动的时候会解析设备树，然后在`/proc/device-tree/`目录下呈现出来。

# 五、特殊节点
&emsp;&emsp;在根节点`/`中有两个特殊的子节点： `aliases` 和 `chosen`，我们接下来看一下这两个特殊的 子节点。 

**1. aliases 子节点**
&emsp;&emsp;单词 aliases 的意思是“别名”，因此 `aliases` 节点的主要功能就是定义别名，定义别名的目的就是了方便访问节点。不过我们一般会在节点命名的时候会加上 `label`，然后通过 `&label` 来访问节点，这样也很方便，而且设备树里面大量的使用 `&label` 的形式来访问节点。

**2. chossen子节点**
&emsp;&emsp;`chosen` 节点主要是为了 `uboot` 向 `Linux` 内核传递数据，重点是 `bootargs` 参数。

&emsp;&emsp;那么 `uboot` 是如何向 `Linux` 内核传递 `bootargs` ？经过查看发现 `chosen` 节点包含 `bootargs` 属性，属性值和  `uboot` 中设置的`bootargs`  一致。最终发现在 `uboot` 中 `bootz` 深层调用的函数 `fch_chosen` 中查找 `chosen` 节点，并且在里面添加 `bootargs` 属性，属性值为`bootargs`变量值。

# 六、特殊的属性
**1.compatible 属性 **
&emsp;&emsp;compatible 属性也叫做“兼容性”属性，这是非常重要的一个属性！ compatible 属性的值是一个字符串列表， compatible 属性用于将设备和驱动**绑定**起来。字符串列表用于选择设备所要使用的驱动程序
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc3NjgwMzQxNiwtMTYzNzg3OTE5MywtMT
I2MjkxMDMxMywxOTg5Mzk5NjM0LC05ODA3MjEyMDAsMTUyNTQ0
NTM5MiwxMzEyNjUxNzY4LC0xMjg5OTcyMzQyLC03MDY1NTU0OT
AsMjA2MTk1MDgzMiw5MzIwNzExOTAsMTY4NTQ3MTY3LDE5NjA3
MTUzNDgsMTQ0MjQ1Mzc0M119
-->
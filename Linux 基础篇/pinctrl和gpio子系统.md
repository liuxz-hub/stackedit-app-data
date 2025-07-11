

# 一、pinctrl 子系统

借助 pinctrl 来设置一个 PIN 的复用和电气属性。
打开 imx6ull.dtsi:

## 1.1、IOMUXC SNVS 控制器
```
iomuxc snvs: iomuxc-snvs@02290000 {
	compatible ="fsl,imx6ull-iomuxc-snvs";
	reg = <0x02290000 0x10000>:
};
```
## 1.2、IOMUXC  控制器
```
iomuxc: iomuxc@020e0000 {
	compatible =“fsl,imx6ul-iomuxc";
	reg =<0x020e0000 0x4000>:
};
```
## 1.3、GPR  控制器
```
gpr: iomuxc-gpr@020e4000 {
	compatible = "fsl,imx6ul-iomuxc-gpr","fsl,imx6q-iomuxc-gpr", "syscon";	
	reg = <0x020e4000 0x4000>:
};
```
## 1.4、如何添加一个 pin 信息
```
pinctrl_hog_1: hoggrp-1 {
	fsl,pins = 
		MX6UL PAD UART1 RTS B GPIO1 I0190x17059 /* SD1 CD */
	>;
};
```
我们在 `imx6ul-pinfunc.h` 中找到:
| mux_reg | conf_reg | input_reg | mux_mode  | input_val |
|---------|----------|-----------|-----------|-----------|
| `0x0090`  | `0x031C`  |`0x0000` | `0x5` | `0x0` |
 
`IOMUXC` 父节点首地址` 0x020e0000`，因此 `UART1_RTS_B` 这个 PIN 的 mux 寄存器地址就是：`0x020e 0000+0x0090=0x020e 0090`。

`conf_reg`：`0x020e 0000+0x031C=0x020e 031C`，这个寄存器就是 `UART1_RTS_B` 的电气属性配置寄存器。

`input_reg` ：表示偏移为 0，表示 `UART1_RTS_B`这个 PIN 没有 input 功能。

`mux_mode`：5 表示复用为 `GPIO1-I019`，将其写入 `0x020e 0090`。

`input_val`：就是写入 `input_reg` 寄存器的值。

`0x17059` ：为PIN 的电器属性配置寄存器的值。

## 1.5、pinctrl 驱动
&emsp;&emsp;如何找到 `IMX6ULL` 对应的 `pinctrl` 子系统驱动，设备树里面的设备节点是如何跟 驱动匹配 的呢?
&emsp;&emsp;通过 `compatible`跟驱动匹配，此属性是一个字符串列表。驱动文件里面有一个描述驱动兼容性的内容，当设备树节点的 `compatible` 属性和驱动里面的 兼容性字符串 匹配，这时也就表示设备和驱动匹配上了。

所以我们只需要全局搜索，设备节点里面的 `compatible` 属性的值，看看在哪个 `.c` 文件里面有，那么此 `.c` 文件就是驱动文件。找到 `pinctrl-imx6u.c` 文件，那么此文件就是 `6UL/6ULL`的 `pinctr` 驱动文件。


# 二、gpio 子系统

借助 pinctrl 来设置一个 PIN 的复用和电气属性。
打开 imx6ull.dtsi:

## 1.1、IOMUXC SNVS 控制器
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMyODg0NDI2N119
-->
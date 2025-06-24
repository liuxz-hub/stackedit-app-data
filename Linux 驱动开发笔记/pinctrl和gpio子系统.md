

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

`MX6UL PAD UART1 RTS B GPIO1 IO19`       &emsp;&emsp;&emsp;&emsp;      `0x0090 0x031C 0x0000 0x5 0x0`

 `<mux_reg     conf_reg   input_reg    mux_mode   input_val>`
 `0x0090` &emsp; `0x031C` &emsp; `0x0000`&emsp;&emsp;&emsp;` 0x5  `&emsp;&emsp;&emsp; `   0x0`
 
`IOMUXC` 父节点首地址` 0x020e0000`，因此 `UART1_RTS_B` 这个 PIN 的 mux 寄存器地址就是：`0x020e0000+0x0090=0x020e0090`。

`conf_reg`：`0x020e0000+0x031C=0x020e 031C`，这个寄存器就是 `UART1_RTS_B` 的电气属性配置寄存器。

`input_reg` ：表示偏移为 0，表示 `UART1_RTS_B`这个 PIN 没有 input 功能。

`mux_mode`：5 表示复用为 `GPIO1-I019`，将其写入 `0x020e 0090`。

`input_val`：就是写入 `input_reg` 寄存器的值。

`0x17059` ：为PIN 的电器属性配置寄存器的值。

## 1.5、pinctrl 驱动

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5Mzc2MDA3Niw4OTY4MDIyOTIsLTgxNz
YyNzYwN119
-->
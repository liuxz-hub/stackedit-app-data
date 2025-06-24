

# 一、pinctrl 子系统

借助 pinctrl 来设置一个 PIN 的复用和电气属性。
打开 imx6ull.dtsi:
## 1
```
iomuxc snvs: iomuxc-snvs@02290000 {
	compatible ="fsl,imx6ull-iomuxc-snvs";
	reg = <0x02290000 0x10000>:
};
```

```
iomuxc: iomuxc@020e0000 {
	compatible =“fsl,imx6ul-iomuxc";
	reg =<0x020e0000 0x4000>:
};
```
```
gpr: iomuxc-gpr@020e4000 {
	compatible = "fsl,imx6ul-iomuxc-gpr","fsl,imx6q-iomuxc-gpr", "syscon";	
	reg = <0x020e4000 0x4000>:
};
```
4
gpr: iomuxc-gpr@020e4000 {~compatible = "fsl,imx6ul-iomuxc-gpr","fsl,imx6q-iomuxc-gpr", "syscon";<reg = <0x020e4000 0x4000>:←
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM3Njk2MzQ3NV19
-->
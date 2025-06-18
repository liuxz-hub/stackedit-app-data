· 问题描述：
&emsp;&emsp;昨天在开发板上还进行了驱动开发实验，今天通过 U-BOOT 系统下载失败，无法进入到 Linux 内核，即在 TFTP 打不开 zImage 和 dtb 文件。

· 问题解决：
&emsp;&emsp;1、首先检查开发版的网络地址是否多设备冲突
&emsp;&emsp;关闭开发版，在 ubuntu 上进行 ping 该网址，若 ping 不通则证明它是唯一的

&emsp;&emsp;2、检查 ubuntu  的网络地址是否多设备冲突
&emsp;&emsp;关闭 ubuntu ，在 Windows 下进行 ping 该网址，若 ping 不通则证明它是唯一的

&emsp;&emsp;3、
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMyNzkwNDQwMCwxMjQ2OTI5NDI4XX0=
-->
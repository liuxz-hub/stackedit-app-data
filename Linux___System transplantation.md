#	U-BOOT 移植
U-Boot 移植是指将 U-Boot（Universal Bootloader）修改、裁剪和适配到你的特定硬件平台（如某款嵌入式开发板、SoC 或定制硬件板）上，使它能够成功启动并加载 Linux 内核或者其他操作系统。
## 目的
目的是在目标硬件上成功启动（跑起来！），简言之：让你的板子“能启动 + 可用 + 可调”。
1、正确初始化关键硬件资源（CPU、内存、存储）；
2、能够加载内核镜像并传递启动参数；
3、提供一个用户交互接口（串口、USB等）；
4、支持后续维护、调试、固件升级。

## 主要工作
 移植CPU启动代码处理低级初始化代码（汇编 startup.S / crt0.S）
1、配置CPU相关寄存器、缓存、MMU/TLB，初始化内存（RAM）
2、配置 DDR 控制器，初始化 SDRAM
3、验证内存是否可正常使用
4、配置串口（UART）
5、确保串口调试信息能打印出来（第一条 "Hello U-Boot!" 很关6、配置 网络支持（如 Ethernet PHY）：用于通过 TFTP 等方式加载镜像，方便开发
7、配置 USB 支持（如USB OTG/Host）


# Linux 内核移植






# 根文件系统移植

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0OTk1NzA5NDIsLTIwNzg2NDM3ODhdfQ
==
-->
# 一、地址映射（MMU 的功能之一）
裸机 LED 灯实验就是操作 6ULL 的寄存器。Linux 驱动开发下，为了方便验证也可以操作寄存器，与裸机区别是不能对寄存器的物理地址直接操作，因为Linux 会使能 MMU ；

1、虚拟地址：对于 32 位的处理器，虚拟地址范围是 2^32=4GB；

2、物理地址：开发版有 512MB 的 DDR3，这 512MB 的内存就是物理地址；

3、经过 MMU 可以将 512MB 的物理内存映射到 4GB 的虚拟空间上，所以这也是为什么在Linux 驱动开发下不能对寄存器的物理地址直接操作的原因。




# 二、LED 设备驱动框架
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjc5ODgxMjYsMTA4ODU0MjQ0NCwtNjc3Nj
c5NjM5LC0xNTMwNjI4MzExXX0=
-->
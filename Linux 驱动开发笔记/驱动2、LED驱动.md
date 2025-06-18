# 一、地址映射（MMU 的功能之一）
裸机 LED 灯实验就是操作 6ULL 的寄存器。Linux 驱动开发下，为了方便验证也可以操作寄存器，与裸机区别是不能对寄存器的物理地址直接操作，因为Linux 会使能 MMU ；

1、虚拟地址：对于 32 位的处理器，虚拟地址范围


# 二、LED 设备驱动框架
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ5MTQ5NTk4MCwtNjc3Njc5NjM5LC0xNT
MwNjI4MzExXX0=
-->
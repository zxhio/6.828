## 环境

实现机器为VMWare的虚拟机，操作系统为 Debian-11(无桌面版本)，内核版本为 5.10.0，指令集为 AMD64(i7 9700K)，编译器为 GCC-10.

### 代码

Lab 的代码克隆自 *https://pdos.csail.mit.edu/6.828/2018/jos.git* 

### QEMU 虚拟化支持
理论上只需要 qemu 提供软件虚拟化即可，所以硬件虚拟化非必要，libvirt 等相关组件也可以不需要；这里只安装 QEMU：*apt install qemu-kvm*

### Lab 相关变动
安装 Lab1 的流程，执行 `make && make qemu` 之后会有报错，由于装的操作系统无桌面，gtk 也就没有安装。
```txt
# qemu-system-i386 -drive file=obj/kern/kernel.img,index=0,media=disk,format=raw -serial mon:stdio -gdb tcp::25000 -D qemu.log
Unable to init server: Could not connect: Connection refused
gtk initialization failed
```
非图形版本修改如下：
```diff
-QEMUOPTS = -drive file=$(OBJDIR)/kern/kernel.img,index=0,media=disk,format=raw -serial mon:stdio -gdb tcp::$(GDBPORT)
+QEMUOPTS = -drive file=$(OBJDIR)/kern/kernel.img,index=0,media=disk,format=raw -nographic -gdb tcp::$(GDBPORT)
```

解释一下 qemu 的这条命令 *qemu-system-i386 -drive file=obj/kern/kernel.img,index=0,media=disk,format=raw -nographic -gdb tcp::25000 -D qemu.log*
- drive 指定驱动类型
- format=raw 文件格式，其他的如有 qcow2
- nographic 无图形页面
- gdb 接受 gdb 的远程连接，后续 *make gdb* 调试会使用到这个点

*make qemu-gdb* 和 *make qemu* 多了一个参数 `-S`，作用为 freeze CPU at startup。


### Lab 相关说明

- [Lab1](./doc/lab1.md)
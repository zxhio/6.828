# mit 6.828

## 准备工作

环境为 **fedora37** 虚拟机，内核版本为 **6.0.7-301.fc37.x86_64**.

安装 qemu
```shell
yum install qemu-kvm -y
```

修复 make 报错，在 *kern/Makefrag* 中添加 **-Wno-error**
```shell
[root@localhost 6.828]# make
+ as kern/entry.S
kern/entry.S: error: STABS debugging information is obsolete and not supported anymore [-Werror]

# kern/Makefrag:11
KERN_CFLAGS += -Wno-error
```

退出 qemu 使用 `ctrl+a x`

## LAB1

---
layout: doc
title: 杂谈
editLink: true
footer: true
lastUpdated: true
outline: [2, 4]
---


## 下载riscv64-unknown-elf-gnu

### 1. 从riscv-gnu-toolchain里安装

使用`riscv-gnu-toolchain`自动安装`riscv64-unknown-elf-gnu`的时候，会自动获取其子模块
由于其子模块的链接都在github，下载过程太慢
虽然可以使用更换其子模块url链接的方式来换成gitee仓库源的，不过在使用`gitee极速加速`的仓库加速时, 发现有一些仓库没有被收录，另外有一些仓库虽然被收录，不过仓库源对应不上。
以下是我自己尝试更新github的submodule，还没有成功,这个方法无疑是最耗时的

``` shell
[submodule "binutils"]
	path = binutils
#	url = https://sourceware.org/git/binutils-gdb.git
	url = https://gitee.com/mirrors/riscv-binutils-gdb.git
	branch = binutils-2_43-branch
	shallow = true
[submodule "gcc"]
	path = gcc
#	url = https://gcc.gnu.org/git/gcc.git
	url = https://gitee.com/mirrors/gcc.git
	branch = releases/gcc-14
	shallow = true
[submodule "glibc"]
	path = glibc
	url = https://gitee.com/mirrors/riscv-glibc.git
#	url = https://sourceware.org/git/glibc.git
	shallow = true
[submodule "dejagnu"]
	path = dejagnu
	url = https://gitee.com/mirrors/riscv-dejagnu.git
#	url = https://git.savannah.gnu.org/git/dejagnu.git
	branch = master
	shallow = true
[submodule "newlib"]
	path = newlib
	url = https://gitee.com/mirrors/newlib-cygwin.git
	#url = https://sourceware.org/git/newlib-cygwin.git
	branch = master
	shallow = true
[submodule "gdb"]
	path = gdb
	url = https://gitee.com/mirrors/riscv-binutils-gdb.git
	#url = https://sourceware.org/git/binutils-gdb.git
	branch = gdb-15-branch
	shallow = true
[submodule "qemu"]
	path = qemu
	url = https://gitee.com/mirrors/qemu.git
#	url = https://gitlab.com/qemu-project/qemu.git
	shallow = true
[submodule "musl"]
	path = musl
	url = https://gitee.com/mirrors/musl.git
#	url = https://git.musl-libc.org/git/musl
	branch = master
	shallow = true
[submodule "spike"]
	path = spike
	url = https://gitee.com/mirrors/riscv-isa-sim.git
#	url = https://github.com/riscv-software-src/riscv-isa-sim.git
	branch = master
	shallow = true
[submodule "pk"]
	path = pk
	url = https://github.com/riscv-software-src/riscv-pk.git
	branch = master
	shallow = true
[submodule "llvm"]
	path = llvm
	url = https://gitee.com/mirrors/llvm-project.git
	#url = https://github.com/llvm/llvm-project.git
	branch = release/19.x
	shallow = true
[submodule "uclibc-ng"]
	path = uclibc-ng
	url = https://github.com/wbx-github/uclibc-ng.git
	shallow = true

```

### 2. 直接使用`riscv-gnu-toolchain`组织编译好的源码
这个方法省事省力

### 3. riscv64-unknown-elf-gcc安装位置
一般把它安装到`/opt/riscv`目录下面，同时设置环境变量`RISCV=/opt/riscv`。


### 4. riscv64-linux-gnu-gcc vs riscv64-unknown-elf-gcc

编译一生一芯相关东西需要用`riscv64-linux-gnu-gcc(apt安装)`
编译其他RISCV程序需要使用`riscv64-unknown-elf-gcc`





### opt/riscv, opt/riscv/bin

### --prefix
--prefinx=/opt/riscv表示被安装到/opt/riscv/bin里面



## spike
### 1. 编译spike的时候需要使用`riscv64-unknown-elf-gcc`, 

### 2. 编译spike的脚本文件
编译spike的时候，通常在`spike`目录新建一个build目录盛放编译后的内容,这个脚本应该在`spike目录里面`
在编译好`spike`后，如果再执行`make install`，spike会被安装到`/opt/riscv/bin/`里面
如果使用`spike`的时候，需要能够找到spike

``` bash
#!/bin/bash

# 判断是否有build目录
if [ ! -d "build" ]; then
    # 如果没有build目录，执行以下操作
    mkdir build
    cd build
    ../configure --prefix=$RISCV #这个表示spike将会
    cd ..
fi

# 进入build目录并执行编译和安装
cd build
make
# 使用echo和管道来自动输入sudo密码
echo "SUDO PASSWORD" | sudo -S make install
```

### 在修改spike源码时，使用ccache编译加速

1. 首先修改`PATH`, 将ccache的路径加到最前面
``` shell
export PATH=/usr/lib/ccache:/opt/riscv/bin:$PATH
```

2. 如果需要使用ccache加速编译`riscv64-unknown-elf-gcc`，那么需要在`usr/lib/ccache`目录下面加上`riscv64-unknown-elf-gcc`的符号链接

``` shell
akun@akun:/usr/lib/ccache$ ll
total 8
drwxr-xr-x   2 root root 4096  3月 12 13:01 ./
drwxr-xr-x 121 root root 4096  3月 12 12:55 ../
lrwxrwxrwx   1 root root   16  3月 12 12:55 c++ -> ../../bin/ccache*
lrwxrwxrwx   1 root root   16  3月 12 12:55 c89-gcc -> ../../bin/ccache*
lrwxrwxrwx   1 root root   16  3月 12 12:55 c99-gcc -> ../../bin/ccache*
lrwxrwxrwx   1 root root   16  3月 12 12:55 cc -> ../../bin/ccache*
lrwxrwxrwx   1 root root   16  3月 12 12:55 g++ -> ../../bin/ccache*
lrwxrwxrwx   1 root root   16  3月 12 12:55 g++-11 -> ../../bin/ccache*
lrwxrwxrwx   1 root root   16  3月 12 12:55 gcc -> ../../bin/ccache*
lrwxrwxrwx   1 root root   16  3月 12 12:55 gcc-11 -> ../../bin/ccache*
lrwxrwxrwx   1 root root   16  3月 12 12:55 riscv64-linux-gnu-g++ -> ../../bin/ccache*
lrwxrwxrwx   1 root root   16  3月 12 12:55 riscv64-linux-gnu-g++-11 -> ../../bin/ccache*
lrwxrwxrwx   1 root root   16  3月 12 12:55 riscv64-linux-gnu-gcc -> ../../bin/ccache*
lrwxrwxrwx   1 root root   16  3月 12 12:55 riscv64-linux-gnu-gcc-11 -> ../../bin/ccache*
lrwxrwxrwx   1 root root   15  3月 12 13:01 riscv64-unknown-elf-g++ -> /usr/bin/ccache*
lrwxrwxrwx   1 root root   15  3月 12 13:01 riscv64-unknown-elf-gcc -> /usr/bin/ccache*
lrwxrwxrwx   1 root root   16  3月 12 12:55 x86_64-linux-gnu-g++ -> ../../bin/ccache*
lrwxrwxrwx   1 root root   16  3月 12 12:55 x86_64-linux-gnu-g++-11 -> ../../bin/ccache*
lrwxrwxrwx   1 root root   16  3月 12 12:55 x86_64-linux-gnu-gcc -> ../../bin/ccache*
lrwxrwxrwx   1 root root   16  3月 12 12:55 x86_64-linux-gnu-gcc-11 -> ../../bin/ccache*
```


## 编译加速

### 1. make多线程编译
```
alias make="make -j $(nproc)"
```
### 2. ccahe编译缓存




## 对于difftest的思考

## Digital-IDE快速实例化


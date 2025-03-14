



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


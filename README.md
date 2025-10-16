# -
这篇对高手无用，仅仅是为了帮助新手克服困难而写

一个学习程度为仅仅安装ubunt 虚拟机操作系统的，目的编译内核，要关注的提前设置（环境各个不同，我的问题全在此，应该能提供帮助）

如果最后的时候编译出现了Kernel: arch/x86/boot/bzImage is ready (#版本号)，就代表成功了


一开始通过看blbl的编译tvm和内核编译，由于视频只单纯的提供了关键命令，但其他的必要的命令没有显示出来由此补充
{
wget https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-6.14.tar.xz
tar xvf linux-6.14.tar.xz
cd linux-6.14
make menuconfig
make -j$(nproc)
} 
这是视频里的主要步骤

但是如果不提前下好需要的库文件，是会一直报错的
sudo apt install -y \
    build-essential \
    libncurses-dev \ 
    libssl-dev \
    libelf-dev \
    bc \
    flex \
    bison \
    dwarves \
    zstd \
    gawk \
    git \
    rsync \
    kmod \
    cpio

如果不下这个，是经常的在make -j几报错，和menuconfig报错，因为有个文件是menuconfig的必需品，没有这个menuconfig运行不了

假设看我这个的人已经下好了源码
cd 源码文件夹里面
然后cp 自己文件系统的config 挪到当前位置，（作用是：就是直接用现在的配置方法来配置新内核）
make -j$(nproc)

编译内核的时候，虚拟机分配资源最好大点内存和多点核心，必须的是要硬盘资源足够，不然不仅编译报错，而且由于硬盘占满，重启时连图形化界面都进不去，要使用如下步骤（建议100G）
按 Ctrl + Alt + F2（或 F3-F6）切换到终端界面登录。 （但注意，如果不仔细看，一开始不是可以直接输入，用翻译软件看是选择账户登录，需要输入用户名和密码）
df -h
sudo growpart /dev/sda 1
sudo resize2fs /dev/sda1
df -h
此时建议仔细读一下命令作用

其实操作挺简单，就是被一些东西卡住了，只需要把这些文件下好，然后make -j多少  就可以了
反正make 时候出错大概是文件没有下全，建议复制代码给ai让ai读一下，然后ai给你要做的命令

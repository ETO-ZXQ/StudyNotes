# Linux

> Linux的设计哲学是“一切皆文件”。它将所有的IO设备如网络接口、usb接口、显示屏、相机、键盘、鼠标、应用都视为文件，和这些“文件”的交互就是以规定的方式进行读写。

## 动态链接库

### 共享库配置文件 `/etc/ld.so.conf`

`/etc/ld.so.conf` 此文件记录了编译时使用的动态库的路径，也就是加载so库的路径。

默认情况下，编译器只会使用/lib和/usr/lib这两个目录下的库文件，而通常通过源码包进行安装时，如果不指定--prefix，会将库安装在/usr/local目录下，而又没有在文件/etc/ld.so.conf中添加/usr/local/lib这个目录。这样虽然安装了源码包，但是使用时仍然找不到相关的.so库，就会报错。也就是说系统不知道安装了源码包。

#### 检查共享库配置文件

```Bash
cat /etc/ld.so.conf
```

#### 添加路径

```Bash
sudo sh -c "echo '/usr/local/lib' >> /etc/ld.so.conf"
```

#### 手动重新加载共享库缓存

```Bash
sudo ldconfig
```

1. 在首次配置共享库或更改共享库路径后：如果添加或修改了共享库配置文件（/etc/ld.so.conf）中的路径，则需要手动运行 sudo ldconfig 以重新加载共享库缓存。

2. 安装了新的共享库：如果在系统中安装了新的共享库文件（例如通过软件包管理器或手动安装），则需要运行 sudo ldconfig 以使系统能够识别和使用这些新的共享库。

### 打印程序或者库文件所依赖的共享库列表

ldd：list dynamic dependencies

```Bash
Usage: ldd [OPTION]... FILE...
      --help              print this help and exit
      --version           print version information and exit
  -d, --data-relocs       process data relocations
  -r, --function-relocs   process data and function relocations
  -u, --unused            print unused direct dependencies
  -v, --verbose           print all information
```

## 软链接（Symbolic Link）

> 类似于Windows的快捷方式

### 创建

`ln -s 被链接对象 链接放置路径/文件名（文件夹名）`

**例如：**

```Linux
ln -s /home/zxq/Downloads/ /home/zxq/Desktop/下载

将Downloads文件夹链接到Desktop文件夹下取名下载
```

### 注意

1. 一定要用绝对路径
2. 文件和文件夹均可创建软链接

## udev 规则

- [在 Linux 中如何编写基本的 udev 规则 - 知乎](https://zhuanlan.zhihu.com/p/33932734)
- [LINUX下 Udev详解 - 知乎](https://zhuanlan.zhihu.com/p/373517974)

## 符号

`/usr` Unix system resources

`/etc` 在Linux系统中，"etc"文件夹的名称来自于英文单词"et cetera"（缩写为"etc"），意思是"以及其他"。这个文件夹被用于存放各种系统配置文件，如网络配置、服务配置、软件配置等。命名为"etc"主要是为了说明该文件夹中包含了许多其他的配置文件，而不仅仅是一些特定的文件。

`.cc` 为(linux/unix)C++文件后缀，vs vim emacs都可以打开。

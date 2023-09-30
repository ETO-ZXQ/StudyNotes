# Linux

> Linux的设计哲学是“一切皆文件”。它将所有的IO设备如网络接口、usb接口、显示屏、相机、键盘
鼠标、应用都视为文件，和这些“文件”的交互就是以规定的方式进行读写。

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

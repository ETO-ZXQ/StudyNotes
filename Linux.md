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

## 文件夹

`/usr` Unix system resources
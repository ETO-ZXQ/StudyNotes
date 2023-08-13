# Python

> 一切皆对象

## Python 模块

- [Python3 模块 | 菜鸟教程](https://www.runoob.com/python3/python3-module.html)
- [详解Python中模块(Module)和包(package)的概念和用法 - 知乎](https://zhuanlan.zhihu.com/p/70556072)
- **[python模块详解 - 知乎](https://zhuanlan.zhihu.com/p/33913131)**

> 概念

- 模块(module)：其实就是`.py`文件，里面定义了一些函数、类、变量等
- 包(package)：是多个模块的聚合体形成的文件夹，里面可以是多个py文件，也可以嵌套文件夹
- 库：是参考其他编程语言的说法，是指完成一定功能的代码集合，在python中的形式就是模块和包

> `from package import item`

对应的 `item` 既可以是包里面的子模块（子包），或者包里面定义的其他名称，比如函数，类或者变量。

import 语法会首先把 item 当作一个包定义的名称，如果没找到，再试图按照一个模块去导入。如果还没找到，抛出一个 :exc:ImportError 异常。

> `import item.subitem.subsubitem`

这种导入形式，除了最后一项，都必须是包，而最后一项则可以是模块或者是包，但是不可以是类，函数或者变量的名字。

## Python 调用动态链接库（.dll .so）

*由ChatGPT v4.0(2K)问答整理*

> 根据.so文件编写和构建的不同，需要使用不同的方式调用。

### 第一种、import直接导入

#### 概念

建立在Python C API基础上的.so文件可以直接用import语句引入，因为它们在创建时是用Python的C接口构建的，Python可以理解和调用它们。这类.so文件经常被称为Python的C扩展模块。Python的许多内置模块就是.so文件。

#### 处理流程

`from Error import ObException`

1. Python 首先会在当前目录和 PYTHONPATH 环境变量所指定的路径中查找名为 "Error.py" 或 "Error/init.py" 或 "Error.so"的文件。在此处，Python 会找到名为 "Error.cpython-39-x86_64-linux-gnu.so" 的文件。这个文件名表示这个 .so 文件是为运行在 x86_64 linux 平台上的 CPython 3.9 编译的。

2. 一旦找到了相应的 .so 文件，Python 会加载这个文件。加载的过程是将这个 .so 文件中的代码载入到内存，在这个过程中，其中定义的所有功能都会变得可用，包括你所导入的 ObException。

3. 可以在 Python 代码中像使用 Python 模块一样使用这个 .so 文件中提供的功能。

### 第二种、使用ctypes或cffi库调用

#### 概念

对于并非特定为Python环境建立，或者说是用标准C或C++无关Python编写的.so文件，直接import语句是不行的，此时就需要利用Python的ctypes库或者cffi库。这些库提供了一个桥梁，让Python能够调用C或C++编写的函数库。

#### 示例

```Python
from ctypes import cdll

# 加载动态链接库
lib = cdll.LoadLibrary('your_library.so')

# 现在你可以调用库中的函数。假设有个名为 'foo' 的函数可以这样调用：
result = lib.foo(args)
```

## Python dir() 与 help() 函数

### `dir([object])`

`dir()` 是一个内置函数，用于列出对象的所有属性及方法。

1. 如果 `dir()` 没有参数，则返回当前作用域中的名称列表；否则，返回给定 `object` 的一个已排序（按字母排序）的属性名称列表。
2. 如果对象提供了 `__dir__()` 方法，则它将会被使用；否则，使用默认的 `dir()` 逻辑，并返回。

### `help([object])`

`help()` 函数用于查看函数或模块用途的详细说明。

1. 如果未给出参数，则交互帮助系统将在解释器控制台上启动。
2. 如果参数是字符串，则该字符串将作为模块、函数、类、方法、关键字或文档主题的名称查找，并在控制台上打印帮助页。
3. 如果参数是任何其他类型的对象，则会生成该对象的帮助页。

```Python
>>>help('sys')             # 查看 sys 模块的帮助
……显示帮助信息……
 
>>>help('str')             # 查看 str 数据类型的帮助
……显示帮助信息……
 
>>>a = [1,2,3]
>>>help(a)                 # 查看列表 list 帮助信息
……显示帮助信息……
 
>>>help(a.append)          # 显示list的append方法的帮助
……显示帮助信息……
```

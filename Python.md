# Python

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

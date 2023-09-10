# Python爬虫学习笔记

---

## UA伪装

---

### UA

+ User-Agent（请求载体的身份信息）

### UA检测

+ 门户网站的服务器会检测对应请求载体的身份标识（UA），如果检测到UA为某一款浏览器，说明该请求是一个正常请求，但是，如果UA不是基于某款浏览器的，则表示该请求为不正常请求（爬虫），则服务器就很可能拒绝该次请求。

### UA伪装

+ 让爬虫对应的UA伪装成某一款浏览器。

---

## 聚焦爬虫

---

*爬取页面中指定的页面内容*

### 编码流程

1. 指定url
2. 发起请求
3. 获取响应数据
4. 数据解析
5. 持久化存储

---

## 数据解析

---

### 分类

+ 正则
+ bs4
+ xpath (***)

### 原理概述

+ 解析的局部的文本内容都会在标签之间或者标签对应的属性中进行存储
+ 1.进行指定标签的定位
+ 2.标签或者标签对应的属性中存储的数据值进行提取（解析）

### bs4

> pip install bs4<br>
> pip install lxml<br>

1. 实例化一个BeautifulSoup对象，并且将页面源码加载到该对象中<br>
`from bs4 import BeautifulSoup`
    + 第一种：将本地的HTML文档中的数据加载到该对象中<br>
    ```python
        fp = open('./XXX.html', 'r', encoding='utf-8')
        soup = BeautifulSoup(fp, 'lxml')
    ```
    + 第二种：将互联网上获取的页面源码加载到该对象中<br>
   ```python
        page_text = response.text
        soup = BeautifulSoup(page_text, 'lxml')
   ```
2. 通过调用BeautifulSoup对象中相关属性或者方法进行标签定位和数据提取<br>
   + `soup.tagName`返回对象中第一次出现的tagName对应的标签
   + `soup.find()`
      1. `soup.find('tagName')` = `soup.tagName`
      2. 属性定位：`soup.find('tagName', class_/id/attr='XXX')`
   + `soup.find_all('tagName')`返回符合要求的所有标签（列表）
   + `soup.select()`
      1. `soup.select('某种选择器（id，class，标签...选择器）')` 返回列表
      2. 层级选择器：
         1. `soup.select('.tang > ul > li > a')` '>'表示的是一个层级
         2. `soup.select('.tang > ul a')` 空格表示多个层级
   + 获取标签之间的文本数据 `XXX.text/string/get_text()`
      1. `.text/get_text()` 可以获取一个标签中所有的文本内容
      2. `.string` 只可以获取该标签下直系的文本内容
   + 获取标签中属性值 `XXX['属性']`

### xpath

*最常用 最高效*

+ 解析原理
  1. 实例化一个etree对象，并将数据加载到该对象中
  2. 调用etree对象中的xpath方法结合xpath表达式实现数据解析
+ 环境安装 `pip install lxml`
+ 实例化etree对象
    ```python
    from lxml import etree
    * python3.5之后的 lxml 模块中不能再直接引入etree模块 *
    from lxml import html
    etree = html.etree
    ```
    1. 本地html文档 `etree.parse(filePath)`
    2. 互联网响应数据 `etree.HTML('page_text)`
+ xpath表达式 `XXX.xpath('xpath表达式')`
    1. `/` 分隔相邻层级，在开头表示从根节点开始定位
    2. `//` 分隔多个层级，表示中间空一个或多个未知层级
    3. 属性定位：//div[@class="song"] `tag[@attrName="attrValue"]`
    4. 索引定位：//div[@class="song"]/p[3] 索引从1开始
    5. 取文本：
        1. `/text()` 获取标签中直系文本内容
        2. `//text()` 获取标签中所有非直系文本内容
    6. 取属性：`/@attrName` 例：img/@src
    7. 解析xpath表达式后，再次继续解析，xpath表达式在最前面加`./`
    8. 可以使用逻辑运算符 `|`或

---

## cookie

---

*用来让服务器端记录客户端的相关状态*

+ cookie值来源：模拟登陆post请求后，由服务器创建
+ session会话对象的作用：
    1. 可以进行请求的发送
    2. 如果请求过程中产生了cookie，则该cookie会被自动储存/携带在该session对象中
+ 自动处理
    1. 创建一个session对象：`session = request.Session()`
    2. 使用session对象进行模拟登陆post请求进行发送（cookie会自动储存在session中）
    3. 使用session对象进行后续操作（携带了cookie）

---

## 异步爬虫

---

### 异步爬虫的方式

+ 多线程，多进程（不建议）
    + 好处：可以为相关阻塞的操作单独开启线程或进程，阻塞操作就可以异步执行。
    + 弊端：无法无限制的开启多线程或多进程。
+ 线程池，进程池（适当使用）
    + 好处：可以降低系统对进程或线程创建和销毁的一个频率，从而降低系统的开销。
    + 弊端：池中进程或线程的数量有上限。

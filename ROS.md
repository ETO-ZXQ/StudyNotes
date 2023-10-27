# ROS

## 认识What

### [ROS机器人操作系统终于有人给讲明白了 - 知乎](https://zhuanlan.zhihu.com/p/500130466)

![ROS计算图](./images/ROS计算图.jpg "ROS计算图")

> 可能很多初学者听到机器人操作系统，就被“操作系统”几个字吓住了。其实简单点说，ROS就是一个分布式的通信框架，帮助程序进程之间更方便地通信。
> 一个机器人通常包含多个部件，每个部件都有配套的控制程序，以实现机器人的运动与视听功能等。那么要协调一个机器人中的这些部件，或者协调由多个机器人组成的机器人集群，怎么办呢？这时就需要让分散的部件能够互相通信，在多机器人集群中，这些分散的部件还分散在不同的机器人上。解决这种分布式通信问题正是ROS的设计初衷。
>
> ROS的核心思想就是将机器人的软件功能做成一个个节点，节点之间通过互相发送消息进行沟通。这些节点可以部署在同一台主机上，也可以部署在不同主机上，甚至还可以部署在互联网上。ROS网络通信机制中的主节点（master）负责对网络中各个节点之间的通信过程进行管理调度，同时提供一个用于配置网络中全局参数的服务。

## ROS1与ROS2

### 架构

![ROS&ROS2架构图](./images/ROS&ROS2架构图.png "ROS&ROS2架构图")

## ROS1

### B站视频教程ROS1-Noetic文档摘录[【Autolabor初级教程】ROS机器人入门](https://www.bilibili.com/video/BV1Ci4y1L7ZZ/)

**go to `ROS1Noetic文档.md`**

## ROS2

### 文件系统

#### 工作空间的目录结构

*[1.5 ROS2体系框架【万字干货来啦，快来码住】 - 知乎](https://zhuanlan.zhihu.com/p/655747465)*

```auto
WorkSpace --- 自定义的工作空间。
    |--- build：存储中间文件的目录，该目录下会为每一个功能包创建一个单独子目录。
    |--- install：安装目录，该目录下会为每一个功能包创建一个单独子目录。
    |--- log：日志目录，用于存储日志文件。
    |--- src：用于存储功能包源码的目录。
        |-- C++功能包
            |-- package.xml：包信息，比如:包名、版本、作者、依赖项。
            |-- CMakeLists.txt：配置编译规则，比如源文件、依赖项、目标文件。
            |-- src：C++源文件目录。
            |-- include：头文件目录。
            |-- msg：消息接口文件目录。
            |-- srv：服务接口文件目录。
            |-- action：动作接口文件目录。
        |-- Python功能包
            |-- package.xml：包信息，比如:包名、版本、作者、依赖项。
            |-- setup.py：与C++功能包的CMakeLists.txt类似。
            |-- setup.cfg：功能包基本配置文件。
            |-- resource：资源目录。
            |-- test：存储测试相关文件。
            |-- 功能包同名目录：Python源文件目录。
```

另外，无论是Python功能包还是C++功能包，都可以自定义一些配置文件相关的目录。上述这些目录也可以定义为其他名称，或者根据需要创建其他一些目录。

```auto
|-- C++或Python功能包
    |-- launch：存储launch文件。
    |-- rviz：存储rviz2配置相关文件。
    |-- urdf：存储机器人建模文件。
    |-- params：存储参数文件。
    |-- world：存储仿真环境相关文件。
    |-- map：存储导航所需地图文件。
    |-- ......
```

### rcl: ROS Client Library

rcl，ROS客户端库，是ROS2的底层通信库，负责处理节点之间的通信、消息传递和服务调用等功能。

- C++：`rclcpp`
    `#include "rclcpp/rclcpp.hpp"`
- Python：`rclpy`
    `import rclpy`

### 开发流程

1. 创建工作空间
2. 编译工作空间：`colcon build` ?????
3. 设置环境变量

    ```Bash
    $ source install/local_setup.sh # 仅在当前终端生效
    $ echo "source .../WorkSpace/install/local_setup.sh" >> ~/.bashrc # 所有终端均生效
    ```

4. 创建功能包：`ros2 pkg create --build-type <build-type> <package_name>`

    ```Bash
    $ cd .../WorkSpace/src
    $ ros2 pkg create --build-type ament_cmake learning_pkg_cpp     # C++
    $ ros2 pkg create --build-type ament_python learning_pkg_python # Python
    ```

5. 编写代码
6. 编译功能包

    ```Bash
    $ cd .../WorkSpace
    $ colcon build   # 编译工作空间所有功能包
    $ source install/local_setup.bash
    ```

## 体会

1. ROS相当于一套神经系统，将各模块整合起来，负责各模块并行运行和各模块间的交互。
2. ROS的运行和编译是分开的。ROS的编译模块相对独立，可安装可移除。

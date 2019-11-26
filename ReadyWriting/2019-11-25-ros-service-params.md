---
title: ROS 入门 - 服务和参数
date: 2019-11-25 20:00:00
---
# ROS 入门 - 服务和参数
***
> 版权声明：本文为 {{ site.name }} 原创文章，可以随意转载，但必须在明确位置注明出处！



## 1、ROS Services

ROS 服务是 ROS 提供的一种节点之间相互通信的方式，一个服务允许节点发送一个请求 request 或者接收一个响应 response。



## 2、rosservice

rosservice 命令可以对服务进行操作，比如调用服务，显示服务类型等，如下：

```sh
rosservice list print information about active services
rosservice call call the service with the provided args
rosservice type print service type
rosservice find find services by service type
rosservice uri print service ROSRPC uri
```

### 2.1 rosservice list

list 命令能够列出当前运行的节点提供的所有服务，让我们先来运行上一篇博客的小乌龟节点，先运行 roscore：

```sh
roscore
```

再开启一个新终端启动小乌龟节点，也可以在一个终端中分屏，参考[这篇](https://dlonng.com/posts/terminator)文章：

```sh
rosrun turtlesim turtlesim_node
```

然后使用 list 命令查看当前运行的小乌龟节点提供的服务：

```sh
rosservice list

/clear
/kill
/reset
/rosout/get_loggers
/rosout/set_logger_level
/spawn
/teleop_turtle/get_loggers
/teleop_turtle/set_logger_level
/turtle1/set_pen
/turtle1/teleport_absolute
/turtle1/teleport_relative
/turtlesim/get_loggers
/turtlesim/set_logger_level
```

你的输出应该跟上面类似，再来详细看看一个服务的类型。

### 2.2 rosservice type

type 命令显示服务的类型，即这个服务发送和接收请求的数据类型：

```sh
rosservice type [service]
```

来看看 clear 服务的 type：

```sh
rosservice type /clear

std_srvs/Empty
```

输出显示这个 clear 服务的类型为空，为什么呢？这是因为 clear 服务是清除功能，调用这个服务不需要传递参数，自然也就不需要指定服务的 type 了。

那如何来调用服务呢？

### 2.3 rosservice call

Call 命令使用方法如下：

```sh
rosservice call [service] [args]
```

来调用 clear 服务试试，这个服务不需要传递参数：

```sh
rosservice call /clear
```

可以发现小乌龟窗口背景中的白色路劲线被清除了，恢复成刚运行的样子：

<div  align="center">
<img src="http://wiki.ros.org/ROS/Tutorials/UnderstandingServicesParams?action=AttachFile&do=get&target=turtlesim.png"/>
</div>









<div  align="center">
<img src="https://dlonng.com/images/xxx/xxx.png"/>
</div>

> {{ site.prompt }}

<div  align="center">
<img src="https://dlonng.com/images/wechart.jpg" width = "200" height = "200"/>
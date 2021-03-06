---
title: circular_buffer 简介及使用
date : 2017-05-23 10:00:00
---

# circular_buffer 简介及使用
***
> 版权声明：本文为 {{ site.name }} 原创文章，可以随意转载，但必须在明确位置注明出处！ 

## 什么是 circular_buffer ?
`circular_buffer` 中文意为**环形缓冲区**，这是一个固定大小的缓冲区，它被定义成一个环形，当缓冲区满了后，新来的数据会覆盖掉旧的数据。


它的形状像下面这样：

![circular_buffer]({{ site.url }}/images/cb/circular_buffer.png)

## 基本实现原理
`circular_buffer` 的内部使用**一块连续的内存**来保存数据，它类似于通过**数组**来实现。



## 基本使用方法
`circular_buffer` 的操作大多数都是放入数据，取出数据，所以常用下面 3 个函数：
```cpp
boost::circular_buffer<int> cb(3);

// 放入元素
cb.push_back(1);
cb.push_back(2);
cb.push_back(3);

// 弹出尾部元素 3
cb.pop_back();  // 3 is removed.

// 弹出头部元素 1
cb.pop_front(); // 1 is removed.

// 现在只剩下元素 2
```
因为 `boost` 封装的很好，所以我们可以像使用 `STL` 一样来使用它。


## 实际项目使用
在最近的开发中，项目要求将动态的数据显示到表格中，**最新的数据在表格最上面，老的数据在最下面**，正好符合 `circular_buffer` 的使用场合，因此我们采用了 `circular_buffer` 这个数据结构并很好实现了这个功能，基本需求如下：

![circular_buffer]({{ site.url }}/images/cb/circular_buf_use.png)

要注意的是，因为项目需求要求我们表格每一行都要显示很多数据，所以我们使用 `vector` 来存储每一行的数据，而 `circular_buffer` 里面存储的是 `vector` 类型，也就是存储一行数据。

```cpp
// 我们定义的缓冲区实际类型，每个 item 代表表格的一行数据
boost::circular_buffer<std::vector<GridData>> m_circularBuf;
```

基本工作流程：
1. 数据到来，新建一个 `std::vector<GridData>` 类型并用新的数据初始化，然后 `push_back` 到 `m_circularBuf` 中
2. 遍历一次 `m_circularBuf`，将其中的每个 `item: std::vector<GridData>` 绑定到表格控件指定的一行上显示。  		

如果你对这个需求有兴趣，你可以通过后面的方式联系我，我可以提供部分核心代码 ^_^。

> 你需要学会使用 boost，即使不了解原理。

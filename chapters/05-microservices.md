微服务
===

微内核与宏内核
---

> 单内核：也称为宏内核。将内核从整体上作为一个大过程实现，并同时运行在一个单独的地址空间。所有的内核服务都在一个地址空间运行，相互之间直接调用函数，简单高效。微内核：功能被划分成独立的过程，过程间通过IPC进行通信。模块化程度高，一个服务失效不会影响另外一个服务。Linux是一个单内核结构，同时又吸收了微内核的优点：模块化设计，支持动态装载内核模块。Linux还避免了微内核设计上的缺陷，让一切都运行在内核态，直接调用函数，无需消息传递。

>微内核――在微内核中，大部分内核都作为单独的进程在特权状态下运行，他们通过消息传递进行通讯。在典型情况下，每个概念模块都有一个进程。因此，假如在设计中有一个系统调用模块，那么就必然有一个相应的进程来接收系统调用，并和能够执行系统调用的其他进程（或模块）通讯以完成所需任务。

Hurd之死
---


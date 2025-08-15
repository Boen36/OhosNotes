# 线程模型

线程是进程中的执行流。进程是系统分配资源的基本单位，线程是系统进行运算调度的基本单位。CPU时间片分配的对象是线程。

## 线程类型

一个线程对应一个ArkTS引擎实例，同一类型的ExtensionAbility也运行在同一进程的同一线程中

线程大致分为三类：

1. 主线程

- 执行UI绘制
- 管理主线程的ArkTS引擎，使得可以让多个应用组件如UIAbility运行在同一个ArkTS引擎上
- 管理其他线程的ArkTS引擎，实现统一的调度和分配。例如管理TaskPool线程和Worker线程中的ArkTS引擎
- 接受TaskPool和Worker线程发送的消息
- 分发交互事件
- 处理应用代码回调，包括事件处理和生命周期管理

2. TaskPool 线程

3. Worker 线程

## 使用EventHub进行线程间通信
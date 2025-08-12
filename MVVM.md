# MVVM模式介绍

ArkUI采用MVVM模式，Model-View-ViewModel实现数据，视图，逻辑的分离

Model数据访问层，最底层的数据处理层

View 用户界面层，不包含业务逻辑，绑定ViewModel，实现界面动态刷新

ViewModel 逻辑层，负责处理View传递的逻辑请求

ArkUI中的状态变量扮演着ViewModel的角色，向下更新数据，向上刷新UI

View层中的UI可以分为页面组件，业务组件，通用组件。业务组件通常包含了独有的业务逻辑，一般无法通用

ViewModel层中的数据通常为页面数据，也就是UI组件所需要显示的数据

Model可以理解为数据源，ViewModel层可以理解为基于这些数据源，构建方便用户理解和前端展示的数据结构

## MVVM架构核心原则

> 不可跨层访问

View层不可以跨过ViewModel层直接访问Model层

> 下层不可访问下层数据

ViewModel 层不能依赖View中的某个数据

> 非父子组件间解藕，不可直接访问

一个组件只能知道自己的子节点有哪些，它的父节点和兄弟节点都是未知的，得实际使用的时候才知道

page负责将组件像积木一样搭建起来

## 备忘录开发实战

ViewModel层负责服务View层，因此又被称为"service"层

共享组件指的是不依赖ViewModel，只需要外部参数就可以正常工作

# 进程模型

进程是操作系统进行资源分配的基本单位

## 基本进程类型

一个应用中的基本进程类型分为三类：

1. 主进程

同一个应用中所有的UIAbility都运行在同一个主进程中，包括来自不同模块的UIAbility

2. ExtensionAbility 进程

默认同一类型的ExtensionAbility位于一个单独的进程中。特定的ExtensionAbility可以通过配置实现，每个实例运行在单独的进程

3. Render 进程

默认同一应用中的所有的Web组件运行在同一个Render进程中，可以通过配置实现对Web组件分组，不同组运行在独立的进程

> 一个应用中可以存在多个AbilityStage，一个AbilityStage中可以存在多个Ability。进程的生命周期与其中的Ability生命周期息息相关，只有进程中所有的Ability都推出，进程才会被销毁

## 其他进程类型

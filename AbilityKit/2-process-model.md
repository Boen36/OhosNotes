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

1. 模块独立进程

如果每个HAP的业务相对独立，为了减少相互的影响，可以考虑为每个HAP配置单独的进程

通过`module.json5`中`isolationMode`字段标签设置为`isolationOnly`或`isolationFirst`，可以为HAP设置独立进程，此时该模块下的UIAbility将运行在独立进程中。`isolationFirst`的逻辑是，系统会优先尝试将HAP加载到独立的进程，如果资源充裕，则为其分配独立的进程，否则还是运行在原来的主进程中

2. 动态指定进程

可以在运行时，动态分配 UIAbility 到指定的进程。借助这个特性，开发者可以实现更精细的控制。例如想要将支付这类安全级别要求很高的UIAbility与其他的UIAbility隔离，就可以为支付相关的UIAbility分配指定的标识符，让它们位于单独的进程中。具体需要配置UIAbility的`isolationProcess`为 true，在实际启动该UIAbility的时候，在want参数中添加该UIAbility类型信息，之后在`AbilityStage`的`onNewProcessRequest`中的回调中根据want参数，动态返回指定的字符串，返回相同字符串的UIAbility会被分配到相同的进程中

3. 子进程

ArkTS只允许一级子进程

可以通过`childProcessManager`创建子进程，子进程的生命周期跟随父进程，父进程消亡，子进程也跟着消亡

> 系统创建应用进程启动后，会默认创建一个主线程并进入消息循环，应用组件（如UIAbility）均运行在主线程中
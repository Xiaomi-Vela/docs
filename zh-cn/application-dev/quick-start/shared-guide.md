# 共享包概述

当前系统提供了两种共享包，[HAR（Harmony Archive）](har-package.md)静态共享包和[HSP（Harmony Shared Package）](in-app-hsp.md)动态共享包。

HAR与HSP都是为了实现代码和资源的共享，都可以包含代码、C++库、资源和配置文件，最大的不同之处在于：HAR中的代码和资源跟随使用方编译，如果有多个使用方，它们的编译产物中会存在多份相同拷贝；而HSP中的代码和资源可以独立编译，运行时在一个进程中代码也只会存在一份。

**图1** HAR和HSP在APP包中的形态示意图
![in-app-hsp-har](figures/in-app-hsp-har.png)

HSP旨在解决多个模块引用相同的HAR，导致APP包大小膨胀的问题。

**使用HSP的约束条件：**
- HSP及其使用方都必须是Stage模型。
- HSP及其使用方都必须使用esmodule编译模式。
- HSP不支持在配置文件中声明abilities、extensionAbilities标签。


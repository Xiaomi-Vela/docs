# display_device.h


## 概述

显示设备控制接口声明。

**Since:**

1.0

**Version:**

2.0

**相关模块:**

[Display](_display.md)


## 汇总


### 类

  | 名称 | 描述 | 
| -------- | -------- |
| [DeviceFuncs](_device_funcs.md) | struct<br/>显示设备控制接口结构体，定义显示设备控制接口函数指针。 | 


### 类型定义

  | 名称 | 描述 | 
| -------- | -------- |
| (\*&nbsp;[HotPlugCallback](_display.md#hotplugcallback))&nbsp;(uint32_t&nbsp;devId,&nbsp;bool&nbsp;connected,&nbsp;void&nbsp;\*data) | typedef&nbsp;void&nbsp;\*<br/>热插拔事件回调 | 
| (\*&nbsp;[VBlankCallback](_display.md#vblankcallback))&nbsp;(unsigned&nbsp;int&nbsp;sequence,&nbsp;uint64_t&nbsp;ns,&nbsp;void&nbsp;\*data) | typedef&nbsp;void&nbsp;\*<br/>VBlank&nbsp;事件回调。 | 
| (\*&nbsp;[RefreshCallback](_display.md#refreshcallback))&nbsp;(uint32_t&nbsp;devId,&nbsp;void&nbsp;\*data) | typedef&nbsp;void&nbsp;\*<br/>刷新请求回调 | 


### 函数

  | 名称 | 描述 | 
| -------- | -------- |
| [DeviceInitialize](_display.md#deviceinitialize)&nbsp;([DeviceFuncs](_device_funcs.md)&nbsp;\*\*funcs) | int32_t<br/>实现显示设备控制接口的初始化，申请操作显示设备控制接口的资源，并获取对应的操作接口。 | 
| [DeviceUninitialize](_display.md#deviceuninitialize)&nbsp;([DeviceFuncs](_device_funcs.md)&nbsp;\*funcs) | int32_t<br/>取消显示设备控制接口的初始化，释放控制接口使用到的资源。 | 

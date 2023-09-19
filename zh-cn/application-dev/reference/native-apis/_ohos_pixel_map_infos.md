# OhosPixelMapInfos


## 概述

用于定义 pixel map 的相关信息。

**起始版本：**

10

**相关模块：**

[Image](image.md)


## 汇总


### 成员变量

| 名称 | 描述 | 
| -------- | -------- |
| [width](#width) | 图片的宽, 用pixels表示 | 
| [height](#height) | 图片的高, 用pixels表示 | 
| [rowSize](#rowsize) | 每行的bytes数 | 
| [pixelFormat](#pixelformat) | Pixel 的格式 | 


## 结构体成员变量说明


### height

```
uint32_t OhosPixelMapInfos::height
```

**描述：**

图片的高, 用pixels表示


### pixelFormat

```
int32_t OhosPixelMapInfos::pixelFormat
```

**描述：**

Pixel 的格式


### rowSize

```
uint32_t OhosPixelMapInfos::rowSize
```

**描述：**

每行的bytes数


### width

```
uint32_t OhosPixelMapInfos::width
```

**描述：**

图片的宽, 用pixels表示
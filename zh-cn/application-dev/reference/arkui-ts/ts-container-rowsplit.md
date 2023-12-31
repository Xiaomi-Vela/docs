# RowSplit

将子组件横向布局，并在每个子组件之间插入一根纵向的分割线。

>  **说明：**
>
> 该组件从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。

## 子组件

可以包含子组件。

该组件会限制子组件的宽度。初始化时，该组件的布局是按照子组件的宽度来计算的。初始化后，后续动态修改子组件的宽度则不生效，使用的宽度为该组件分割线的间距，该宽度可以通过手势移动分割线进行变更。
## 接口

RowSplit()


## 属性

| 名称 | 参数类型 | 描述 | 
| -------- | -------- | -------- |
| resizeable | boolean | 分割线是否可拖拽，默认为false。 | 

>  **说明：**
>
> RowSplit的分割线可以改变左右两边子组件的宽度，子组件可改变宽度的范围取决于子组件的最大最小宽度。
>
> 支持clip、margin等通用属性，clip不设置的时候默认值为true。


## 示例

```ts
// xxx.ets
@Entry
@Component
struct RowSplitExample {
  build() {
    Column() {
      Text('The second line can be dragged').fontSize(9).fontColor(0xCCCCCC).width('90%')
      RowSplit() {
        Text('1').width('10%').height(100).backgroundColor(0xF5DEB3).textAlign(TextAlign.Center)
        Text('2').width('10%').height(100).backgroundColor(0xD2B48C).textAlign(TextAlign.Center)
        Text('3').width('10%').height(100).backgroundColor(0xF5DEB3).textAlign(TextAlign.Center)
        Text('4').width('10%').height(100).backgroundColor(0xD2B48C).textAlign(TextAlign.Center)
        Text('5').width('10%').height(100).backgroundColor(0xF5DEB3).textAlign(TextAlign.Center)
      }
      .resizeable(true) // 可拖动
      .width('90%').height(100)
    }.width('100%').margin({ top: 5 })
  }
}
```

![zh-cn_image_0000001219982729](figures/zh-cn_image_0000001219982729.gif)

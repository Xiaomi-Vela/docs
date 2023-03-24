# 自定义弹窗

>  **说明：**
> 从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。


通过CustomDialogController类显示自定义弹窗。使用弹窗组件时，可优先考虑自定义弹窗，便于自定义弹窗的样式与内容。


## 接口

CustomDialogController(value:{builder: CustomDialog, cancel?: () =&gt; void, autoCancel?: boolean, alignment?: DialogAlignment, offset?: Offset, customStyle?: boolean})


- 参数
  | 参数名 | 参数类型 | 必填 | 默认值 | 参数描述 |
  | -------- | -------- | -------- | -------- | -------- |
  | builder | any | 是 | - | 自定义弹窗内容构造器。 |
  | cancel | ()&nbsp;=&gt;&nbsp;void | 否 | - | 点击遮障层退出时的回调。 |
  | autoCancel | boolean | 否 | true | 是否允许点击遮障层退出。 |
  | alignment | DialogAlignment | 否 | DialogAlignment.Default | 弹窗在竖直方向上的对齐方式。 |
  | offset | {<br/>dx:&nbsp;Length&nbsp;\|&nbsp;[Resource](ts-types.md#resource),<br/>dy:&nbsp;Length&nbsp;&nbsp;\|&nbsp;[Resource](ts-types.md#resource)<br/>} | 否 | - | 弹窗相对alignment所在位置的偏移量。 |
  | customStyle | boolean | 否 | false | 弹窗容器样式是否自定义。 |
  | gridCount<sup>8+</sup> | number | 否 | - | 弹窗宽度占栅格宽度的个数。 |
  
## DialogAlignment枚举说明
| 名称 | 描述 |
| -------- | -------- |
| Top | 垂直顶部对齐。 |
| Center | 垂直居中对齐。 |
| Bottom | 垂直底部对齐。 |
| Default | 默认对齐。<br/>**说明：**<br/>与枚举值Center效果相同。 |
| TopStart<sup>8+</sup> | 左上对齐。 |
| TopEnd<sup>8+</sup> | 右上对齐。 |
| CenterStart<sup>8+</sup> | 左中对齐。 |
| CenterEnd<sup>8+</sup> | 右中对齐。 |
| BottomStart<sup>8+</sup> | 左下对齐。 |
| BottomEnd<sup>8+</sup> | 右下对齐。 |


## CustomDialogController

### 导入对象

```
dialogController : CustomDialogController = new CustomDialogController(value:{builder: CustomDialog, cancel?: () => void, autoCancel?: boolean})
```
**说明**：CustomDialogController仅在作为@CustomDialog和@Component struct的成员变量，且在@Component struct内部定义时赋值才有效，具体用法可看下方示例。

### open()
open(): void


显示自定义弹窗内容，若已显示，则不生效。


### close
close(): void


关闭显示的自定义弹窗，若已关闭，则不生效。


## 示例

```
// xxx.ets
@CustomDialog
struct CustomDialogExample {
  @Link textValue: string
  @Link inputValue: string
  controller: CustomDialogController
  cancel: () => void
  confirm: () => void

  build() {
    Column() {
      Text('Change text').fontSize(20).margin({ top: 10, bottom: 10 })
      TextInput({ placeholder: '', text: this.textValue }).height(60).width('90%')
        .onChange((value: string) => {
          this.textValue = value
        })
      Text('Whether to change a text?').fontSize(16).margin({ bottom: 10 })
      Flex({ justifyContent: FlexAlign.SpaceAround }) {
        Button('cancel')
          .onClick(() => {
            this.controller.close()
            this.cancel()
          }).backgroundColor(0xffffff).fontColor(Color.Black)
        Button('confirm')
          .onClick(() => {
            this.inputValue = this.textValue
            this.controller.close()
            this.confirm()
          }).backgroundColor(0xffffff).fontColor(Color.Red)
      }.margin({ bottom: 10 })
    }
  }
}

@Entry
@Component
struct CustomDialogUser {
  @State textValue: string = ''
  @State inputValue: string = 'click me'
  dialogController: CustomDialogController = new CustomDialogController({
    builder: CustomDialogExample({ cancel: this.onCancel, confirm: this.onAccept, textValue: $textValue, inputValue: $inputValue }),
    cancel: this.existApp,
    autoCancel: true
  })

  onCancel() {
    console.info('Callback when the first button is clicked')
  }
  onAccept() {
    console.info('Callback when the second button is clicked')
  }
  existApp() {
    console.info('Click the callback in the blank area')
  }

  build() {
    Column() {
      Button(this.inputValue)
        .onClick(() => {
          this.dialogController.open()
        }).backgroundColor(0x317aff)
    }.width('100%').margin({ top: 5 })
  }
}
```

![zh-cn_image_0000001219744203](figures/zh-cn_image_0000001219744203.gif)

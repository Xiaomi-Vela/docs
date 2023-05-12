# 显式动画

>  **说明：**
>
>  从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。


| 接口名称                                     | 功能描述                                     |
| ---------------------------------------- | ---------------------------------------- |
| animateTo(value:&nbsp;[AnimationOptions](#animationoptions对象说明),&nbsp;event:&nbsp;()=&gt;&nbsp;void)&nbsp;:&nbsp;void | 提供全局animateTo显式动画接口来指定由于闭包代码导致的状态变化插入过渡动效。<br/>event指定显示动效的闭包函数，在闭包函数中导致的状态变化系统会自动插入过渡动画。 |


## AnimationOptions对象说明

| 名称       | 类型                | 必填 | 默认值    | 描述                                  |
| ---------- | ------------------------- | ----- | ------ | ----------------------------------- |
| duration   | number                    |  否   | 1000   | 动画持续时间，单位为毫秒。                       |
| tempo      | number                    |  否   | 1.0    | 动画的播放速度，值越大动画播放越快，值越小播放越慢，为0时无动画效果。 |
| curve      | Curve&nbsp;\|&nbsp;Curves |  否   | Curve.Linear | 动画曲线。                               |
| delay      | number                    |  否   | 0      | 单位为ms(毫秒)，默认不延时播放。                  |
| iterations | number                    |  否   | 1      | 默认播放一次，设置为-1时表示无限次播放。               |
| playMode   | [PlayMode](ts-appendix-enums.md#playmode)| 否   | PlayMode.Normal | 设置动画播放模式，默认播放完成后重头开始播放。             |
| onFinish   | ()&nbsp;=&gt;&nbsp;void   |  否   |   -    | 动效播放完成回调。 |

## 示例

```ts
// xxx.ets
@Entry
@Component
struct AnimateToExample {
  @State widthSize: number = 200
  @State heightSize: number = 100
  @State rotateAngle: number = 0
  private flag: boolean = true

  build() {
    Column() {
      Button('click me')
        .width(this.widthSize)
        .height(this.heightSize)
        .backgroundColor(0x317aff)
        .onClick((event: ClickEvent) => {
          // 对Button组件的宽高属性进行动画配置
          if (this.flag) {
            animateTo({
              duration: 1000, // 动画时长
              tempo: 0.5, // 播放速率
              curve: Curve.EaseInOut, // 动画曲线
              delay: 200, // 动画延迟
              iterations: 1, // 播放次数
              playMode: PlayMode.Normal, // 动画模式
              onFinish: () => {
                console.info('play end')
              }
            }, () => {
              this.widthSize = 100
              this.heightSize = 50
            })
          } else {
            animateTo({
              duration: 200, // 动画时长
              curve: Curve.Ease, // 动画曲线
              delay: 200, // 动画延迟
              iterations: 1, // 播放次数
              playMode: PlayMode.Normal, // 动画模式
              onFinish: () => {
                console.info('play end')
              }
            }, () => {
              this.widthSize = 200
              this.heightSize = 100
            })
          }
          this.flag = !this.flag
        })
      Button('change rotate angle')
        .margin(50)
        .rotate({ x: 0, y: 0, z: 1, angle: this.rotateAngle })
        .onClick(() => {
          animateTo({
            duration: 1200,
            curve: Curve.Friction,
            delay: 500,
            iterations: -1, // 设置-1表示动画无限循环
            playMode: PlayMode.AlternateReverse,
            onFinish: () => {
              console.info('play end')
            }
          }, () => {
            this.rotateAngle = 90
          })
        })
    }.width('100%').margin({ top: 5 })
  }
}
```

![zh-cn_image_0000001174104398](figures/zh-cn_image_0000001174104398.gif)

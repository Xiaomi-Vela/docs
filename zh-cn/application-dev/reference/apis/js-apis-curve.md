# @ohos.curves (插值计算)

本模块提供设置动画插值曲线功能，用于构造阶梯曲线对象、构造三阶贝塞尔曲线对象和构造弹簧曲线对象。

> **说明：**
> 
> 本模块首批接口从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。


## 导入模块

```ts
import Curves from '@ohos.curves'
```


## Curves.initCurve<sup>9+</sup>

initCurve(curve?: Curve)：ICurve


插值曲线的初始化函数，可以根据入参创建一个插值曲线对象。

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型                                                         | 必填 | 默认值       | 说明       |
| ------ | ------------------------------------------------------------ | ---- | ------------ | ---------- |
| curve  | [Curve](../arkui-ts/ts-appendix-enums.md#curve) | 否   | Curve.Linear | 曲线类型。 |

**返回值：**

| 类型                           | 说明             |
| ---------------------------------- | ---------------- |
|  [ICurve](#icurve) | 曲线的插值对象。 |


**示例：**

```ts
import Curves from '@ohos.curves'
Curves.initCurve(Curve.EaseIn) // 创建一个默认先慢后快插值曲线
```


##  Curves.stepsCurve<sup>9+</sup>

stepsCurve(count: number, end: boolean)：ICurve


构造阶梯曲线对象。

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型    | 必填 | 说明                                                         |
| ------ | ------- | ----| ------------------------------------------------------------ |
| count  | number  | 是   | 阶梯的数量，需要为正整数。                                   |
| end    | boolean | 是   | 在每个间隔的起点或是终点发生阶跃变化。<br>-true：在终点发生阶跃变化。<br>-false：在起点发生阶跃变化。 |

**返回值：**

| 类型                           | 说明             |
| ---------------------------------- | ---------------- |
|  [ICurve](#icurve) | 曲线的插值对象。 |


**示例：**

```ts
import Curves from '@ohos.curves'
Curves.stepsCurve(9, true)  //创建一个阶梯曲线
```


## Curves.cubicBezierCurve<sup>9+</sup>

cubicBezierCurve(x1: number, y1: number, x2: number, y2: number)：ICurve


构造三阶贝塞尔曲线对象，曲线的值必须处于0-1之间。

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**参数：**
| 参数名  | 类型     | 必填   | 说明             |
| ---- | ------ | ---- | -------------- |
| x1   | number | 是    | 确定贝塞尔曲线第一点横坐标。 |
| y1   | number | 是    | 确定贝塞尔曲线第一点纵坐标。 |
| x2   | number | 是    | 确定贝塞尔曲线第二点横坐标。 |
| y2   | number | 是    | 确定贝塞尔曲线第二点纵坐标。 |

**返回值：**

| 类型                           | 说明             |
| ---------------------------------- | ---------------- |
|  [ICurve](#icurve) | 曲线的插值对象。 |


**示例：**

```ts
import Curves from '@ohos.curves'
Curves.cubicBezierCurve(0.1, 0.0, 0.1, 1.0) // 创建一个三阶贝塞尔曲线
```


##  Curves.springCurve<sup>9+</sup>

springCurve(velocity: number, mass: number, stiffness: number, damping: number)：ICurve


构造弹簧曲线对象。

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**参数：**
| 参数名       | 类型     | 必填   | 说明    |
| --------- | ------ | ---- | ----- |
| velocity  | number | 是    | 初始速度。是由外部因素对弹性动效产生的影响参数，其目的是保证对象从之前的运动状态平滑的过渡到弹性动效。 |
| mass      | number | 是    | 质量。弹性系统的受力对象，会对弹性系统产生惯性影响。质量越大，震荡的幅度越大，恢复到平衡位置的速度越慢。 |
| stiffness | number | 是    | 刚度。是物体抵抗施加的力而形变的程度。在弹性系统中，刚度越大，抵抗变形的能力越强，恢复到平衡位置的速度就越快。 |
| damping   | number | 是    | 阻尼。是一个纯数，无真实的物理意义，用于描述系统在受到扰动后震荡及衰减的情形。阻尼越大，弹性运动的震荡次数越少、震荡幅度越小。 |


**返回值：**

| 类型                           | 说明             |
| ---------------------------------- | ---------------- |
|  [ICurve](#icurve)| 曲线的插值对象。 |


**示例：**

```ts
import Curves from '@ohos.curves'
Curves.springCurve(100, 1, 228, 30) // 创建一个弹簧插值曲线
```


##  Curves.springMotion<sup>9+</sup>

springMotion(response?: number, dampingFraction?: number, overlapDuration?: number): ICurve

构造弹性动画曲线对象。如果对同一对象的同一属性进行多个弹性动画，每个动画会替换掉前一个动画，并继承之前的速度。

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**参数：**
| 参数名       | 类型     | 必填   | 说明    |
| --------- | ------ | ---- | ----- |
| response  | number | 否    | 弹簧自然振动周期，决定弹簧复位的速度。单位：秒，默认值：0.55。 |
| dampingFraction      | number | 否    | 阻尼系数。<br>0表示无阻尼，一直处于震荡状态；<br>大于0小于1的值为欠阻尼，运动过程中会超出目标值；<br>等于1为临界阻尼；<br>大于1为过阻尼，运动过程中逐渐趋于目标值。<br>默认值：0.825。 |
| overlapDuration | number | 否    | 弹性动画衔接时长。发生动画继承时，如果前后两个弹性动画response不一致，response参数会在overlapDuration时间内平滑过渡。单位：秒，默认值：0。 |


**返回值：**

| 类型                           | 说明             |
| ---------------------------------- | ---------------- |
|  [ICurve](#icurve)| 曲线对象。<br>**说明:** 弹性动画曲线为物理曲线，animation、animateTo中的duration参数不生效，动画持续时间取决于springMotion动画曲线参数和之前的速度。时间不能归一，故不能通过该曲线的[interpolate](#interpolate)函数获得插值。 |

**示例：**

```ts
import Curves from '@ohos.curves'
Curves.springMotion() // 创建一个默认弹性动画曲线
Curves.springMotion(0.5) // 创建指定response、其余参数默认的弹性动画曲线
Curves.springMotion(0.5, 0.6) // 创建指定response和dampingFraction、其余参数默认的弹性动画曲线
Curves.springMotion(0.5, 0.6, 0) // 创建三个参数均自定义的弹性动画曲线
```


##  Curves.responsiveSpringMotion<sup>9+</sup>

responsiveSpringMotion(response?: number, dampingFraction?: number, overlapDuration?: number): ICurve

构造弹性跟手动画曲线对象，是[springMotion](#curvesspringmotion9)的一种特例，仅默认参数不同，可与springMotion混合使用。

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**参数：**
| 参数名       | 类型     | 必填   | 说明    |
| --------- | ------ | ---- | ----- |
| response  | number | 否    | 解释同springMotion中的response。单位：秒，默认值：0.15。 |
| dampingFraction      | number | 否    | 解释同springMotion中的dampingFraction。默认值：0.86。 |
| overlapDuration | number | 否    | 解释同springMotion中的overlapDuration。单位：秒，默认值：0.25。 |

**返回值：**

| 类型                           | 说明             |
| ---------------------------------- | ---------------- |
|  [ICurve](#icurve)| 曲线对象。<br>**说明:** <br>1.弹性跟手动画曲线为springMotion的一种特例，仅默认值不同。如果使用自定义参数的弹性曲线，推荐使用springMotion构造曲线；如果使用跟手动画，推荐使用默认参数的弹性跟手动画曲线。<br>2.animation、animateTo中的duration参数不生效，动画持续时间取决于responsiveSpringMotion动画曲线参数和之前的速度，也不能通过该曲线的[interpolate](#interpolate)函数获得插值。 |

**示例：**

```ts
import Curves from '@ohos.curves'
Curves.responsiveSpringMotion() // 创建一个默认弹性跟手动画曲线
```


## ICurve


### interpolate

interpolate(fraction:&nbsp;number): number

插值曲线的插值计算函数，可以通过传入的归一化时间参数返回当前的插值

从API version 9开始，该接口支持在ArkTS卡片中使用。

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名   | 类型   | 必填 | 说明                                         |
| -------- | ------ | ---- | -------------------------------------------- |
| fraction | number | 是   | &nbsp;当前的归一化时间参数，有效值范围0到1。 |

**返回值：**

| 类型   | 说明                                 |
| ------ | ------------------------------------ |
| number | 返回归一化time时间点对应的曲线插值。 |

**示例：**

```ts
import Curves from '@ohos.curves'
let curve = Curves.initCurve(Curve.EaseIn) // 创建一个默认先慢后快插值曲线
let value: number = curve.interpolate(0.5) // 计算得到时间到一半时的插值
```


## Curves.init<sup>(deprecated)</sup>

init(curve?: Curve): string


插值曲线的初始化函数，可以根据入参创建一个插值曲线对象，从API version9开始废弃，推荐使用[Curves.initCurve](#curvesinitcurve9)。

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型                                                         | 必填 | 默认值       | 说明       |
| ------ | ------------------------------------------------------------ | ---- | ------------ | ---------- |
| curve  |[Curve](../arkui-ts/ts-appendix-enums.md#curve) | 否   | Curve.Linear | 曲线类型。 |


## Curves.steps<sup>(deprecated)</sup>

steps(count: number, end: boolean): string


构造阶梯曲线对象，从API version9开始废弃，推荐使用[Curves. stepsCurve](# curvesstepscurve9)。

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型    | 必填 | 说明                                                         |
| ------ | ------- | ----| ------------------------------------------------------------ |
| count  | number  | 是   | 阶梯的数量，需要为正整数。                                   |
| end    | boolean | 是   | 在每个间隔的起点或是终点发生阶跃变化。<br>-true：在终点发生阶跃变化。<br>-false：在起点发生阶跃变化。 |


## Curves.cubicBezier<sup>(deprecated)</sup>

cubicBezier(x1: number, y1: number, x2: number, y2: number): string


构造三阶贝塞尔曲线对象，曲线的值必须处于0-1之间，API version9开始废弃，推荐使用 [Curves.cubicBezierCurve](#curvescubicbeziercurve9)。

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**参数：**
| 参数名  | 类型     | 必填   | 说明             |
| ---- | ------ | ---- | -------------- |
| x1   | number | 是    | 确定贝塞尔曲线第一点横坐标。 |
| y1   | number | 是    | 确定贝塞尔曲线第一点纵坐标。 |
| x2   | number | 是    | 确定贝塞尔曲线第二点横坐标。 |
| y2   | number | 是    | 确定贝塞尔曲线第二点纵坐标。 |


## Curves.spring<sup>(deprecated)</sup>

spring(velocity: number, mass: number, stiffness: number, damping: number): string


构造弹簧曲线对象，从API version9开始废弃，推荐使用[Curves.springCurve](#curvesspringcurve9)。

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名       | 类型     | 必填   | 说明    |
| --------- | ------ | ---- | ----- |
| velocity  | number | 是    | 初始速度。是由外部因素对弹性动效产生的影响参数，其目的是保证对象从之前的运动状态平滑的过渡到弹性动效。 |
| mass      | number | 是    | 质量。弹性系统的受力对象，会对弹性系统产生惯性影响。质量越大，震荡的幅度越大，恢复到平衡位置的速度越慢。 |
| stiffness | number | 是    | 刚度。是物体抵抗施加的力而形变的程度。在弹性系统中，刚度越大，抵抗变形的能力越强，恢复到平衡位置的速度就越快。 |
| damping   | number | 是    | 阻尼。是一个纯数，无真实的物理意义，用于描述系统在受到扰动后震荡及衰减的情形。阻尼越大，弹性运动的震荡次数越少、震荡幅度越小。 |

## 整体示例

```ts
// xxx.ets
import Curves from '@ohos.curves'

@Entry
@Component
struct ImageComponent {
  @State widthSize: number = 200
  @State heightSize: number = 200

  build() {
    Column() {
      Text()
        .margin({ top: 100 })
        .width(this.widthSize)
        .height(this.heightSize)
        .backgroundColor(Color.Red)
        .onClick(() => {
          let curve = Curves.cubicBezierCurve(0.25, 0.1, 0.25, 1.0);
          this.widthSize = curve.interpolate(0.5) * this.widthSize;
          this.heightSize = curve.interpolate(0.5) * this.heightSize;
        })
        .animation({ duration: 2000, curve: Curves.stepsCurve(9, true) })
    }.width("100%").height("100%")
  }
}
```

![zh-cn_image_0000001174104410](figures/zh-cn_image_0000001174104410.gif)

# Property Animation APIs


ArkUI provides two types of APIs, namely, [animateTo](../reference/arkui-ts/ts-explicit-animation.md) and [animation](../reference/arkui-ts/ts-animatorproperty.md), to implement a property animation – a visual illusion of continuity created by driving component attributes to change over time based on animation parameters such as the animation curve.


| Property Animation API| Scope| Principle| Application Scenario |
| -------- | -------- | -------- | -------- |
| animateTo | GUI changes caused by attribute changes in closures.<br>Transition for appearance and disappearance.| This API is a common function. It animates the differences between the UIs before and after the state variable in the closure is changed.<br>This API can be called multiple times and can be nested. | - A single set of animation parameters is used to animate multiple attributes.<br>- Animations need to be nested. |
| animation | GUI changes caused by attribute changes bound to components through attribute APIs.| This API identifies the change of the animatable attributes of a component and automatically adds an animation.<br>As the API call sequence of the component is from bottom to top, this API applies only to the attributes above it.<br>In a component, you can set individual **animation** for attributes based on the API call sequence. | Different sets of animation parameters are used to animate different attributes. |


## animateTo


```
animateTo(value: AnimateParam, event: () => void): void
```

Among the parameters of [animateTo](../reference/arkui-ts/ts-explicit-animation.md), **value** indicates the [animation parameters](../reference/arkui-ts/ts-explicit-animation.md#animateparam) (including duration and [curve](../reference/apis/js-apis-curve.md#curve)); **event** indicates the closure of the animation. Property animations generated by variable changes within a closure follow the same animation parameters.


```ts
import curves from '@ohos.curves'

@Entry
@Component
struct AnimateToDemo {
  @State animate: boolean = false;
  // Step 1: Declare related state variables.
  @State rotateValue: number = 0; // Rotation angle of component 1.
  @State translateY: number = 0; // Offset of component 2
  @State opacityValue: number = 1; // Opacity of component 2.

  // Step 2: Set the declared state variables to the related animatable attribute APIs.
  build() {
    Column() {
      // Component 1
      Column() {
        Text('ArkUI')
          .fontWeight(FontWeight.Bold)
          .fontSize(20)
          .fontColor(Color.White)
      }
      .justifyContent(FlexAlign.Center)
      .width(150)
      .height(150)
      .borderRadius(10)
      .rotate({ angle: this.rotateValue })
      .backgroundColor(0xf56c6c)

      // Component 2
      Column() {
        Text('ArkUI')
          .fontWeight(FontWeight.Bold)
          .fontSize(20)
          .fontColor(Color.White)
      }
      .justifyContent(FlexAlign.Center)
      .width(150)
      .height(150)
      .backgroundColor(0x67C23A)
      .borderRadius(10)
      .opacity(this.opacityValue)
      .translate({ y: this.translateY })

      Button('Click')
        .margin({ top: 120 })
        .onClick(() => {
          this.animate = !this.animate;
          // Step 3: Enable property animation.
          animateTo({ curve: curves.springMotion() }, () => {
            // Step 4: Change the state variables in the closure to update the UI.
            // You can write any logic that can change the UI, such as array adding and visibility control. The system detects the differences between the new UI and the previous UI and adds animations for the differences.
            // The rotate attribute of component 1 is changed. Therefore, a rotate animation is added to component 1.
            this.rotateValue = this.animate ? 90 : 0;
            // The scale attribute of component 2 is changed. Therefore, a scale animation is added to component 2.
            this.opacityValue = this.animate ? 0.6 : 1;
            // The offset attribute of component 2 is changed. Therefore, an offset animation is added to component 2.
            this.translateY = this.animate ? 100 : 0;
          })
        })
    }
    .width('100%')
    .height('100%')
    .justifyContent(FlexAlign.Center)
  }
}
```

![en-us_image_0000001599958466](figures/en-us_image_0000001599958466.gif)


## animation

Compared with the **animateTo** API, the [animation](../reference/arkui-ts/ts-animatorproperty.md) API does not need to use a closure. Just add it to the end of the target animatable attribute, and the API will automatically add a property animation once it detects that the bound attribute is changed.


```ts
import curves from '@ohos.curves';

@Entry
@Component
struct AnimationDemo {
  @State animate: boolean = false;
  // Step 1: Declare related state variables.
  @State rotateValue: number = 0; // Rotation angle of component 1.
  @State translateY: number = 0; // Offset of component 2
  @State color: Color = Color.White; // Font color of component 2.
  @State opacityValue: number = 1; // Opacity of the parent component.

  // Step 2: Set the declared state variables to the related animatable attribute APIs.
  build() {
    Column() {
      Column() {
        // Component 1
        Text('ArkUI')
          .fontWeight(FontWeight.Bold)
          .fontSize(20)
          .fontColor(Color.White)
          .textAlign(TextAlign.Center)
          .borderRadius(10)
          .backgroundColor(0xf56c6c)
          .rotate({ angle: this.rotateValue })
            // Step 3: Enable property animation. As the API call sequence of the component is from bottom to top, the API takes effect on the preceding rotate attribute.
          .animation({ curve: curves.springMotion(0.3, 1.0) })
          .width(150)
          .height(150)

        // Component 2
        Text('ArkUI')
          .fontWeight(FontWeight.Bold)
          .fontSize(20)
          .fontColor(this.color)
            // Step 3: Enable property animation. As the API call sequence of the component is from bottom to top, the API takes effect on the preceding fontColor attribute.
          .animation({ curve: curves.springMotion(0.6, 1.2) })
          .textAlign(TextAlign.Center)
          .borderRadius(10)
          .backgroundColor(0x67C23A)
          .width(150)
          .height(150)
          .translate({ y: this.translateY })
            // Step 3: Enable property animation. As the API call sequence of the component is from bottom to top, the API takes effect on the preceding translate attribute.
          .animation({ curve: curves.springMotion(0.3, 0.6) })
      }
      .justifyContent(FlexAlign.Center)
      .opacity(this.opacityValue)
      // The animation API takes effect on the opacity attribute. This results in an opacity change of the parent component <Column>, which in turn results in an opacity change of its child components. Therefore, animations are added to the opacity attributes of <Column> and its child components.
      .animation({ curve: curves.springMotion() })

      // Step 4: Change the state variable to update the UI. The system detects the differences between the new UI and the previous UI and adds animations for the differences.
      Button('Click')
        .margin({ top: 120 })
        .onClick(() => {
          this.animate = !this.animate;
          // The rotate attribute of component 1 is changed. Therefore, a rotate animation is added to component 1.
          this.rotateValue = this.animate ? 90 : 0;
          // The translate attribute of component 2 is changed. Therefore, a translate animation is added to component 2.
          this.translateY = this.animate ? 100 : 0;
          // The fontColor attribute of component 2 is changed. Therefore, a fontColor animation is added to component 2.
          this.color = this.animate ? Color.Black : Color.White;
          // The opacity attribute of the parent component <Column> is changed, which results in an opacity change of its child components. Therefore, opacity animations are added to <Column> and its child components.
          this.opacityValue = this.animate ? 0.6 : 1;
        })

    }
    .width('100%')
    .height('100%')
    .justifyContent(FlexAlign.Center)
  }
}
```

![en-us_image_0000001649279705](figures/en-us_image_0000001649279705.gif)

> **NOTE**
> - When an animation is applied to the position or size change of a component, as layout measurement is involved, performance overheads are high. To reduce performance overheads, use the [scale](../reference/arkui-ts/ts-universal-attributes-transformation.md) instead, whose value change does not involve layout measurement. This practice is applicable where the component location and size change continuously, for example, where the component size changes as a response to gestures.
> 
> - Property animations should be applied to the components that are always present. For the components that may appear or disappear, use the [transition animation](arkts-transition-overview.md).
> 
> - Avoid using animation end callbacks, which are invoked when an animation ends. Property animations are applied to states that have occurred, and therefore you do not need to process the end logic. If animation end callbacks are needed, be sure to handle the data management of continuous operations correctly.

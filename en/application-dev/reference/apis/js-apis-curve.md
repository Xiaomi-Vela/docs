# @ohos.curves

The **Curves** module provides APIs for interpolation calculation to create step, cubic Bezier, and spring curves.

> **NOTE**
> 
> The initial APIs of this module are supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.


## Modules to Import

```ts
import Curves from '@ohos.curves'
```


## Curves.initCurve<sup>9+</sup>

initCurve(curve?: Curve): ICurve


Implements initialization for the interpolation curve, which is used to create an interpolation curve based on the input parameter.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type                                                        | Mandatory| Default Value      | Description      |
| ------ | ------------------------------------------------------------ | ---- | ------------ | ---------- |
| curve  | [Curve](../arkui-ts/ts-appendix-enums.md#curve) | No  | Curve.Linear | Curve type.|

**Return value**

| Type                          | Description            |
| ---------------------------------- | ---------------- |
|  [ICurve](#icurve) | Interpolation curve.|


**Example**

```ts
import Curves from '@ohos.curves'
Curves.initCurve(Curve.EaseIn) // Create a default ease-in curve, where the interpolation starts slowly and then picks up speed.
```


##  Curves.stepsCurve<sup>9+</sup>

stepsCurve(count: number, end: boolean): ICurve


Creates a step curve.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type   | Mandatory| Description                                                        |
| ------ | ------- | ----| ------------------------------------------------------------ |
| count  | number  | Yes  | Number of steps. The value must be a positive integer.                                  |
| end    | boolean | Yes  | Whether jumping occurs when the interpolation ends.<br>- **true**: Jumping occurs when the interpolation ends.<br>- **false**: Jumping occurs when the interpolation starts.|

**Return value**

| Type                          | Description            |
| ---------------------------------- | ---------------- |
|  [ICurve](#icurve) | Interpolation curve.|


**Example**

```ts
import Curves from '@ohos.curves'
Curves.stepsCurve(9, true) // Create a step curve.
```


## Curves.cubicBezierCurve<sup>9+</sup>

cubicBezierCurve(x1: number, y1: number, x2: number, y2: number): ICurve


Creates a cubic Bezier curve. The curve values must be between 0 and 1.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**
| Name | Type    | Mandatory  | Description            |
| ---- | ------ | ---- | -------------- |
| x1   | number | Yes   | X coordinate of the first point on the Bezier curve.|
| y1   | number | Yes   | Y coordinate of the first point on the Bezier curve.|
| x2   | number | Yes   | X coordinate of the second point on the Bezier curve.|
| y2   | number | Yes   | Y coordinate of the second point on the Bezier curve.|

**Return value**

| Type                          | Description            |
| ---------------------------------- | ---------------- |
|  [ICurve](#icurve) | Interpolation curve.|


**Example**

```ts
import Curves from '@ohos.curves'
Curves.cubicBezierCurve(0.1, 0.0, 0.1, 1.0) // Create a cubic Bezier curve.
```


##  Curves.springCurve<sup>9+</sup>

springCurve(velocity: number, mass: number, stiffness: number, damping: number): ICurve


Creates a spring curve.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**
| Name      | Type    | Mandatory  | Description   |
| --------- | ------ | ---- | ----- |
| velocity  | number | Yes   | Initial velocity. It is applied by external factors to the elastic animation. It aims to help ensure the smooth transition from the previous motion state to the elastic animation.|
| mass      | number | Yes   | Mass, which influences the inertia in the spring system. The greater the mass, the greater the amplitude of the oscillation, and the slower the speed of restoring to the equilibrium position.|
| stiffness | number | Yes   | Stiffness. It is the degree to which an object deforms by resisting the force applied. In an elastic system, the greater the stiffness, the stronger the ability to resist deformation, and the faster the speed of restoring to the equilibrium position.|
| damping   | number | Yes   | Damping. It is a pure number and has no real physical meaning. It is used to describe the oscillation and attenuation of the system after being disturbed. The larger the damping, the smaller the number of oscillations of elastic motion, and the smaller the oscillation amplitude.|


**Return value**

| Type                          | Description            |
| ---------------------------------- | ---------------- |
|  [ICurve](#icurve)| Interpolation curve.|


**Example**

```ts
import Curves from '@ohos.curves'
Curves.springCurve(100, 1, 228, 30) // Create a spring curve.
```


##  Curves.springMotion<sup>9+</sup>

springMotion(response?: number, dampingFraction?: number, overlapDuration?: number): ICurve

Creates a spring animation curve. If multiple spring animations are applied to the same attribute of an object, each animation replaces their predecessor and inherits the velocity.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**
| Name      | Type    | Mandatory  | Description   |
| --------- | ------ | ---- | ----- |
| response  | number | No   | Duration of one complete oscillation, in seconds.<br>Default value: **0.55**|
| dampingFraction      | number | No   | Damping coefficient.<br>**0**: undamped. In this case, the spring oscillates forever.<br>> 0 and < 1: underdamped. In this case, the spring overshoots the equilibrium position.<br>**1**: critically damped.<br>> 1: overdamped. In this case, the spring approaches equilibrium gradually.<br>Default value: **0.825**|
| overlapDuration | number | No   | Duration for animations to overlap, in seconds. When animations overlap, if the **response** values of the two animations are different, they will transit smoothly over this duration.<br> Default value: **0**|


**Return value**

| Type                          | Description            |
| ---------------------------------- | ---------------- |
|  [ICurve](#icurve)| Curve.<br>Note: The spring animation curve is physics-based. Its duration depends on the **springMotion** parameters and the previous velocity, rather than the **duration** parameter in **animation** or **animateTo**. The time cannot be normalized. Therefore, the interpolation cannot be obtained by using the [interpolate](#interpolate) function of the curve.|

**Example**

```ts
import Curves from '@ohos.curves'
Curves.springMotion() // Create a spring animation curve with default settings.
Curves.springMotion(0.5) // Create a spring animation curve with the specified response value.
Curves.springMotion (0.5, 0.6) // Create a spring animation curve with the specified response and dampingFraction values.
Curves.springMotion(0.5, 0.6, 0) // Create a spring animation curve with the specified parameter values.
```


##  Curves.responsiveSpringMotion<sup>9+</sup>

responsiveSpringMotion(response?: number, dampingFraction?: number, overlapDuration?: number): ICurve

Creates a responsive spring animation curve. It is a special case of [springMotion](#curvesspringmotion9), with the only difference in the default values. It can be used together with **springMotion**.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**
| Name      | Type    | Mandatory  | Description   |
| --------- | ------ | ---- | ----- |
| response  | number | No   | See **response** in **springMotion**. Default value: **0.15**|
| dampingFraction      | number | No   | See **dampingFraction** in **springMotion**. Default value: **0.86**|
| overlapDuration | number | No   | See **overlapDuration** in **springMotion**. Default value: **0.25**|

**Return value**

| Type                          | Description            |
| ---------------------------------- | ---------------- |
|  [ICurve](#icurve)| Curve.<br>**NOTE**<br>1. To apply custom settings for a spring animation, you are advised to use **springMotion**. When using **responsiveSpringMotion**, you are advised to retain the default settings.<br>2. The duration of the responsive spring animation depends on the **responsiveSpringMotion** parameters and the previous velocity, rather than the **duration** parameter in **animation** or **animateTo**. In addition, the interpolation cannot be obtained by using the [interpolate](#interpolate) function of the curve.|

**Example**

```ts
import Curves from '@ohos.curves'
Curves.responsiveSpringMotion() // Create a responsive spring animation curve with default settings.
```


## ICurve


### interpolate

interpolate(fraction: number): number


Implements calculation.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name  | Type  | Mandatory| Description                                        |
| -------- | ------ | ---- | -------------------------------------------- |
| fraction | number | Yes  | Current normalized time. The value ranges from 0 to 1.|

**Return value**

| Type  | Description                                |
| ------ | ------------------------------------ |
| number | Curve interpolation corresponding to the normalized time point.|

**Example**

```ts
import Curves from '@ohos.curves'
let curve = Curves.initCurve(Curve.EaseIn) // Create an ease-in curve.
let value: number = curve.interpolate(0.5) // Calculate the interpolation for half of the time.
```


## Curves.init<sup>(deprecated)</sup>

init(curve?: Curve): string


Implements initialization to create a curve. This API is deprecated since API version 9. You are advised to use [Curves.initCurve](#curvesinitcurve9) instead.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type                                                        | Mandatory| Default Value      | Description      |
| ------ | ------------------------------------------------------------ | ---- | ------------ | ---------- |
| curve  |[Curve](../arkui-ts/ts-appendix-enums.md#curve) | No  | Curve.Linear | Curve type.|


## Curves.steps<sup>(deprecated)</sup>

steps(count: number, end: boolean): string


Creates a step curve. This API is deprecated since API version 9. You are advised to use [Curves.stepsCurve](#curvesstepscurve9) instead.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type   | Mandatory| Description                                                        |
| ------ | ------- | ----| ------------------------------------------------------------ |
| count  | number  | Yes  | Number of steps. The value must be a positive integer.                                  |
| end    | boolean | Yes  | Whether jumping occurs when the interpolation ends.<br>- **true**: Jumping occurs when the interpolation ends.<br>- **false**: Jumping occurs when the interpolation starts.|


## Curves.cubicBezier<sup>(deprecated)</sup>

cubicBezier(x1: number, y1: number, x2: number, y2: number): string


Creates a cubic Bezier curve. The curve value must range from 0 to 1. This API is deprecated since API version 9. You are advised to use [Curves.cubicBezierCurve](#curvescubicbeziercurve9) instead.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**
| Name | Type    | Mandatory  | Description            |
| ---- | ------ | ---- | -------------- |
| x1   | number | Yes   | X coordinate of the first point on the Bezier curve.|
| y1   | number | Yes   | Y coordinate of the first point on the Bezier curve.|
| x2   | number | Yes   | X coordinate of the second point on the Bezier curve.|
| y2   | number | Yes   | Y coordinate of the second point on the Bezier curve.|


## Curves.spring<sup>(deprecated)</sup>

spring(velocity: number, mass: number, stiffness: number, damping: number): string


Creates a spring curve. This API is deprecated since API version 9. You are advised to use [Curves.springCurve](#curvesspringcurve9) instead.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name      | Type    | Mandatory  | Description   |
| --------- | ------ | ---- | ----- |
| velocity  | number | Yes   | Initial velocity. It is applied by external factors to the elastic animation. It aims to help ensure the smooth transition from the previous motion state to the elastic animation.|
| mass      | number | Yes   | Mass, which influences the inertia in the spring system. The greater the mass, the greater the amplitude of the oscillation, and the slower the speed of restoring to the equilibrium position.|
| stiffness | number | Yes   | Stiffness. It is the degree to which an object deforms by resisting the force applied. In an elastic system, the greater the stiffness, the stronger the ability to resist deformation, and the faster the speed of restoring to the equilibrium position.|
| damping   | number | Yes   | Damping. It is a pure number and has no real physical meaning. It is used to describe the oscillation and attenuation of the system after being disturbed. The larger the damping, the smaller the number of oscillations of elastic motion, and the smaller the oscillation amplitude.|

## Example

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

![en-us_image_0000001174104410](figures/en-us_image_0000001174104410.gif)

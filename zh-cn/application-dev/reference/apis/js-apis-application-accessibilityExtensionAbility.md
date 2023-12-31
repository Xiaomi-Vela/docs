# @ohos.application.AccessibilityExtensionAbility (辅助功能扩展能力)

**AccessibilityExtensionAbility**基于ExtensionAbility框架，提供辅助功能业务的能力。

> **说明：**
>
> 本模块首批接口从API version 9开始支持，后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import AccessibilityExtensionAbility from '@ohos.application.AccessibilityExtensionAbility';
```

### 属性

**系统能力：** SystemCapability.BarrierFree.Accessibility.Core

| 名称      | 类型                                       | 可读   | 可写   | 说明           |
| ------- | ---------------------------------------- | ---- | ---- | ------------ |
| context | [AccessibilityExtensionContext](js-apis-inner-application-accessibilityExtensionContext.md) | 是    | 否    | 表示辅助扩展能力上下文。 |

## AccessibilityEvent

辅助事件信息。

**系统能力**：以下各项对应的系统能力均为 SystemCapability.BarrierFree.Accessibility.Core

### 属性

| 名称      | 类型                                                         | 可读 | 可写 | 说明                                                         |
| --------- | ------------------------------------------------------------ | ---- | ---- | ------------------------------------------------------------ |
| eventType | [accessibility.EventType](js-apis-accessibility.md#EventType) \| [accessibility.WindowUpdateType](js-apis-accessibility.md#WindowUpdateType)\| [TouchGuideType](#touchguidetype) \| [GestureType](#gesturetype) \| [PageUpdateType](#pageupdatetype) | 是   | 否   | 具体事件类型。<br />EventType：无障碍事件类型；<br />WindowUpdateType：窗口变化类型；TouchGuideType：触摸浏览事件类型；<br />GestureType：手势事件类型；<br />PageUpdateType：页面刷新类型，当前版本暂不支持。 |
| target    | [AccessibilityElement](js-apis-inner-application-accessibilityExtensionContext.md#accessibilityelement9) | 是   | 否   | 发生事件的目标组件。                                         |
| timeStamp | number                                                       | 是   | 否   | 事件时间戳。                                                 |


## AccessibilityElement<sup>10+</sup>

[AccessibilityElement](js-apis-inner-application-accessibilityExtensionContext.md#accessibilityelement9)二级模块

**示例：**

```ts
import { AccessibilityElement } from '@ohos.application.AccessibilityExtensionAbility';

let AccessibilityElement: AccessibilityElement;
```

## ElementAttributeValues<sup>10+</sup>

[ElementAttributeValues](js-apis-inner-application-accessibilityExtensionContext.md#elementattributevalues)二级模块

**示例：**

```ts
import { ElementAttributeValues } from '@ohos.application.AccessibilityExtensionAbility';

let ElementAttributeValues: ElementAttributeValues;
```

## FocusDirection<sup>10+</sup>

[FocusDirection](js-apis-inner-application-accessibilityExtensionContext.md#focusdirection)二级模块，表示查询下一焦点元素的方向。

**示例：**

```ts
import { FocusDirection } from '@ohos.application.AccessibilityExtensionAbility';

let FocusDirection: FocusDirection;
```

## ElementAttributeKeys<sup>10+</sup>

ElementAttributeKeys keyof [ElementAttributeValues](js-apis-inner-application-accessibilityExtensionContext.md#elementattributevalues)

**示例：**

```ts
import { ElementAttributeKeys } from '@ohos.application.AccessibilityExtensionAbility';

let ElementAttributeKeys: ElementAttributeKeys;
```

## FocusType<sup>10+</sup>

[FocusType](js-apis-inner-application-accessibilityExtensionContext.md#focustype)二级模块，表示查询焦点元素的类型。

**示例：**

```ts
import { FocusType } from '@ohos.application.AccessibilityExtensionAbility';

let FocusType: FocusType;
```

## WindowType <sup>10+</sup>

[WindowType](js-apis-inner-application-accessibilityExtensionContext.md#windowtype)二级模块，表示窗口的类型。

**示例：**

```ts
import { WindowType } from '@ohos.application.AccessibilityExtensionAbility';

let WindowType: WindowType;
```

## Rect<sup>10+</sup>

[Rect](js-apis-inner-application-accessibilityExtensionContext.md#rect)二级模块，表示矩形区域。

**示例：**

```ts
import { Rect } from '@ohos.application.AccessibilityExtensionAbility';

let Rect: Rect;
```

## GestureType

手势事件类型。

**系统能力**：以下各项对应的系统能力均为 SystemCapability.BarrierFree.Accessibility.Core

| 名称            | 类型            | 描述                  |
| ------------- | ------------- | ------------------- |
| left          | string          | 表示向左的手势。     |
| leftThenRight | string          | 表示先向左再向右的手势。 |
| leftThenUp    | string          | 表示先向左再向上的手势。 |
| leftThenDown  | string          | 表示先向左再向下的手势。 |
| right         | string          | 表示向右的手势。     |
| rightThenLeft | string          | 表示先向右再向左的手势。 |
| rightThenUp   | string          | 表示先向右再向上的手势。 |
| rightThenDown | string          | 表示先向右再向下的手势。 |
| up            | string          | 表示向上的手势。     |
| upThenLeft    | string          | 表示先向上再向左的手势。 |
| upThenRight   | string          | 表示先向上再向右的手势。 |
| upThenDown    | string          | 表示先向上再向下的手势。 |
| down          | string          | 表示向下的手势。     |
| downThenLeft  | string          | 表示先向下再向左的手势。 |
| downThenRight | string          | 表示先向下再向右的手势。 |
| downThenUp    | string          | 表示先向下再向上的手势。 |
| twoFingerSingleTap<sup>11+</sup>    | string          | 表示双指单击的手势。 |
| twoFingerDoubleTap<sup>11+</sup>    | string          | 表示双指双击的手势。 |
| twoFingerDoubleTapAndHold<sup>11+</sup>    | string          | 表示双指双击长按的手势。 |
| twoFingerTripleTap<sup>11+</sup>    | string          | 表示双指三击的手势。 |
| twoFingerTripleTapAndHold<sup>11+</sup>    | string          | 表示双指三击长按的手势。 |
| threeFingerSingleTap<sup>11+</sup>    | string          | 表示三指单击的手势。 |
| threeFingerDoubleTap<sup>11+</sup>    | string          | 表示三指双击的手势。 |
| threeFingerDoubleTapAndHold<sup>11+</sup>    | string          | 表示三指双击长按的手势。 |
| threeFingerTripleTap<sup>11+</sup>    | string          | 表示三指三击的手势。 |
| threeFingerTripleTapAndHold<sup>11+</sup>    | string          | 表示三指三击长按的手势。 |
| fourFingerSingleTap<sup>11+</sup>    | string          | 表示四指单击的手势。 |
| fourFingerDoubleTap<sup>11+</sup>    | string          | 表示四指双击的手势。 |
| fourFingerDoubleTapAndHold<sup>11+</sup>    | string          | 表示四指双击长按的手势。 |
| fourFingerTripleTap<sup>11+</sup>    | string          | 表示四指三击的手势。 |
| fourFingerTripleTapAndHold<sup>11+</sup>    | string          | 表示四指三击长按的手势。 |
| threeFingerSwiperUp<sup>11+</sup>    | string          | 表示三指向上滑动的手势。 |
| threeFingerSwiperDown<sup>11+</sup>    | string          | 表示三指向下滑动的手势。 |
| threeFingerSwiperLeft<sup>11+</sup>    | string          | 表示三指向左滑动的手势。 |
| threeFingerSwiperRight<sup>11+</sup>    | string          | 表示三指向右滑动的手势。 |
| fourFingerSwiperUp<sup>11+</sup>    | string          | 表示四指向上滑动的手势。 |
| fourFingerSwiperDown<sup>11+</sup>    | string          | 表示四指向下滑动的手势。 |
| fourFingerSwiperLeft<sup>11+</sup>    | string          | 表示四指向左滑动的手势。 |
| fourFingerSwiperRight<sup>11+</sup>    | string          | 表示四指向右滑动的手势。 |

## PageUpdateType

页面刷新类型；当前版本暂不支持。

**系统能力**：以下各项对应的系统能力均为 SystemCapability.BarrierFree.Accessibility.Core

| 名称                | 类型                | 描述               |
| ----------------- | ----------------- | ---------------- |
| pageContentUpdate | string | 表示页面内容刷新。 |
| pageStateUpdate   | string | 表示页面状态刷新。 |

## TouchGuideType

触摸浏览事件类型。

**系统能力**：以下各项对应的系统能力均为 SystemCapability.BarrierFree.Accessibility.Core

| 名称         | 类型                | 描述                  |
| ---------- | ---------- | ------------------- |
| touchBegin | string | 表示触摸浏览时开始触摸。 |
| touchEnd   | string | 表示触摸浏览时结束触摸。 |

## AccessibilityExtensionAbility.onConnect

onConnect(): void;

用户启用AccessibilityExtensionAbility时，系统服务完成连接后，回调此接口，可以该方法中执行初始化业务逻辑操作。该方法可以选择性重写。

**系统能力：**  SystemCapability.BarrierFree.Accessibility.Core

**示例：**

```ts
import AccessibilityExtensionAbility from '@ohos.application.AccessibilityExtensionAbility';

class MyAccessibilityExtensionAbility extends AccessibilityExtensionAbility {
  onConnect(): void {
    console.log('AxExtensionAbility onConnect');
  }
}
```

## AccessibilityExtensionAbility.onDisconnect

onDisconnect(): void;

用户停用AccessibilityExtensionAbility时，系统服务完成断开连接后，回调此接口，可以该方法中执行资源回收退出业务逻辑操作。该方法可以选择性重写。

**系统能力：**  SystemCapability.BarrierFree.Accessibility.Core

**示例：**

```ts
import AccessibilityExtensionAbility from '@ohos.application.AccessibilityExtensionAbility';

class MyAccessibilityExtensionAbility extends AccessibilityExtensionAbility {
  onDisconnect(): void {
    console.log('AxExtensionAbility onDisconnect');
  }
}
```

## AccessibilityExtensionAbility.onAccessibilityEvent

onAccessibilityEvent(event: AccessibilityEvent): void;

在关注的应用及事件类型对应的事件发生时回调此接口，可以在该方法中根据事件信息进行业务逻辑处理。一般情况下需要重写该方法完成业务。

**系统能力：**  SystemCapability.BarrierFree.Accessibility.Core

**参数：**

| 参数名   | 类型                                       | 必填   | 说明              |
| ----- | ---------------------------------------- | ---- | --------------- |
| event | [AccessibilityEvent](#accessibilityevent) | 是    | 无障碍事件回调函数。无返回值。 |

**示例：**

```ts
import AccessibilityExtensionAbility , { AccessibilityEvent } from '@ohos.application.AccessibilityExtensionAbility';

class MyAccessibilityExtensionAbility extends AccessibilityExtensionAbility {
  onAccessibilityEvent(event: AccessibilityEvent): void {
    console.log('AxExtensionAbility onAccessibilityEvent');
    if (event.eventType === 'click') {
      console.log('AxExtensionAbility onAccessibilityEvent: click');
    }
  }
}
```

## AccessibilityExtensionAbility.onKeyEvent

onKeyEvent(keyEvent: KeyEvent): boolean;

在物理按键按下时回调此方法，可以在该方法中根据业务判断是否对事件进行拦截。

**系统能力：**  SystemCapability.BarrierFree.Accessibility.Core

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                      |
| -------- | ---------------------------------------- | ---- | ----------------------- |
| keyEvent | [KeyEvent](js-apis-keyevent.md#keyevent) | 是    | 按键事件回调函数。返回true表示拦截此按键。 |

**示例：**

```ts
import AccessibilityExtensionAbility from '@ohos.application.AccessibilityExtensionAbility';
import { KeyEvent } from '@ohos.multimodalInput.keyEvent';

class MyAccessibilityExtensionAbility extends AccessibilityExtensionAbility {
  onKeyEvent(keyEvent: KeyEvent): boolean {
    console.log('AxExtensionAbility onKeyEvent');
    if (keyEvent.key.code === 16) {
      console.log('AxExtensionAbility onKeyEvent: intercept 16');
      return true;
    }
    return false;
  }
}
```

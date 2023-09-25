# @ohos.multimodalInput.inputEventClient (设备注入)

设备注入模块，提供设备注入能力。

> **说明：**
>
> - 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>
> - 本模块接口为系统接口。

## 导入模块

```js
import inputEventClient from '@ohos.multimodalInput.inputEventClient';
```

## inputEventClient.injectEvent

injectEvent({KeyEvent: KeyEvent}): void

按键(包括单个按键和组合键)注入。

**系统能力：** SystemCapability.MultimodalInput.Input.InputSimulator

**参数：**

| 参数名       | 类型                    | 必填   | 说明        |
| -------- | --------------------- | ---- | --------- |
| KeyEvent | [KeyEvent](#keyevent) | 是    | 按键注入描述信息。 |

**示例：**

```js
try {
  let backKeyDown: inputEventClient.KeyEvent = {
    isPressed: true,
    keyCode: 2,
    keyDownDuration: 0,
    isIntercepted: false
  }
  inputEventClient.injectEvent({ KeyEvent: backKeyDown });

  let backKeyUp: inputEventClient.KeyEvent = {
    isPressed: false,
    keyCode: 2,
    keyDownDuration: 0,
    isIntercepted: false
  };
  inputEventClient.injectEvent({ KeyEvent: backKeyUp });
} catch (error) {
  console.log(`Failed to inject KeyEvent, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```
## inputEventClient.injectMouseEvent<sup>11+</sup>

injectMouseEvent({mouseEvent: MouseEvent}): void;

鼠标/触摸板事件注入。

**系统能力：** SystemCapability.MultimodalInput.Input.InputSimulator

**参数：**

| 参数名       | 类型                    | 必填   | 说明        |
| -------- | --------------------- | ---- | --------- |
| mouseEvent | [MouseEvent](../apis/js-apis-mouseevent.md) | 是    | 鼠标/触摸板事件注入描述信息。 |

**示例：**

```js
try {
  let mouseButtonUp = {
      action: 2,
      screenX: 200,
      screenY: 620,
      button: 0,
      toolType: 1,
  }
  inputEventClient.injectMouseEvent({ mouseEvent: mouseButtonUp });

  let mouseButtonDown = {
      action: 3,
      screenX: 200,
      screenY: 620,
      button: 0,
      toolType: 1,
  };
  inputEventClient.injectMouseEvent({ mouseEvent: mouseButtonDown });
} catch (error) {
  console.log(`Failed to inject MouseEvent, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputEventClient.injectTouchEvent<sup>11+</sup>

injectTouchEvent({touchEvent: TouchEvent}): void;

触摸屏事件注入。

**系统能力：** SystemCapability.MultimodalInput.Input.InputSimulator

**参数：**

| 参数名       | 类型                    | 必填   | 说明        |
| -------- | --------------------- | ---- | --------- |
| touchEvent | [TouchEvent](../apis/js-apis-touchevent.md) | 是    | 触摸屏事件注入描述信息。 |

**示例：**

```js
try {
  let touchEventUp = {
      action: 1,
      sourceType: 0,
      screenX: 200,
      screenY: 620,
      pressedTime: 0,
  };
  inputEventClient.injectTouchEvent({ touchEvent: touchEventUp });

  let touchEventDown = {
      action: 3,
      sourceType: 0,
      screenX: 200,
      screenY: 620,
      pressedTime: 0,
  };
    inputEventClient.injectTouchEvent({ touchEvent: touchEventDown });
} catch (error) {
    console.log(`Failed to inject touchEvent, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## KeyEvent

按键注入描述信息。

**系统能力：** SystemCapability.MultimodalInput.Input.InputSimulator

| 名称        | 类型   | 可读   | 可写   | 说明      |
| --------- | ------ | ---- | ---- | ------- |
| isPressed       | boolean | 是    |  否 | 按键是否按下。<br>ture表示按键按下，false表示按键抬起。   |
| keyCode         | number  | 是    |  否 | 按键键码值。当前仅支持返回键/KEYCODE_BACK键。 |
| keyDownDuration | number  | 是    |  否 | 按键按下持续时间，单位为微秒（μs）。           |
| isIntercepted   | boolean | 是    |  否 | 按键是否可以被拦截。<br>ture表示可以被拦截，false表示不可被拦截。 |


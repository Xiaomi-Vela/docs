# 有源标签

本模块提供有源标签的使用，包括初始化有源标签芯片、读取有源标签内容、写入内容到有源标签等。

> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```js
import connectedTag from '@ohos.connectedTag';
```

## connectedTag.init

init(): boolean

初始化有源标签芯片。

**需要权限**：ohos.permission.NFC_TAG

**系统能力**：SystemCapability.Communication.ConnectedTag

**返回值：**

| **类型** | **说明** |
| -------- | -------- |
| boolean | true:初始化成功，&nbsp;false:初始化失败。 |

## connectedTag.uninit

uninit(): boolean

卸载有源标签芯片资源。

**需要权限**：ohos.permission.NFC_TAG

**系统能力**：SystemCapability.Communication.ConnectedTag

**返回值：**

| **类型** | **说明** |
| -------- | -------- |
| boolean | true:卸载操作成功，&nbsp;false:卸载操作失败。 |

## connectedTag.readNdefTag

readNdefTag(): Promise&lt;string&gt;

读取有源标签内容，使用promise方式作为异步方法。

**需要权限**：ohos.permission.NFC_TAG

**系统能力**：SystemCapability.Communication.ConnectedTag

**返回值：**

| **类型** | **说明** |
| -------- | -------- |
| Promise&lt;string&gt; | 返回读取有源标签内容。 |

**示例：**

```js
import connectedTag from '@ohos.connectedTag';

connectedTag.readNdefTag().then(result => {
    console.log("promise recv ndef response: " + result);
});
```

## connectedTag.readNdefTag

readNdefTag(callback: AsyncCallback&lt;string&gt;): void

读取有源标签内容，使用callback方式作为异步方法。

**需要权限**：ohos.permission.NFC_TAG

**系统能力**：SystemCapability.Communication.ConnectedTag

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;string&gt; | 是 | 读取有源标签内容回调函数。 |

**示例：**

```js
import connectedTag from '@ohos.connectedTag';

connectedTag.readNdefTag(result => {
    console.log("callback recv ndef response: " + result);
});
```

## connectedTag.writeNdefTag

writeNdefTag(data: string): Promise&lt;void&gt;

写入内容到有源标签，使用promise方式作为异步方法。

**需要权限**：ohos.permission.NFC_TAG

**系统能力**：SystemCapability.Communication.ConnectedTag

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| data | string | 是 | 有源标签内容, 长度最大是1024个字节。 |

**返回值：**

| **类型** | **说明** |
| -------- | -------- |
| Promise&lt;void&gt; | 无返回值。 |

**示例：**

```js
import connectedTag from '@ohos.connectedTag';

connectedTag.write("010203")
    .then((value) => {
        // 事件写入正常
        console.log(`success to write event: ${value}`);
    }).catch((err) => {
        // 事件写入异常
        console.error(`failed to write event because ${err.code}`);
    });
```

## connectedTag.writeNdefTag

writeNdefTag(data: string, callback: AsyncCallback&lt;void&gt;): void

写入内容到有源标签，使用callback方式作为异步方法。

**需要权限**：ohos.permission.NFC_TAG

**系统能力**：SystemCapability.Communication.ConnectedTag

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| data | string | 是 | 有源标签内容, 长度最大是1024个字节。 |
| callback | AsyncCallback&lt;string&gt; | 是 | 读取有源标签内容回调函数。 |

**示例：**

```js
import connectedTag from '@ohos.connectedTag';

connectedTag.writeNdefTag("010203", (err, value) => {
    if (err) {
        // 事件写入异常
        console.error(`failed to write event because ${err.code}`);
        return;
    }

    // 事件写入正常
    console.log(`success to write event: ${value}`);
});
```

## connectedTag.on('notify')

on(type: "notify", callback: Callback&lt;number&gt;): void

注册NFC场强状态事件。

**需要权限**：ohos.permission.NFC_TAG

**系统能力**：SystemCapability.Communication.ConnectedTag

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 固定填"notify"字符串 |
| callback | Callback&lt;number&gt; | 是 | 状态改变回调函数，返回值参见[NfcRfType](#nfcrftype)。 |

## connectedTag.off('notify')

off(type: "notify", callback?: Callback&lt;number&gt;): void

取消NFC场强状态事件的注册。

**需要权限**：ohos.permission.NFC_TAG

**系统能力**：SystemCapability.Communication.ConnectedTag

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 固定填"notify"字符串 |
| callback | Callback&lt;number&gt; | 否 | 状态改变回调函数。如果callback不填，将“去注册”该事件关联的所有回调函数。|

**示例：**

```js
import connectedTag from '@ohos.connectedTag';

var recvNfcRfNotifyFunc = result => {
    console.info("nfc rf receive state: " + result);
}
  
// Register event
connectedTag.on("notify", recvNfcRfNotifyFunc);

// Unregister event
connectedTag.off("notify", recvNfcRfNotifyFunc);
```

## NfcRfType

表示NFC场强状态的枚举。

**系统能力**：SystemCapability.Communication.ConnectedTag

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| NFC_RF_LEAVE | 0 | NFC离场事件 |
| NFC_RF_ENTER | 1 | NFC进场事件 |

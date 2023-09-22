# @ohos.identifier.oaid (广告标识服务)


本模块提供开放匿名设备标识符（Open Anonymous Device Identifier, OAID，以下简称OAID）的获取和重置能力。


> **说明：**
> 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```
import identifier from '@ohos.identifier.oaid';
```


## identifer.getOAID

getOAID():Promise&lt;string&gt;

获取开放匿名设备标识符（Open Anonymous Device Identifier, OAID）。

**模型约束：**此接口仅可在Stage模型下使用。

**需要权限：**ohos.permission.APP_TRACKING_CONSENT

**系统能力：**SystemCapability.Advertising.OAID

**返回值：**

| 类型 | 说明 | 
| -------- | -------- |
| Promise&lt;string&gt; | Promise对象。返回开放匿名设备标识符（Open&nbsp;Anonymous&nbsp;Device&nbsp;Identifier,&nbsp;OAID）。 | 

**错误码：**

以下错误码的详细介绍请参见[广告标识服务错误码参考](../errorcodes/errorcode-oaid.md)。

| 错误码ID | 错误信息 | 
| -------- | -------- |
| 17300001 | System&nbsp;internal&nbsp;error. | 

**示例：**
```
import identifier from '@ohos.identifier.oaid';
import hilog from '@ohos.hilog'; 
import { BusinessError } from '@ohos.base';
 
try {  
  identifier.getOAID().then((data) => {
    const oaid: string = data;
    hilog.info(0x0000, 'testTag', '%{public}s', `get oaid by callback success`);
  }).catch((err) => {
    hilog.info(0x0000, 'testTag', '%{public}s', `get oaid failed, message: ${(err as BusinessError).message}`);
  })
} catch (err) {
  const e: BusinessError = err as BusinessError;
  hilog.error(0x0000, 'testTag', 'get oaid catch error: %{public}d %{public}s', e.code, e.message);
}
```


## identifer.getOAID

getOAID(callback: AsyncCallback&lt;string&gt;): void

获取开放匿名设备标识符（Open Anonymous Device Identifier, OAID）。

**模型约束：**此接口仅可在Stage模型下使用。

**需要权限：**ohos.permission.APP_TRACKING_CONSENT

**系统能力：**SystemCapability.Advertising.OAID

**参数：**


| **参数**名 | **类型** | 必填 | 说明 | 
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;string&gt; | 是 | 获取开放匿名设备标识符（Open&nbsp;Anonymous&nbsp;Device&nbsp;Identifier,&nbsp;OAID）的回调函数。 | 


**错误码：**


以下错误码的详细介绍请参见[广告标识服务错误码参考](../errorcodes/errorcode-oaid.md)。


| 错误码ID | 错误信息 | 
| -------- | -------- |
| 17300001 | System&nbsp;internal&nbsp;error. | 


**示例：**
```
import identifier from '@ohos.identifier.oaid';
import hilog from '@ohos.hilog'; 
import { BusinessError } from '@ohos.base';
 
try {
  identifier.getOAID((err, data) => {
    if (err.code) {
      hilog.info(0x0000, 'testTag', '%{public}s', `get oaid failed, message: ${err.message}`);
    } else {
      const oaid: string = data;
      hilog.info(0x0000, 'testTag', '%{public}s', `get oaid by callback success`);
    }
   });
} catch (err) {
  const e: BusinessError = err as BusinessError;
  hilog.error(0x0000, 'testTag', 'get oaid catch error: %{public}d %{public}s', e.code, e.message);
}
```


## identifer.resetOAID

resetOAID(): void

重置开放匿名设备标识符（Open Anonymous Device Identifier, OAID）。

**系统接口：** 此接口为系统接口。

**模型约束：**此接口仅可在Stage模型下使用。

**需要权限：**ohos.permission.APP_TRACKING_CONSENT

**系统能力：**SystemCapability.Advertising.OAID

**错误码：**

以下错误码的详细介绍请参见[广告标识服务错误码参考](../errorcodes/errorcode-oaid.md)。

| 错误码ID | 错误信息 | 
| -------- | -------- |
| 17300001 | System&nbsp;internal&nbsp;error. | 

**示例：**
```
import identifier from '@ohos.identifier.oaid';
import hilog from '@ohos.hilog'; 
import { BusinessError } from '@ohos.base';

try {
  identifier.resetOAID();
} catch (err) {
  const e: BusinessError = err as BusinessError;
  hilog.error(0x0000, 'testTag', 'reset oaid catch error: %{public}d %{public}s', e.code, e.message);
}
```

# @ohos.identifier.oaid (OAID)


The **OAID** module provides APIs for obtaining and resetting Open Anonymous Device Identifiers (OAIDs).


> **NOTE**
>
> The initial APIs of this module are supported since API version 10. Newly added APIs will be marked with a superscript to indicate their earliest API version.


## Modules to Import

```
import identifier from '@ohos.identifier.oaid';
```


## identifier.getOAID

getOAID():Promise&lt;string&gt;

Obtains an OAID. This API uses a promise to return the result.

**Model restriction**: This API can be used only in the stage model.

**Required permissions**: ohos.permission.APP_TRACKING_CONSENT

**System capability**: SystemCapability.Advertising.OAID

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;string&gt; | Promise used to return the OAID.|

**Error codes**

For details about the following error codes, see [OAID Error Codes](../errorcodes/errorcode-oaid.md).

| ID| Error Message|
| -------- | -------- |
| 17300001 | System&nbsp;internal&nbsp;error. |

**Example**
```
import identifier from '@ohos.identifier.oaid';
import hilog from '@ohos.hilog'; 
import { BusinessError } from '@ohos.base';
 
try {  
  identifier.getOAID().then((data) => {
    const oaid: string = data;
    hilog.info(0x0000, 'testTag', '%{public}s', `get oaid by callback success`);
  }).catch((err: BusinessError) => {
    hilog.info(0x0000, 'testTag', '%{public}s', `get oaid failed, message: ${err.message}`);
  })
} catch (err: BusinessError) {
  hilog.error(0x0000, 'testTag', 'get oaid catch error: %{public}d %{public}s', err.code, err.message);
}
```


## identifier.getOAID

getOAID(callback: AsyncCallback&lt;string&gt;): void

Obtains an OAID. This API uses an asynchronous callback to return the result.

**Model restriction**: This API can be used only in the stage model.

**Required permissions**: ohos.permission.APP_TRACKING_CONSENT

**System capability**: SystemCapability.Advertising.OAID

**Parameters**


| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;string&gt; | Yes| Callback used to return the OAID.|


**Error codes**


For details about the following error codes, see [OAID Error Codes](../errorcodes/errorcode-oaid.md).


| ID| Error Message|
| -------- | -------- |
| 17300001 | System&nbsp;internal&nbsp;error. |


**Example**
```
import identifier from '@ohos.identifier.oaid';
import hilog from '@ohos.hilog'; 
import { BusinessError } from '@ohos.base';
 
try {
  identifier.getOAID((err: BusinessError, data) => {
    if (err.code) {
      hilog.info(0x0000, 'testTag', '%{public}s', `get oaid failed, message: ${err.message}`);
    } else {
      const oaid: string = data;
      hilog.info(0x0000, 'testTag', '%{public}s', `get oaid by callback success`);
    }
   });
} catch (err: BusinessError) {
  hilog.error(0x0000, 'testTag', 'get oaid catch error: %{public}d %{public}s', err.code, err.message);
}
```


## identifier.resetOAID

resetOAID(): void

Resets an OAID.

**System API**: This is a system API.

**Model restriction**: This API can be used only in the stage model.

**Required permissions**: ohos.permission.APP_TRACKING_CONSENT

**System capability**: SystemCapability.Advertising.OAID

**Error codes**

For details about the following error codes, see [OAID Error Codes](../errorcodes/errorcode-oaid.md).

| ID| Error Message|
| -------- | -------- |
| 17300001 | System&nbsp;internal&nbsp;error. |

**Example**
```
import identifier from '@ohos.identifier.oaid';
import hilog from '@ohos.hilog'; 
import { BusinessError } from '@ohos.base';

try {
  identifier.resetOAID();
} catch (err: BusinessError) {
  hilog.error(0x0000, 'testTag', 'reset oaid catch error: %{public}d %{public}s', err.code, err.message);
}
```
# @ohos.resourceManager (Resource Management)

The **resourceManager** module provides APIs to obtain information about application resources based on the current configuration, including the language, region, screen direction, MCC/MNC, as well as device capability and density.

> **NOTE**
>
> The initial APIs of this module are supported since API version 6. Newly added APIs will be marked with a superscript to indicate their earliest API version.


## Modules to Import

```js
import resourceManager from '@ohos.resourceManager';
```

## How to Use

Since API version 9, the stage model allows an application to obtain a **ResourceManager** object based on **context** and call its resource management APIs without first importing the required bundle. This approach, however, is not applicable to the FA model. For the FA model, you need to import the required bundle and then call the [getResourceManager](#resourcemanagergetresourcemanager) API to obtain a **ResourceManager** object.
For details about how to reference context in the stage model, see [Context in the Stage Model](../../application-models/application-context-stage.md).

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';

export default class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    let context = this.context;
    let resourceManager = context.resourceManager;
  }
}
```

## resourceManager.getResourceManager

getResourceManager(callback: AsyncCallback&lt;ResourceManager&gt;): void

Obtains the **ResourceManager** object of this application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the FA model.

**Parameters**

| Name     | Type                                      | Mandatory  | Description                           |
| -------- | ---------------------------------------- | ---- | ----------------------------- |
| callback | AsyncCallback&lt;[ResourceManager](#resourcemanager)&gt; | Yes   | Callback used to return the result.|

**Example**
  ```js
  resourceManager.getResourceManager((error, mgr) => {
    if (error != null) {
      console.log("error is " + error);
      return;
    }
    mgr.getStringValue(0x1000000, (error, value) => {
      if (error != null) {
        console.log("error is " + error);
      } else {
        let str = value;
      }
    });
  });
  ```
> **NOTE**<br>In the sample code, **0x1000000** indicates the resource ID, which can be found in the compiled **ResourceTable.txt** file.


## resourceManager.getResourceManager

getResourceManager(bundleName: string, callback: AsyncCallback&lt;ResourceManager&gt;): void

Obtains the **ResourceManager** object of an application based on the specified bundle name. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the FA model.

**Parameters**

| Name       | Type                                      | Mandatory  | Description                           |
| ---------- | ---------------------------------------- | ---- | ----------------------------- |
| bundleName | string                                   | Yes   | Bundle name of the application.                |
| callback   | AsyncCallback&lt;[ResourceManager](#resourcemanager)&gt; | Yes   | Callback used to return the result.|

**Example**
  ```js
  resourceManager.getResourceManager("com.example.myapplication", (error, mgr) => {
  });
  ```


## resourceManager.getResourceManager

getResourceManager(): Promise&lt;ResourceManager&gt;

Obtains the **ResourceManager** object of this application. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the FA model.

**Return value**

| Type                                      | Description               |
| ---------------------------------------- | ----------------- |
| Promise&lt;[ResourceManager](#resourcemanager)&gt; | Promise used to return the result.|

**Example**
  ```js
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  resourceManager.getResourceManager().then((mgr: resourceManager.ResourceManager) => {
    mgr.getStringValue(0x1000000, (error, value) => {
      if (error != null) {
        console.log("error is " + error);
      } else {
        let str = value;
      }
    });
  }).catch((error: BusinessError) => {
    console.log("error is " + error);
  });
  ```
> **NOTE**<br>In the sample code, **0x1000000** indicates the resource ID, which can be found in the compiled **ResourceTable.txt** file.


## resourceManager.getResourceManager

getResourceManager(bundleName: string): Promise&lt;ResourceManager&gt;

Obtains the **ResourceManager** object of an application based on the specified bundle name. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the FA model.

**Parameters**

| Name       | Type    | Mandatory  | Description           |
| ---------- | ------ | ---- | ------------- |
| bundleName | string | Yes   | Bundle name of the application.|

**Return value**

| Type                                      | Description                |
| ---------------------------------------- | ------------------ |
| Promise&lt;[ResourceManager](#resourcemanager)&gt; | Promise used to return the result.|

**Example**
  ```js
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  resourceManager.getResourceManager("com.example.myapplication").then((mgr: resourceManager.ResourceManager) => {
  }).catch((error: BusinessError) => {
  });
  ```

## resourceManager.getSystemResourceManager<sup>10+</sup>

getSystemResourceManager(): ResourceManager

Obtains a **ResourceManager** object.

**System capability**: SystemCapability.Global.ResourceManager

**Return value**

| Type                                      | Description                |
| ---------------------------------------- | ------------------ |
| [Resourcemanager](#resourcemanager) | **ResourceManager** object.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001009  | If application can't access system resource.                       |

**Example**
  ```js
import resourceManager from '@ohos.resourceManager';
import { BusinessError } from '@ohos.base';

  try {
    let systemResourceManager = resourceManager.getSystemResourceManager();
    systemResourceManager.getStringValue($r('sys.string.ohos_lab_vibrate').id).then((value: string) => {
      let str = value;
    }).catch((error: BusinessError) => {
      console.log("systemResourceManager getStringValue promise error is " + error);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`systemResourceManager getStringValue failed, error code: ${code}, message: ${message}.`);
  }
  ```


## Direction

Enumerates the screen directions.

**System capability**: SystemCapability.Global.ResourceManager

| Name                  | Value | Description  |
| -------------------- | ---- | ---- |
| DIRECTION_VERTICAL   | 0    | Portrait.  |
| DIRECTION_HORIZONTAL | 1    | Landscape.  |


## DeviceType

Enumerates the device types.

**System capability**: SystemCapability.Global.ResourceManager

| Name                  | Value | Description  |
| -------------------- | ---- | ---- |
| DEVICE_TYPE_TABLET   | 0x01 | Tablet.  |
| DEVICE_TYPE_CAR      | 0x02 | Head unit.  |
| DEVICE_TYPE_TV       | 0x04 | TV.  |
| DEVICE_TYPE_WEARABLE | 0x06 | Wearable.  |


## ScreenDensity

Enumerates the screen density types.

**System capability**: SystemCapability.Global.ResourceManager

| Name            | Value | Description        |
| -------------- | ---- | ---------- |
| SCREEN_SDPI    | 120  | Screen density with small-scale dots per inch (SDPI).  |
| SCREEN_MDPI    | 160  | Screen density with medium-scale dots per inch (MDPI).  |
| SCREEN_LDPI    | 240  | Screen density with large-scale dots per inch (LDPI).  |
| SCREEN_XLDPI   | 320  | Screen density with extra-large-scale dots per inch (XLDPI). |
| SCREEN_XXLDPI  | 480  | Screen density with extra-extra-large-scale dots per inch (XXLDPI). |
| SCREEN_XXXLDPI | 640  | Screen density with extra-extra-extra-large-scale dots per inch (XXXLDPI).|


## Configuration

Defines the device configuration.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name       | Type                   | Readable  | Writable  | Description      |
| --------- | ----------------------- | ---- | ---- | -------- |
| direction | [Direction](#direction) | Yes   | No   | Screen direction of the device.|
| locale    | string                  | Yes   | No   | Current system language.  |


## DeviceCapability

Defines the device capability.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name           | Type                           | Readable  | Writable  | Description      |
| ------------- | ------------------------------- | ---- | ---- | -------- |
| screenDensity | [ScreenDensity](#screendensity) | Yes   | No   | Screen density of the device.|
| deviceType    | [DeviceType](#devicetype)       | Yes   | No   | Device type.  |


## RawFileDescriptor<sup>8+</sup>

Defines the descriptor of the raw file.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name    | Type   | Readable  | Writable | Description          |
| ------ | ------  | ---- | ---- | ------------------ |
| fd     | number  | Yes   | No| File descriptor of the HAP where the raw file is located.|
| offset | number  | Yes   | No| Start offset of the raw file.     |
| length | number  | Yes   | No| Length of the raw file.      |

## Resource<sup>9+</sup>

Defines the resource information of an application.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name        | Type    | Readable  | Writable |Description         |
| ---------- | ------ | ----- | ----  | ---------------|
| bundleName | string | Yes   | No| Bundle name of the application.|
| moduleName | string | Yes   | No| Module name of the application.|
| id         | number | Yes   | No| Resource ID.     |
| params     | any[] | Yes   | No| Other resource parameters, which are optional.     |
| type       | number | Yes   | No| Resource type, which is optional.     |


## ResourceManager

Defines the capability of accessing application resources.

> **NOTE**
>
> - The methods involved in **ResourceManager** are applicable only to the TypeScript-based declarative development paradigm.
>
> - Resource files are defined in the **resources** directory of the project. You can obtain the resource ID using **$r(resource address).id**, for example, **$r('app.string.test').id**.
>
> - You can specify whether to access intra-package resources in an application by resource ID or resource name. To access cross-package resources, you need to specify the [resource object](#resource9) or [context](../../application-models/application-context-stage.md#creating-context-of-another-application-or-module) of the corresponding packages. The service logic is similar to access to intra-package resources. You are advised to access cross-package resources by context.

### getStringSync<sup>9+</sup>

getStringSync(resId: number): string

Obtains the string corresponding to the specified resource ID. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|

**Return value**

| Type    | Description         |
| ------ | ----------- |
| string | String corresponding to the specified resource ID.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getStringSync($r('app.string.test').id);
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getStringSync failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getStringSync<sup>10+</sup>

getStringSync(resId: number, ...args: Array<string | number>): string

Obtains the string corresponding to the specified resource ID and formats the string based on **args**. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|
| args | Array<string \| number> | No   | Arguments for formatting strings.<br> Supported arguments:<br> %d, %f, %s, and %%<br> Note: **%%** is used to translate **%**.<br>Example: **%%d** is translated into the **%d** string.|

**Return value**

| Type    | Description         |
| ------ | ---------------------------- |
| string | Formatted string.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ----------------------------------------------- |
| 9001001  | If the resId invalid.                               |
| 9001002  | If the resource not found by resId.                 |
| 9001006  | If the resource re-ref too much.                    |
| 9001007  | If the resource obtained by resId formatting error. |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getStringSync($r('app.string.test').id, "format string", 10, 98.78);
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getStringSync failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getStringSync<sup>9+</sup>

getStringSync(resource: Resource): string

Obtains the string corresponding to the specified resource object. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name     | Type                    | Mandatory  | Description  |
| -------- | ---------------------- | ---- | ---- |
| resource | [Resource](#resource9) | Yes   | Resource object.|

**Return value**

| Type    | Description              |
| ------ | ---------------- |
| string | String corresponding to the specified resource object.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.string.test').id
  };
  try {
    this.context.resourceManager.getStringSync(resource);
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getStringSync failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getStringSync<sup>10+</sup>

getStringSync(resource: Resource, ...args: Array<string | number>): string

Obtains the string corresponding to the specified resource object and formats the string based on **args**. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name     | Type                    | Mandatory  | Description  |
| -------- | ---------------------- | ---- | ---- |
| resource | [Resource](#resource9) | Yes   | Resource object.|
| args | Array<string \| number> | No   | Arguments for formatting strings.<br> Supported arguments:<br> %d, %f, %s, and %%<br> Note: **%%** is used to translate **%**.<br>Example: **%%d** is translated into the **%d** string.|

**Return value**

| Type    | Description         |
| ------ | ---------------------------- |
| string | Formatted string.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |
| 9001007  | If the resource obtained by resId formatting error. |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.string.test').id
  };
  try {
    this.context.resourceManager.getStringSync(resource, "format string", 10, 98.78);
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getStringSync failed, error code: ${code}, message: ${message}.`);
  }
 ```

### getStringByNameSync<sup>9+</sup>

getStringByNameSync(resName: string): string

Obtains the string corresponding to the specified resource name. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name    | Type    | Mandatory  | Description  |
| ------- | ------ | ---- | ---- |
| resName | string | Yes   | Resource name.|

**Return value**

| Type    | Description        |
| ------ | ---------- |
| string | String corresponding to the specified resource name.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                     |
| 9001004  | If the resource not found by resName.       |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getStringByNameSync("test");
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getStringByNameSync failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getStringByNameSync<sup>10+</sup>

getStringByNameSync(resName: string, ...args: Array<string | number>): string

Obtains the string corresponding to the specified resource name and formats the string based on **args**. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name    | Type    | Mandatory  | Description  |
| ------- | ------ | ---- | ---- |
| resName | string | Yes   | Resource name.|
| args | Array<string \| number> | No   | Arguments for formatting strings.<br> Supported arguments:<br> %d, %f, %s, and %%<br> Note: **%%** is used to translate **%**.<br>Example: **%%d** is translated into the **%d** string.|

**Return value**

| Type    | Description         |
| ------ | ---------------------------- |
| string | Formatted string.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                     |
| 9001004  | If the resource not found by resName.       |
| 9001006  | If the resource re-ref too much.            |
| 9001008  | If the resource obtained by resName formatting error. |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getStringByNameSync("test", "format string", 10, 98.78);
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getStringByNameSync failed, error code: ${code}, message: ${message}.`);
  }
 ```

### getStringValue<sup>9+</sup>

getStringValue(resId: number, callback: AsyncCallback&lt;string&gt;): void

Obtains the string corresponding to the specified resource ID. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                         | Mandatory  | Description             |
| -------- | --------------------------- | ---- | --------------- |
| resId    | number                      | Yes   | Resource ID.          |
| callback | AsyncCallback&lt;string&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the module resId invalid.             |
| 9001002  | If the resource not found by resId.      |
| 9001006  | If the resource re-ref too much.         |

**Example (stage)**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getStringValue($r('app.string.test').id, (error, value) => {
      if (error != null) {
        console.log("error is " + error);
      } else {
        let str = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getStringValue failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getStringValue<sup>9+</sup>

getStringValue(resId: number): Promise&lt;string&gt;

Obtains the string corresponding to the specified resource ID. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|

**Return value**

| Type                   | Description         |
| --------------------- | ----------- |
| Promise&lt;string&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getStringValue($r('app.string.test').id).then((value: string) => {
      let str = value;
    }).catch((error: BusinessError) => {
      console.log("getStringValue promise error is " + error);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getStringValue failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getStringValue<sup>9+</sup>

getStringValue(resource: Resource, callback: AsyncCallback&lt;string&gt;): void

Obtains the string corresponding to the specified resource object. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name     | Type                         | Mandatory  | Description             |
| -------- | --------------------------- | ---- | --------------- |
| resource | [Resource](#resource9)      | Yes   | Resource object.           |
| callback | AsyncCallback&lt;string&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.string.test').id
  };
  try {
    this.context.resourceManager.getStringValue(resource, (error, value) => {
      if (error != null) {
        console.log("error is " + error);
      } else {
        let str = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getStringValue failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getStringValue<sup>9+</sup>

getStringValue(resource: Resource): Promise&lt;string&gt;

Obtains the string corresponding to the specified resource object. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name     | Type                    | Mandatory  | Description  |
| -------- | ---------------------- | ---- | ---- |
| resource | [Resource](#resource9) | Yes   | Resource object.|

**Return value**

| Type                   | Description              |
| --------------------- | ---------------- |
| Promise&lt;string&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.string.test').id
  };
  try {
    this.context.resourceManager.getStringValue(resource).then((value: string) => {
      let str = value;
    }).catch((error: BusinessError) => {
      console.log("getStringValue promise error is " + error);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getStringValue failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getStringByName<sup>9+</sup>

getStringByName(resName: string, callback: AsyncCallback&lt;string&gt;): void

Obtains the string corresponding to the specified resource name. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                         | Mandatory  | Description             |
| -------- | --------------------------- | ---- | --------------- |
| resName  | string                      | Yes   | Resource name.           |
| callback | AsyncCallback&lt;string&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                     |
| 9001004  | If the resource not found by resName.       |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getStringByName("test", (error, value) => {
      if (error != null) {
        console.log("error is " + error);
      } else {
        let str = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getStringByName failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getStringByName<sup>9+</sup>

getStringByName(resName: string): Promise&lt;string&gt;

Obtains the string corresponding to the specified resource name. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name    | Type    | Mandatory  | Description  |
| ------- | ------ | ---- | ---- |
| resName | string | Yes   | Resource name.|

**Return value**

| Type                   | Description        |
| --------------------- | ---------- |
| Promise&lt;string&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                     |
| 9001004  | If the resource not found by resName.       |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getStringByName("test").then((value: string) => {
      let str = value;
    }).catch((error: BusinessError) => {
      console.log("getStringByName promise error is " + error);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getStringByName failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getStringArrayValueSync<sup>10+</sup>

getStringArrayValueSync(resId: number): Array&lt;string&gt;

Obtains the string array corresponding to the specified resource ID. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|

**Return value**

| Type                   | Description         |
| --------------------- | ----------- |
| Array&lt;string&gt; | String array corresponding to the specified resource ID.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getStringArrayValueSync($r('app.strarray.test').id);
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getStringArrayValueSync failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getStringArrayValueSync<sup>10+</sup>

getStringArrayValueSync(resource: Resource): Array&lt;string&gt;

Obtains the string array corresponding to the specified resource object. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resource | [Resource](#resource9) | Yes   | Resource object.|

**Return value**

| Type                   | Description         |
| --------------------- | ----------- |
| Array&lt;string&gt; | String array corresponding to the specified resource object.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.strarray.test').id
  };
  try {
    this.context.resourceManager.getStringArrayValueSync(resource);
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getStringArrayValueSync failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getStringArrayByNameSync<sup>10+</sup>

getStringArrayByNameSync(resName: string): Array&lt;string&gt;

Obtains the string array corresponding to the specified resource name. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resName | string | Yes   | Resource name.|

**Return value**

| Type                   | Description         |
| --------------------- | ----------- |
| Array&lt;string&gt; | String array corresponding to the specified resource name.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                       |
| 9001004  | If the resource not found by resName.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  try {
    this.context.resourceManager.getStringArrayByNameSync("test");
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getStringArrayByNameSync failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getStringArrayValue<sup>9+</sup>

getStringArrayValue(resId: number, callback: AsyncCallback&lt;Array&lt;string&gt;&gt;): void

Obtains the string array corresponding to the specified resource ID. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                                      | Mandatory  | Description               |
| -------- | ---------------------------------------- | ---- | ----------------- |
| resId    | number                                   | Yes   | Resource ID.            |
| callback | AsyncCallback&lt;Array&lt;string&gt;&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getStringArrayValue($r('app.strarray.test').id, (error, value) => {
      if (error != null) {
        console.log("error is " + error);
      } else {
        let strArray = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getStringArrayValue failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getStringArrayValue<sup>9+</sup>

getStringArrayValue(resId: number): Promise&lt;Array&lt;string&gt;&gt;

Obtains the string array corresponding to the specified resource ID. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|

**Return value**

| Type                                | Description           |
| ---------------------------------- | ------------- |
| Promise&lt;Array&lt;string&gt;&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getStringArrayValue($r('app.strarray.test').id).then((value: Array<string>) => {
      let strArray = value;
    }).catch((error: BusinessError) => {
      console.log("getStringArrayValue promise error is " + error);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getStringArrayValue failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getStringArrayValue<sup>9+</sup>

getStringArrayValue(resource: Resource, callback: AsyncCallback&lt;Array&lt;string&gt;&gt;): void

Obtains the string array corresponding to the specified resource object. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name     | Type                                      | Mandatory  | Description               |
| -------- | ---------------------------------------- | ---- | ----------------- |
| resource | [Resource](#resource9)                   | Yes   | Resource object.             |
| callback | AsyncCallback&lt;Array&lt;string&gt;&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.strarray.test').id
  };
  try {
    this.context.resourceManager.getStringArrayValue(resource, (error, value) => {
      if (error != null) {
        console.log("error is " + error);
      } else {
        let strArray = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getStringArrayValue failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getStringArrayValue<sup>9+</sup>

getStringArrayValue(resource: Resource): Promise&lt;Array&lt;string&gt;&gt;

Obtains the string array corresponding to the specified resource object. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name     | Type                    | Mandatory  | Description  |
| -------- | ---------------------- | ---- | ---- |
| resource | [Resource](#resource9) | Yes   | Resource object.|

**Return value**

| Type                                | Description                |
| ---------------------------------- | ------------------ |
| Promise&lt;Array&lt;string&gt;&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.strarray.test').id
  };
  try {
    this.context.resourceManager.getStringArrayValue(resource).then((value: Array<string>) => {
      let strArray = value;
    }).catch((error: BusinessError) => {
      console.log("getStringArray promise error is " + error);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getStringArrayValue failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getStringArrayByName<sup>9+</sup>

getStringArrayByName(resName: string, callback: AsyncCallback&lt;Array&lt;string&gt;&gt;): void

Obtains the string array corresponding to the specified resource name. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                                      | Mandatory  | Description               |
| -------- | ---------------------------------------- | ---- | ----------------- |
| resName  | string                                   | Yes   | Resource name.             |
| callback | AsyncCallback&lt;Array&lt;string&gt;&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                     |
| 9001004  | If the resource not found by resName.       |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getStringArrayByName("test", (error, value) => {
      if (error != null) {
        console.log("error is " + error);
      } else {
        let strArray = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getStringArrayByName failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getStringArrayByName<sup>9+</sup>

getStringArrayByName(resName: string): Promise&lt;Array&lt;string&gt;&gt;

Obtains the string array corresponding to the specified resource name. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name    | Type    | Mandatory  | Description  |
| ------- | ------ | ---- | ---- |
| resName | string | Yes   | Resource name.|

**Return value**

| Type                                | Description          |
| ---------------------------------- | ------------ |
| Promise&lt;Array&lt;string&gt;&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                     |
| 9001004  | If the resource not found by resName.       |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getStringArrayByName("test").then((value: Array<string>) => {
      let strArray = value;
    }).catch((error: BusinessError) => {
      console.log("getStringArrayByName promise error is " + error);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getStringArrayByName failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getPluralStringValueSync<sup>10+</sup>

getPluralStringValueSync(resId: number, num: number): string

Obtains the singular-plural string corresponding to the specified resource ID based on the specified number. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|
| num   | number | Yes   | Number.  |

**Return value**

| Type                   | Description         |
| -------- | ----------- |
| string   | Singular-plural string corresponding to the specified resource ID.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getPluralStringValueSync($r('app.plural.test').id, 1);
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getPluralStringValueSync failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getPluralStringValueSync<sup>10+</sup>

getPluralStringValueSync(resource: Resource, num: number): string

Obtains the singular-plural string corresponding to the specified resource object based on the specified number. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resource | [Resource](#resource9) | Yes   | Resource object.|
| num      | number                 | Yes   | Number.  |

**Return value**

| Type                   | Description         |
| --------------------- | ----------- |
| string | Singular-plural string corresponding to the specified resource object.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.plural.test').id
  };
  try {
    this.context.resourceManager.getPluralStringValueSync(resource, 1);
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getPluralStringValueSync failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getPluralStringByNameSync<sup>10+</sup>

getPluralStringByNameSync(resName: string, num: number): string

Obtains the singular-plural string corresponding to the specified resource name based on the specified number. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resName | string | Yes   | Resource name.|
| num      | number                 | Yes   | Number.  |

**Return value**

| Type                   | Description         |
| --------------------- | ----------- |
| string | Singular-plural string corresponding to the specified resource name.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                       |
| 9001004  | If the resource not found by resName.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getPluralStringByNameSync("test", 1);
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getPluralStringByNameSync failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getPluralStringValue<sup>9+</sup>

getPluralStringValue(resId: number, num: number, callback: AsyncCallback&lt;string&gt;): void

Obtains the singular-plural string corresponding to the specified resource ID based on the specified number. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                         | Mandatory  | Description                             |
| -------- | --------------------------- | ---- | ------------------------------- |
| resId    | number                      | Yes   | Resource ID.                          |
| num      | number                      | Yes   | Number.                            |
| callback | AsyncCallback&lt;string&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getPluralStringValue($r("app.plural.test").id, 1, (error, value) => {
      if (error != null) {
        console.log("error is " + error);
      } else {
        let str = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getPluralStringValue failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getPluralStringValue<sup>9+</sup>

getPluralStringValue(resId: number, num: number): Promise&lt;string&gt;

Obtains the singular-plural string corresponding to the specified resource ID based on the specified number. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|
| num   | number | Yes   | Number.  |

**Return value**

| Type                   | Description                       |
| --------------------- | ------------------------- |
| Promise&lt;string&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getPluralStringValue($r("app.plural.test").id, 1).then((value: string) => {
      let str = value;
    }).catch((error: BusinessError) => {
      console.log("getPluralStringValue promise error is " + error);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getPluralStringValue failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getPluralStringValue<sup>9+</sup>

getPluralStringValue(resource: Resource, num: number, callback: AsyncCallback&lt;string&gt;): void

Obtains the singular-plural string corresponding to the specified resource object based on the specified number. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name     | Type                         | Mandatory  | Description                                  |
| -------- | --------------------------- | ---- | ------------------------------------ |
| resource | [Resource](#resource9)      | Yes   | Resource object.                                |
| num      | number                      | Yes   | Number.                                 |
| callback | AsyncCallback&lt;string&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.plural.test').id
  };
  try {
    this.context.resourceManager.getPluralStringValue(resource, 1, (error, value) => {
      if (error != null) {
        console.log("error is " + error);
      } else {
        let str = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getPluralStringValue failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getPluralStringValue<sup>9+</sup>

getPluralStringValue(resource: Resource, num: number): Promise&lt;string&gt;

Obtains the singular-plural string corresponding to the specified resource object based on the specified number. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name     | Type                    | Mandatory  | Description  |
| -------- | ---------------------- | ---- | ---- |
| resource | [Resource](#resource9) | Yes   | Resource object.|
| num      | number                 | Yes   | Number. |

**Return value**

| Type                   | Description                            |
| --------------------- | ------------------------------ |
| Promise&lt;string&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.plural.test').id
  };
  try {
    this.context.resourceManager.getPluralStringValue(resource, 1).then((value: string) => {
      let str = value;
    }).catch((error: BusinessError) => {
      console.log("getPluralStringValue promise error is " + error);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getPluralStringValue failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getPluralStringByName<sup>9+</sup>

getPluralStringByName(resName: string, num: number, callback: AsyncCallback&lt;string&gt;): void

Obtains the plural string corresponding to the specified resource name based on the specified number. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                         | Mandatory  | Description                           |
| -------- | --------------------------- | ---- | ----------------------------- |
| resName  | string                      | Yes   | Resource name.                         |
| num      | number                      | Yes   | Number.                          |
| callback | AsyncCallback&lt;string&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                     |
| 9001004  | If the resource not found by resName.       |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getPluralStringByName("test", 1, (error, value) => {
      if (error != null) {
        console.log("error is " + error);
      } else {
        let str = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getPluralStringByName failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getPluralStringByName<sup>9+</sup>

getPluralStringByName(resName: string, num: number): Promise&lt;string&gt;

Obtains the plural string corresponding to the specified resource name based on the specified number. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name    | Type    | Mandatory  | Description  |
| ------- | ------ | ---- | ---- |
| resName | string | Yes   | Resource name.|
| num     | number | Yes   | Number. |

**Return value**

| Type                   | Description                    |
| --------------------- | ---------------------- |
| Promise&lt;string&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                     |
| 9001004  | If the resource not found by resName.       |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getPluralStringByName("test", 1).then((value: string) => {
      let str = value;
    }).catch((error: BusinessError) => {
      console.log("getPluralStringByName promise error is " + error);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getPluralStringByName failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaContentSync<sup>10+</sup>

getMediaContentSync(resId: number, density?: number): Uint8Array

Obtains the media file content (with the default or specified screen density) corresponding to the specified resource ID. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|
| [density](#screendensity) | number | No   | Screen density. The default value or value **0** indicates the default screen density.|

**Return value**

| Type                   | Description         |
| -------- | ----------- |
| Uint8Array   | Media file content corresponding to the specified resource ID.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getMediaContentSync($r('app.media.test').id); // Default screen density
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getMediaContentSync failed, error code: ${code}, message: ${message}.`);
  }

  try {
    this.context.resourceManager.getMediaContentSync($r('app.media.test').id, 120); // Specified screen density
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getMediaContentSync failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaContentSync<sup>10+</sup>

getMediaContentSync(resource: Resource, density?: number): Uint8Array

Obtains the media file content (with the default or specified screen density) corresponding to the specified resource object. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resource | [Resource](#resource9) | Yes   | Resource object.|
| [density](#screendensity) | number | No   | Screen density. The default value or value **0** indicates the default screen density.|

**Return value**

| Type                   | Description         |
| --------------------- | ----------- |
| Uint8Array | Media file content corresponding to the specified resource object.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.media.test').id
  };
  try {
    this.context.resourceManager.getMediaContentSync(resource); // Default screen density
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getMediaContentSync failed, error code: ${code}, message: ${message}.`);
  }

  try {
    this.context.resourceManager.getMediaContentSync(resource, 120); // Specified screen density
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getMediaContentSync failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaByNameSync<sup>10+</sup>

getMediaByNameSync(resName: string, density?: number): Uint8Array

Obtains the media file content (with the default or specified screen density) corresponding to the specified resource name. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resName | string | Yes   | Resource name.|
| [density](#screendensity) | number | No   | Screen density. The default value or value **0** indicates the default screen density.|

**Return value**

| Type                   | Description         |
| --------------------- | ----------- |
| Uint8Array | Media file content corresponding to the resource name.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                       |
| 9001004  | If the resource not found by resName.         |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getMediaByNameSync("test"); // Default screen density
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getMediaByNameSync failed, error code: ${code}, message: ${message}.`);
  }

  try {
    this.context.resourceManager.getMediaByNameSync("test", 120); // Specified screen density
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getMediaByNameSync failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaContent<sup>9+</sup>

getMediaContent(resId: number, callback: AsyncCallback&lt;Uint8Array&gt;): void

Obtains the media file content corresponding to the specified resource ID. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                             | Mandatory  | Description                |
| -------- | ------------------------------- | ---- | ------------------ |
| resId    | number                          | Yes   | Resource ID.             |
| callback | AsyncCallback&lt;Uint8Array&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getMediaContent($r('app.media.test').id, (error, value) => {
      if (error != null) {
        console.log("error is " + error);
      } else {
        let media = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getMediaContent failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaContent<sup>10+</sup>

getMediaContent(resId: number, density: number, callback: AsyncCallback&lt;Uint8Array&gt;): void

Obtains the media file content (with the specified screen density) corresponding to the specified resource ID. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                             | Mandatory  | Description                |
| -------- | ------------------------------- | ---- | ------------------ |
| resId    | number                          | Yes   | Resource ID.             |
| [density](#screendensity)  | number                          | Yes   | Screen density. The value **0** indicates the default screen density.   |
| callback | AsyncCallback&lt;Uint8Array&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getMediaContent($r('app.media.test').id, 120, (error, value) => {
      if (error != null) {
        console.error(`callback getMediaContent failed, error code: ${error.code}, message: ${error.message}.`);
      } else {
        let media = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getMediaContent failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaContent<sup>9+</sup>

getMediaContent(resId: number): Promise&lt;Uint8Array&gt;

Obtains the media file content corresponding to the specified resource ID. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|

**Return value**

| Type                       | Description            |
| ------------------------- | -------------- |
| Promise&lt;Uint8Array&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getMediaContent($r('app.media.test').id).then((value: Uint8Array) => {
      let media = value;
    }).catch((error: BusinessError) => {
      console.log("getMediaContent promise error is " + error);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getMediaContent failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaContent<sup>10+</sup>

getMediaContent(resId: number, density: number): Promise&lt;Uint8Array&gt;

Obtains the media file content (with the specified screen density) corresponding to the specified resource ID. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|
| [density](#screendensity)  | number                          | Yes   | Screen density. The value **0** indicates the default screen density.   |

**Return value**

| Type                       | Description            |
| ------------------------- | -------------- |
| Promise&lt;Uint8Array&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getMediaContent($r('app.media.test').id, 120).then((value: Uint8Array) => {
      let media = value;
    }).catch((error: BusinessError) => {
      console.error(`promise getMediaContent failed, error code: ${error.code}, message: ${error.message}.`);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getMediaContent failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaContent<sup>9+</sup>

getMediaContent(resource: Resource, callback: AsyncCallback&lt;Uint8Array&gt;): void

Obtains the media file content corresponding to the specified resource object. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name     | Type                             | Mandatory  | Description                |
| -------- | ------------------------------- | ---- | ------------------ |
| resource | [Resource](#resource9)          | Yes   | Resource object.              |
| callback | AsyncCallback&lt;Uint8Array&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.media.test').id
  };
  try {
    this.context.resourceManager.getMediaContent(resource, (error, value) => {
      if (error != null) {
        console.log("error is " + error);
      } else {
        let media = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getMediaContent failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaContent<sup>10+</sup>

getMediaContent(resource: Resource, density: number, callback: AsyncCallback&lt;Uint8Array&gt;): void

Obtains the media file content (with the specified screen density) corresponding to the specified resource object. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name     | Type                             | Mandatory  | Description                |
| -------- | ------------------------------- | ---- | ------------------ |
| resource | [Resource](#resource9)          | Yes   | Resource object.              |
| [density](#screendensity)  | number        | Yes   | Screen density. The value **0** indicates the default screen density.   |
| callback | AsyncCallback&lt;Uint8Array&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.media.test').id
  };
  try {
    this.context.resourceManager.getMediaContent(resource, 120, (error, value) => {
      if (error != null) {
        console.error(`callback getMediaContent failed, error code: ${error.code}, message: ${error.message}.`);
      } else {
        let media = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getMediaContent failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaContent<sup>9+</sup>

getMediaContent(resource: Resource): Promise&lt;Uint8Array&gt;

Obtains the media file content corresponding to the specified resource object. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name     | Type                    | Mandatory  | Description  |
| -------- | ---------------------- | ---- | ---- |
| resource | [Resource](#resource9) | Yes   | Resource object.|

**Return value**

| Type                       | Description                 |
| ------------------------- | ------------------- |
| Promise&lt;Uint8Array&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.media.test').id
  };
  try {
    this.context.resourceManager.getMediaContent(resource).then((value: Uint8Array) => {
      let media = value;
    }).catch((error: BusinessError) => {
      console.log("getMediaContent promise error is " + error);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getMediaContent failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaContent<sup>10+</sup>

getMediaContent(resource: Resource, density: number): Promise&lt;Uint8Array&gt;

Obtains the media file content (with the specified screen density) corresponding to the specified resource object. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name     | Type                    | Mandatory  | Description  |
| -------- | ---------------------- | ---- | ---- |
| resource | [Resource](#resource9) | Yes   | Resource object.|
| [density](#screendensity)  | number                          | Yes   | Screen density. The value **0** indicates the default screen density.   |

**Return value**

| Type                       | Description                 |
| ------------------------- | ------------------- |
| Promise&lt;Uint8Array&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.media.test').id
  };
  try {
    this.context.resourceManager.getMediaContent(resource, 120).then((value: Uint8Array) => {
      let media = value;
    }).catch((error: BusinessError) => {
      console.error(`promise getMediaContent failed, error code: ${error.code}, message: ${error.message}.`);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getMediaContent failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaByName<sup>9+</sup>

getMediaByName(resName: string, callback: AsyncCallback&lt;Uint8Array&gt;): void

Obtains the media file content corresponding to the specified resource ID. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                             | Mandatory  | Description                |
| -------- | ------------------------------- | ---- | ------------------ |
| resName  | string                          | Yes   | Resource name.              |
| callback | AsyncCallback&lt;Uint8Array&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                     |
| 9001004  | If the resource not found by resName.       |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getMediaByName("test", (error, value) => {
      if (error != null) {
        console.log("error is " + error);
      } else {
        let media = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getMediaByName failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaByName<sup>10+</sup>

getMediaByName(resName: string, density: number, callback: AsyncCallback&lt;Uint8Array&gt;): void

Obtains the media file content (with the specified screen density) corresponding to the specified resource ID. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                             | Mandatory  | Description                |
| -------- | ------------------------------- | ---- | ------------------ |
| resName  | string                          | Yes   | Resource name.              |
| [density](#screendensity)  | number        | Yes   | Screen density. The value **0** indicates the default screen density.   |
| callback | AsyncCallback&lt;Uint8Array&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                     |
| 9001004  | If the resource not found by resName.       |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getMediaByName("test", 120, (error, value) => {
      if (error != null) {
        console.error(`callback getMediaByName failed, error code: ${error.code}, message: ${error.message}.`);
      } else {
        let media = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getMediaByName failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaByName<sup>9+</sup>

getMediaByName(resName: string): Promise&lt;Uint8Array&gt;

Obtains the media file content corresponding to the specified resource name. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name    | Type    | Mandatory  | Description  |
| ------- | ------ | ---- | ---- |
| resName | string | Yes   | Resource name.|

**Return value**

| Type                       | Description           |
| ------------------------- | ------------- |
| Promise&lt;Uint8Array&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                     |
| 9001004  | If the resource not found by resName.       |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getMediaByName("test").then((value: Uint8Array) => {
      let media = value;
    }).catch((error: BusinessError) => {
      console.log("getMediaByName promise error is " + error);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getMediaByName failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaByName<sup>10+</sup>

getMediaByName(resName: string, density: number): Promise&lt;Uint8Array&gt;

Obtains the media file content (with the specified screen density) corresponding to the specified resource name. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name    | Type    | Mandatory  | Description  |
| ------- | ------ | ---- | ---- |
| resName | string | Yes   | Resource name.|
| [density](#screendensity)  | number                          | Yes   | Screen density. The value **0** indicates the default screen density.   |

**Return value**

| Type                       | Description           |
| ------------------------- | ------------- |
| Promise&lt;Uint8Array&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                     |
| 9001004  | If the resource not found by resName.       |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getMediaByName("test", 120).then((value: Uint8Array) => {
      let media = value;
    }).catch((error: BusinessError) => {
      console.error(`promise getMediaByName failed, error code: ${error.code}, message: ${error.message}.`);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getMediaByName failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaContentBase64Sync<sup>10+</sup>

getMediaContentBase64Sync(resId: number, density?: number): string

Obtains the Base64 code of the image (with the default or specified screen density) corresponding to the specified resource ID.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|
| [density](#screendensity) | number | No   | Screen density. The default value or value **0** indicates the default screen density.|

**Return value**

| Type                   | Description         |
| -------- | ----------- |
| string   | Base64 code of the image corresponding to the specified resource ID.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getMediaContentBase64Sync($r('app.media.test').id); // Default screen density
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getMediaContentBase64Sync failed, error code: ${code}, message: ${message}.`);
  }

  try {
    this.context.resourceManager.getMediaContentBase64Sync($r('app.media.test').id, 120); // Specified screen density
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getMediaContentBase64Sync failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaContentBase64Sync<sup>10+</sup>

getMediaContentBase64Sync(resource: Resource, density?: number): string

Obtains the Base64 code of the image (with the default or specified screen density) corresponding to the specified resource object.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resource | [Resource](#resource9) | Yes   | Resource object.|
| [density](#screendensity) | number | No   | Screen density. The default value or value **0** indicates the default screen density.|

**Return value**

| Type                   | Description         |
| --------------------- | ----------- |
| string | Base64 code of the media file corresponding to the specified resource object.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.media.test').id
  };
  try {
    this.context.resourceManager.getMediaContentBase64Sync(resource); // Default screen density
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getMediaContentBase64Sync failed, error code: ${code}, message: ${message}.`);
  }

  try {
    this.context.resourceManager.getMediaContentBase64Sync(resource, 120); // Specified screen density
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getMediaContentBase64Sync failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaBase64ByNameSync<sup>10+</sup>

getMediaBase64ByNameSync(resName: string, density?: number): string

Obtains the Base64 code of the image (with the default or specified screen density) corresponding to the specified resource name.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resName | string | Yes   | Resource name.|
| [density](#screendensity) | number | No   | Screen density. The default value or value **0** indicates the default screen density.|

**Return value**

| Type                   | Description         |
| --------------------- | ----------- |
| string | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                       |
| 9001004  | If the resource not found by resName.         |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getMediaBase64ByNameSync("test"); // Default screen density
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getMediaBase64ByNameSync failed, error code: ${code}, message: ${message}.`);
  }

  try {
    this.context.resourceManager.getMediaBase64ByNameSync("test", 120); // Specified screen density
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getMediaBase64ByNameSync failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaContentBase64<sup>9+</sup>

getMediaContentBase64(resId: number, callback: AsyncCallback&lt;string&gt;): void

Obtains the Base64 code of the image corresponding to the specified resource ID. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                         | Mandatory  | Description                      |
| -------- | --------------------------- | ---- | ------------------------ |
| resId    | number                      | Yes   | Resource ID.                   |
| callback | AsyncCallback&lt;string&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getMediaContentBase64($r('app.media.test').id, (error, value) => {
      if (error != null) {
        console.log("error is " + error);
      } else {
        let media = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getMediaContentBase64 failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaContentBase64<sup>10+</sup>

getMediaContentBase64(resId: number, density: number, callback: AsyncCallback&lt;string&gt;): void

Obtains the Base64 code of an image with the screen density corresponding to the specified resource ID. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                         | Mandatory  | Description                      |
| -------- | --------------------------- | ---- | ------------------------ |
| resId    | number                      | Yes   | Resource ID.                   |
| [density](#screendensity)  | number        | Yes   | Screen density. The value **0** indicates the default screen density.   |
| callback | AsyncCallback&lt;string&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getMediaContentBase64($r('app.media.test').id, 120, (error, value) => {
      if (error != null) {
        console.error(`callback getMediaContentBase64 failed, error code: ${error.code}, message: ${error.message}.`);
      } else {
        let media = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getMediaContentBase64 failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaContentBase64<sup>9+</sup>

getMediaContentBase64(resId: number): Promise&lt;string&gt;

Obtains the Base64 code of the image corresponding to the specified resource ID. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|

**Return value**

| Type                   | Description                  |
| --------------------- | -------------------- |
| Promise&lt;string&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getMediaContentBase64($r('app.media.test').id).then((value: string) => {
      let media = value;
    }).catch((error: BusinessError) => {
      console.log("getMediaContentBase64 promise error is " + error);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getMediaContentBase64 failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaContentBase64<sup>10+</sup>

getMediaContentBase64(resId: number, density: number): Promise&lt;string&gt;

Obtains the Base64 code of an image with the screen density corresponding to the specified resource ID. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|
| [density](#screendensity)  | number                          | Yes   | Screen density. The value **0** indicates the default screen density.   |

**Return value**

| Type                   | Description                  |
| --------------------- | -------------------- |
| Promise&lt;string&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getMediaContentBase64($r('app.media.test').id, 120).then((value: string) => {
      let media = value;
    }).catch((error: BusinessError) => {
      console.error(`promise getMediaContentBase64 failed, error code: ${error.code}, message: ${error.message}.`);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getMediaContentBase64 failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaContentBase64<sup>9+</sup>

getMediaContentBase64(resource: Resource, callback: AsyncCallback&lt;string&gt;): void

Obtains the Base64 code of the image corresponding to the specified resource object. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name     | Type                         | Mandatory  | Description                      |
| -------- | --------------------------- | ---- | ------------------------ |
| resource | [Resource](#resource9)      | Yes   | Resource object.                    |
| callback | AsyncCallback&lt;string&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.media.test').id
  };
  try {
    this.context.resourceManager.getMediaContentBase64(resource, (error, value) => {
      if (error != null) {
        console.log("error is " + error);
      } else {
        let media = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getMediaContentBase64 failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaContentBase64<sup>10+</sup>

getMediaContentBase64(resource: Resource, density: number, callback: AsyncCallback&lt;string&gt;): void

Obtains the Base64 code of an image with the screen density corresponding to the specified resource object. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name     | Type                         | Mandatory  | Description                      |
| -------- | --------------------------- | ---- | ------------------------ |
| resource | [Resource](#resource9)      | Yes   | Resource object.                    |
| [density](#screendensity)  | number        | Yes   | Screen density. The value **0** indicates the default screen density.   |
| callback | AsyncCallback&lt;string&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.media.test').id
  };
  try {
    this.context.resourceManager.getMediaContentBase64(resource, 120, (error, value) => {
      if (error != null) {
        console.error(`callback getMediaContentBase64 failed, error code: ${error.code}, message: ${error.message}.`);
      } else {
        let media = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getMediaContentBase64 failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaContentBase64<sup>9+</sup>

getMediaContentBase64(resource: Resource): Promise&lt;string&gt;

Obtains the Base64 code of the image corresponding to the specified resource object. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name     | Type                    | Mandatory  | Description  |
| -------- | ---------------------- | ---- | ---- |
| resource | [Resource](#resource9) | Yes   | Resource object.|

**Return value**

| Type                   | Description                       |
| --------------------- | ------------------------- |
| Promise&lt;string&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.media.test').id
  };
  try {
    this.context.resourceManager.getMediaContentBase64(resource).then((value: string) => {
      let media = value;
    }).catch((error: BusinessError) => {
      console.log("getMediaContentBase64 promise error is " + error);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getMediaContentBase64 failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaContentBase64<sup>10+</sup>

getMediaContentBase64(resource: Resource, density: number): Promise&lt;string&gt;

Obtains the Base64 code of an image with the screen density corresponding to the specified resource object. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name     | Type                    | Mandatory  | Description  |
| -------- | ---------------------- | ---- | ---- |
| resource | [Resource](#resource9) | Yes   | Resource object.|
| [density](#screendensity)  | number                          | Yes   | Screen density. The value **0** indicates the default screen density.   |

**Return value**

| Type                   | Description                       |
| --------------------- | ------------------------- |
| Promise&lt;string&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.media.test').id
  };
  try {
    this.context.resourceManager.getMediaContentBase64(resource, 120).then((value: string) => {
      let media = value;
    }).catch((error: BusinessError) => {
      console.error(`promise getMediaContentBase64 failed, error code: ${error.code}, message: ${error.message}.`);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getMediaContentBase64 failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaBase64ByName<sup>9+</sup>

getMediaBase64ByName(resName: string, callback: AsyncCallback&lt;string&gt;): void

Obtains the Base64 code of the image corresponding to the specified resource name. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                         | Mandatory  | Description                      |
| -------- | --------------------------- | ---- | ------------------------ |
| resName  | string                      | Yes   | Resource name.                    |
| callback | AsyncCallback&lt;string&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                     |
| 9001004  | If the resource not found by resName.       |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getMediaBase64ByName("test", (error, value) => {
      if (error != null) {
        console.log("error is " + error);
      } else {
        let media = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getMediaBase64ByName failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaBase64ByName<sup>10+</sup>

getMediaBase64ByName(resName: string, density: number, callback: AsyncCallback&lt;string&gt;): void

Obtains the Base64 code of an image with the screen density corresponding to the specified resource name. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                         | Mandatory  | Description                      |
| -------- | --------------------------- | ---- | ------------------------ |
| resName  | string                      | Yes   | Resource name.                    |
| [density](#screendensity)  | number        | Yes   | Screen density. The value **0** indicates the default screen density.   |
| callback | AsyncCallback&lt;string&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                     |
| 9001004  | If the resource not found by resName.       |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getMediaBase64ByName("test", 120, (error, value) => {
      if (error != null) {
        console.error(`callback getMediaBase64ByName failed, error code: ${error.code}, message: ${error.message}.`);
      } else {
        let media = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getMediaBase64ByName failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaBase64ByName<sup>9+</sup>

getMediaBase64ByName(resName: string): Promise&lt;string&gt;

Obtains the Base64 code of the image corresponding to the specified resource name. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name    | Type    | Mandatory  | Description  |
| ------- | ------ | ---- | ---- |
| resName | string | Yes   | Resource name.|

**Return value**

| Type                   | Description                 |
| --------------------- | ------------------- |
| Promise&lt;string&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                     |
| 9001004  | If the resource not found by resName.       |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getMediaBase64ByName("test").then((value: string) => {
      let media = value;
    }).catch((error: BusinessError) => {
      console.log("getMediaBase64ByName promise error is " + error);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getMediaBase64ByName failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getMediaBase64ByName<sup>10+</sup>

getMediaBase64ByName(resName: string, density: number): Promise&lt;string&gt;

Obtains the Base64 code of an image with the screen density corresponding to the specified resource name. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name    | Type    | Mandatory  | Description  |
| ------- | ------ | ---- | ---- |
| resName | string | Yes   | Resource name.|
| [density](#screendensity)  | number                          | Yes   | Screen density. The value **0** indicates the default screen density.   |

**Return value**

| Type                   | Description                 |
| --------------------- | ------------------- |
| Promise&lt;string&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                     |
| 9001004  | If the resource not found by resName.       |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getMediaBase64ByName("test", 120).then((value: string) => {
      let media = value;
    }).catch((error: BusinessError) => {
      console.error(`promise getMediaBase64ByName failed, error code: ${error.code}, message: ${error.message}.`);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getMediaBase64ByName failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getDrawableDescriptor<sup>10+</sup>

getDrawableDescriptor(resId: number, density?: number): DrawableDescriptor;

Obtains the **DrawableDescriptor** object corresponding to the specified resource ID. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|
| [density](#screendensity) | number | No   | Screen density. The default value or value **0** indicates the default screen density.|

**Return value**

| Type    | Description        |
| ------ | ---------- |
| DrawableDescriptor | **DrawableDescriptor** object corresponding to the specified resource ID.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getDrawableDescriptor($r('app.media.icon').id);
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getDrawableDescriptor failed, error code: ${code}, message: ${message}.`);
  }
  try {
    this.context.resourceManager.getDrawableDescriptor($r('app.media.icon').id, 120);
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getDrawableDescriptor failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getDrawableDescriptor<sup>10+</sup>

getDrawableDescriptor(resource: Resource, density?: number): DrawableDescriptor;

Obtains the **DrawableDescriptor** object corresponding to the specified resource object. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name     | Type                    | Mandatory  | Description  |
| -------- | ---------------------- | ---- | ---- |
| resource | [Resource](#resource9) | Yes   | Resource object.|
| [density](#screendensity) | number | No   | Screen density. The default value or value **0** indicates the default screen density.|

**Return value**

| Type     | Description               |
| ------- | ----------------- |
| DrawableDescriptor | **DrawableDescriptor** object corresponding to the specified resource ID.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.media.icon').id
  };
  try {
    this.context.resourceManager.getDrawableDescriptor(resource);
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getDrawableDescriptor failed, error code: ${code}, message: ${message}.`);
  }
  try {
    this.context.resourceManager.getDrawableDescriptor(resource, 120);
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getDrawableDescriptor failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getDrawableDescriptorByName<sup>10+</sup>

getDrawableDescriptorByName(resName: string, density?: number): DrawableDescriptor;

Obtains the **DrawableDescriptor** object corresponding to the specified resource name. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name    | Type    | Mandatory  | Description  |
| ------- | ------ | ---- | ---- |
| resName | string | Yes   | Resource name.|
| [density](#screendensity) | number | No   | Screen density. The default value or value **0** indicates the default screen density.|

**Return value**

| Type    | Description       |
| ------ | --------- |
| DrawableDescriptor | **DrawableDescriptor** object corresponding to the specified resource ID.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                     |
| 9001004  | If the resource not found by resName.       |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getDrawableDescriptorByName('icon');
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getDrawableDescriptorByName failed, error code: ${code}, message: ${message}.`);
  }
  try {
    this.context.resourceManager.getDrawableDescriptorByName('icon', 120);
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getDrawableDescriptorByName failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getBoolean<sup>9+</sup>

getBoolean(resId: number): boolean

Obtains the Boolean result corresponding to the specified resource ID. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|

**Return value**

| Type     | Description          |
| ------- | ------------ |
| boolean | Boolean result corresponding to the specified resource ID.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getBoolean($r('app.boolean.boolean_test').id);
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getBoolean failed, error code: ${code}, message: ${message}.`);
  }
  ```
### getBoolean<sup>9+</sup>

getBoolean(resource: Resource): boolean

Obtains the Boolean result corresponding to the specified resource object. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name     | Type                    | Mandatory  | Description  |
| -------- | ---------------------- | ---- | ---- |
| resource | [Resource](#resource9) | Yes   | Resource object.|

**Return value**

| Type     | Description               |
| ------- | ----------------- |
| boolean | Boolean result corresponding to the specified resource object.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.boolean.boolean_test').id
  };
  try {
    this.context.resourceManager.getBoolean(resource);
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getBoolean failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getBooleanByName<sup>9+</sup>

getBooleanByName(resName: string): boolean

Obtains the Boolean result corresponding to the specified resource name. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name    | Type    | Mandatory  | Description  |
| ------- | ------ | ---- | ---- |
| resName | string | Yes   | Resource name.|

**Return value**

| Type     | Description         |
| ------- | ----------- |
| boolean | Boolean result corresponding to the specified resource name.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                     |
| 9001004  | If the resource not found by resName.       |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getBooleanByName("boolean_test");
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getBooleanByName failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getNumber<sup>9+</sup>

getNumber(resId: number): number

Obtains the integer or float value corresponding to the specified resource ID. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|

**Return value**

| Type    | Description        |
| ------ | ---------- | 
| number | Integer or float value corresponding to the specified resource ID. Wherein, the integer value is the original value, and the float value is the actual pixel value. For details, see the sample code.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getNumber($r('app.integer.integer_test').id); // integer refers to the original value.
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getNumber failed, error code: ${code}, message: ${message}.`);
  }

  try {
    this.context.resourceManager.getNumber($r('app.float.float_test').id); // float refers to the actual pixel value.
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getNumber failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getNumber<sup>9+</sup>

getNumber(resource: Resource): number

Obtains the integer or float value corresponding to the specified resource object. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name     | Type                    | Mandatory  | Description  |
| -------- | ---------------------- | ---- | ---- |
| resource | [Resource](#resource9) | Yes   | Resource object.|

**Return value**

| Type    | Description             |
| ------ | --------------- |
| number | Integer or float value corresponding to the specified resource object. Wherein, the integer value is the original value, and the float value is the actual pixel value. For details, see the sample code.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.integer.integer_test').id
  };
  try {
    this.context.resourceManager.getNumber(resource);// integer refers to the original value; float refers to the actual pixel value.
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getNumber failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getNumberByName<sup>9+</sup>

getNumberByName(resName: string): number

Obtains the integer or float value corresponding to the specified resource name. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name    | Type    | Mandatory  | Description  |
| ------- | ------ | ---- | ---- |
| resName | string | Yes   | Resource name.|

**Return value**

| Type    | Description       |
| ------ | --------- |
| number | Integer or float value corresponding to the specified resource name.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                     |
| 9001004  | If the resource not found by resName.       |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getNumberByName("integer_test");
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getNumberByName failed, error code: ${code}, message: ${message}.`);
  }

  try {
    this.context.resourceManager.getNumberByName("float_test");
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getNumberByName failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getColorSync<sup>10+</sup>

getColorSync(resId: number) : number;

Obtains the color value (decimal) corresponding to the specified resource ID. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|

**Return value**

| Type    | Description         |
| ------ | ----------- |
| number | Color value corresponding to the resource ID.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getColorSync($r('app.color.test').id);
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getColorSync failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getColorSync<sup>10+</sup>

getColorSync(resource: Resource): number

Obtains the color value (decimal) corresponding to the specified resource object. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name     | Type                    | Mandatory  | Description  |
| -------- | ---------------------- | ---- | ---- |
| resource | [Resource](#resource9) | Yes   | Resource object.|

**Return value**

| Type    | Description              |
| ------ | ---------------- |
| number | Color value corresponding to the resource object.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.color.test').id
  };
  try {
    this.context.resourceManager.getColorSync(resource);
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getColorSync failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getColorByNameSync<sup>10+</sup>

getColorByNameSync(resName: string) : number;

Obtains the color value (decimal) corresponding to the specified resource name. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name    | Type    | Mandatory  | Description  |
| ------- | ------ | ---- | ---- |
| resName | string | Yes   | Resource name.|

**Return value**

| Type    | Description        |
| ------ | ---------- |
| number | Color value corresponding to the resource name.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                     |
| 9001004  | If the resource not found by resName.       |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getColorByNameSync("test");
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getColorByNameSync failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getColor<sup>10+</sup>

getColor(resId: number, callback: AsyncCallback&lt;number&gt;): void;

Obtains the color value (decimal) corresponding to the specified resource ID. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                         | Mandatory  | Description             |
| -------- | --------------------------- | ---- | --------------- |
| resId    | number                      | Yes   | Resource ID.          |
| callback | AsyncCallback&lt;number&gt; | Yes   | Asynchronous callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the module resId invalid.             |
| 9001002  | If the resource not found by resId.      |
| 9001006  | If the resource re-ref too much.         |

**Example (stage)**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getColor($r('app.color.test').id, (error, value) => {
      if (error != null) {
        console.log("error is " + error);
      } else {
        let str = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getColor failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getColor<sup>10+</sup>

getColor(resId: number): Promise&lt;number&gt;

Obtains the color value (decimal) corresponding to the specified resource ID. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|

**Return value**

| Type                   | Description         |
| --------------------- | ----------- |
| Promise&lt;number&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getColor($r('app.color.test').id).then((value: number) => {
      let str = value;
    }).catch((error: BusinessError) => {
      console.log("getColor promise error is " + error);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getColor failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getColor<sup>10+</sup>

getColor(resource: Resource, callback: AsyncCallback&lt;number&gt;): void;

Obtains the color value (decimal) corresponding to the specified resource object. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name     | Type                         | Mandatory  | Description             |
| -------- | --------------------------- | ---- | --------------- |
| resource | [Resource](#resource9)      | Yes   | Resource object.           |
| callback | AsyncCallback&lt;number&gt; | Yes   | Asynchronous callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.color.test').id
  };
  try {
    this.context.resourceManager.getColor(resource, (error, value) => {
      if (error != null) {
        console.log("error is " + error);
      } else {
        let str = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getColor failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getColor<sup>10+</sup>

getColor(resource: Resource): Promise&lt;number&gt;;

Obtains the color value (decimal) corresponding to the specified resource object. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name     | Type                    | Mandatory  | Description  |
| -------- | ---------------------- | ---- | ---- |
| resource | [Resource](#resource9) | Yes   | Resource object.|

**Return value**

| Type                   | Description              |
| --------------------- | ---------------- |
| Promise&lt;number&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001001  | If the resId invalid.                       |
| 9001002  | If the resource not found by resId.         |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  let resource: resourceManager.Resource = {
    bundleName: "com.example.myapplication",
    moduleName: "entry",
    id: $r('app.color.test').id
  };
  try {
    this.context.resourceManager.getColor(resource).then((value: number) => {
      let str = value;
    }).catch((error: BusinessError) => {
      console.log("getColor promise error is " + error);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getColor failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getColorByName<sup>10+</sup>

getColorByName(resName: string, callback: AsyncCallback&lt;number&gt;): void

Obtains the color value (decimal) corresponding to the specified resource name. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                         | Mandatory  | Description             |
| -------- | --------------------------- | ---- | --------------- |
| resName  | string                      | Yes   | Resource name.           |
| callback | AsyncCallback&lt;number&gt; | Yes   | Asynchronous callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                     |
| 9001004  | If the resource not found by resName.       |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getColorByName("test", (error, value) => {
      if (error != null) {
        console.log("error is " + error);
      } else {
        let string = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getColorByName failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getColorByName<sup>10+</sup>

getColorByName(resName: string): Promise&lt;number&gt;

Obtains the color value (decimal) corresponding to the specified resource name. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name    | Type    | Mandatory  | Description  |
| ------- | ------ | ---- | ---- |
| resName | string | Yes   | Resource name.|

**Return value**

| Type                   | Description        |
| --------------------- | ---------- |
| Promise&lt;number&gt; | Promise used to return the color value corresponding to the resource name.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001003  | If the resName invalid.                     |
| 9001004  | If the resource not found by resName.       |
| 9001006  | If the resource re-ref too much.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getColorByName("test").then((value: number) => {
      let string = value;
    }).catch((error: BusinessError) => {
      console.log("getColorByName promise error is " + error);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getColorByName failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getRawFileContentSync<sup>10+</sup>

getRawFileContentSync(path: string): Uint8Array

Obtains the content of the raw file in the **resources/rawfile** directory. This API returns the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                             | Mandatory  | Description                     |
| -------- | ------------------------------- | ---- | ----------------------- |
| path     | string                          | Yes   | Path of the raw file.            |

**Return value**

| Type                   | Description        |
| --------------------- | ---------- |
| Uint8Array | Content of the raw file.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001005  | If the resource not found by path.          |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getRawFileContentSync("test.txt");
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getRawFileContentSync failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getRawFileContent<sup>9+</sup>

getRawFileContent(path: string, callback: AsyncCallback&lt;Uint8Array&gt;): void

Obtains the content of the raw file in the **resources/rawfile** directory. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                             | Mandatory  | Description                     |
| -------- | ------------------------------- | ---- | ----------------------- |
| path     | string                          | Yes   | Path of the raw file.            |
| callback | AsyncCallback&lt;Uint8Array&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001005  | If the resource not found by path.          |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getRawFileContent("test.txt", (error, value) => {
      if (error != null) {
        console.log("error is " + error);
      } else {
        let rawFile = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getRawFileContent failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getRawFileContent<sup>9+</sup>

getRawFileContent(path: string): Promise&lt;Uint8Array&gt;

Obtains the content of the raw file in the **resources/rawfile** directory. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name | Type    | Mandatory  | Description         |
| ---- | ------ | ---- | ----------- |
| path | string | Yes   | Path of the raw file.|

**Return value**

| Type                       | Description         |
| ------------------------- | ----------- |
| Promise&lt;Uint8Array&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001005  | If the resource not found by path.          |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getRawFileContent("test.txt").then((value: Uint8Array) => {
      let rawFile = value;
    }).catch((error: BusinessError) => {
      console.log("getRawFileContent promise error is " + error);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getRawFileContent failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getRawFileListSync<sup>10+</sup>

getRawFileListSync(path: string): Array\<string\>

Obtains the list of files in the **resources/rawfile** directory. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                             | Mandatory  | Description                     |
| -------- | ------------------------------- | ---- | ----------------------- |
| path     | string                          | Yes   | Path of the **rawfile** folder.            |

**Return value**

| Type                       | Description         |
| ------------------------- | ----------- |
| Array\<string\> | List of files in the **resources/rawfile** directory.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001005  | If the resource not found by path.       |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try { // Passing "" means to obtain the list of files in the root directory of the raw file.
    this.context.resourceManager.getRawFileListSync("")
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getRawFileListSync failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getRawFileList<sup>10+</sup>

getRawFileList(path: string, callback: AsyncCallback&lt;Array\<string\>&gt;): void;

Obtains the list of files in the **resources/rawfile** directory. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                             | Mandatory  | Description                     |
| -------- | ------------------------------- | ---- | ----------------------- |
| path     | string                          | Yes   | Path of the **rawfile** folder.            |
| callback | AsyncCallback&lt;Array\<string\>&gt; | Yes| Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001005  | If the resource not found by path.       |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try { // Passing "" means to obtain the list of files in the root directory of the raw file.
    this.context.resourceManager.getRawFileList("", (error, value) => {
      if (error != null) {
        console.error(`callback getRawFileList failed, error code: ${error.code}, message: ${error.message}.`);
      } else {
        let rawFile = value;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getRawFileList failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getRawFileList<sup>10+</sup>

getRawFileList(path: string): Promise&lt;Array\<string\>&gt;

Obtains the list of files in the **resources/rawfile** directory. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name | Type    | Mandatory  | Description         |
| ---- | ------ | ---- | ----------- |
| path | string | Yes   | Path of the **rawfile** folder.|

**Return value**

| Type                       | Description         |
| ------------------------- | ----------- |
| Promise&lt;Array\<string\>&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001005  | If the resource not found by path.          |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try { // Passing "" means to obtain the list of files in the root directory of the raw file.
    this.context.resourceManager.getRawFileList("").then((value: Array<string>) => {
      let rawFile = value;
    }).catch((error: BusinessError) => {
      console.error(`promise getRawFileList failed, error code: ${error.code}, message: ${error.message}.`);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getRawFileList failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getRawFdSync<sup>10+</sup>

getRawFdSync(path: string): RawFileDescriptor

Obtains the descriptor of the raw file in the **resources/rawfile** directory. 

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                                      | Mandatory  | Description                              |
| -------- | ---------------------------------------- | ---- | -------------------------------- |
| path     | string                                   | Yes   | Path of the raw file.                     |

**Return value**

| Type                       | Description         |
| ------------------------- | ----------- |
| [RawFileDescriptor](#rawfiledescriptor8) | Descriptor of the raw file.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001005  | If the resource not found by path.          |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getRawFdSync("test.txt");
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getRawFdSync failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getRawFd<sup>9+</sup>

getRawFd(path: string, callback: AsyncCallback&lt;RawFileDescriptor&gt;): void

Obtains the descriptor of the raw file in the **resources/rawfile** directory. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                                      | Mandatory  | Description                              |
| -------- | ---------------------------------------- | ---- | -------------------------------- |
| path     | string                                   | Yes   | Path of the raw file.                     |
| callback | AsyncCallback&lt;[RawFileDescriptor](#rawfiledescriptor8)&gt; | Yes   | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001005  | If the resource not found by path.          |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getRawFd("test.txt", (error, value) => {
      if (error != null) {
        console.log(`callback getRawFd failed error code: ${error.code}, message: ${error.message}.`);
      } else {
        let fd = value.fd;
        let offset = value.offset;
        let length = value.length;
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback getRawFd failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getRawFd<sup>9+</sup>

getRawFd(path: string): Promise&lt;RawFileDescriptor&gt;

Obtains the descriptor of the raw file in the **resources/rawfile** directory. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name | Type    | Mandatory  | Description         |
| ---- | ------ | ---- | ----------- |
| path | string | Yes   | Path of the raw file.|

**Return value**

| Type                                      | Description                 |
| ---------------------------------------- | ------------------- |
| Promise&lt;[RawFileDescriptor](#rawfiledescriptor8)&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001005  | If the resource not found by path.          |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getRawFd("test.txt").then((value: resourceManager.RawFileDescriptor) => {
      let fd = value.fd;
      let offset = value.offset;
      let length = value.length;
    }).catch((error: BusinessError) => {
      console.log(`promise getRawFd error error code: ${error.code}, message: ${error.message}.`);
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise getRawFd failed, error code: ${code}, message: ${message}.`);
  }
  ```

### closeRawFdSync<sup>10+</sup>

closeRawFdSync(path: string): void

Closes the descriptor of the raw file in the **resources/rawfile** directory.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                       | Mandatory  | Description         |
| -------- | ------------------------- | ---- | ----------- |
| path     | string                    | Yes   | Path of the raw file.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001005  | The resource not found by path.          |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.closeRawFdSync("test.txt");
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`closeRawFd failed, error code: ${code}, message: ${message}.`);
  }
  ```

### closeRawFd<sup>9+</sup>

closeRawFd(path: string, callback: AsyncCallback&lt;void&gt;): void

Closes the descriptor of the raw file in the **resources/rawfile** directory. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                       | Mandatory  | Description         |
| -------- | ------------------------- | ---- | ----------- |
| path     | string                    | Yes   | Path of the raw file.|
| callback | AsyncCallback&lt;void&gt; | Yes   | Callback used to return the result.       |

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001005  | The resource not found by path.          |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.closeRawFd("test.txt", (error, value) => {
      if (error != null) {
        console.log("error is " + error);
      }
    });
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`callback closeRawFd failed, error code: ${code}, message: ${message}.`);
  }
  ```

### closeRawFd<sup>9+</sup>

closeRawFd(path: string): Promise&lt;void&gt;

Closes the descriptor of the raw file in the **resources/rawfile** directory. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name | Type    | Mandatory  | Description         |
| ---- | ------ | ---- | ----------- |
| path | string | Yes   | Path of the raw file.|

**Return value**

| Type                 | Description  |
| ------------------- | ---- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001005  | If the resource not found by path.          |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.closeRawFd("test.txt");
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`promise closeRawFd failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getConfigurationSync

getConfigurationSync(): Configuration

Obtains the device configuration. This API return the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Return value**

| Type                                      | Description              |
| ---------------------------------------- | ---------------- |
| [Configuration](#configuration) | Promise used to return the result.|

**Example**
  ```ts
  try {
    let value = this.context.resourceManager.getConfigurationSync();
    let direction = value.direction;
    let locale = value.locale;
  } catch (error) {
    console.error("getConfigurationSync error is " + error);
  }
  ```

### getConfiguration

getConfiguration(callback: AsyncCallback&lt;Configuration&gt;): void

Obtains the device configuration. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                                      | Mandatory  | Description                       |
| -------- | ---------------------------------------- | ---- | ------------------------- |
| callback | AsyncCallback&lt;[Configuration](#configuration)&gt; | Yes   | Callback used to return the result.|

**Example**
  ```ts
  try {
    this.context.resourceManager.getConfiguration((error, value) => {
      if (error != null) {
        console.error("getConfiguration callback error is " + error);
      } else {
        let direction = value.direction;
        let locale = value.locale;
      }
    });
  } catch (error) {
    console.error("getConfiguration callback error is " + error);
  }
  ```

### getConfiguration

getConfiguration(): Promise&lt;Configuration&gt;

Obtains the device configuration. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Return value**

| Type                                      | Description              |
| ---------------------------------------- | ---------------- |
| Promise&lt;[Configuration](#configuration)&gt; | Promise used to return the result.|

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getConfiguration().then((value: resourceManager.Configuration) => {
      let direction = value.direction;
      let locale = value.locale;
    }).catch((error: BusinessError) => {
      console.error("getConfiguration promise error is " + error);
    });
  } catch (error) {
    console.error("getConfiguration promise error is " + error);
  }
  ```

### getDeviceCapabilitySync

getDeviceCapabilitySync(): DeviceCapability

Obtains the device capability. This API return the result synchronously.

**System capability**: SystemCapability.Global.ResourceManager

**Return value**

| Type                                      | Description                 |
| ---------------------------------------- | ------------------- |
| [DeviceCapability](#devicecapability) | Promise used to return the result.|

**Example**
  ```ts
  try {
    let value = this.context.resourceManager.getDeviceCapabilitySync();
    let screenDensity = value.screenDensity;
    let deviceType = value.deviceType;
  } catch (error) {
    console.error("getDeviceCapabilitySync error is " + error);
  }
  ```

### getDeviceCapability

getDeviceCapability(callback: AsyncCallback&lt;DeviceCapability&gt;): void

Obtains the device capability. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                                      | Mandatory  | Description                          |
| -------- | ---------------------------------------- | ---- | ---------------------------- |
| callback | AsyncCallback&lt;[DeviceCapability](#devicecapability)&gt; | Yes   | Callback used to return the result.|

**Example**
  ```ts
  try {
    this.context.resourceManager.getDeviceCapability((error, value) => {
      if (error != null) {
        console.error("getDeviceCapability callback error is " + error);
      } else {
        let screenDensity = value.screenDensity;
        let deviceType = value.deviceType;
      }
    });
  } catch (error) {
    console.error("getDeviceCapability callback error is " + error);
  }
  ```

### getDeviceCapability

getDeviceCapability(): Promise&lt;DeviceCapability&gt;

Obtains the device capability. This API uses a promise to return the result.

**System capability**: SystemCapability.Global.ResourceManager

**Return value**

| Type                                      | Description                 |
| ---------------------------------------- | ------------------- |
| Promise&lt;[DeviceCapability](#devicecapability)&gt; | Promise used to return the result.|

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getDeviceCapability().then((value: resourceManager.DeviceCapability) => {
      let screenDensity = value.screenDensity;
      let deviceType = value.deviceType;
    }).catch((error: BusinessError) => {
      console.error("getDeviceCapability promise error is " + error);
    });
  } catch (error) {
    console.error("getDeviceCapability promise error is " + error);
  }
  ```

### release<sup>7+</sup>

release()

Releases a **ResourceManager** object. This API is not supported currently.

**System capability**: SystemCapability.Global.ResourceManager

**Example**
  ```ts
  try {
    this.context.resourceManager.release();
  } catch (error) {
    console.error("release error is " + error);
  }
  ```

### addResource<sup>10+</sup>

addResource(path: string) : void;

Loads resources from the specified path.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                    | Mandatory  | Description  |
| -------- | ---------------------- | ---- | ---- |
| path | string | Yes   | Resource path.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001010  | If the overlay path is invalid.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  let path = getContext().bundleCodeDir + "/library1-default-signed.hsp";
  try {
    this.context.resourceManager.addResource(path);
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`addResource failed, error code: ${code}, message: ${message}.`);
  }
  ```

### removeResource<sup>10+</sup>

removeResource(path: string) : void;

Removes the resources loaded from the specified path to restore the original resources.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type           | Mandatory  | Description  |
| -------- | ---------------------- | ---- | ---- |
| path | string | Yes   | Resource path.|

**Error codes**

For details about the error codes, see [Resource Manager Error Codes](../errorcodes/errorcode-resource-manager.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 9001010  | If the overlay path is invalid.            |

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  let path = getContext().bundleCodeDir + "/library1-default-signed.hsp";
  try {
    this.context.resourceManager.removeResource(path);
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`removeResource failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getLocales<sup>11+</sup>

getLocales(includeSystem?: boolean): Array\<string>

Obtains the language list of an application.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name        | Type   | Mandatory  | Description      |
| -------------- | ------- | ------ | -------------------- |
| includeSystem  | boolean |  No   | Whether system resources are included. The default value is **false**.<br> **false**: Only application resources are included.<br>**true**: Both system and application resources are included.<br>If the value of **includeSystem** is invalid, the language list of system resources will be returned.|

**Return value**

| Type                       | Description         |
| ------------------------- | ----------- |
| Array\<string> | Language list. The strings in the list are comprised of the language, script (optional), and region (optional), which are connected by a hyphen (-).|

**Example**
  ```ts
  import resourceManager from '@ohos.resourceManager';
  import { BusinessError } from '@ohos.base';

  try {
    this.context.resourceManager.getLocales(); // Obtain only the language list of application resources.
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getLocales failed, error code: ${code}, message: ${message}.`);
  }

  try {
    resourceManager.getSystemResourceManager().getLocales(); // Obtain only the language list of system resources.
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getLocales failed, error code: ${code}, message: ${message}.`);
  }

  try {
    this.context.resourceManager.getLocales(true); // Obtain the language list of application resources and resources.
  } catch (error) {
    let code = (error as BusinessError).code;
    let message = (error as BusinessError).message;
    console.error(`getLocales failed, error code: ${code}, message: ${message}.`);
  }
  ```

### getString<sup>(deprecated)</sup>

getString(resId: number, callback: AsyncCallback&lt;string&gt;): void

Obtains the string corresponding to the specified resource ID. This API uses an asynchronous callback to return the result.

This API is deprecated since API version 9. You are advised to use [getStringValue](#getstringvalue9) instead.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                         | Mandatory  | Description             |
| -------- | --------------------------- | ---- | --------------- |
| resId    | number                      | Yes   | Resource ID.          |
| callback | AsyncCallback&lt;string&gt; | Yes   | Callback used to return the result.|

**Example**
  ```ts
  resourceManager.getResourceManager((error, mgr) => {
      mgr.getString($r('app.string.test').id, (error, value) => {
          if (error != null) {
              console.log("error is " + error);
          } else {
              let str = value;
          }
      });
  });
  ```


### getString<sup>(deprecated)</sup>

getString(resId: number): Promise&lt;string&gt;

Obtains the string corresponding to the specified resource ID. This API uses a promise to return the result.

This API is deprecated since API version 9. You are advised to use [getStringValue](#getstringvalue9-1) instead.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|

**Return value**

| Type                   | Description         |
| --------------------- | ----------- |
| Promise&lt;string&gt; | Promise used to return the result.|

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  resourceManager.getResourceManager((error, mgr) => {
      mgr.getString($r('app.string.test').id).then((value: string) => {
          let str = value;
      }).catch((error: BusinessError) => {
          console.log("getstring promise error is " + error);
      });
  });
  ```


### getStringArray<sup>(deprecated)</sup>

getStringArray(resId: number, callback: AsyncCallback&lt;Array&lt;string&gt;&gt;): void

Obtains the string array corresponding to the specified resource ID. This API uses an asynchronous callback to return the result.

This API is deprecated since API version 9. You are advised to use [getStringArrayValue](#getstringarrayvalue9) instead.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                                      | Mandatory  | Description               |
| -------- | ---------------------------------------- | ---- | ----------------- |
| resId    | number                                   | Yes   | Resource ID.            |
| callback | AsyncCallback&lt;Array&lt;string&gt;&gt; | Yes   | Callback used to return the result.|

**Example**
  ```ts
  resourceManager.getResourceManager((error, mgr) => {
      mgr.getStringArray($r('app.strarray.test').id, (error, value) => {
          if (error != null) {
              console.log("error is " + error);
          } else {
              let strArray = value;
          }
      });
  });
  ```


### getStringArray<sup>(deprecated)</sup>

getStringArray(resId: number): Promise&lt;Array&lt;string&gt;&gt;

Obtains the string array corresponding to the specified resource ID. This API uses a promise to return the result.

This API is deprecated since API version 9. You are advised to use [getStringArrayValue](#getstringarrayvalue9-1) instead.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|

**Return value**

| Type                                | Description           |
| ---------------------------------- | ------------- |
| Promise&lt;Array&lt;string&gt;&gt; | Promise used to return the result.|

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  resourceManager.getResourceManager((error, mgr) => {
       mgr.getStringArray($r('app.strarray.test').id).then((value: Array<string>) => {
          let strArray = value;
      }).catch((error: BusinessError) => {
          console.log("getStringArray promise error is " + error);
      });
  });
  ```


### getMedia<sup>(deprecated)</sup>

getMedia(resId: number, callback: AsyncCallback&lt;Uint8Array&gt;): void

Obtains the media file content corresponding to the specified resource ID. This API uses an asynchronous callback to return the result.

This API is deprecated since API version 9. You are advised to use [getMediaContent](#getmediacontent9) instead.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                             | Mandatory  | Description                |
| -------- | ------------------------------- | ---- | ------------------ |
| resId    | number                          | Yes   | Resource ID.             |
| callback | AsyncCallback&lt;Uint8Array&gt; | Yes   | Callback used to return the result.|

**Example**
  ```ts
  resourceManager.getResourceManager((error, mgr) => {
      mgr.getMedia($r('app.media.test').id, (error, value) => {
          if (error != null) {
              console.log("error is " + error);
          } else {
              let media = value;
          }
      });
  });
  ```


### getMedia<sup>(deprecated)</sup>

getMedia(resId: number): Promise&lt;Uint8Array&gt;

Obtains the media file content corresponding to the specified resource ID. This API uses a promise to return the result.

This API is deprecated since API version 9. You are advised to use [getMediaContent](#getmediacontent9-1) instead.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|

**Return value**

| Type                       | Description            |
| ------------------------- | -------------- |
| Promise&lt;Uint8Array&gt; | Promise used to return the result.|

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  resourceManager.getResourceManager((error, mgr) => {
      mgr.getMedia($r('app.media.test').id).then((value: Uint8Array) => {
          let media = value;
      }).catch((error: BusinessError) => {
          console.log("getMedia promise error is " + error);
      });
  });
  ```


### getMediaBase64<sup>(deprecated)</sup>

getMediaBase64(resId: number, callback: AsyncCallback&lt;string&gt;): void

Obtains the Base64 code of the image corresponding to the specified resource ID. This API uses an asynchronous callback to return the result.

This API is deprecated since API version 9. You are advised to use [getMediaContentBase64](#getmediacontentbase649) instead.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                         | Mandatory  | Description                      |
| -------- | --------------------------- | ---- | ------------------------ |
| resId    | number                      | Yes   | Resource ID.                   |
| callback | AsyncCallback&lt;string&gt; | Yes   | Callback used to return the result.|

**Example**
  ```ts
  resourceManager.getResourceManager((error, mgr) => {
      mgr.getMediaBase64($r('app.media.test').id, (error, value) => {
          if (error != null) {
              console.log("error is " + error);
          } else {
              let media = value;
          }
      });
  });
  ```


### getMediaBase64<sup>(deprecated)</sup>

getMediaBase64(resId: number): Promise&lt;string&gt;

Obtains the Base64 code of the image corresponding to the specified resource ID. This API uses a promise to return the result.

This API is deprecated since API version 9. You are advised to use [getMediaContentBase64](#getmediacontentbase649-1) instead.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|

**Return value**

| Type                   | Description                  |
| --------------------- | -------------------- |
| Promise&lt;string&gt; | Promise used to return the result.|

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  resourceManager.getResourceManager((error, mgr) => {
      mgr.getMediaBase64($r('app.media.test').id).then((value: string) => {
          let media = value;
      }).catch((error: BusinessError) => {
          console.log("getMediaBase64 promise error is " + error);
      });
  });
  ```


### getPluralString<sup>(deprecated)</sup>

getPluralString(resId: number, num: number): Promise&lt;string&gt;

Obtains the singular-plural string corresponding to the specified resource ID based on the specified number. This API uses a promise to return the result.

This API is deprecated since API version 9. You are advised to use [getPluralStringValue](#getpluralstringvalue9) instead.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name  | Type    | Mandatory  | Description   |
| ----- | ------ | ---- | ----- |
| resId | number | Yes   | Resource ID.|
| num   | number | Yes   | Number.  |

**Return value**

| Type                   | Description                       |
| --------------------- | ------------------------- |
| Promise&lt;string&gt; | Promise used to return the result.|

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  resourceManager.getResourceManager((error, mgr) => {
      mgr.getPluralString($r("app.plural.test").id, 1).then((value: string) => {
          let str = value;
      }).catch((error: BusinessError) => {
          console.log("getPluralString promise error is " + error);
      });
  });
  ```


### getPluralString<sup>(deprecated)</sup>

getPluralString(resId: number, num: number, callback: AsyncCallback&lt;string&gt;): void

Obtains the singular-plural string corresponding to the specified resource ID based on the specified number. This API uses an asynchronous callback to return the result.

This API is deprecated since API version 9. You are advised to use [getPluralStringValue](#getpluralstringvalue9-1) instead.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                         | Mandatory  | Description                             |
| -------- | --------------------------- | ---- | ------------------------------- |
| resId    | number                      | Yes   | Resource ID.                          |
| num      | number                      | Yes   | Number.                            |
| callback | AsyncCallback&lt;string&gt; | Yes   | Callback used to return the result.|

**Example**
  ```ts
  resourceManager.getResourceManager((error, mgr) => {
      mgr.getPluralString($r("app.plural.test").id, 1, (error, value) => {
          if (error != null) {
              console.log("error is " + error);
          } else {
              let str = value;
          }
      });
  });
  ```


### getRawFile<sup>(deprecated)</sup>

getRawFile(path: string, callback: AsyncCallback&lt;Uint8Array&gt;): void

Obtains the content of the raw file in the **resources/rawfile** directory. This API uses an asynchronous callback to return the result.

This API is deprecated since API version 9. You are advised to use [getRawFileContent](#getrawfilecontent9) instead.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                             | Mandatory  | Description                     |
| -------- | ------------------------------- | ---- | ----------------------- |
| path     | string                          | Yes   | Path of the raw file.            |
| callback | AsyncCallback&lt;Uint8Array&gt; | Yes   | Callback used to return the result.|

**Example**
  ```ts
  resourceManager.getResourceManager((error, mgr) => {
      mgr.getRawFile("test.txt", (error, value) => {
          if (error != null) {
              console.log("error is " + error);
          } else {
              let rawFile = value;
          }
      });
  });
  ```


### getRawFile<sup>(deprecated)</sup>

getRawFile(path: string): Promise&lt;Uint8Array&gt;

Obtains the content of the raw file in the **resources/rawfile** directory. This API uses a promise to return the result.

This API is deprecated since API version 9. You are advised to use [getRawFileContent](#getrawfilecontent9-1) instead.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name | Type    | Mandatory  | Description         |
| ---- | ------ | ---- | ----------- |
| path | string | Yes   | Path of the raw file.|

**Return value**

| Type                       | Description         |
| ------------------------- | ----------- |
| Promise&lt;Uint8Array&gt; | Promise used to return the result.|

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  resourceManager.getResourceManager((error, mgr) => {
      mgr.getRawFile("test.txt").then((value: Uint8Array) => {
          let rawFile = value;
      }).catch((error: BusinessError) => {
          console.log("getRawFile promise error is " + error);
      });
  });
  ```


### getRawFileDescriptor<sup>(deprecated)</sup>

getRawFileDescriptor(path: string, callback: AsyncCallback&lt;RawFileDescriptor&gt;): void

Obtains the descriptor of the raw file in the **resources/rawfile** directory. This API uses an asynchronous callback to return the result.

This API is deprecated since API version 9. You are advised to use [getRawFd](#getrawfd9) instead.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                                      | Mandatory  | Description                              |
| -------- | ---------------------------------------- | ---- | -------------------------------- |
| path     | string                                   | Yes   | Path of the raw file.                     |
| callback | AsyncCallback&lt;[RawFileDescriptor](#rawfiledescriptor8)&gt; | Yes   | Callback used to return the result.|

**Example**
  ```ts
  resourceManager.getResourceManager((error, mgr) => {
      mgr.getRawFileDescriptor("test.txt", (error, value) => {
          if (error != null) {
              console.log("error is " + error);
          } else {
              let fd = value.fd;
              let offset = value.offset;
              let length = value.length;
          }
      });
  });
  ```

### getRawFileDescriptor<sup>(deprecated)</sup>

getRawFileDescriptor(path: string): Promise&lt;RawFileDescriptor&gt;

Obtains the descriptor of the raw file in the **resources/rawfile** directory. This API uses a promise to return the result.

This API is deprecated since API version 9. You are advised to use [getRawFd](#getrawfd9-1) instead.

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name | Type    | Mandatory  | Description         |
| ---- | ------ | ---- | ----------- |
| path | string | Yes   | Path of the raw file.|

**Return value**

| Type                                      | Description                 |
| ---------------------------------------- | ------------------- |
| Promise&lt;[RawFileDescriptor](#rawfiledescriptor8)&gt; | Promise used to return the result.|

**Example**
  ```ts
  import { BusinessError } from '@ohos.base';

  resourceManager.getResourceManager((error, mgr) => {
      mgr.getRawFileDescriptor("test.txt").then((value: resourceManager.RawFileDescriptor) => {
          let fd = value.fd;
          let offset = value.offset;
          let length = value.length;
      }).catch((error: BusinessError) => {
          console.log("getRawFileDescriptor promise error is " + error);
      });
  });
  ```

### closeRawFileDescriptor<sup>(deprecated)</sup>

closeRawFileDescriptor(path: string, callback: AsyncCallback&lt;void&gt;): void

Closes the descriptor of the raw file in the **resources/rawfile** directory. This API uses an asynchronous callback to return the result.

This API is deprecated since API version 9. You are advised to use [closeRawFd](#closerawfd9).

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name     | Type                       | Mandatory  | Description         |
| -------- | ------------------------- | ---- | ----------- |
| path     | string                    | Yes   | Path of the raw file.|
| callback | AsyncCallback&lt;void&gt; | Yes   | Callback used to return the result.       |

**Example**
  ```ts
  resourceManager.getResourceManager((error, mgr) => {
      mgr.closeRawFileDescriptor("test.txt", (error, value) => {
          if (error != null) {
              console.log("error is " + error);
          }
      });
  });
  ```

### closeRawFileDescriptor<sup>(deprecated)</sup>

closeRawFileDescriptor(path: string): Promise&lt;void&gt;

Closes the descriptor of the raw file in the **resources/rawfile** directory. This API uses a promise to return the result.

This API is deprecated since API version 9. You are advised to use [closeRawFd](#closerawfd9-1).

**System capability**: SystemCapability.Global.ResourceManager

**Parameters**

| Name | Type    | Mandatory  | Description         |
| ---- | ------ | ---- | ----------- |
| path | string | Yes   | Path of the raw file.|

**Return value**

| Type                 | Description  |
| ------------------- | ---- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**
  ```ts
  resourceManager.getResourceManager((error, mgr) => {
      mgr.closeRawFileDescriptor("test.txt");
  });
  ```

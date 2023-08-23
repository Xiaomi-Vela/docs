# @ohos.app.form.formObserver (formObserver)

The **formObserver** module provides APIs related to widget listeners. You can use the APIs to subscribe to and unsubscribe from widget addition, removal, and visibility change events, and obtain information about running widgets.

> **NOTE**
>
> The initial APIs of this module are supported since API version 10. Newly added APIs will be marked with a superscript to indicate their earliest API version.
> The APIs provided by this module are system APIs.

## Modules to Import

```ts
import formObserver from '@ohos.app.form.formObserver';
```

## on('formAdd')

 on(type: 'formAdd', observerCallback: Callback&lt;formInfo.RunningFormInfo&gt;): void

Subscribes to widget addition events. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.OBSERVE_FORM_RUNNING

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type   | Mandatory| Description   |
| ------ | ------ | ---- | ------- |
| type | string | Yes  | Event type. The value **'formAdd'** indicates a widget addition event.|
| callback | Callback&lt;formInfo.RunningFormInfo&gt; | Yes| Callback used to return **RunningFormInfo** of the widget.|

**Example**

```ts
import formObserver from '@ohos.app.form.formObserver';
let callback = function(data) {
  console.log('a new form added, data: ${JSON.stringify(data)');
}

formObserver.on('formAdd', callback);
```

## on('formAdd')

 on(type: 'formAdd', bundleName: string, observerCallback: Callback&lt;formInfo.RunningFormInfo&gt;): void

Subscribes to widget addition events for a given bundle that functions as the widget host. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.OBSERVE_FORM_RUNNING

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type   | Mandatory| Description   |
| ------ | ------ | ---- | ------- |
| type | string | Yes  | Event type. The value **'formAdd'** indicates a widget addition event.|
| bundleName | string | Yes| Name of the bundle that functions as the widget host. If no value is passed in, widget addition events of all widget hosts are subscribed to.|
| callback | Callback&lt;formInfo.RunningFormInfo&gt; | Yes| Callback used to return **RunningFormInfo** of the widget.|


**Example**

```ts
import formObserver from '@ohos.app.form.formObserver';
let bundleName = 'ohos.samples.FormApplication';
let callback = function(data) {
  console.log('a new form added, data: ${JSON.stringify(data)');
}

formObserver.on('formAdd', bundleName, callback);
```

## off('formAdd')

 off(type: "formAdd", bundleName?: string, observerCallback?: Callback&lt;formInfo.RunningFormInfo&gt;): void

Unsubscribes from widget addition events. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.OBSERVE_FORM_RUNNING

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type   | Mandatory| Description   |
| ------ | ------ | ---- | ------- |
| type | string | Yes  | Event type. The value **'formAdd'** indicates a widget addition event.|
| bundleName | string | No| Name of the bundle that functions as the widget host.<br>To cancel the subscription for a given bundle name, this parameter must be set to the same value as **bundleName** in **on('formAdd')**.<br>If no value is passed in, the subscriptions for all the widget hosts are canceled. |
| callback | Callback&lt;formInfo.RunningFormInfo&gt; | No| Callback used to return **RunningFormInfo** of the widget. If no value is passed in, all the subscriptions to the specified event are canceled.<br>To cancel the subscription with a given callback, this parameter must be set to the same value as **callback** in **on('formAdd')**. |


**Example**

```ts
import formObserver from '@ohos.app.form.formObserver';
let bundleName = 'ohos.samples.FormApplication';
let callback = function(data) {
  console.log('a new form added, data: ${JSON.stringify(data)');
}

formObserver.off('formAdd', callback);
formObserver.off('formAdd', bundleName, callback);
```
> **NOTE**
> **on('formAdd', callback)** and **off('formAdd', callback)** must be used in pairs.
> **on('formAdd', bundleName, callback)** and **off('formAdd', bundleName, callback)** must be used in pairs.
> To cancel the subscription with a given callback or for a given bundle name, the **callback** or **bundleName** parameter in **off()** must be set to the same value as that in **on()**.

## on('formRemove')

 on(type: 'formRemove', observerCallback: Callback&lt;formInfo.RunningFormInfo&gt;): void

Subscribes to widget removal events. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.OBSERVE_FORM_RUNNING

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type   | Mandatory| Description   |
| ------ | ------ | ---- | ------- |
| type | string | Yes  | Event type. The value **'formRemove'** indicates a widget removal event.|
| callback | Callback&lt;formInfo.RunningFormInfo&gt; | Yes| Callback used to return **RunningFormInfo** of the widget.|

**Example**

```ts
import formObserver from '@ohos.app.form.formObserver';
let callback = function(data) {
  console.log('form deleted, data: ${JSON.stringify(data)');
}

formObserver.on('formRemove', callback);
```

## on('formRemove')

 on(type: 'formRemove', bundleName: string, observerCallback: Callback&lt;formInfo.RunningFormInfo&gt;): void

Subscribes to widget removal events for a given bundle, which functions as the widget host. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.OBSERVE_FORM_RUNNING

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type   | Mandatory| Description   |
| ------ | ------ | ---- | ------- |
| type | string | Yes  | Event type. The value **'formRemove'** indicates a widget removal event.|
| bundleName | string | Yes| Name of the bundle that functions as the widget host. If no value is passed in, widget removal events of all widget hosts are subscribed to.|
| callback | Callback&lt;formInfo.RunningFormInfo&gt; | Yes| Callback used to return **RunningFormInfo** of the widget.|


**Example**

```ts
import formObserver from '@ohos.app.form.formObserver';
let bundleName = 'ohos.samples.FormApplication';
let callback = function(data) {
  console.log('form deleted, data: ${JSON.stringify(data)');
}

formObserver.on('formRemove', bundleName, callback);
```

## off('formRemove')

off(type: "formRemove", bundleName?: string, observerCallback?: Callback&lt;formInfo.RunningFormInfo&gt;): void

Unsubscribes from widget removal events. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.OBSERVE_FORM_RUNNING

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type   | Mandatory| Description   |
| ------ | ------ | ---- | ------- |
| type | string | Yes  | Event type. The value **'formRemove'** indicates a widget removal event.|
| bundleName | string | No| Name of the bundle that functions as the widget host.<br>To cancel the subscription for a given bundle name, this parameter must be set to the same value as **bundleName** in **on('formRemove')**.<br>If no value is passed in, the subscriptions for all the widget hosts are canceled. |
| callback | Callback&lt;formInfo.RunningFormInfo&gt; | No| Callback used to return **RunningFormInfo** of the widget. If no value is passed in, all the subscriptions to the specified event are canceled.<br>To cancel the subscription with a given callback, this parameter must be set to the same value as **callback** in **on('formRemove')**. |

**Example**

```ts
import formObserver from '@ohos.app.form.formObserver';
let bundleName = 'ohos.samples.FormApplication';
let callback = function(data) {
  console.log('a new form added, data: ${JSON.stringify(data)');
}

formObserver.off('formRemove', callback);
formObserver.off('formRemove', bundleName, callback);
```
> **NOTE**
> **on('formRemove', callback)** and **off('formRemove', callback)** must be used in pairs.
> **on('formRemove', bundleName, callback)** and **off('formRemove', bundleName, callback)** must be used in pairs.
> To cancel the subscription with a given callback or for a given bundle name, the **callback** or **bundleName** parameter in **off()** must be set to the same value as that in **on()**.

## on('notifyVisible')

 on(type: 'notifyVisible', observerCallback: Callback&lt;Array&lt;[formInfo.RunningFormInfo](js-apis-app-form-formInfo.md)&gt;&gt;): void

Subscribes to events indicating that a widget becomes visible.

This event is triggered when **notifyVisibleForms** is called to make a widget visible.

**Required permissions**: ohos.permission.OBSERVE_FORM_RUNNING

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name    | Type                                                        | Mandatory| Description                                                        |
| ---------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type       | string                                                       | Yes  | Event type. This value **'notifyVisible'** indicates a widget visibility event.     |
| callback   | Callback &lt;Array&lt;[formInfo.RunningFormInfo](js-apis-app-form-formInfo.md)&gt;&gt; | Yes  | Callback used to return **RunningFormInfo** of the widget.           |

**Example**

```ts
import formObserver from '@ohos.app.form.formObserver';
let callback = function(data) {
  console.log('form change visibility, data: ${JSON.stringify(data)');
}

formObserver.on('notifyVisible', callback);
```

## on('notifyVisible')

 on(type: 'notifyVisible', bundleName: string, observerCallback: Callback&lt;Array&lt;[formInfo.RunningFormInfo](js-apis-app-form-formInfo.md)&gt;&gt;): void

Subscribes to events indicating that a widget becomes visible for a given bundle, which functions as the widget host.

This event is triggered when **notifyVisibleForms** is called to make a widget visible.

**Required permissions**: ohos.permission.OBSERVE_FORM_RUNNING

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name    | Type                                                        | Mandatory| Description                                                        |
| ---------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type       | string                                                       | Yes  | Event type. This value **'notifyVisible'** indicates a widget visibility event.     |
| bundleName | string                                                       | Yes  | Name of the bundle that functions as the widget host, on which the widget visibility state changes are subscribed.|
| callback   | Callback &lt;Array&lt;[formInfo.RunningFormInfo](js-apis-app-form-formInfo.md)&gt;&gt; | Yes  | Callback used to return **RunningFormInfo** of the widget.           |


**Example**

```ts
import formObserver from '@ohos.app.form.formObserver';
let bundleName = 'ohos.samples.FormApplication';
let callback = function(data) {
  console.log('form change visibility, data: ${JSON.stringify(data)');
}

formObserver.on('notifyVisible', bundleName, callback);
```

## off('notifyVisible')

 off(type: "notifyVisible", bundleName?: string, observerCallback?: Callback&lt;Array&lt;[formInfo.RunningFormInfo](js-apis-app-form-formInfo.md)&gt;&gt;): void

Unsubscribes from events indicating that a widget becomes visible.

**Required permissions**: ohos.permission.OBSERVE_FORM_RUNNING

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name    | Type                                                        | Mandatory| Description                                                        |
| ---------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type       | string                                                       | Yes  | Event type. This value **'notifyVisible'** indicates a widget visibility event.|
| bundleName | string                                                       | No  | Name of the bundle that functions as the widget host, on which the widget visibility state changes are subscribed.<br>To cancel the subscription for a given bundle name, this parameter must be set to the same value as **bundleName** in **on('notifyVisible')**. |
| callback   | Callback &lt;Array&lt;[formInfo.RunningFormInfo](js-apis-app-form-formInfo.md)&gt;&gt; | No  | Callback registered during the subscription. If no value is passed in, all the subscriptions to the specified event are canceled.<br>To cancel the subscription with a given callback, this parameter must be set to the same value as **callback** in **on('notifyVisible')**. |


**Example**

```ts
import formObserver from '@ohos.app.form.formObserver';
let bundleName = 'ohos.samples.FormApplication';
let callback = function(data) {
  console.log('form change visibility, data: ${JSON.stringify(data)');
}

formObserver.off('notifyVisible', callback);
formObserver.off('notifyVisible', bundleName, callback);
```

> **NOTE**
> **on('notifyVisible', callback)** and **off('notifyVisible', callback)** must be used in pairs.
> **on('notifyVisible', bundleName, callback)** and **off('notifyVisible', bundleName, callback)** must be used in pairs.
> To cancel the subscription with a given callback or for a given bundle name, the **callback** or **bundleName** parameter in **off()** must be set to the same value as that in **on()**.

## on('notifyInvisible')

 on(type: 'notifyInvisible', observerCallback: Callback&lt;Array&lt;[formInfo.RunningFormInfo](js-apis-app-form-formInfo.md)&gt;>): void

Subscribes to events indicating that a widget becomes invisible.

This event is triggered when **notifyInvisibleForms** is called to make a widget invisible.

**Required permissions**: ohos.permission.OBSERVE_FORM_RUNNING

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name    | Type                                                        | Mandatory| Description                                                        |
| ---------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type       | string                                                       | Yes  | Event type. This value **'notifyInvisible'** indicates a widget invisibility event.     |
| callback   | Callback &lt;Array&lt;[formInfo.RunningFormInfo](js-apis-app-form-formInfo.md)&gt;&gt; | Yes  | Callback used to return **RunningFormInfo** of the widget.         |

**Example**

```ts
import formObserver from '@ohos.app.form.formObserver';
let callback = function(data) {
  console.log('form change invisibility, data: ${JSON.stringify(data)');
}

formObserver.on('notifyInvisible', callback);
```


## on('notifyInvisible')

 on(type: 'notifyInvisible', bundleName: string, observerCallback: Callback&lt;Array&lt;[formInfo.RunningFormInfo](js-apis-app-form-formInfo.md)&gt;>): void

Subscribes to events indicating that a widget becomes invisible for a given bundle, which functions as the widget host.

This event is triggered when **notifyInvisibleForms** is called to make a widget invisible.

**Required permissions**: ohos.permission.OBSERVE_FORM_RUNNING

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name    | Type                                                        | Mandatory| Description                                                        |
| ---------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type       | string                                                       | Yes  | Event type. This value **'notifyInvisible'** indicates a widget invisibility event.     |
| bundleName | string                                                       | Yes  | Name of the bundle that functions as the widget host, on which the widget visibility state changes are subscribed.|
| callback   | Callback &lt;Array&lt;[formInfo.RunningFormInfo](js-apis-app-form-formInfo.md)&gt;&gt; | Yes  | Callback used to return **RunningFormInfo** of the widget.         |

**Example**

```ts
import formObserver from '@ohos.app.form.formObserver';
let bundleName = 'ohos.samples.FormApplication';
let callback = function(data) {
  console.log('form change invisibility, data: ${JSON.stringify(data)');
}

formObserver.on('notifyInvisible', bundleName, callback);
```

## off('notifyInvisible')

 off(type: "notifyInvisible", bundleName?: string, observerCallback?: Callback&lt;Array&lt;[formInfo.RunningFormInfo](js-apis-app-form-formInfo.md)>&gt;): void

Unsubscribes from events indicating that a widget becomes invisible.

**Required permissions**: ohos.permission.OBSERVE_FORM_RUNNING

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name    | Type                                                        | Mandatory| Description                                                        |
| ---------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type       | string                                                       | Yes  | Event type. This value **'notifyInvisible'** indicates a widget invisibility event.   |
| bundleName | string                                                       | No  | Name of the bundle that functions as the widget host, on which the widget visibility state changes are subscribed.<br>To cancel the subscription for a given bundle name, this parameter must be set to the same value as **bundleName** in **on('notifyInvisible')**. |
| callback   | Callback &lt;Array&lt;[formInfo.RunningFormInfo](js-apis-app-form-formInfo.md)&gt;&gt; | No  | Callback registered during the subscription. If no value is passed in, all the subscriptions to the specified event are canceled.<br>To cancel the subscription with a given callback, this parameter must be set to the same value as **callback** in **on('notifyInvisible')**. |

**Example**

```ts
import formObserver from '@ohos.app.form.formObserver';
let bundleName = 'ohos.samples.FormApplication';
let callback = function(data) {
  console.log('form change invisibility, data: ${JSON.stringify(data)');
}

formObserver.off('notifyInvisible', callback);
formObserver.off('notifyInvisible', bundleName, callback);
```

> **NOTE**
> **on('notifyInvisible', callback)** and **off('notifyInvisible', callback)** must be used in pairs.
> **on('notifyInvisible', bundleName, callback)** and **off('notifyInvisible', bundleName, callback)** must be used in pairs.
> To cancel the subscription with a given callback or for a given bundle name, the **callback** or **bundleName** parameter in **off()** must be set to the same value as that in **on()**.


## getRunningFormInfos

getRunningFormInfos(callback: AsyncCallback&lt;Array&lt;formInfo.RunningFormInfo&gt;&gt;, hostBundleName?: string): void

Obtains information about all non-temporary widgets running on the device. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.OBSERVE_FORM_RUNNING

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type   | Mandatory| Description   |
| ------ | ------ | ---- | ------- |
| callback | AsyncCallback&lt;Array&lt;formInfo.RunningFormInfo&gt;&gt; | Yes| Callback used to return the result. If the widget information is obtained, **error** is undefined and **data** is the information obtained.|
| hostBundleName | string | No| Name of the bundle that functions as the widget host. If a value is passed in, only the information about the non-temporary widgets that are running under the widget host is returned.<br>If no value is passed in, information about all running non-temporary widgets on the device is returned. |

**Error codes**
For details about the error codes, see [Form Error Codes](../errorcodes/errorcode-form.md).

| ID| Error Message|
| -------- | -------- |
| 16500050 | An IPC connection error happened. |
| 16500060 | A service connection error happened, please try again later. |

**Example**

```ts
import formObserver from '@ohos.app.form.formObserver';

try {
  formObserver.getRunningFormInfos((error, data) => {
    if (error) {
      console.error(`error, code: ${error.code}, message: ${error.message}`);
    } else {
      console.log('formObserver getRunningFormInfos, data: ${JSON.stringify(data)}');
    }
  }, 'com.example.ohos.formjsdemo');
} catch(error) {
  console.error(`catch error, code: ${error.code}, message: ${error.message}`);
}
```

## getRunningFormInfos

getRunningFormInfos(hostBundleName?: string):  Promise&lt;Array&lt;formInfo.RunningFormInfo&gt;&gt;

Obtains information about all non-temporary widgets running on the device. This API uses a promise to return the result.

**Required permissions**: ohos.permission.OBSERVE_FORM_RUNNING

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type   | Mandatory| Description   |
| ------ | ------ | ---- | ------- |
| hostBundleName | string | No| Name of the bundle that functions as the widget host. If a value is passed in, only the information about the non-temporary widgets that are running under the widget host is returned.<br>If no value is passed in, information about all running non-temporary widgets on the device is returned. |

**Return value**

| Type                                                        | Description                               |
| :----------------------------------------------------------- | :---------------------------------- |
| Promise&lt;Array&lt;[formInfo.RunningFormInfo](js-apis-app-form-formInfo.md)&gt;&gt; | Promise used to return the information obtained.|

**Error codes**
For details about the error codes, see [Form Error Codes](../errorcodes/errorcode-form.md).

| ID| Error Message|
| -------- | -------- |
| 16500050 | An IPC connection error happened. |
| 16500060 | A service connection error happened, please try again later. |

**Example**

```ts
import formObserver from '@ohos.app.form.formObserver';

try {
  formObserver.getRunningFormInfos('com.example.ohos.formjsdemo').then((data) => {
    console.log('formObserver getRunningFormInfos, data: ${JSON.stringify(data)}');
  }).catch((error) => {
    console.error(`error, code: ${error.code}, message: ${error.message}`);
  });
} catch(error) {
  console.error(`catch error, code: ${error.code}, message: ${error.message}`);
}
```

## getRunningFormInfosByFilter

getRunningFormInfosByFilter(formProviderFilter: formInfo.FormProviderFilter): Promise&lt;Array&lt;formInfo.RunningFormInfo&gt;&gt;

Obtains the information about widget hosts based on the widget provider information. This API uses a promise to return the result.

**Required permissions**: ohos.permission.OBSERVE_FORM_RUNNING

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name     | Type           | Mandatory| Description                            |
| ----------- | --------------- | ---- | -------------------------------- |
| formProviderFilter     | [formInfo.FormProviderFilter](js-apis-app-form-formInfo.md#formProviderFilter) | Yes  | Information about the widget provider.|

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;Array&lt;[formInfo.RunningFormInfo](js-apis-app-form-formInfo.md#RunningFormInfo)&gt;&gt; | Promise used to return the widget host information obtained.|

**Error codes**

For details about the error codes, see [Form Error Codes](../errorcodes/errorcode-form.md).

| ID| Error Message|
| -------- | -------- |
| 201 | Permissions denied. |
| 202 | The application is not a system application. |
| 401 | If the input parameter is not valid parameter. |
| 16500050 | An IPC connection error happened. |
| 16500100 | Failed to obtain the configuration information. |
| 16501000  | An internal functional error occurred. |


```ts
import formObserver from '@ohos.app.form.formObserver';

let formInstanceFilter = {
  bundleName: "com.example.formprovide",
  abilityName: "EntryFormAbility",
  formName: "widget",
  moduleName: "entry"
}
try {
  formObserver.getRunningFormInfosByFilter(formInstanceFilter).then(data1 => {
    console.info('formObserver getRunningFormInfosByFilter return err :');
  }).catch((error) => {
    console.error(`error, code: ${error.code}, message: ${error.message}`);
  });
} catch(error) {
  console.error(`catch error, code: ${error.code}, message: ${error.message}`);
}
```

## getRunningFormInfosByFilter

getRunningFormInfosByFilter(formProviderFilter: formInfo.FormProviderFilter, callback: AsyncCallback&lt;Array&lt;formInfo.RunningFormInfo&gt;&gt;): void

Obtains the information about widget hosts based on the widget provider information. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.OBSERVE_FORM_RUNNING

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name     | Type           | Mandatory| Description                            |
| ----------- | --------------- | ---- | -------------------------------- |
| formProviderFilter     | [formInfo.FormProviderFilter](js-apis-app-form-formInfo.md#formProviderFilter) | Yes  | Information about the widget provider.|
| callback | AsyncCallback&lt;Array&lt;[formInfo.RunningFormInfo](js-apis-app-form-formInfo.md)&gt;&gt; | Yes| Callback used to return the result. If the widget host information is obtained, **error** is **undefined** and **data** is the information obtained; otherwise, **error** is an error object.|

**Error codes**

For details about the error codes, see [Form Error Codes](../errorcodes/errorcode-form.md).

| ID| Error Message|
| -------- | -------- |
| 201 | Permissions denied. |
| 202 | The application is not a system application. |
| 401 | If the input parameter is not valid parameter. |
| 16500050 | An IPC connection error happened. |
| 16500100 | Failed to obtain the configuration information. |
| 16501000  | An internal functional error occurred. |


```ts
import formObserver from '@ohos.app.form.formObserver';

let formInstanceFilter = {
  bundleName: "com.example.formprovide",
  abilityName: "EntryFormAbility",
  formName: "widget",
  moduleName: "entry"
}
try {
  formObserver.getRunningFormInfosByFilter(formInstanceFilter,(error, data) => {
    if (error) {
      console.error(`error, code: ${error.code}, message: ${error.message}`);
    } else {
      console.log('formObserver getRunningFormInfosByFilter, data: ${JSON.stringify(data)}');
    }
  });
} catch(error) {
  console.error(`catch error, code: ${error.code}, message: ${error.message}`);
}
```

## getRunningFormInfoById

getRunningFormInfoById(formId: string): Promise&lt;formInfo.RunningFormInfo&gt;


Obtains the information about widget hosts based on the widget ID. This API uses a promise to return the result.

**Required permissions**: ohos.permission.OBSERVE_FORM_RUNNING

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name     | Type           | Mandatory| Description                            |
| ----------- | --------------- | ---- | -------------------------------- |
| formId     | string | Yes  | Widget ID.|

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;[formInfo.RunningFormInfo](js-apis-app-form-formInfo.md)&gt; | Promise used to return the widget host information obtained.|

**Error codes**

For details about the error codes, see [Form Error Codes](../errorcodes/errorcode-form.md).

| ID| Error Message|
| -------- | -------- |
| 201 | Permissions denied. |
| 202 | The application is not a system application. |
| 401 | If the input parameter is not valid parameter. |
| 16500050 | An IPC connection error happened. |
| 16500100 | Failed to obtain the configuration information. |
| 16501000  | An internal functional error occurred. |


```ts
import formObserver from '@ohos.app.form.formObserver';
let formId = '12400633174999288';
try {
  formObserver.getRunningFormInfoById(formId).then(data1 => {
    console.info('formObserver getRunningFormInfoById return err :');
  }).catch((error) => {
    console.error(`error, code: ${error.code}, message: ${error.message}`);
  });
} catch(error) {
  console.error(`catch error, code: ${error.code}, message: ${error.message}`);
}
```

## getRunningFormInfoById

getRunningFormInfoById(formId: string, callback: AsyncCallback&lt;formInfo.RunningFormInfo&gt;): void

Obtains the information about widget hosts based on the widget provider information. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.OBSERVE_FORM_RUNNING

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name     | Type           | Mandatory| Description                            |
| ----------- | --------------- | ---- | -------------------------------- |
| formId     | string | Yes  | Widget ID.|
| callback | AsyncCallback&lt;[formInfo.RunningFormInfo](js-apis-app-form-formInfo.md)&gt; | Yes| Callback used to return the result. If the widget host information is obtained, **error** is **undefined** and **data** is the information obtained; otherwise, **error** is an error object.|

**Error codes**

For details about the error codes, see [Form Error Codes](../errorcodes/errorcode-form.md).

| ID| Error Message|
| -------- | -------- |
| 201 | Permissions denied. |
| 202 | The application is not a system application. |
| 401 | If the input parameter is not valid parameter. |
| 16500050 | An IPC connection error happened. |
| 16500100 | Failed to obtain the configuration information. |
| 16501000  | An internal functional error occurred. |

```ts
import formObserver from '@ohos.app.form.formObserver';

let formId = '12400633174999288';
try {
  formObserver.getRunningFormInfoById(formId,(error, data) => {
    if (error) {
      console.error(`error, code: ${error.code}, message: ${error.message}`);
    } else {
      console.log('formObserver getRunningFormInfoById, data: ${JSON.stringify(data)}');
    }
  });
} catch(error) {
  console.error(`catch error, code: ${error.code}, message: ${error.message}`);
}
```

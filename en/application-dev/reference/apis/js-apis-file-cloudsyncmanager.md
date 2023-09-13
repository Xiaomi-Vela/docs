# @ohos.file.cloudSyncManager (Device-Cloud Synchronization Management)

The **cloudSyncManager** module provides APIs for managing device-cloud synergy for applications. You can use the APIs to enable or disable device-cloud synergy, change the device-cloud synchronization switch for an application, notify cloud data changes, and clear or retain cloud files when a cloud account exits.

> **NOTE**
>
> - The initial APIs of this module are supported since API version 10. Newly added APIs will be marked with a superscript to indicate their earliest API version.
> - The APIs of this module are system APIs and cannot be called by third-party applications.

## Modules to Import

```js
import cloudSyncManager from '@ohos.file.cloudSyncManager'
```

## cloudSyncManager.changeAppCloudSwitch

changeAppCloudSwitch(accountId: string, bundleName: string, status: boolean): Promise&lt;void&gt;

Changes the device-cloud file synchronization switch for an application. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.DistributedFileService.CloudSyncManager

**Parameters**

| Name    | Type  | Mandatory| Description|
| ---------- | ------ | ---- | ---- |
| accountId | string | Yes  | Account ID.|
| bundleName | string | Yes  | Bundle name of the application.|
| status | boolean | Yes  | State of the cloud-device file synchronization switch to set. The value **true** means to enable this function; the value **false** means the opposite.|

**Return value**

| Type                 | Description            |
| --------------------- | ---------------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID                    | Error Message       |
| ---------------------------- | ---------- |
| 201 | Permission verification failed. |
| 202 | The caller is not a system application. |
| 401 | The input parameter is invalid. |

**Example**

  ```js
  let accountId = "testAccount";
  let bundleName = "com.example.bundle";
  cloudSyncManager.changeAppCloudSwitch(accountId, bundleName, true).then(function() {
      console.info("changeAppCloudSwitch successfully");
  }).catch(function(err) {
      console.info("changeAppCloudSwitch failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## cloudSyncManager.changeAppCloudSwitch

changeAppCloudSwitch(accountId: string, bundleName: string, status: boolean, callback: AsyncCallback&lt;void&gt;): void

Changes the device-cloud file synchronization switch for an application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.DistributedFileService.CloudSyncManager

**Parameters**

| Name    | Type  | Mandatory| Description|
| ---------- | ------ | ---- | ---- |
| accountId | string | Yes  | Account ID.|
| bundleName | string | Yes  | Bundle name of the application.|
| status | boolean | Yes  | State of the cloud-device file synchronization switch to set. The value **true** means to enable this function; the value **false** means the opposite.|
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback invoked to return the result.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID                    | Error Message       |
| ---------------------------- | ---------- |
| 201 | Permission verification failed. |
| 202 | The caller is not a system application. |
| 401 | The input parameter is invalid. |

**Example**

  ```js
  let accountId = "testAccount";
  let bundleName = "com.example.bundle";
  cloudSyncManager.changeAppCloudSwitch(accountId, bundleName, true, (err) => {
    if (err) {
      console.info("changeAppCloudSwitch failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("changeAppCloudSwitch successfully");
    }
  });
  ```

## cloudSyncManager.notifyDataChange

notifyDataChange(accountId: string, bundleName: string): Promise&lt;void&gt;

Notifies the cloud and device services of the application data change in the cloud. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.DistributedFileService.CloudSyncManager

**Parameters**

| Name    | Type  | Mandatory| Description|
| ---------- | ------ | ---- | ---- |
| accountId | string | Yes  | Account ID.|
| bundleName | string | Yes  | Bundle name of the application.|

**Return value**

| Type                 | Description            |
| --------------------- | ---------------- |
| Promise&lt;void&gt; | Promise used to return the application data change in the cloud.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID                    | Error Message       |
| ---------------------------- | ---------- |
| 201 | Permission verification failed. |
| 202 | The caller is not a system application. |
| 401 | The input parameter is invalid. |

**Example**

  ```js
  let accountId = "testAccount";
  let bundleName = "com.example.bundle";
  cloudSyncManager.notifyDataChange(accountId, bundleName).then(function() {
      console.info("notifyDataChange successfully");
  }).catch(function(err) {
      console.info("notifyDataChange failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## cloudSyncManager.notifyDataChange

notifyDataChange(accountId: string, bundleName: string, callback: AsyncCallback&lt;void&gt;): void

Notifies the cloud and device services of the application data change in the cloud. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.DistributedFileService.CloudSyncManager

**Parameters**

| Name    | Type  | Mandatory| Description|
| ---------- | ------ | ---- | ---- |
| accountId | string | Yes  | Account ID.|
| bundleName | string | Yes  | Bundle name of the application.|
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback invoked to return the application data change in the cloud.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID                    | Error Message       |
| ---------------------------- | ---------- |
| 201 | Permission verification failed. |
| 202 | The caller is not a system application. |
| 401 | The input parameter is invalid. |

**Example**

  ```js
  let accountId = "testAccount";
  let bundleName = "com.example.bundle";
  cloudSyncManager.notifyDataChange(accountId, bundleName, (err) => {
    if (err) {
      console.info("notifyDataChange failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("notifyDataChange successfully");
    }
  });
  ```

## cloudSyncManager.enableCloud

enableCloud(accountId: string, switches: { [bundleName: string]: boolean }): Promise&lt;void&gt;

Enables device-cloud synergy. This API uses a promise to return the result.

**Required permissions**: ohos.permission.CLOUDFILE_SYNC_MANAGER

**System capability**: SystemCapability.FileManagement.DistributedFileService.CloudSyncManager

**Parameters**

| Name    | Type  | Mandatory| Description|
| ---------- | ------ | ---- | ---- |
| accountId | string | Yes  | Account ID.|
| switches | object | Yes  | Whether to enable the device-cloud synergy feature. **bundleName** indicates the application bundle name. The switch status is a Boolean value.|

**Return value**

| Type                 | Description            |
| --------------------- | ---------------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID                    | Error Message       |
| ---------------------------- | ---------- |
| 201 | Permission verification failed. |
| 202 | The caller is not a system application. |
| 401 | The input parameter is invalid. |

**Example**

  ```js
  let accountId = "testAccount";
  let switches = {"com.example.bundleName1": true, "com.example.bundleName2": false};
  cloudSyncManager.enableCloud(accountId, switches).then(function() {
      console.info("enableCloud successfully");
  }).catch(function(err) {
      console.info("enableCloud failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## cloudSyncManager.enableCloud

enableCloud(accountId: string, switches: { [bundleName: string]: boolean }, callback: AsyncCallback&lt;void&gt;): void

Enables device-cloud synergy. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.CLOUDFILE_SYNC_MANAGER

**System capability**: SystemCapability.FileManagement.DistributedFileService.CloudSyncManager

**Parameters**

| Name    | Type  | Mandatory| Description|
| ---------- | ------ | ---- | ---- |
| accountId | string | Yes  | Account ID.|
| switches | object | Yes  | Whether to enable the device-cloud synergy feature. **bundleName** indicates the application bundle name. The switch status is a Boolean value.|
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback invoked to return the result.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID                    | Error Message       |
| ---------------------------- | ---------- |
| 201 | Permission verification failed. |
| 202 | The caller is not a system application. |
| 401 | The input parameter is invalid. |

**Example**

  ```js
  let accountId = "testAccount";
  let switches = {"com.example.bundleName1": true, "com.example.bundleName2": false};
  cloudSyncManager.enableCloud(accountId, switches, (err) => {
    if (err) {
      console.info("enableCloud failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("enableCloud successfully");
    }
  });
  ```

## cloudSyncManager.disableCloud

disableCloud(accountId: string): Promise&lt;void&gt;

Disables device-cloud synergy. This API uses a promise to return the result.

**Required permissions**: ohos.permission.CLOUDFILE_SYNC_MANAGER

**System capability**: SystemCapability.FileManagement.DistributedFileService.CloudSyncManager

**Parameters**

| Name    | Type  | Mandatory| Description|
| ---------- | ------ | ---- | ---- |
| accountId | string | Yes  | Account ID.|

**Return value**

| Type                 | Description            |
| --------------------- | ---------------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID                    | Error Message       |
| ---------------------------- | ---------- |
| 201 | Permission verification failed. |
| 202 | The caller is not a system application. |
| 401 | The input parameter is invalid. |

**Example**

  ```js
  let accountId = "testAccount";
  cloudSyncManager.disableCloud(accountId).then(function() {
      console.info("disableCloud successfully");
  }).catch(function(err) {
      console.info("disableCloud failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## cloudSyncManager.disableCloud

disableCloud(accountId: string, callback: AsyncCallback&lt;void&gt;): void

Disables device-cloud synergy. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.CLOUDFILE_SYNC_MANAGER

**System capability**: SystemCapability.FileManagement.DistributedFileService.CloudSyncManager

**Parameters**

| Name    | Type  | Mandatory| Description|
| ---------- | ------ | ---- | ---- |
| accountId | string | Yes  | Account ID.|
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback invoked to return the result.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID                    | Error Message       |
| ---------------------------- | ---------- |
| 201 | Permission verification failed. |
| 202 | The caller is not a system application. |
| 401 | The input parameter is invalid. |

**Example**

  ```js
  let accountId = "testAccount";
  cloudSyncManager.disableCloud(accountId, (err) => {
    if (err) {
      console.info("disableCloud failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("disableCloud successfully");
    }
  });
  ```

## Action

Enumerates the actions that can be taken to clear local cloud data.

**Required permissions**: ohos.permission.CLOUDFILE_SYNC_MANAGER

**System capability**: SystemCapability.FileManagement.DistributedFileService.CloudSyncManager

| Name|  Value|  Description|
| ----- |  ---- |  ---- |
| RETAIN_DATA |  0 |  Clear the cloud identifier but retain the files cached locally.|
| CLEAR_DATA |  1 |  Clear the cloud identifier and the files cached locally.|

## cloudSyncManager.clean

clean(accountId: string, appActions: { [bundleName: string]: Action }): Promise&lt;void&gt;

Clears the cloud data locally. This API uses a promise to return the result.

**Required permissions**: ohos.permission.CLOUDFILE_SYNC_MANAGER

**System capability**: SystemCapability.FileManagement.DistributedFileService.CloudSyncManager

**Parameters**

| Name    | Type  | Mandatory| Description|
| ---------- | ------ | ---- | ---- |
| accountId | string | Yes  | Account ID.|
| appActions | object | Yes  | Action to take. **bundleName** indicates the application bundle to clear, and [Action](#action) indicates the action to take.|

**Return value**

| Type                 | Description            |
| --------------------- | ---------------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID                    | Error Message       |
| ---------------------------- | ---------- |
| 201 | Permission verification failed. |
| 202 | The caller is not a system application. |
| 401 | The input parameter is invalid. |

**Example**

  ```js
  let accountId = "testAccount";
  let appActions = {"com.example.bundleName1": cloudSyncManager.Action.RETAIN_DATA,
                    "com.example.bundleName2": cloudSyncManager.Action.CLEAR_DATA};
  cloudSyncManager.clean(accountId, appActions).then(function() {
      console.info("clean successfully");
  }).catch(function(err) {
      console.info("clean failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## cloudSyncManager.clean

clean(accountId: string, appActions: { [bundleName: string]: Action }, callback: AsyncCallback&lt;void&gt;): void

Clears the cloud data locally. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.CLOUDFILE_SYNC_MANAGER

**System capability**: SystemCapability.FileManagement.DistributedFileService.CloudSyncManager

**Parameters**

| Name    | Type  | Mandatory| Description|
| ---------- | ------ | ---- | ---- |
| accountId | string | Yes  | Account ID.|
| appActions | object | Yes  | Action to take. **bundleName** indicates the application bundle to clear, and [Action](#action) indicates the action to take.|
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback invoked to clear the cloud data locally.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID                    | Error Message       |
| ---------------------------- | ---------- |
| 201 | Permission verification failed. |
| 202 | The caller is not a system application. |
| 401 | The input parameter is invalid. |

**Example**

  ```js
  let accountId = "testAccount";
  let appActions = {"com.example.bundleName1": cloudSyncManager.Action.RETAIN_DATA,
                    "com.example.bundleName2": cloudSyncManager.Action.CLEAR_DATA};
  cloudSyncManager.clean(accountId, appActions, (err) => {
    if (err) {
      console.info("clean failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("clean successfully");
    }
  });
  ```

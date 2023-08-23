# @ohos.file.fileAccess (User File Access and Management)

The **fileAccess** module provides a framework for accessing and operating user files based on the ExtensionAbility mechanism. This module interacts with a variety of file management services, such as the storage management service, and provides a set of unified file access and management interfaces for system applications. The storage management service manages both the directories of the built-in storage and resources on external devices, such as shared disks, USB flash drives, and SD cards.

>**NOTE**
>
> - The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.
> - The APIs provided by this module are system APIs and cannot be called by third-party applications. Currently, the APIs can be called only by **FilePicker** and **FileManager**.

## Modules to Import

```js
import fileAccess from '@ohos.file.fileAccess';
```

## fileAccess.getFileAccessAbilityInfo

getFileAccessAbilityInfo() : Promise&lt;Array&lt;Want&gt;&gt;

Obtains information about all Wants with **extension** set to **fileAccess** in the system. A Want contains information for starting an ability. This API uses a promise to return the result.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER and ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**Return value**

  | Type| Description|
  | --- | -- |
  | Promise&lt;Array&lt;[Want](js-apis-app-ability-want.md)&gt;&gt; | Promise used to return the Want information obtained.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  async getFileAccessAbilityInfo() {
    let wantInfos = [];
    try {
      wantInfos = await fileAccess.getFileAccessAbilityInfo();
      console.log("getFileAccessAbilityInfo data " + JSON.stringify(wantInfos));
    } catch (error) {
      console.error("getFileAccessAbilityInfo failed, errCode:" + error.code + ", errMessage:" + error.message);
    }
  }
  ```

## fileAccess.getFileAccessAbilityInfo

getFileAccessAbilityInfo(callback: AsyncCallback&lt;Array&lt;Want&gt;&gt;): void

Obtains information about all Wants with **extension** set to **fileAccess** in the system. A Want contains information for starting an ability. This API uses an asynchronous callback to return the result.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER and ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**Parameters**

  | Name| Type| Mandatory| Description|
  | --- | --- | --- | -- |
  | callback | AsyncCallback&lt;Array&lt;[Want](js-apis-app-ability-want.md)&gt;&gt; | Yes| Promise used to return the Want information obtained.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  async getFileAccessAbilityInfo() {
    try {
      fileAccess.getFileAccessAbilityInfo(function (err, wantInfos) {
        if (err) {
          console.error("Failed to getFileAccessAbilityInfo in async, errCode:" + err.code + ", errMessage:" + err.message);
          return;
        }
        console.log("getFileAccessAbilityInfo data " + JSON.stringify(wantInfos));
      });
    } catch (error) {
      console.error("getFileAccessAbilityInfo failed, errCode:" + error.code + ", errMessage:" + error.message);
    }
  }
  ```

## fileAccess.createFileAccessHelper

createFileAccessHelper(context: Context, wants: Array&lt;Want&gt;) : FileAccessHelper

Synchronously creates a **Helper** object to connect to the specified Wants. The **Helper** object provides file access and management capabilities.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER and ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**Parameters**

  | Name| Type| Mandatory| Description|
  | --- | --- | --- | -- |
  | context | [Context](js-apis-inner-application-context.md) | Yes| Context of the ability.|
  | wants | Array&lt;[Want](js-apis-app-ability-want.md)&gt; | Yes| Wants to connect.|

**Return value**

  | Type| Description|
  | --- | -- |
  | [FileAccessHelper](#fileaccesshelper) | **Helper** object created.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  createFileAccessHelper() {
    let fileAccessHelper = null;
    // Obtain wantInfos by using getFileAccessAbilityInfo().
    let wantInfos = [
      {
        "bundleName": "com.ohos.UserFile.ExternalFileManager",
        "abilityName": "FileExtensionAbility",
      },
    ]
    try {
      // this.context is passed by EntryAbility.
      fileAccessHelper = fileAccess.createFileAccessHelper(this.context, wantInfos);
      if (!fileAccessHelper)
        console.error("createFileAccessHelper interface returns an undefined object");
    } catch (error) {
      console.error("createFileAccessHelper failed, errCode:" + error.code + ", errMessage:" + error.message);
    }
  }
  ```

## fileAccess.createFileAccessHelper

createFileAccessHelper(context: Context) : FileAccessHelper

Synchronously creates a **Helper** object to connect to all file management services in the system.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER and ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**Parameters**

  | Name| Type| Mandatory| Description|
  | --- | --- | --- | -- |
  | context | [Context](js-apis-inner-application-context.md) | Yes| Context of the ability.|

**Return value**

  | Type| Description|
  | --- | -- |
  | [FileAccessHelper](#fileaccesshelper) | **Helper** object created.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  createFileAccessHelper() {
    let fileAccessHelperAllServer = null;
    // Create a Helper object to interact with all file management services configured with fileAccess in the system.
    try {
      // this.context is passed by EntryAbility.
      fileAccessHelperAllServer = fileAccess.createFileAccessHelper(this.context);
      if (!fileAccessHelperAllServer)
        console.error("createFileAccessHelper interface returns an undefined object");
    } catch (error) {
      console.error("createFileAccessHelper failed, errCode:" + error.code + ", errMessage:" + error.message);
    }
  }
  ```

## FileInfo

Provides the file or directory attribute information and APIs.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

### Attributes

| Name| Type  | Readable| Writable| Description    |
| ------ | ------ | -------- | ------ | -------- |
| uri | string | Yes| No| URI of the file or directory.|
| relativePath<sup>10+</sup> | string | Yes| No| Relative path of the file or directory.|
| fileName | string | Yes| No| Name of the file or directory.|
| mode | number | Yes| No| Permissions on the file or directory.|
| size | number | Yes| No|  Size of the file or directory.|
| mtime | number | Yes| No|  Time when the file or directory was last modified.|
| mimeType | string | Yes| No|  Multipurpose Internet Mail Extensions (MIME) type of the file or directory.|

### listFile

listFile(filter?: Filter) : FileIterator

Synchronously obtains a **FileIterator** object that lists the next-level files (directories) matching the conditions of the filter from a directory and returns [FileInfo](#fileinfo) using [next()](#next). Currently, only built-in storage devices support the file filter.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

  | Name| Type| Mandatory| Description|
  | --- | --- | -- | -- |
  | filter | [Filter](js-apis-file-fs.md#filter) | No| **Filter** object. |

**Return value**

  | Type| Description|
  | --- | -- |
  | [FileIterator](#fileiterator) | **FileIterator** object obtained.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  // fileInfoDir indicates information about a directory.
  // let filter = { suffix : [".txt", ".jpg", ".xlsx"] };
  let fileInfoDir = fileInfos[0];
  let subfileInfos = [];
  let isDone = false;
  try {
    let fileIterator = fileInfoDir.listFile();
    // listFile() with the filter implementation.
    // let fileIterator = fileInfoDir.listFile(filter);
    if (!fileIterator) {
      console.error("listFile interface returns an undefined object");
      return;
    }
    while (!isDone) {
      let result = fileIterator.next();
      console.log("next result = " + JSON.stringify(result));
      isDone = result.done;
      if (!isDone)
        subfileInfos.push(result.value);
    }
  } catch (error) {
    console.error("listFile failed, errCode:" + error.code + ", errMessage:" + error.message);
  }
  ```

### scanFile

scanFile(filter?: Filter) : FileIterator;

Synchronously obtains a **FileIterator** object that recursively retrieves the files matching the conditions of the filter from a directory and returns [FileInfo](#fileinfo) using [next()](#next). Currently, this API supports only built-in storage devices.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

  | Name| Type| Mandatory| Description|
  | --- | --- | -- | -- |
  | filter | [Filter](js-apis-file-fs.md#filter) | No| **Filter** object. |

**Return value**

  | Type| Description|
  | --- | -- |
  | [FileIterator](#fileiterator) | **FileIterator** object obtained.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  // fileInfoDir indicates information about a directory.
  // let filter = {suffix : [".txt", ".jpg", ".xlsx"]};
  let fileInfoDir = fileInfos[0];
  let subfileInfos = [];
  let isDone = false;
  try {
    let fileIterator = fileInfoDir.scanFile();
    // scanFile() with the filter implementation.
    // let fileIterator = fileInfoDir.scanFile(filter);
    if (!fileIterator) {
      console.error("scanFile interface returns an undefined object");
      return;
    }
    while (!isDone) {
      let result = fileIterator.next();
      console.log("next result = " + JSON.stringify(result));
      isDone = result.done;
      if (!isDone)
        subfileInfos.push(result.value);
    }
  } catch (error) {
    console.error("scanFile failed, errCode:" + error.code + ", errMessage:" + error.message);
  }
  ```

## FileIterator

Provides a **FileIterator** object.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

### next

next() : { value: FileInfo, done: boolean }

Obtains information about the next-level files or directories.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Return value**

| Type| Description|
| --- | -- |
| {value: [FileInfo](#fileinfo), done: boolean} | File or directory information obtained. This API traverses the specified directory until **true** is returned. The **value** field contains the file or directory information obtained.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

## RootInfo

Provides the device's root attribute information and APIs.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

### Attributes

| Name| Type  | Readable| Writable| Description    |
| ------ | ------ | -------- | ------ | -------- |
| deviceType | number | Yes| No|Type of the device.|
| uri | string | Yes| No| Root directory URI of the device.|
| relativePath<sup>10+</sup> | string | Yes| No| Relative path of the root directory.|
| displayName | string | Yes| No| Device name.|
| deviceFlags | number | Yes| No| Capabilities supported by the device.|

### listFile

listFile(filter?: Filter) : FileIterator

Synchronously obtains a **FileIterator** object that lists the first-level files (directories) matching the conditions of the filter from the device root directory and returns [FileInfo](#fileinfo) using [next()](#next). Currently, only built-in storage devices support the file filter.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

  | Name| Type| Mandatory| Description|
  | --- | --- | -- | -- |
  | filter | [Filter](js-apis-file-fs.md#filter) | No| **Filter** object. |

**Return value**

  | Type| Description|
  | --- | -- |
  | [FileIterator](#fileiterator) | **FileIterator** object obtained.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  // Obtain rootInfos by using getRoots().
  // let filter = {suffix : [".txt", ".jpg", ".xlsx"]};
  let rootInfo = rootinfos[0];
  let fileInfos = [];
  let isDone = false;
  try {
    let fileIterator = rootInfo.listFile();
    // listFile() with the filter implementation.
    // let fileIterator = rootInfo.listFile(filter);
    if (!fileIterator) {
      console.error("listFile interface returns an undefined object");
      return;
    }
    while (!isDone) {
      let result = fileIterator.next();
      console.log("next result = " + JSON.stringify(result));
      isDone = result.done;
      if (!isDone)
        fileInfos.push(result.value);
    }
  } catch (error) {
    console.error("listFile failed, errCode:" + error.code + ", errMessage:" + error.message);
  }
  ```

### scanFile

scanFile(filter?: Filter) : FileIterator

Synchronously obtains a **FileIterator** object that recursively retrieves the files matching the conditions of the filter from the device root directory and returns [FileInfo](#fileinfo)using [next()](#next). Currently, this API supports only built-in storage devices.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

  | Name| Type| Mandatory| Description|
  | --- | --- | -- | -- |
  | filter | [Filter](js-apis-file-fs.md#filter) | No| **Filter** object. |

**Return value**

  | Type| Description|
  | --- | -- |
  | [FileIterator](#fileiterator) | **FileIterator** object obtained.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  // Obtain rootInfos by using getRoots().
  // let filter = {suffix : [".txt", ".jpg", ".xlsx"]};
  let rootInfo = rootInfos[0];
  let fileInfos = [];
  let isDone = false;
  try {
    let fileIterator = rootInfo.scanFile();
    // scanFile with the filter implementation.
    // let fileIterator = rootInfo.scanFile(filter);
    if (!fileIterator) {
      console.error("scanFile interface returns undefined object");
      return;
    }
    while (!isDone) {
      let result = fileIterator.next();
      console.log("next result = " + JSON.stringify(result));
      isDone = result.done;
      if (!isDone)
        fileInfos.push(result.value);
    }
  } catch (error) {
    console.error("scanFile failed, errCode:" + error.code + ", errMessage:" + error.message);
  }
  ```

## RootIterator

Provides an iterator object of the device root directory.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

### next

next() : { value: RootInfo, done: boolean }

Obtains the root directory of the next-level device.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Return value**

| Type| Description|
| --- | -- |
| {value: [RootInfo](#rootinfo), done: boolean} | Root directory information obtained. This API traverses the directory until **true** is returned. The **value** field contains the root directory information.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

## FileAccessHelper

Provides a **FileAccessHelper** object.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

### getRoots

getRoots() : Promise&lt;RootIterator&gt;

Obtains information about the device root nodes of the file management service connected to the **Helper** object. This API uses a promise to return a **RootIterator** object,
which returns [RootInfo](#rootinfo) by using [next](#next-1).

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Return value**

| Type| Description|
| --- | -- |
| Promise&lt;[RootIterator](#rootiterator)&gt; | Promise used to return the **RootIterator** object obtained.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  async getRoots() {
    let rootIterator = null;
    let rootinfos = [];
    let isDone = false;
    try {
      // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
      rootIterator = await fileAccessHelper.getRoots();
      if (!rootIterator) {
        console.error("getRoots interface returns an undefined object");
        return;
      }
      while (!isDone) {
        let result = rootIterator.next();
        console.log("next result = " + JSON.stringify(result));
        isDone = result.done;
        if (!isDone)
          rootinfos.push(result.value);
      }
    } catch (error) {
      console.error("getRoots failed, errCode:" + error.code + ", errMessage:" + error.message);
    }
  }
  ```

### getRoots

getRoots(callback:AsyncCallback&lt;RootIterator&gt;) : void

Obtains information about the device root nodes of the file management service connected to the **Helper** object. This API uses an asynchronous callback to return a **RootIterator** object,
which returns [RootInfo](#rootinfo) by using [next](#next-1).

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name| Type| Mandatory| Description|
| --- | --- | --- | -- |
| callback | AsyncCallback&lt;[RootIterator](#rootiterator)&gt; | Yes| Callback invoked to return the **RootIterator** object obtained.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  async getRoots() {
    let rootinfos = [];
    let isDone = false;
    try {
      // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
      fileAccessHelper.getRoots(function (err, rootIterator) {
        if (err) {
          console.error("Failed to getRoots in async, errCode:" + err.code + ", errMessage:" + err.message);
          return;
        }
        while (!isDone) {
          let result = rootIterator.next();
          console.log("next result = " + JSON.stringify(result));
          isDone = result.done;
          if (!isDone)
            rootinfos.push(result.value);
        }
      });
    } catch (error) {
      console.error("getRoots failed, errCode:" + error.code + ", errMessage:" + error.message);
    }
  }
  ```

### createFile

createFile(uri: string, displayName: string) : Promise&lt;string&gt;

Creates a file in a directory. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name| Type| Mandatory| Description|
| --- | --- | --- | -- |
| uri | string | Yes| URI of the destination directory for the file to create.|
| displayName | string | Yes| Name of the file to create. By default, the name of a local file must contain the file name extension.|

**Return value**

| Type| Description|
| --- | -- |
| Promise&lt;string&gt; | Promise used to return the URI of the file created.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  // A built-in storage directory is used as an example.
  // In the sample code, sourceUri indicates the Download directory. The URI is the URI in fileInfo.
  // You can use the URI obtained.
  let sourceUri = "file://docs/storage/Users/currentUser/Download";
  let displayName = "file1"
  let fileUri = null;
  try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    fileUri = await fileAccessHelper.createFile(sourceUri, displayName)
    if (!fileUri) {
      console.error("createFile return undefined object");
      return;
    }
    console.log("createFile sucess, fileUri: " + JSON.stringify(fileUri));
  } catch (error) {
    console.error("createFile failed, errCode:" + error.code + ", errMessage:" + error.message);
  };
  ```

### createFile

createFile(uri: string, displayName: string, callback: AsyncCallback&lt;string&gt;) : void

Creates a file in a directory. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name| Type| Mandatory| Description|
| --- | --- | --- | -- |
| uri | string | Yes| URI of the destination directory for the file to create.|
| displayName | string | Yes| Name of the file to create. By default, the name of a local file must contain the file name extension.|
| callback | AsyncCallback&lt;string&gt; | Yes| Callback invoked to return the URI of the file created.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  // A built-in storage directory is used as an example.
  // In the sample code, sourceUri indicates the Download directory. The URI is the URI in fileInfo.
  // You can use the URI obtained.
  let sourceUri = "file://docs/storage/Users/currentUser/Download";
  let displayName = "file1"
  try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    fileAccessHelper.createFile(sourceUri, displayName, function (err, fileUri) {
      if (err) {
        console.error("Failed to createFile in async, errCode:" + err.code + ", errMessage:" + err.message);
        return;
      }
      console.log("createFile sucess, fileUri: " + JSON.stringify(fileUri));
    });
  } catch (error) {
    console.error("createFile failed, errCode:" + error.code + ", errMessage:" + error.message);
  };
  ```

### mkDir

mkDir(parentUri: string, displayName: string) : Promise&lt;string&gt;

Creates a directory. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name| Type| Mandatory| Description|
| --- | --- | --- | -- |
| parentUri | string | Yes| URI of the destination directory for the directory to create.|
| displayName | string | Yes| Name of the directory to create.|

**Return value**

| Type| Description|
| --- | -- |
| Promise&lt;string&gt; | Promise used to return the URI of the directory created.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  // A built-in storage directory is used as an example.
  // In the sample code, sourceUri indicates the Download directory. The URI is the URI in fileInfo.
  // You can use the URI obtained.
  let sourceUri = "file://docs/storage/Users/currentUser/Download";
  let dirName = "dirTest"
  let dirUri = null;
  try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    dirUri = await fileAccessHelper.mkDir(sourceUri, dirName)
    if (!dirUri) {
      console.error("mkDir return undefined object");
      return;
    }
    console.log("mkDir sucess, dirUri: " + JSON.stringify(dirUri));
  } catch (error) {
    console.error("mkDir failed, errCode:" + error.code + ", errMessage:" + error.message);
  };
  ```

### mkDir

mkDir(parentUri: string, displayName: string, callback: AsyncCallback&lt;string&gt;) : void

Creates a directory. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name| Type| Mandatory| Description|
| --- | --- | --- | -- |
| parentUri | string | Yes| URI of the destination directory for the directory to create.|
| displayName | string | Yes| Name of the directory to create.|
| callback | AsyncCallback&lt;string&gt; | Yes| Callback invoked to return the URI of the directory created.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  // A built-in storage directory is used as an example.
  // In the sample code, sourceUri indicates the Download directory. The URI is the URI in fileInfo.
  // You can use the URI obtained.
  let sourceUri = "file://docs/storage/Users/currentUser/Download";
  let dirName = "dirTest"
  try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    fileAccessHelper.mkDir(sourceUri, dirName, function (err, dirUri) {
      if (err) {
        console.error("Failed to mkDir in async, errCode:" + err.code + ", errMessage:" + err.message);
        return;
      }
      console.log("mkDir sucess, dirUri: " + JSON.stringify(dirUri));
    });
  } catch (error) {
    console.error("mkDir failed, errCode:" + error.code + ", errMessage:" + error.message);
  };
  ```

### openFile

openFile(uri: string, flags: OPENFLAGS) : Promise&lt;number&gt;

Opens a file. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name| Type| Mandatory| Description|
| --- | --- | --- | -- |
| uri | string | Yes| URI of the file to open.|
| flags | [OPENFLAGS](#openflags) | Yes| File open mode.|

**Return value**

| Type| Description|
| --- | -- |
| Promise&lt;number&gt; | Promise used to return the file descriptor (FD) of the file opened.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  // A built-in storage directory is used as an example.
  // In the sample code, targetUri indicates a file in the Download directory. The URI is the URI in fileInfo.
  // You can use the URI obtained.
  let targetUri  = "file://docs/storage/Users/currentUser/Download/1.txt";
  try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    let fd = await fileAccessHelper.openFile(targetUri, fileAccess.OPENFLAGS.READ);
  } catch (error) {
    console.error("openFile failed, errCode:" + error.code + ", errMessage:" + error.message);
  };
  ```

### openFile

openFile(uri: string, flags: OPENFLAGS, callback: AsyncCallback&lt;number&gt;) : void

Opens a file. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name| Type| Mandatory| Description|
| --- | --- | --- | -- |
| uri | string | Yes| URI of the file to open.|
| flags | [OPENFLAGS](#openflags) | Yes| File open mode.|
| callback | AsyncCallback&lt;number&gt; | Yes| Callback invoked to return the FD of the file opened.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  // A built-in storage directory is used as an example.
  // In the sample code, targetUri indicates a file in the Download directory. The URI is the URI in fileInfo.
  // You can use the URI obtained.
  let targetUri  = "file://docs/storage/Users/currentUser/Download/1.txt";
  try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    fileAccessHelper.openFile(targetUri, fileAccess.OPENFLAGS.READ, function (err, fd) {
      if (err) {
        console.error("Failed to openFile in async, errCode:" + err.code + ", errMessage:" + err.message);
        return;
      }
      console.log("openFile sucess, fd: " + fd);
    });
  } catch (error) {
    console.error("openFile failed, errCode:" + error.code + ", errMessage:" + error.message);
  };
  ```

### delete

delete(uri: string) : Promise&lt;number&gt;

Deletes a file or directory. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name| Type| Mandatory| Description|
| --- | --- | --- | -- |
| uri | string | Yes| URI of the file or directory to delete.|

**Return value**

| Type| Description|
| --- | -- |
| Promise&lt;number&gt | Promise used to return the result.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  // A built-in storage directory is used as an example.
  // In the sample code, targetUri indicates a file in the Download directory. The URI is the URI in fileInfo.
  // You can use the URI obtained.
  let targetUri = "file://docs/storage/Users/currentUser/Download/1.txt";
  try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    let code = await fileAccessHelper.delete(targetUri);
    if (code != 0)
      console.error("delete failed, code " + code);
  } catch (error) {
    console.error("delete failed, errCode:" + error.code + ", errMessage:" + error.message);
  };
  ```

### delete

delete(uri: string, callback: AsyncCallback&lt;number&gt;) : void

Deletes a file or directory. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name| Type| Mandatory| Description|
| --- | --- | --- | -- |
| uri | string | Yes| URI of the file or directory to delete.|
| callback | AsyncCallback&lt;number&gt; | Yes| Callback invoked to return the result.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  // A built-in storage directory is used as an example.
  // In the sample code, targetUri indicates a file in the Download directory. The URI is the URI in fileInfo.
  // You can use the URI obtained.
  let targetUri = "file://docs/storage/Users/currentUser/Download/1.txt";
  try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    fileAccessHelper.delete(targetUri, function (err, code) {
      if (err) {
        console.error("Failed to delete in async, errCode:" + err.code + ", errMessage:" + err.message);
        return;
      }
      console.log("delete sucess, code: " + code);
    });
  } catch (error) {
    console.error("delete failed, errCode:" + error.code + ", errMessage:" + error.message);
  };
  ```

### move

move(sourceFile: string, destFile: string) : Promise&lt;string&gt;

Moves a file or directory. This API uses a promise to return the result. Currently, this API does not support move of files or directories across devices.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name| Type| Mandatory| Description|
| --- | --- | --- | -- |
| sourceFile | string | Yes| URI of the file or directory to move.|
| destFile | string | Yes| URI of the destination directory, to which the file or directory will be moved.|

**Return value**

| Type| Description|
| ----- | ------ |
| Promise&lt;string&gt; | Promise used to return the URI of the file or directory in the destination directory.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  // A built-in storage directory is used as an example.
  // In the sample code, sourceFile and destFile indicate the files or directories in the Download directory. The URI is the URI in fileInfo.
  // You can use the URI obtained.
  let sourceFile = "file://docs/storage/Users/currentUser/Download/1.txt";
  let destFile = "file://docs/storage/Users/currentUser/Download/test";
  try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    let fileUri = await fileAccessHelper.move(sourceFile, destFile);
    console.log("move sucess, fileUri: " + JSON.stringify(fileUri));
  } catch (error) {
    console.error("move failed, errCode:" + error.code + ", errMessage:" + error.message);
  };
  ```

### move

move(sourceFile: string, destFile: string, callback: AsyncCallback&lt;string&gt;) : void

Moves a file or directory. This API uses an asynchronous callback to return the result. Currently, this API does not support move of files or directories across devices.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name| Type| Mandatory| Description|
| --- | --- | --- | -- |
| sourceFile | string | Yes| URI of the file or directory to move.|
| destFile | string | Yes| URI of the destination directory, to which the file or directory will be moved.|
| callback | AsyncCallback&lt;string&gt; | Yes| Callback invoked to return the URI of the file or directory in the destination directory.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  // A built-in storage directory is used as an example.
  // In the sample code, sourceFile and destFile indicate the files or directories in the Download directory. The URI is the URI in fileInfo.
  // You can use the URI obtained.
  let sourceFile = "file://docs/storage/Users/currentUser/Download/1.txt";
  let destFile = "file://docs/storage/Users/currentUser/Download/test";
  try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    fileAccessHelper.move(sourceFile, destFile, function (err, fileUri) {
      if (err) {
        console.error("Failed to move in async, errCode:" + err.code + ", errMessage:" + err.message);
        return;
      }
      console.log("move sucess, fileUri: " + JSON.stringify(fileUri));
    });
  } catch (error) {
    console.error("move failed, errCode:" + error.code + ", errMessage:" + error.message);
  };
  ```

### rename

rename(uri: string, displayName: string) : Promise&lt;string&gt;

Renames a file or directory. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name| Type| Mandatory| Description|
| --- | --- | --- | -- |
| uri | string | Yes| URI of the file or directory to rename.|
| displayName | string | Yes| New name of the file or directory, which can contain the file name extension.|

**Return value**

| Type| Description|
| --- | -- |
| Promise&lt;string&gt; | Promise used to return the URI of the renamed file or directory.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  // A built-in storage directory is used as an example.
  // In the sample code, sourceDir indicates a file in the Download directory. The URI is the URI in fileInfo.
  // You can use the URI obtained.
  let sourceDir = "file://docs/storage/Users/currentUser/Download/1.txt";
  try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    let DestDir = await fileAccessHelper.rename(sourceDir, "testDir");
    console.log("rename sucess, DestDir: " + JSON.stringify(DestDir));
  } catch (error) {
    console.error("rename failed, errCode:" + error.code + ", errMessage:" + error.message);
  };
  ```

### rename

rename(uri: string, displayName: string, callback: AsyncCallback&lt;string&gt;) : void

Renames a file or directory. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name| Type| Mandatory| Description|
| --- | --- | --- | -- |
| uri | string | Yes| URI of the file or directory to rename.|
| displayName | string | Yes| New name of the file or directory, which can contain the file name extension.|
| callback | AsyncCallback&lt;string&gt; | Yes| Callback invoked to return the URI of the renamed file or directory.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  // A built-in storage directory is used as an example.
  // In the sample code, sourceDir indicates a file in the Download directory. The URI is the URI in fileInfo.
  // You can use the URI obtained.
  let sourceDir = "file://docs/storage/Users/currentUser/Download/1.txt";
  try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    fileAccessHelper.rename(sourceDir, "testDir", function (err, DestDir) {
      if (err) {
        console.error("Failed to rename in async, errCode:" + err.code + ", errMessage:" + err.message);
        return;
      }
      console.log("rename sucess, DestDir: " + JSON.stringify(DestDir));
    });
  } catch (error) {
    console.error("rename failed, errCode:" + error.code + ", errMessage:" + error.message);
  };
  ```

### access

access(sourceFileUri: string) : Promise&lt;boolean&gt;

Checks whether a file or directory exists. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name| Type| Mandatory| Description|
| --- | --- | --- | -- |
| sourceFileUri | string | Yes| URI of the file or directory to check.|

**Return value**

| Type| Description|
| --- | -- |
| Promise&lt;boolean&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  // A built-in storage directory is used as an example.
  // In the sample code, sourceDir indicates a file in the Download directory. The URI is the URI in fileInfo.
  // You can use the URI obtained.
  let sourceDir = "file://docs/storage/Users/currentUser/Download/1.txt";
  try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    let existJudgment = await fileAccessHelper.access(sourceDir);
    if (existJudgment)
      console.log("sourceDir exists");
    else
      console.log("sourceDir does not exist");
  } catch (error) {
    console.error("access failed, errCode:" + error.code + ", errMessage:" + error.message);
  };
  ```

### access

access(sourceFileUri: string, callback: AsyncCallback&lt;boolean&gt;) : void

Checks whether a file or directory exists. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name| Type| Mandatory| Description|
| --- | --- | --- | -- |
| sourceFileUri | string | Yes| URI of the file or directory to check.|
| callback | AsyncCallback&lt;boolean&gt; | Yes| Callback invoked to return the result.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

**Example**

  ```js
  // A built-in storage directory is used as an example.
  // In the sample code, sourceDir indicates a folder in the Download directory. The URI is the URI in fileInfo.
  // You can use the URI obtained.
  let sourceDir = "file://docs/storage/Users/currentUser/Download/test";
  try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    fileAccessHelper.access(sourceDir, function (err, existJudgment) {
      if (err) {
        console.error("Failed to access in async, errCode:" + err.code + ", errMessage:" + err.message);
        return;
      }
      if (existJudgment)
        console.log("sourceDir exists");
      else
        console.log("sourceDir does not exist");
    });
  } catch (error) {
    console.error("access failed, errCode:" + error.code + ", errMessage:" + error.message);
  };
  ```

### getFileInfoFromUri<sup>10+</sup>

getFileInfoFromUri(uri: string) : Promise\<FileInfo>

Obtains a **FileInfo** object based on the specified URI. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name| Type| Mandatory| Description|
| --- | --- | --- | -- |
| uri | string | Yes| URI of the file or directory.|

**Return value**

| Type| Description|
| --- | -- |
| Promise\<[FileInfo](#fileinfo)> | Promise used to return the **FileInfo** object obtained.|

**Example**

  ```js
  // A built-in storage directory is used as an example.
  // In the sample code, sourceUri indicates the Download directory. The URI is the URI in fileInfo.
  // You can use the URI obtained.
  let sourceUri = "file://docs/storage/Users/currentUser/Download";
  try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    let fileInfo = await fileAccessHelper.getFileInfoFromUri(sourceUri);
  } catch (error) {
    console.error("getFileInfoFromUri failed, errCode:" + error.code + ", errMessage:" + error.message);
  };
  ```

### getFileInfoFromUri<sup>10+</sup>

getFileInfoFromUri(uri: string, callback: AsyncCallback\<FileInfo>) : void

Obtains a **FileInfo** object based on the specified URI. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

  | Name| Type| Mandatory| Description|
  | --- | --- | --- | -- |
  | uri | string | Yes| URI of the file or directory.|
  | callback | AsyncCallback&lt;[FileInfo](#fileinfo)&gt; | Yes| Callback invoked to return the **FileInfo** object obtained.|

**Example**

  ```js
  // A built-in storage directory is used as an example.
  // In the sample code, sourceUri indicates the Download directory. The URI is the URI in fileInfo.
  // You can use the URI obtained.
  let sourceUri = "file://docs/storage/Users/currentUser/Download";
  try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    fileAccessHelper.getFileInfoFromUri(sourceUri, function (err, fileInfo) {
      if (err) {
        console.error("Failed to getFileInfoFromUri in async, errCode:" + err.code + ", errMessage:" + err.message);
        return;
      }
      console.log("getFileInfoFromUri success, fileInfo: " + JSON.stringify(fileInfo));
    });
  } catch (error) {
    console.error("getFileInfoFromUri failed, errCode:" + error.code + ", errMessage:" + error.message);
  };
  ```


### getFileInfoFromRelativePath<sup>10+</sup>

getFileInfoFromRelativePath(relativePath: string) : Promise\<FileInfo>

Obtains a **FileInfo** object based on the **relativePath**. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name| Type| Mandatory| Description|
| --- | --- | --- | -- |
| relativePath | string | Yes| Relative path of the file or directory.|

**Return value**

| Type| Description|
| --- | -- |
| Promise\<[FileInfo](#fileinfo)> | Promise used to return the **FileInfo** object obtained.|

**Example**

  ```js
  // In the sample code, relativePath indicates the Download directory, which is the relativePath in fileInfo.
  // You can use the relativePath obtained.
  let relativePath = "Download/";
  try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    let fileInfo = await fileAccessHelper.getFileInfoFromRelativePath(relativePath);
  } catch (error) {
    console.error("getFileInfoFromRelativePath failed, errCode:" + error.code + ", errMessage:" + error.message);
  };
  ```

### getFileInfoFromRelativePath<sup>10+</sup>

getFileInfoFromRelativePath(relativePath: string, callback: AsyncCallback\<FileInfo>) : void

Obtains a **FileInfo** object based on the **relativePath**. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name| Type| Mandatory| Description|
| --- | --- | --- | -- |
| relativePath | string | Yes| Relative path of the file or directory.|
| callback | AsyncCallback&lt;[FileInfo](#fileinfo)&gt; | Yes| Callback invoked to return the **FileInfo** object obtained.|

**Example**

  ```js
  // In the sample code, relativePath indicates the Download directory, which is the relativePath in fileInfo.
  // You can use the relativePath obtained.
  let relativePath = "Download/";
  try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    fileAccessHelper.getFileInfoFromRelativePath(relativePath, function (err, fileInfo) {
      if (err) {
        console.error("Failed to getFileInfoFromRelativePath in async, errCode:" + err.code + ", errMessage:" + err.message);
        return;
      }
      console.log("getFileInfoFromRelativePath success, fileInfo: " + JSON.stringify(fileInfo));
    });
  } catch (error) {
    console.error("getFileInfoFromRelativePath failed, errCode:" + error.code + ", errMessage:" + error.message);
  };
  ```

### query<sup>10+</sup>

query(uri:string, metaJson: string) : Promise&lt;string&gt;

Queries the attribute information about a file or directory based on the URI. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name  | Type  | Mandatory| Description                                                |
| -------- | ------ | ---- | ---------------------------------------------------- |
| uri      | string | Yes  | URI of the file or directory (obtained from [FileInfo](#fileinfo)).|
| metaJson | string | Yes  | Attribute [FILEKEY](#filekey10) to query.       |

**Return value**

| Type                 | Description                            |
| :-------------------- | :------------------------------- |
| Promise&lt;string&gt; | Promised used to return the attribute queried and the value obtained.|

**Example**

```js
var imageFileRelativePath = "/storage/Users/currentUser/Download/queryTest/image/01.jpg";
var jsonStrSingleRelativepath = JSON.stringify({ [fileAccess.FileKey.RELATIVE_PATH]: "" });
try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    var fileInfo = await fileAccessHelper.getFileInfoFromRelativePath(imageFileRelativePath);
    let queryResult = await fileAccessHelper.query(fileInfo.uri, jsonStrSingleRelativepath);
    console.log("query_file_single faf query, queryResult.relative_path: " + JSON.parse(queryResult).relative_path);
} catch (error) {
     console.error("query_file_single faf query failed, error.code :" + error.code + ", errorMessage :" + error.message);
};
```

### query<sup>10+</sup>

query(uri:string, metaJson: string, callback: AsyncCallback&lt;string&gt;) : void

Queries the attribute information about a file or directory based on the URI. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name  | Type                       | Mandatory| Description                                                |
| -------- | --------------------------- | ---- | ---------------------------------------------------- |
| uri      | string | Yes  | URI of the file or directory (obtained from [FileInfo](#fileinfo)).|
| metaJson | string | Yes  | Attribute [FILEKEY](#filekey10) to query.       |
| callback | AsyncCallback&lt;string&gt; | Yes  | Callback invoked to return the attribute queried and the value obtained.                    |

**Example**

```js
var imageFileRelativePath = "/storage/Users/currentUser/Download/queryTest/image/01.jpg";
var jsonStrSingleRelativepath = JSON.stringify({ [fileAccess.FileKey.RELATIVE_PATH]: "" });
try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    var fileInfo = await fileAccessHelper.getFileInfoFromRelativePath(imageFileRelativePath);
    fileAccessHelper.query(fileInfo.uri, jsonStrSingleRelativepath, (err, queryResult)=>{
        if (err) {
            console.log("query_file_single faf query Failed, errCode:" + err.code + ", errMessage:" + err.message);
            return;
        }
        console.log("query_file_single faf query, queryResult.relative_path: " + JSON.parse(queryResult).relative_path);
    })
} catch (error) {
   console.error("query_file_single faf query failed, error.code :" + error.code + ", errorMessage :" + error.message);
};
```

### copy<sup>10+</sup>

copy(sourceUri: string, destUri: string, force?: boolean) : Promise&lt;Array&lt;CopyResult&gt;&gt;

Copies a file or directory. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name   | Type   | Mandatory| Description                                                        |
| --------- | ------- | ---- | ------------------------------------------------------------ |
| sourceUri | string  | Yes  | URI of the file or folder to copy, for example, **file://docs/storage/Users/currentUser/Download/1.txt**. |
| destUri   | string  | Yes  | URI of the file or folder created, for example, **file://docs/storage/Users/currentUser/Download/test**.       |
| force     | boolean | No  | Whether to forcibly overwrite the file with the same name. <br>If **force** is **true**, the file with the same name will be overwritten. If **force** is **false** or not specified, the file with the same name will not be overwritten.|

**Return value**

| Type                                                   | Description                                                        |
| :------------------------------------------------------ | :----------------------------------------------------------- |
| Promise&lt;Array&lt;[CopyResult](#copyresult10)&gt;&gt; | Promise used to return the result. If the file or directory is copied successfully, no information is returned. If the file copy fails, **copyResult** is returned.|

Example 1: Copy a file with **force** unspecified.

```js
// A built-in storage directory is used as an example.
// In the sample code, sourceFile indicates the file (directory) in the Download directory to copy, destFile indicates the destination directory in the Download directory, and uri is to URI in fileInfo.
// You can use the URI obtained.
let sourceFile = "file://docs/storage/Users/currentUser/Download/1.txt";
let destFile = "file://docs/storage/Users/currentUser/Download/test";
try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    let copyResult = await fileAccessHelper.copy(sourceFile, destFile);
    if (copyResult.length === 0) {
        console.log("copy success");
    } else {
        for (let i = 0; i < copyResult.length; i++) {
            console.error("errCode" + copyResult[i].errCode);
            console.error("errMsg" + copyResult[i].errMsg);
            console.error("sourceUri" + copyResult[i].sourceUri);
            console.error("destUri" + copyResult[i].destUri);
        }
    }
} catch (error) {
    console.error("copy failed, errCode:" + error.code + ", errMessage:" + error.message);
}
```

Example 2: Copy a file or directory when **force** set to **true**.

```js
// A built-in storage directory is used as an example.
// In the sample code, sourceFile indicates the file (directory) in the Download directory to copy, destFile indicates the destination directory in the Download directory, and uri is to URI in fileInfo.
// You can use the URI obtained.
let sourceFile = "file://docs/storage/Users/currentUser/Download/1.txt";
let destFile = "file://docs/storage/Users/currentUser/Download/test";
try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    let copyResult = await fileAccessHelper.copy(sourceFile, destFile, true);
    if (copyResult.length === 0) {
        console.log("copy success");
    } else {
        for (let i = 0; i < copyResult.length; i++) {
            console.error("errCode" + copyResult[i].errCode);
            console.error("errMsg" + copyResult[i].errMsg);
            console.error("sourceUri" + copyResult[i].sourceUri);
            console.error("destUri" + copyResult[i].destUri);
        }
    }
} catch (error) {
    console.error("copy failed, errCode:" + error.code + ", errMessage:" + error.message);
}
```

### copy<sup>10+</sup>

copy(sourceUri: string, destUri: string, callback: AsyncCallback&lt;Array&lt;CopyResult&gt;&gt;) : void

Copies a file or directory. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name   | Type                                            | Mandatory| Description                                                        |
| --------- | ------------------------------------------------ | ---- | ------------------------------------------------------------ |
| sourceUri | string                                           | Yes  | URI of the file or folder to copy, for example, **file://docs/storage/Users/currentUser/Download/1.txt**. |
| destUri   | string                                           | Yes  | URI of the file or folder created, for example, **file://docs/storage/Users/currentUser/Download/test**.        |
| callback  | AsyncCallback&lt;Array&lt;[CopyResult](#copyresult10)&gt;&gt; | Yes  | Callback invoked to return the result. If the file or directory is copied successfully, no information is returned. If the file copy fails, **copyResult** is returned.|

**Example**

```js
// A built-in storage directory is used as an example.
// In the sample code, sourceFile indicates the file (directory) in the Download directory to copy, destFile indicates the destination directory in the Download directory, and uri is to URI in fileInfo.
// You can use the URI obtained.
let sourceFile = "file://docs/storage/Users/currentUser/Download/1.txt";
let destFile = "file://docs/storage/Users/currentUser/Download/test";
try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    fileAccessHelper.copy(sourceFile, destFile, async (err, copyResult) => {
        if (err) {
            console.error("copy failed, errCode:" + err.code + ", errMessage:" + err.message);
            return;
        }
        if (copyResult.length === 0) {
            console.log("copy success");
        } else {
            for (let i = 0; i < copyResult.length; i++) {
                console.error("errCode" + copyResult[i].errCode);
                console.error("errMsg" + copyResult[i].errMsg);
                console.error("sourceUri" + copyResult[i].sourceUri);
                console.error("destUri" + copyResult[i].destUri);
            }
        }
    });
} catch (error) {
    console.error("copy failed, errCode:" + error.code + ", errMessage:" + error.message);
}
```

### copy<sup>10+</sup>

copy(sourceUri: string, destUri: string, force: boolean, callback: AsyncCallback&lt;Array&lt;CopyResult&gt;&gt;) : void

Copies a file or directory. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name   | Type                                            | Mandatory| Description                                                        |
| --------- | ------------------------------------------------ | ---- | ------------------------------------------------------------ |
| sourceUri | string                                           | Yes  | URI of the file or folder to copy, for example, **file://docs/storage/Users/currentUser/Download/1.txt**. |
| destUri   | string                                           | Yes  | URI of the file or folder created, for example, **file://docs/storage/Users/currentUser/Download/test**.        |
| force     | boolean                                          | Yes  | Whether to forcibly overwrite the file with the same name. <br>If **force** is **true**, the file with the same name will be overwritten. If **force** is **false** or not specified, the file with the same name will not be overwritten.|
| callback  | AsyncCallback&lt;Array&lt;[CopyResult](#copyresult10)&gt;&gt; | Yes  | Callback invoked to return the result. If the file or directory is copied successfully, no information is returned. If the file copy fails, **copyResult** is returned.|

**Example**

```js
// A built-in storage directory is used as an example.
// In the sample code, sourceFile indicates the file (directory) in the Download directory to copy, destFile indicates the destination directory in the Download directory, and uri is to URI in fileInfo.
// You can use the URI obtained.
let sourceFile = "file://docs/storage/Users/currentUser/Download/1.txt";
let destFile = "file://docs/storage/Users/currentUser/Download/test";
try {
    // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
    fileAccessHelper.copy(sourceFile, destFile, true, async (err, copyResult) => {
        if (err) {
            console.error("copy failed, errCode:" + err.code + ", errMessage:" + err.message);
            return;
        }
        if (copyResult.length === 0) {
            console.log("copy success");
        } else {
            for (let i = 0; i < copyResult.length; i++) {
                console.error("errCode" + copyResult[i].errCode);
                console.error("errMsg" + copyResult[i].errMsg);
                console.error("sourceUri" + copyResult[i].sourceUri);
                console.error("destUri" + copyResult[i].destUri);
            }
        }
    });
} catch (error) {
    console.error("copy failed, errCode:" + error.code + ", errMessage:" + error.message);
}
```

### registerObserver<sup>10+</sup>

registerObserver(uri: string, notifyForDescendants: boolean, callback: Callback&lt;NotifyMessage&gt;): void

Registers a callback for the specified URI. URIs and callbacks can be in many-to-many relationships. You are advised to use one callback to observe one URI.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name              | Type                                             | Mandatory| Description                          |
| -------------------- | ------------------------------------------------- | ---- | ------------------------------ |
| uri                  | string                                            | Yes  | URI of the file or directory to observe.               |
| notifyForDescendants | boolean                                           | Yes  | Whether to observe changes of the files in the directory.|
| callback             | Callback&lt;[NotifyMessage](#notifymessage10)&gt; | Yes  | Callback invoked to return the notification.                  |

**Example 1**

```js
let DirUri = 'file://docs/storage/Users/currentUser/Documents';
try {
  // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
  let dirUri = await fileAccessHelper.mkDir(DirUri, 'NOTIFY_DIR');
  // In the following example, uri is 'file://docs/storage/Users/currentUser/Documents', and the observed event type is NOTIFY_DELETE.
  const callbackDir = (NotifyMessageDir) => {
    if (NotifyMessageDir != undefined) {
      console.log('NotifyType: ' + NotifyMessageDir.NotifyType + 'NotifyUri:' +
      NotifyMessageDir.uris[0]);
    } else {
      console.error("NotifyMessageDir is undefined");
    }
  }
  fileAccessHelper.registerObserver(dirUri, true, callbackDir);
  await fileAccessHelper.delete(dirUri);
  fileAccessHelper.unregisterObserver(dirUri, callbackDir);
} catch (error) {
  console.error("registerObserver failed, errCode:" + error.code + ", errMessage:" + error.message);
}
```

Example 2: Use the same **uri**, **notifyForDescendants**, and **callback** to register repeatedly.

```js
let DirUri = 'file://docs/storage/Users/currentUser/Documents';
try {
  // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
  let dirUri = await fileAccessHelper.mkDir(DirUri, 'NOTIFY_DIR');
  // In the following example, uri is 'file://docs/storage/Users/currentUser/Documents', and the observed event type is NOTIFY_DELETE.
  const callbackDir = (NotifyMessageDir) => {
    if (NotifyMessageDir != undefined) {
      console.log('NotifyType: ' + NotifyMessageDir.NotifyType + 'NotifyUri:' +
      NotifyMessageDir.uris[0]);
    } else {
      console.error("NotifyMessageDir is undefined");
    }
  }
  fileAccessHelper.registerObserver(dirUri, true, callbackDir);
  // A message is returned indicating that the registration is successful. Repeated registration is reported only in the log.
  fileAccessHelper.registerObserver(dirUri, true, callbackDir);
  await fileAccessHelper.delete(dirUri);
  sleep(100);
  fileAccessHelper.unregisterObserver(dirUri, callbackDir);
} catch (error) {
  console.error("registerObserver failed, errCode:" + error.code + ", errMessage:" + error.message);
}
```

Example 3: Use the same **uri** and **callback** but different **notifyForDescendants** for registration. In this case, **notifyForDescendants** will be reset.

```js
let DirUri = 'file://docs/storage/Users/currentUser/Documents';
try {
  // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
  let dirUri = await fileAccessHelper.mkDir(DirUri, 'NOTIFY_DIR');
  // In the following example, uri is 'file://docs/storage/Users/currentUser/Documents', and the observed event type is NOTIFY_DELETE.
  const callbackDir = (NotifyMessageDir) => {
    if (NotifyMessageDir != undefined) {
      console.log('NotifyType: ' + NotifyMessageDir.NotifyType + 'NotifyUri:' +
      NotifyMessageDir.uris[0]);
    } else {
      console.error("NotifyMessageDir is undefined");
    }
  }
  fileAccessHelper.registerObserver(dirUri, true, callbackDir);
  // After the registration is successful, change notifyForDescendants to false.
  fileAccessHelper.registerObserver(dirUri, false, callbackDir);
  await fileAccessHelper.delete(dirUri);
  fileAccessHelper.unregisterObserver(dirUri, callbackDir);
} catch (error) {
  console.error("registerObserver failed, errCode:" + error.code + ", errMessage:" + error.message);
}
```

### unregisterObserver<sup>10+</sup>

 unregisterObserver(uri: string, callback: Callback&lt;NotifyMessage&gt;): void

Unregisters a callback of the specified URI.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name  | Type                                             | Mandatory| Description                     |
| -------- | ------------------------------------------------- | ---- | ------------------------- |
| uri      | string                                            | Yes  | URI of the target file or directory.          |
| callback | Callback&lt;[NotifyMessage](#notifymessage10)&gt; | Yes  | Callback to unregister.|

**Example**

```js
let DirUri = 'file://docs/storage/Users/currentUser/Documents';
try {
  // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
  let dirUri = await fileAccessHelper.mkDir(DirUri, 'NOTIFY_DIR');
  // In the following example, uri is 'file://docs/storage/Users/currentUser/Documents', and the observed event type is NOTIFY_DELETE.
  const callbackDir = (NotifyMessageDir) => {
    if (NotifyMessageDir != undefined) {
      console.log('NotifyType: ' + NotifyMessageDir.NotifyType + 'NotifyUri:' +
      NotifyMessageDir.uris[0]);
    } else {
      console.error("NotifyMessageDir is undefined");
    }
  }
  fileAccessHelper.registerObserver(dirUri, true, callbackDir);
  await fileAccessHelper.delete(dirUri);
  fileAccessHelper.unregisterObserver(dirUri, callbackDir);
} catch (error) {
  console.error("unregisterObserver failed, errCode:" + error.code + ", errMessage:" + error.message);
}
```

### unregisterObserver<sup>10+</sup>

 unregisterObserver(uri: string): void

Unregisters all callbacks of the specified URI.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

**Parameters**

| Name| Type  | Mandatory| Description           |
| ------ | ------ | ---- | --------------- |
| uri    | string | Yes  | URI of the target file or directory.|

**Example**

```js
let DirUri = 'file://docs/storage/Users/currentUser/Documents';
try {
  // Obtain fileAccessHelper by referring to the sample code of fileAccess.createFileAccessHelper.
  let dirUri = await fileAccessHelper.mkDir(DirUri, 'NOTIFY_DIR');
  // In the following example, uri is 'file://docs/storage/Users/currentUser/Documents', and the observed event type is NOTIFY_DELETE.
  const callbackDir1 = (NotifyMessageDir) => {
    if (NotifyMessageDir != undefined) {
      console.log('NotifyType: ' + NotifyMessageDir.NotifyType + 'NotifyUri:' +
      NotifyMessageDir.uris[0]);
    } else {
      console.error("NotifyMessageDir is undefined");
    }
  }
  const callbackDir2 = (NotifyMessageDir) => {
    if (NotifyMessageDir != undefined) {
      console.log('NotifyType: ' + NotifyMessageDir.NotifyType + 'NotifyUri:' +
      NotifyMessageDir.uris[0]);
    } else {
      console.error("NotifyMessageDir is undefined");
    }
  }
  fileAccessHelper.registerObserver(dirUri, true, callbackDir1);
  fileAccessHelper.registerObserver(dirUri, true, callbackDir2);
  await fileAccessHelper.delete(dirUri);
  // Unregister all callbacks (callbackDir1 and callbackDir2) of dirUri.
  fileAccessHelper.unregisterObserver(dirUri);
} catch (error) {
  console.error("unregisterObserver failed, errCode:" + error.code + ", errMessage:" + error.message);
}
```

## CopyResult<sup>10+</sup>

Defines the information returned when the file copy operation fails. If the copy operation is successful, no information is returned.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

| Name     | Type  | Readable| Writable| Description               |
| --------- | ------ | ---- | ---- | ----------------- |
| sourceUri | string | Yes  | No  | URI of the source file or directory.                                        |
| destUri   | string | Yes  | No  | URI of the conflict file. If the error is not caused by a conflict, **destUri** is empty.|
| errCode   | number | Yes  | No  | Error code.                                                |
| errMsg    | string | Yes  | No  | Error information.                                              |

## OPENFLAGS

Enumerates the file open modes.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.FileManagement.UserFileService

| Name| Value| Description|
| ----- | ------ | ------ |
| READ | 0o0 | Read mode.|
| WRITE | 0o1 | Write mode.|
| WRITE_READ | 0o2 | Read/Write mode.|

## FILEKEY<sup>10+</sup>

Enumerates the keys of the file attributes to query.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.FileManagement.UserFileService

| Name         | Value           | Description                               |
| ------------- | ------------- | ----------------------------------- |
| DISPLAY_NAME  | 'display_name'  | Name of the file.                             |
| DATE_ADDED    | 'date_added'   | Date when the file was created, for example, **1501925454**.     |
| DATE_MODIFIED | 'date_modified' | Date when a file was modified, for example, **1665310670**.     |
| RELATIVE_PATH | 'relative_path' | Relative path of the file, for example, **Pictures/Screenshots/**.|
| FILE_SIZE     | 'size'          | Size of a file, in bytes.       |

## NotifyType<sup>10+</sup>

Enumerates the notification types.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

| Name             | Value  | Description                                                        |
| ----------------- | ---- | ------------------------------------------------------------ |
| NOTIFY_ADD        | 0    | File added.                                                |
| NOTIFY_DELETE     | 1    | File deleted.                                                |
| NOTIFY_MOVED_TO   | 2    | File or folder moved in (for example, **rename()** is performed on a file or folder in this directory or a file or directory is moved to this directory)|
| NOTIFY_MOVED_FROM | 3    | File or folder moved out.|
| NOTIFY_MOVE_SELF  | 4    | File moved (for example, **rename()** or **move()** is performed on a file or folder).    |

## NotifyMessage<sup>10+</sup>

Represents the notification message.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.FileManagement.UserFileService

**Required permissions**: ohos.permission.FILE_ACCESS_MANAGER

| Name| Type                       | Readable| Writable| Description                                                     |
| ---- | --------------------------- | ---- | ---- | --------------------------------------------------------- |
| type | [NotifyType](#notifytype10) | Yes  | No  | Notification type.                                           |
| uris | Array&lt;string&gt;         | Yes  | No  | URIs of the changed files. Currently, only one notification is supported. A collection of multiple notifications will be supported in later versions.|

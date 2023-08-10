# @ohos.file.fs (File Management)

The **fs** module provides APIs for file operations, including basic file management, directory management, file information statistics, and data read and write using a stream.

> **NOTE**
>
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```js
import fs from '@ohos.file.fs';
```

## Guidelines

Before using the APIs provided by this module to perform operations on a file or directory, obtain the application sandbox path of the file or directory as follows:

**Stage Model**

 ```js
import UIAbility from '@ohos.app.ability.UIAbility';

export default class EntryAbility extends UIAbility {
    onWindowStageCreate(windowStage) {
        let context = this.context;
        let pathDir = context.filesDir;
    }
}
 ```

FA Model

 ```js
 import featureAbility from '@ohos.ability.featureAbility';
 
 let context = featureAbility.getContext();
 context.getFilesDir().then((data) => {
      let pathDir = data;
 })
 ```

For details about how to obtain the FA model context, see [Context](js-apis-inner-app-context.md#context).

## fs.stat

stat(file: string|number): Promise&lt;Stat&gt;

Obtains detailed file information. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name| Type  | Mandatory| Description                      |
| ------ | ------ | ---- | -------------------------- |
| file   | string\|number | Yes  | Application sandbox path or file descriptor (FD) of the file.|

**Return value**

  | Type                          | Description        |
  | ---------------------------- | ---------- |
  | Promise&lt;[Stat](#stat)&gt; | Promise used to return the file information obtained.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  fs.stat(filePath).then((stat) => {
      console.info("get file info succeed, the size of file is " + stat.size);
  }).catch((err) => {
      console.info("get file info failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## fs.stat

stat(file: string|number, callback: AsyncCallback&lt;Stat&gt;): void

Obtains detailed file information. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name  | Type                              | Mandatory| Description                          |
| -------- | ---------------------------------- | ---- | ------------------------------ |
| file     | string\|number                            | Yes  | Application sandbox path or FD of the file.    |
| callback | AsyncCallback&lt;[Stat](#stat)&gt; | Yes  | Callback invoked to return the file information obtained.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  fs.stat(pathDir, (err, stat) => {
    if (err) {
      console.info("get file info failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("get file info succeed, the size of file is " + stat.size);
    }
  });
  ```

## fs.statSync

statSync(file: string|number): Stat

Obtains detailed file information synchronously. 

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name| Type  | Mandatory| Description                      |
| ------ | ------ | ---- | -------------------------- |
| file   | string\|number | Yes  | Application sandbox path or file descriptor (FD) of the file.|

**Return value**

  | Type           | Description        |
  | ------------- | ---------- |
  | [Stat](#stat) | File information obtained.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let stat = fs.statSync(pathDir);
  console.info("get file info succeed, the size of file is " + stat.size);
  ```

## fs.access

access(path: string): Promise&lt;boolean&gt;

Checks whether a file exists. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name| Type  | Mandatory| Description                                                        |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| path   | string | Yes  | Application sandbox path of the file.                                  |

**Return value**

  | Type                 | Description                          |
  | ------------------- | ---------------------------- |
  | Promise&lt;boolean&gt; | Promise used to return the result. The value **true** means the file exists; the value **false** means the opposite.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  fs.access(filePath).then((res) => {
    if (res) {
      console.info("file exists");
    }
  }).catch((err) => {
    console.info("access failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## fs.access

access(path: string, callback: AsyncCallback&lt;boolean&gt;): void

Checks whether a file exists. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name  | Type                     | Mandatory| Description                                                        |
| -------- | ------------------------- | ---- | ------------------------------------------------------------ |
| path     | string                    | Yes  | Application sandbox path of the file.                                  |
| callback | AsyncCallback&lt;boolean&gt; | Yes  | Callback invoked to return the result. The value **true** means the file exists; the value **false** means the opposite.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  fs.access(filePath, (err, res) => {
    if (err) {
      console.info("access failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      if (res) {
        console.info("file exists");
      }
    }
  });
  ```

## fs.accessSync

accessSync(path: string): boolean

Synchronously checks whether a file exists.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name| Type  | Mandatory| Description                                                        |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| path   | string | Yes  | Application sandbox path of the file.                                  |

**Return value**

  | Type                 | Description                          |
  | ------------------- | ---------------------------- |
  | boolean | Returns **true** if the file exists; returns **false** otherwise.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  try {
      let res = fs.accessSync(filePath);
      if (res) {
        console.info("file exists");
      }
  } catch(err) {
      console.info("accessSync failed with error message: " + err.message + ", error code: " + err.code);
  }
  ```


## fs.close

close(file: number|File): Promise&lt;void&gt;

Closes a file. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name | Type    | Mandatory  | Description          |
  | ---- | ------ | ---- | ------------ |
  | file   | number\|[File](#file) | Yes   | File object or FD of the file to close.|

**Return value**

  | Type                 | Description                          |
  | ------------------- | ---------------------------- |
  | Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath);
  fs.close(file).then(() => {
      console.info("File closed");
  }).catch((err) => {
      console.info("close file failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## fs.close

close(file: number|File, callback: AsyncCallback&lt;void&gt;): void

Closes a file. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name     | Type                       | Mandatory  | Description          |
  | -------- | ------------------------- | ---- | ------------ |
  | file       | number\|[File](#file)                  | Yes   | File object or FD of the file to close.|
  | callback | AsyncCallback&lt;void&gt; | Yes   | Callback invoked immediately after the file is closed.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath);
  fs.close(file, (err) => {
    if (err) {
      console.info("close file failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("close file success");
    }
  });
  ```

## fs.closeSync

closeSync(file: number|File): void

Synchronously closes a file.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name | Type    | Mandatory  | Description          |
  | ---- | ------ | ---- | ------------ |
  | file   | number\|[File](#file) | Yes   | File object or FD of the file to close.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath);
  fs.closeSync(file);
  ```

## fs.copyFile

copyFile(src: string|number, dest: string|number, mode?: number): Promise&lt;void&gt;

Copies a file. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name | Type                        | Mandatory  | Description                                      |
  | ---- | -------------------------- | ---- | ---------------------------------------- |
  | src  | string\|number | Yes   | Path or FD of the file to copy.                     |
  | dest | string\|number | Yes   | Destination path of the file or FD of the file created.                         |
  | mode | number                     | No   | Whether to overwrite the file with the same name in the destination directory. The default value is **0**, which is the only value supported.<br>**0**: overwrite the file with the same name.|

**Return value**

  | Type                 | Description                          |
  | ------------------- | ---------------------------- |
  | Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let srcPath = pathDir + "/srcDir/test.txt";
  let dstPath = pathDir + "/dstDir/test.txt";
  fs.copyFile(srcPath, dstPath).then(() => {
      console.info("copy file succeed");
  }).catch((err) => {
      console.info("copy file failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## fs.copyFile

copyFile(src: string|number, dest: string|number, mode?: number, callback: AsyncCallback&lt;void&gt;): void

Copies a file. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name     | Type                        | Mandatory  | Description                                      |
  | -------- | -------------------------- | ---- | ---------------------------------------- |
  | src      | string\|number | Yes   | Path or FD of the file to copy.                     |
  | dest     | string\|number | Yes   | Destination path of the file or FD of the file created.                         |
  | mode     | number                     | No   | Whether to overwrite the file with the same name in the destination directory. The default value is **0**, which is the only value supported.<br>**0**: overwrite the file with the same name and truncate the part that is not overwritten.|
  | callback | AsyncCallback&lt;void&gt;  | Yes   | Callback invoked immediately after the file is copied.                            |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let srcPath = pathDir + "/srcDir/test.txt";
  let dstPath = pathDir + "/dstDir/test.txt";
  fs.copyFile(srcPath, dstPath, (err) => {
    if (err) {
      console.info("copy file failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("copy file success");
    }
  });
  ```


## fs.copyFileSync

copyFileSync(src: string|number, dest: string|number, mode?: number): void

Synchronously copies a file.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name | Type                        | Mandatory  | Description                                      |
  | ---- | -------------------------- | ---- | ---------------------------------------- |
  | src  | string\|number | Yes   | Path or FD of the file to copy.                     |
  | dest | string\|number | Yes   | Destination path of the file or FD of the file created.                         |
  | mode | number                     | No   | Whether to overwrite the file with the same name in the destination directory. The default value is **0**, which is the only value supported.<br>**0**: overwrite the file with the same name and truncate the part that is not overwritten.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let srcPath = pathDir + "/srcDir/test.txt";
  let dstPath = pathDir + "/dstDir/test.txt";
  fs.copyFileSync(srcPath, dstPath);
  ```

## fs.copyDir<sup>10+</sup>

copyDir(src: string, dest: string, mode?: number): Promise\<void>

Copies a directory to the specified directory. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name   | Type    | Mandatory  | Description                         |
  | ------ | ------ | ---- | --------------------------- |
  | src | string | Yes   | Application sandbox path of the directory to copy.|
  | dest | string | Yes   | Application sandbox path of the destination directory.|
  | mode | number | No   | Copy mode. The default value is **0**.<br>- **0**: Throw an exception if a file conflict occurs.<br> Throw an exception if there is a directory with the same name in the destination directory and files with the same name exist in the conflicting directory. All the non-conflicting files in the source directory will be moved to the destination directory, and the non-conflicting files in the destination directory will be retained. The **data** attribute in the error returned provides information about the conflicting files in the Array\<[ConflictFiles](#conflictfiles)> format.<br>- **1**: Forcibly overwrite the files with the same name in the destination directory.<br>If there is a directory with the same name in the destination directory and files with the same name exist in the conflicting directory, all the files with the same name in the destination directory will be overwritten and the non-conflicting files will be retained.|

**Return value**

  | Type                 | Description                          |
  | ------------------- | ---------------------------- |
  | Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  // Copy srcPath to destPath.
  let srcPath = pathDir + "/srcDir/";
  let destPath = pathDir + "/destDir/";
  fs.copyDir(srcPath, destPath, 0).then(() => {
    console.info("copy directory succeed");
  }).catch((err) => {
    if (err.code == 13900015) {
      for (let i = 0; i < err.data.length; i++) {
        console.info("copy directory failed with conflicting files: " + err.data[i].srcFile +
          " " + err.data[i].destFile);
      }
    } else {
      console.info("copy directory failed with error message: " + err.message + ", error code: " + err.code);
    }
  });
  ```

## fs.copyDir<sup>10+</sup>

copyDir(src: string, dest: string, mode?: number, callback: AsyncCallback\<void>): void

Copies a directory to the specified directory. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name   | Type    | Mandatory  | Description                         |
  | ------ | ------ | ---- | --------------------------- |
  | src | string | Yes   | Application sandbox path of the directory to copy.|
  | dest | string | Yes   | Application sandbox path of the destination directory.|
  | mode | number | No   | Copy mode. The default value is **0**.<br>- **0**: Throw an exception if a file conflict occurs.<br> Throw an exception if there is a directory with the same name in the destination directory and files with the same name exist in the conflicting directory. All the non-conflicting files in the source directory will be moved to the destination directory, and the non-conflicting files in the destination directory will be retained. The **data** attribute in the error returned provides information about the conflicting files in the Array\<[ConflictFiles](#conflictfiles)> format.<br>- **1**: Forcibly overwrite the files with the same name in the destination directory.<br>If there is a directory with the same name in the destination directory and files with the same name exist in the conflicting directory, all the files with the same name in the destination directory will be overwritten and the non-conflicting files will be retained.|
  | callback | AsyncCallback&lt;void&gt; | Yes   | Callback invoked immediately after the directory is copied.             |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  // Copy srcPath to destPath.
  let srcPath = pathDir + "/srcDir/";
  let destPath = pathDir + "/destDir/";
  fs.copyDir(srcPath, destPath, 0, (err) => {
    if (err && err.code == 13900015) {
      for (let i = 0; i < err.data.length; i++) {
        console.info("copy directory failed with conflicting files: " + err.data[i].srcFile +
          " " + err.data[i].destFile);
      }
    } else if (err) {
      console.info("copy directory failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("copy directory succeed");
    }  
  });
  ```

## fs.mkdir

mkdir(path: string): Promise&lt;void&gt;

Creates a directory. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name| Type  | Mandatory| Description                                                        |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| path   | string | Yes  | Application sandbox path of the directory.                                  |

**Return value**

  | Type                 | Description                          |
  | ------------------- | ---------------------------- |
  | Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let dirPath = pathDir + "/testDir";
  fs.mkdir(dirPath).then(() => {
      console.info("Directory created");
  }).catch((err) => {
      console.info("mkdir failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## fs.mkdir

mkdir(path: string, callback: AsyncCallback&lt;void&gt;): void

Creates a directory. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name  | Type                     | Mandatory| Description                                                        |
| -------- | ------------------------- | ---- | ------------------------------------------------------------ |
| path     | string                    | Yes  | Application sandbox path of the directory.                                  |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback invoked when the directory is created asynchronously.                            |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let dirPath = pathDir + "/testDir";
  fs.mkdir(dirPath, (err) => {
    if (err) {
      console.info("mkdir failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("mkdir success");
    }
  });
  ```

## fs.mkdirSync

mkdirSync(path: string): void

Synchronously creates a directory.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name| Type  | Mandatory| Description                                                        |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| path   | string | Yes  | Application sandbox path of the directory.                                  |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let dirPath = pathDir + "/testDir";
  fs.mkdirSync(dirPath);
  ```

## fs.open

open(path: string, mode?: number): Promise&lt;File&gt;

Opens a file. This API uses a promise to return the result. File uniform resource identifiers (URIs) are supported. 

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name| Type  | Mandatory| Description                                                        |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| path   | string | Yes  | Application sandbox path or URI of the file.                                  |
| mode  | number | No  | [Mode](#openmode) for opening the file. You must specify one of the following options. By default, the file is open in read-only mode.<br>- **OpenMode.READ_ONLY(0o0)**: Open the file in read-only mode.<br>- **OpenMode.WRITE_ONLY(0o1)**: Open the file in write-only mode.<br>- **OpenMode.READ_WRITE(0o2)**: Open the file in read/write mode.<br>You can also specify the following options, separated by a bitwise OR operator (&#124;). By default, no additional options are given.<br>- **OpenMode.CREATE(0o100)**: If the file does not exist, create it.<br>- **OpenMode.TRUNC(0o1000)**: If the file exists and is open in write-only or read/write mode, truncate the file length to 0.<br>- **OpenMode.APPEND(0o2000)**: Open the file in append mode. New data will be added to the end of the file.<br>- **OpenMode.NONBLOCK(0o4000)**: If **path** points to a named pipe (also known as a FIFO), block special file, or character special file, perform non-blocking operations on the opened file and in subsequent I/Os.<br>- **OpenMode.DIR(0o200000)**: If **path** does not point to a directory, throw an exception.<br>- **OpenMode.NOFOLLOW(0o400000)**: If **path** points to a symbolic link, throw an exception.<br>- **OpenMode.SYNC(0o4010000)**: Open the file in synchronous I/O mode.|

**Return value**

  | Type                   | Description         |
  | --------------------- | ----------- |
  | Promise&lt;[File](#file)&gt; | Promise used to return the file object.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  fs.open(filePath, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE).then((file) => {
      console.info("file fd: " + file.fd);
  }).catch((err) => {
      console.info("open file failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```


## fs.open

open(path: string, mode?: number, callback: AsyncCallback&lt;File&gt;): void

Opens a file. This API uses an asynchronous callback to return the result. File URIs are supported. 

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name  | Type                           | Mandatory| Description                                                        |
| -------- | ------------------------------- | ---- | ------------------------------------------------------------ |
| path     | string                          | Yes  | Application sandbox path or URI of the file.                                  |
| mode  | number | No  | [Mode](#openmode) for opening the file. You must specify one of the following options. By default, the file is open in read-only mode.<br>- **OpenMode.READ_ONLY(0o0)**: Open the file in read-only mode.<br>- **OpenMode.WRITE_ONLY(0o1)**: Open the file in write-only mode.<br>- **OpenMode.READ_WRITE(0o2)**: Open the file in read/write mode.<br>You can also specify the following options, separated by a bitwise OR operator (&#124;). By default, no additional options are given.<br>- **OpenMode.CREATE(0o100)**: If the file does not exist, create it.<br>- **OpenMode.TRUNC(0o1000)**: If the file exists and is open in write-only or read/write mode, truncate the file length to 0.<br>- **OpenMode.APPEND(0o2000)**: Open the file in append mode. New data will be added to the end of the file.<br>- **OpenMode.NONBLOCK(0o4000)**: If **path** points to a named pipe (also known as a FIFO), block special file, or character special file, perform non-blocking operations on the opened file and in subsequent I/Os.<br>- **OpenMode.DIR(0o200000)**: If **path** does not point to a directory, throw an exception.<br>- **OpenMode.NOFOLLOW(0o400000)**: If **path** points to a symbolic link, throw an exception.<br>- **OpenMode.SYNC(0o4010000)**: Open the file in synchronous I/O mode.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  fs.open(filePath, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE, (err, file) => {
    if (err) {
      console.info("mkdir failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("file fd: " + file.fd);
    }
  });
  ```

## fs.openSync

openSync(path: string, mode?: number): File

Synchronously opens a file. File URIs are supported. 

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name| Type  | Mandatory| Description                                                        |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| path   | string | Yes  | Application sandbox path or URI of the file.                                  |
| mode  | number | No  | [Mode](#openmode) for opening the file. You must specify one of the following options. By default, the file is open in read-only mode.<br>- **OpenMode.READ_ONLY(0o0)**: Open the file in read-only mode.<br>- **OpenMode.WRITE_ONLY(0o1)**: Open the file in write-only mode.<br>- **OpenMode.READ_WRITE(0o2)**: Open the file in read/write mode.<br>You can also specify the following options, separated by a bitwise OR operator (&#124;). By default, no additional options are given.<br>- **OpenMode.CREATE(0o100)**: If the file does not exist, create it.<br>- **OpenMode.TRUNC(0o1000)**: If the file exists and is open in write-only or read/write mode, truncate the file length to 0.<br>- **OpenMode.APPEND(0o2000)**: Open the file in append mode. New data will be added to the end of the file.<br>- **OpenMode.NONBLOCK(0o4000)**: If **path** points to a named pipe (also known as a FIFO), block special file, or character special file, perform non-blocking operations on the opened file and in subsequent I/Os.<br>- **OpenMode.DIR(0o200000)**: If **path** does not point to a directory, throw an exception.<br>- **OpenMode.NOFOLLOW(0o400000)**: If **path** points to a symbolic link, throw an exception.<br>- **OpenMode.SYNC(0o4010000)**: Open the file in synchronous I/O mode.|

**Return value**

  | Type    | Description         |
  | ------ | ----------- |
  | [File](#file) | File object opened.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
  console.info("file fd: " + file.fd);
  fs.closeSync(file);
  ```

## fs.read

read(fd: number, buffer: ArrayBuffer, options?: { offset?: number; length?: number; }): Promise&lt;number&gt;

Reads data from a file. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name | Type       | Mandatory| Description                                                        |
| ------- | ----------- | ---- | ------------------------------------------------------------ |
| fd      | number      | Yes  | FD of the file.                                    |
| buffer  | ArrayBuffer | Yes  | Buffer used to store the file data read.                          |
| options | Object      | No  | The options are as follows:<br>- **offset** (number): start position to read the data. This parameter is optional. By default, data is read from the current position.<br>- **length** (number): length of the data to read. This parameter is optional. The default value is the buffer length.|

**Return value**

  | Type                                | Description    |
  | ---------------------------------- | ------ |
  | Promise&lt;number&gt; | Promise used to return the data read.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath, fs.OpenMode.READ_WRITE);
  let buf = new ArrayBuffer(4096);
  fs.read(file.fd, buf).then((readLen) => {
      console.info("Read file data successfully");
      console.info(String.fromCharCode.apply(null, new Uint8Array(buf.slice(0, readLen))));
      fs.closeSync(file);
  }).catch((err) => {
      console.info("read file data failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## fs.read

read(fd: number, buffer: ArrayBuffer, options?: { offset?: number; length?: number; }, callback: AsyncCallback&lt;number&gt;): void

Reads data from a file. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name     | Type                                      | Mandatory  | Description                                      |
  | -------- | ---------------------------------------- | ---- | ---------------------------------------- |
  | fd       | number                                   | Yes   | FD of the file.                            |
  | buffer   | ArrayBuffer                              | Yes   | Buffer used to store the file data read.                       |
  | options | Object      | No  | The options are as follows:<br>- **offset** (number): start position to read the data. This parameter is optional. By default, data is read from the current position.<br>- **length** (number): length of the data to read. This parameter is optional. The default value is the buffer length.|
  | callback | AsyncCallback&lt;number&gt; | Yes   | Callback invoked when the data is read asynchronously.                            |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath, fs.OpenMode.READ_WRITE);
  let buf = new ArrayBuffer(4096);
  fs.read(file.fd, buf, (err, readLen) => {
    if (err) {
      console.info("mkdir failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("Read file data successfully");
      console.info(String.fromCharCode.apply(null, new Uint8Array(buf.slice(0, readLen))));
      fs.closeSync(file);
    }
  });
  ```

## fs.readSync

readSync(fd: number, buffer: ArrayBuffer, options?: { offset?: number; length?: number; }): number

Synchronously reads data from a file.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name    | Type         | Mandatory  | Description                                      |
  | ------- | ----------- | ---- | ---------------------------------------- |
  | fd      | number      | Yes   | FD of the file.                            |
  | buffer  | ArrayBuffer | Yes   | Buffer used to store the file data read.                       |
  | options | Object      | No  | The options are as follows:<br>- **offset** (number): start position to read the data. This parameter is optional. By default, data is read from the current position.<br>- **length** (number): length of the data to read. This parameter is optional. The default value is the buffer length.|

**Return value**

  | Type    | Description      |
  | ------ | -------- |
  | number | Length of the data read.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath, fs.OpenMode.READ_WRITE);
  let buf = new ArrayBuffer(4096);
  let num = fs.readSync(file.fd, buf);
  fs.closeSync(file);
  ```

## fs.rmdir

rmdir(path: string): Promise&lt;void&gt;

Deletes a directory. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name| Type  | Mandatory| Description                      |
| ------ | ------ | ---- | -------------------------- |
| path   | string | Yes  | Application sandbox path of the directory.|

**Return value**

  | Type                 | Description                          |
  | ------------------- | ---------------------------- |
  | Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let dirPath = pathDir + "/testDir";
  fs.rmdir(dirPath).then(() => {
      console.info("Directory deleted");
  }).catch((err) => {
      console.info("rmdir failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## fs.rmdir

rmdir(path: string, callback: AsyncCallback&lt;void&gt;): void

Deletes a directory. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name  | Type                     | Mandatory| Description                      |
| -------- | ------------------------- | ---- | -------------------------- |
| path     | string                    | Yes  | Application sandbox path of the directory.|
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback invoked when the directory is deleted asynchronously.  |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let dirPath = pathDir + "/testDir";
  fs.rmdir(dirPath, (err) => {
    if (err) {
      console.info("rmdir failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("Directory deleted");
    }
  });
  ```

## fs.rmdirSync

rmdirSync(path: string): void

Synchronously deletes a directory.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name| Type  | Mandatory| Description                      |
| ------ | ------ | ---- | -------------------------- |
| path   | string | Yes  | Application sandbox path of the directory.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let dirPath = pathDir + "/testDir";
  fs.rmdirSync(dirPath);
  ```

## fs.unlink

unlink(path: string): Promise&lt;void&gt;

Deletes a file. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name| Type  | Mandatory| Description                      |
| ------ | ------ | ---- | -------------------------- |
| path   | string | Yes  | Application sandbox path of the file.|

**Return value**

  | Type                 | Description                          |
  | ------------------- | ---------------------------- |
  | Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  fs.unlink(filePath).then(() => {
      console.info("File deleted");
  }).catch((err) => {
      console.info("remove file failed with error message: " + err.message + ", error code: " + err.codeor);
  });
  ```

## fs.unlink

unlink(path: string, callback: AsyncCallback&lt;void&gt;): void

Deletes a file. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name  | Type                     | Mandatory| Description                      |
| -------- | ------------------------- | ---- | -------------------------- |
| path     | string                    | Yes  | Application sandbox path of the file.|
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback invoked immediately after the file is deleted.  |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  fs.unlink(filePath, (err) => {
    if (err) {
      console.info("remove file failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("File deleted");
    }
  });
  ```

## fs.unlinkSync

unlinkSync(path: string): void

Synchronously deletes a file.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name| Type  | Mandatory| Description                      |
| ------ | ------ | ---- | -------------------------- |
| path   | string | Yes  | Application sandbox path of the file.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  fs.unlinkSync(filePath);
  ```


## fs.write

write(fd: number, buffer: ArrayBuffer|string, options?: { offset?: number; length?: number; encoding?: string; }): Promise&lt;number&gt;

Writes data into a file. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name    | Type                             | Mandatory  | Description                                      |
  | ------- | ------------------------------- | ---- | ---------------------------------------- |
  | fd      | number                          | Yes   | FD of the file.                            |
  | buffer  | ArrayBuffer\|string | Yes   | Data to write. It can be a string or data from a buffer.                    |
  | options | Object                          | No   | The options are as follows:<br>- **offset** (number): start position to write the data in the file. This parameter is optional. By default, data is written from the current position.<br>- **length** (number): length of the data to write. This parameter is optional. The default value is the buffer length.<br>- **encoding** (string): format of the data to be encoded when the data is a string. The default value is **'utf-8'**, which is the only value supported currently.|

**Return value**

  | Type                   | Description      |
  | --------------------- | -------- |
  | Promise&lt;number&gt; | Promise used to return the length of the data written.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
  fs.write(file.fd, "hello, world").then((writeLen) => {
    console.info("write data to file succeed and size is:" + writeLen);
    fs.closeSync(file);
  }).catch((err) => {
    console.info("write data to file failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## fs.write

write(fd: number, buffer: ArrayBuffer|string, options?: { offset?: number; length?: number; encoding?: string; }, callback: AsyncCallback&lt;number&gt;): void

Writes data into a file. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name     | Type                             | Mandatory  | Description                                      |
  | -------- | ------------------------------- | ---- | ---------------------------------------- |
  | fd       | number                          | Yes   | FD of the file.                            |
  | buffer   | ArrayBuffer\|string | Yes   | Data to write. It can be a string or data from a buffer.                    |
  | options | Object                          | No   | The options are as follows:<br>- **offset** (number): start position to write the data in the file. This parameter is optional. By default, data is written from the current position.<br>- **length** (number): length of the data to write. This parameter is optional. The default value is the buffer length.<br>- **encoding** (string): format of the data to be encoded when the data is a string. The default value is **'utf-8'**, which is the only value supported currently.|
  | callback | AsyncCallback&lt;number&gt;     | Yes   | Callback invoked when the data is written asynchronously.                      |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
  fs.write(file.fd, "hello, world", (err, writeLen) => {
    if (err) {
      console.info("write failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("write data to file succeed and size is:" + writeLen);
      fs.closeSync(file);
    }
  });
  ```

## fs.writeSync

writeSync(fd: number, buffer: ArrayBuffer|string, options?: { offset?: number; length?: number; encoding?: string; }): number

Synchronously writes data into a file.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name    | Type                             | Mandatory  | Description                                      |
  | ------- | ------------------------------- | ---- | ---------------------------------------- |
  | fd      | number                          | Yes   | FD of the file.                            |
  | buffer  | ArrayBuffer\|string | Yes   | Data to write. It can be a string or data from a buffer.                    |
  | options | Object                          | No   | The options are as follows:<br>- **offset** (number): start position to write the data in the file. This parameter is optional. By default, data is written from the current position.<br>- **length** (number): length of the data to write. This parameter is optional. The default value is the buffer length.<br>- **encoding** (string): format of the data to be encoded when the data is a string. The default value is **'utf-8'**, which is the only value supported currently.|

**Return value**

  | Type    | Description      |
  | ------ | -------- |
  | number | Length of the data written in the file.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
  let writeLen = fs.writeSync(file.fd, "hello, world");
  console.info("write data to file succeed and size is:" + writeLen);
  fs.closeSync(file);
  ```

## fs.truncate

truncate(file: string|number, len?: number): Promise&lt;void&gt;

Truncates a file. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name| Type  | Mandatory| Description                            |
| ------ | ------ | ---- | -------------------------------- |
| file   | string\|number | Yes  | Application sandbox path or FD of the file.      |
| len    | number | No  | File length, in bytes, after truncation. The default value is **0**.|

**Return value**

  | Type                 | Description                          |
  | ------------------- | ---------------------------- |
  | Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let len = 5;
  fs.truncate(filePath, len).then(() => {
      console.info("File truncated");
  }).catch((err) => {
      console.info("truncate file failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## fs.truncate

truncate(file: string|number, len?: number, callback: AsyncCallback&lt;void&gt;): void

Truncates a file. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name  | Type                     | Mandatory| Description                            |
| -------- | ------------------------- | ---- | -------------------------------- |
| file     | string\|number                    | Yes  | Application sandbox path or FD of the file.      |
| len      | number                    | No  | File length, in bytes, after truncation. The default value is **0**.|
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback that returns no value.  |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let len = 5;
  fs.truncate(filePath, len, (err) => {
    if (err) {
      console.info("truncate failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("truncate success");
    }
  });
  ```

## fs.truncateSync

truncateSync(file: string|number, len?: number): void

Synchronously truncates a file.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name| Type  | Mandatory| Description                            |
| ------ | ------ | ---- | -------------------------------- |
| file   | string\|number | Yes  | Application sandbox path or FD of the file.      |
| len    | number | No  | File length, in bytes, after truncation. The default value is **0**.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let len = 5;
  fs.truncateSync(filePath, len);
  ```

## fs.readText

readText(filePath: string, options?: { offset?: number; length?: number; encoding?: string; }): Promise&lt;string&gt;

Reads the text content of a file. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name  | Type  | Mandatory| Description                                                        |
| -------- | ------ | ---- | ------------------------------------------------------------ |
| filePath | string | Yes  | Application sandbox path of the file.                                  |
| options  | Object | No  | The options are as follows:<br>- **offset** (number): start position to read the data. This parameter is optional. By default, data is read from the current position.<br>- **length** (number): length of the data to read. This parameter is optional. The default value is the file length.<br>- **encoding** (string): format of the data (string) to be encoded. The default value is **'utf-8'**, which is the only value supported.|

**Return value**

  | Type                   | Description        |
  | --------------------- | ---------- |
  | Promise&lt;string&gt; | Promise used to return the file content read.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  fs.readText(filePath).then((str) => {
      console.info("readText succeed:" + str);
  }).catch((err) => {
      console.info("readText failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## fs.readText

readText(filePath: string, options?: { offset?: number; length?: number; encoding?: string; }, callback: AsyncCallback&lt;string&gt;): void

Reads the text content of a file. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name  | Type                       | Mandatory| Description                                                        |
| -------- | --------------------------- | ---- | ------------------------------------------------------------ |
| filePath | string                      | Yes  | Application sandbox path of the file.                                  |
| options  | Object                      | No  | The options are as follows:<br>- **offset** (number): start position to read the data. This parameter is optional. By default, data is read from the current position.<br>- **length** (number): length of the data to read. This parameter is optional. The default value is the file length.<br>- **encoding**: format of the data to be encoded. The default value is **'utf-8'**, which is the only value supported.|
| callback | AsyncCallback&lt;string&gt; | Yes  | Callback invoked to return the content read.                        |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  fs.readText(filePath, { offset: 1, encoding: 'UTF-8' }, (err, str) => {
    if (err) {
      console.info("read text failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("readText succeed:" + str);
    }
  });
  ```

## fs.readTextSync

readTextSync(filePath: string, options?: { offset?: number; length?: number; encoding?: string; }): string

Synchronously reads the text of a file. 

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name  | Type  | Mandatory| Description                                                        |
| -------- | ------ | ---- | ------------------------------------------------------------ |
| filePath | string | Yes  | Application sandbox path of the file.                                  |
| options  | Object | No  | The options are as follows:<br>- **offset** (number): start position to read the data. This parameter is optional. By default, data is read from the current position.<br>- **length** (number): length of the data to read. This parameter is optional. The default value is the file length.<br>- **encoding** (string): format of the data (string) to be encoded. The default value is **'utf-8'**, which is the only value supported.|

**Return value**

  | Type  | Description                |
  | ------ | -------------------- |
  | string | Returns the content of the file read.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let str = fs.readTextSync(filePath, {offset: 1, length: 3});
  console.info("readText succeed:" + str);
  ```

## fs.lstat

lstat(path: string): Promise&lt;Stat&gt;

Obtains information about a symbolic link. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| path   | string | Yes  | Application sandbox path of the file.|

**Return value**

  | Type                          | Description        |
  | ---------------------------- | ---------- |
  | Promise&lt;[Stat](#stat)&gt; | Promise used to return the symbolic link information obtained. For details, see **stat**.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  fs.lstat(filePath).then((stat) => {
      console.info("get link status succeed, the size of file is" + stat.size);
  }).catch((err) => {
      console.info("get link status failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## fs.lstat

lstat(path: string, callback: AsyncCallback&lt;Stat&gt;): void

Obtains information about a symbolic link. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name  | Type                              | Mandatory| Description                                  |
| -------- | ---------------------------------- | ---- | -------------------------------------- |
| path     | string                             | Yes  | Application sandbox path of the file.|
| callback | AsyncCallback&lt;[Stat](#stat)&gt; | Yes  | Callback invoked to return the symbolic link information obtained.      |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  fs.lstat(filePath, (err, stat) => {
      if (err) {
        console.info("lstat failed with error message: " + err.message + ", error code: " + err.code);
      } else {
        console.info("get link status succeed, the size of file is" + stat.size);
      }
  });
  ```

## fs.lstatSync

lstatSync(path: string): Stat

Obtains information about a symbolic link synchronously.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| path   | string | Yes  | Application sandbox path of the file.|

**Return value**

  | Type           | Description        |
  | ------------- | ---------- |
  | [Stat](#stat) | File information obtained.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let stat = fs.lstatSync(filePath);
  ```

## fs.rename

rename(oldPath: string, newPath: string): Promise&lt;void&gt;

Renames a file or folder. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name | Type  | Mandatory| Description                        |
| ------- | ------ | ---- | ---------------------------- |
| oldPath | string | Yes  | Application sandbox path of the file to rename.|
| newPath | string | Yes  | Application sandbox path of the renamed file.  |

**Return value**

  | Type                 | Description                          |
  | ------------------- | ---------------------------- |
  | Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let srcFile = pathDir + "/test.txt";
  let dstFile = pathDir + "/new.txt";
  fs.rename(srcFile, dstFile).then(() => {
      console.info("File renamed");
  }).catch((err) => {
      console.info("rename failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## fs.rename

rename(oldPath: string, newPath: string, callback: AsyncCallback&lt;void&gt;): void

Renames a file or folder. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name  | Type                     | Mandatory| Description                        |
| -------- | ------------------------- | ---- | ---------------------------- |
| oldPath | string | Yes  | Application sandbox path of the file to rename.|
| newPath | string | Yes  | Application sandbox path of the renamed file.  |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback invoked when the file is asynchronously renamed.  |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let srcFile = pathDir + "/test.txt";
  let dstFile = pathDir + "/new.txt";
  fs.rename(srcFile, dstFile, (err) => {
    if (err) {
      console.info("rename failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("rename success");
    }
  });
  ```

## fs.renameSync

renameSync(oldPath: string, newPath: string): void

Renames a file or folder synchronously.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name | Type  | Mandatory| Description                        |
| ------- | ------ | ---- | ---------------------------- |
| oldPath | string | Yes  | Application sandbox path of the file to rename.|
| newPath | string | Yes  | Application sandbox path of the renamed file.  |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let srcFile = pathDir + "/test.txt";
  let dstFile = pathDir + "/new.txt";
  fs.renameSync(srcFile, dstFile);
  ```

## fs.fsync

fsync(fd: number): Promise&lt;void&gt;

Flushes data of a file to disk. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name | Type    | Mandatory  | Description          |
  | ---- | ------ | ---- | ------------ |
  | fd   | number | Yes   | FD of the file.|

**Return value**

  | Type                 | Description                          |
  | ------------------- | ---------------------------- |
  | Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath);
  fs.fsync(file.fd).then(() => {
      console.info("Data flushed");
  }).catch((err) => {
      console.info("sync data failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## fs.fsync

fsync(fd: number, callback: AsyncCallback&lt;void&gt;): void

Flushes data of a file to disk. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name     | Type                       | Mandatory  | Description             |
  | -------- | ------------------------- | ---- | --------------- |
  | fd       | number                    | Yes   | FD of the file.   |
  | Callback | AsyncCallback&lt;void&gt; | Yes   | Callback invoked when the file data is synchronized in asynchronous mode.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath);
  fs.fsync(file.fd, (err) => {
    if (err) {
      console.info("fsync failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("fsync success");
      fs.closeSync(file);
    }
  });
  ```


## fs.fsyncSync

fsyncSync(fd: number): void

Flushes data of a file to disk synchronously.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name | Type    | Mandatory  | Description          |
  | ---- | ------ | ---- | ------------ |
  | fd   | number | Yes   | FD of the file.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath);
  fs.fsyncSync(file.fd);
  fs.closeSync(file);
  ```

## fs.fdatasync

fdatasync(fd: number): Promise&lt;void&gt;

Flushes data of a file to disk. This API uses a promise to return the result. **fdatasync()** is similar to **fsync()**, but does not flush modified metadata unless that metadata is needed.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name | Type    | Mandatory  | Description          |
  | ---- | ------ | ---- | ------------ |
  | fd   | number | Yes   | FD of the file.|

**Return value**

  | Type                 | Description                          |
  | ------------------- | ---------------------------- |
  | Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath);
  fs.fdatasync(file.fd).then((err) => {
    console.info("Data flushed");
    fs.closeSync(file);
  }).catch((err) => {
    console.info("sync data failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## fs.fdatasync

fdatasync(fd: number, callback: AsyncCallback&lt;void&gt;): void

Flushes data of a file to disk. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name     | Type                             | Mandatory  | Description               |
  | -------- | ------------------------------- | ---- | ----------------- |
  | fd       | number                          | Yes   | FD of the file.     |
  | callback | AsyncCallback&lt;void&gt; | Yes   | Callback invoked when the file data is synchronized in asynchronous mode.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath);
  fs.fdatasync (file.fd, (err) => {
    if (err) {
      console.info("fdatasync failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("fdatasync success");
      fs.closeSync(file);
    }
  });
  ```

## fs.fdatasyncSync

fdatasyncSync(fd: number): void

Synchronizes data in a file synchronously.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name | Type    | Mandatory  | Description          |
  | ---- | ------ | ---- | ------------ |
  | fd   | number | Yes   | FD of the file.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath);
  let stat = fs.fdatasyncSync(file.fd);
  fs.closeSync(file);
  ```

## fs.symlink

symlink(target: string, srcPath: string): Promise&lt;void&gt;

Creates a symbolic link based on a file path. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name | Type  | Mandatory| Description                        |
| ------- | ------ | ---- | ---------------------------- |
| target  | string | Yes  | Application sandbox path of the source file.    |
| srcPath | string | Yes  | Application sandbox path of the symbolic link.|

**Return value**

  | Type                 | Description                          |
  | ------------------- | ---------------------------- |
  | Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let srcFile = pathDir + "/test.txt";
  let dstFile = pathDir + "/test";
  fs.symlink(srcFile, dstFile).then(() => {
      console.info("Symbolic link created");
  }).catch((err) => {
      console.info("symlink failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```


## fs.symlink
symlink(target: string, srcPath: string, callback: AsyncCallback&lt;void&gt;): void

Creates a symbolic link based on a file path. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name  | Type                     | Mandatory| Description                            |
| -------- | ------------------------- | ---- | -------------------------------- |
| target   | string                    | Yes  | Application sandbox path of the source file.        |
| srcPath  | string                    | Yes  | Application sandbox path of the symbolic link.    |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback invoked when the symbolic link is created asynchronously.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let srcFile = pathDir + "/test.txt";
  let dstFile = pathDir + "/test";
  fs.symlink(srcFile, dstFile, (err) => {
    if (err) {
      console.info("symlink failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("symlink success");
    }
  });
  ```

## fs.symlinkSync

symlinkSync(target: string, srcPath: string): void

Synchronously creates a symbolic link based on a file path.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name | Type  | Mandatory| Description                        |
| ------- | ------ | ---- | ---------------------------- |
| target  | string | Yes  | Application sandbox path of the source file.    |
| srcPath | string | Yes  | Application sandbox path of the symbolic link.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let srcFile = pathDir + "/test.txt";
  let dstFile = pathDir + "/test";
  fs.symlinkSync(srcFile, dstFile);
  ```

## fs.listFile
listFile(path: string, options?: {
    recursion?: boolean;
    listNum?: number;
    filter?: Filter;
}): Promise<string[]>

Lists all files in a folder. This API uses a promise to return the result.<br>This API supports recursive listing of all files (including files in subfolders) and file filtering.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name   | Type    | Mandatory  | Description                         |
  | ------ | ------ | ---- | --------------------------- |
  | path | string | Yes   | Application sandbox path of the folder.|
  | options | Object | No   | File filtering options. The files are not filtered by default.|

**options parameters**

  | Name   | Type    | Mandatory  | Description                         |
  | ------ | ------ | ---- | --------------------------- |
  | recursion | boolean | No   | Whether to list all files in subfolders recursively. The default value is **false**.|
  | listNum | number | No   | Number of file names to list. The default value **0** means to list all files.|
  | filter | [Filter](#filter) | No   | File filtering options. Currently, only the match by file name extension, fuzzy search by file name, and filter by file size or latest modification time are supported.|

**Return value**

  | Type                  | Description        |
  | --------------------- | ---------- |
  | Promise&lt;string[]&gt; | Promise used to return the file names listed.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let options = {
    "recursion": false,
    "listNum": 0,
    "filter": {
      "suffix": [".png", ".jpg", ".jpeg"],
      "displayName": ["%abc", "efg%"],
      "fileSizeOver": 1024,
      "lastModifiedAfter": new Date().getTime(),
    }
  };
  fs.listFile(pathDir, options).then((filenames) => {
    console.info("listFile succeed");
    for (let i = 0; i < filenames.length; i++) {
      console.info("fileName: %s", filenames[i]);
    }
  }).catch((err) => {
      console.info("list file failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## fs.listFile
listFile(path: string, options?: {
    recursion?: boolean;
    listNum?: number;
    filter?: Filter;
}, callback: AsyncCallback<string[]>): void

Lists all files in a folder. This API uses an asynchronous callback to return the result.<br>This API supports recursive listing of all files (including files in subfolders) and file filtering.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name   | Type    | Mandatory  | Description                         |
  | ------ | ------ | ---- | --------------------------- |
  | path | string | Yes   | Application sandbox path of the folder.|
  | options | Object | No   | File filtering options. The files are not filtered by default.|
  | callback | AsyncCallback&lt;string[]&gt; | Yes   | Callback invoked to return the file names listed.             |

**options parameters**

  | Name   | Type    | Mandatory  | Description                         |
  | ------ | ------ | ---- | --------------------------- |
  | recursion | boolean | No   | Whether to list all files in subfolders recursively. The default value is **false**.|
  | listNum | number | No   | Number of file names to list. The default value **0** means to list all files.|
  | filter | [Filter](#filter) | No   | File filtering options. Currently, only the match by file name extension, fuzzy search by file name, and filter by file size or latest modification time are supported.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let options = {
    "recursion": false,
    "listNum": 0,
    "filter": {
      "suffix": [".png", ".jpg", ".jpeg"],
      "displayName": ["%abc", "efg%"],
      "fileSizeOver": 1024,
      "lastModifiedAfter": new Date().getTime(),
    }
  };
  fs.listFile(pathDir, options, (err, filenames) => {
    if (err) {
      console.info("list file failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("listFile succeed");
      for (let i = 0; i < filenames.length; i++) {
        console.info("filename: %s", filenames[i]);
      }
    }
  });
  ```

## fs.listFileSync

listFileSync(path: string, options?: {
    recursion?: boolean;
    listNum?: number;
    filter?: Filter;
}): string[]

Lists all files in a folder synchronously. This API supports recursive listing of all files (including files in subfolders) and file filtering.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name   | Type    | Mandatory  | Description                         |
  | ------ | ------ | ---- | --------------------------- |
  | path | string | Yes   | Application sandbox path of the folder.|
  | options | Object | No   | File filtering options. The files are not filtered by default.|

**options parameters**

  | Name   | Type    | Mandatory  | Description                         |
  | ------ | ------ | ---- | --------------------------- |
  | recursion | boolean | No   | Whether to list all files in subfolders recursively. The default value is **false**.|
  | listNum | number | No   | Number of file names to list. The default value **0** means to list all files.|
  | filter | [Filter](#filter) | No   | File filtering options. Currently, only the match by file name extension, fuzzy search by file name, and filter by file size or latest modification time are supported.|

**Return value**

  | Type                  | Description        |
  | --------------------- | ---------- |
  | string[] | File names listed.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let options = {
    "recursion": false,
    "listNum": 0,
    "filter": {
      "suffix": [".png", ".jpg", ".jpeg"],
      "displayName": ["%abc", "efg%"],
      "fileSizeOver": 1024,
      "lastModifiedAfter": new Date().getTime(),
    }
  };
  let filenames = fs.listFileSync(pathDir, options);
  console.info("listFile succeed");
  for (let i = 0; i < filenames.length; i++) {
    console.info("filename: %s", filenames[i]);
  }
  ```

## fs.moveDir<sup>10+</sup>

moveDir(src: string, dest: string, mode?: number): Promise\<void>

Moves a directory. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name   | Type    | Mandatory  | Description                         |
  | ------ | ------ | ---- | --------------------------- |
  | src | string | Yes   | Application sandbox path of the directory to move.|
  | dest | string | Yes   | Application sandbox path of the destination directory.|
  | mode | number | No   | Mode for moving the directory. The default value is **0**.<br>- **0**: Throw an exception if a directory conflict occurs.<br> Throw an exception if there is a directory with the same name in the destination directory.<br>- **1**: Throw an exception if a file conflict occurs.<br> Throw an exception if there is a directory with the same name in the destination directory and files with the same name exist in the conflicting directory. All the non-conflicting files in the source directory will be moved to the destination directory, and the non-conflicting files in the destination directory will be retained. The **data** attribute in the error returned provides information about the conflicting files in the Array\<[ConflictFiles](#conflictfiles)> format.<br>- **2**: Forcibly overwrite the conflicting files in the destination directory.<br>If there is a directory with the same name in the destination directory and files with the same name exist in the conflicting directory, all the files with the same name in the destination directory will be overwritten and the non-conflicting files will be retained.<br>- **3**: Forcibly overwrite the conflicting directory.<br> Move the source directory to the destination directory and overwrite the conflicting directory completely. That is, if there is a directory with the same name in the destination directory, all the original files in that directory will not be retained.|

**Return value**

  | Type                 | Description                          |
  | ------------------- | ---------------------------- |
  | Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  // move directory from srcPath to destPath
  let srcPath = pathDir + "/srcDir/";
  let destPath = pathDir + "/destDir/";
  fs.moveDir(srcPath, destPath, 1).then(() => {
      console.info("move directory succeed");
  }).catch((err) => {
    if (err.code == 13900015) {
      for (let i = 0; i < err.data.length; i++) {
        console.info("move directory failed with conflicting files: " + err.data[i].srcFile +
          " " + err.data[i].destFile);
      }
    } else {
      console.info("move directory failed with error message: " + err.message + ", error code: " + err.code);
    }
  });
  ```

## fs.moveDir<sup>10+</sup>

moveDir(src: string, dest: string, mode?: number, callback: AsyncCallback\<void>): void

Moves a directory. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name   | Type    | Mandatory  | Description                         |
  | ------ | ------ | ---- | --------------------------- |
  | src | string | Yes   | Application sandbox path of the source directory.|
  | dest | string | Yes   | Application sandbox path of the destination directory.|
  | mode | number | No   | Mode for moving the directory. The default value is **0**.<br>- **0**: Throw an exception if a directory conflict occurs.<br> Throw an exception if there is a directory with the same name in the destination directory.<br>- **1**: Throw an exception if a file conflict occurs.<br> Throw an exception if there is a directory with the same name in the destination directory and files with the same name exist in the conflicting directory. All the non-conflicting files in the source directory will be moved to the destination directory, and the non-conflicting files in the destination directory will be retained. The **data** attribute in the error returned provides information about the conflicting files in the Array\<[ConflictFiles](#conflictfiles)> format.<br>- **2**: Forcibly overwrite the conflicting files in the destination directory. If there is a directory with the same name in the destination directory and files with the same name exist in the conflicting directory, all the files with the same name in the destination directory will be overwritten and the non-conflicting files will be retained.<br>- **3**: Forcibly overwrite the conflicting directory.<br> Move the source directory to the destination directory and overwrite the conflicting directory completely. That is, if there is a directory with the same name in the destination directory, all the original files in that directory will not be retained.|
  | callback | AsyncCallback&lt;void&gt; | Yes   | Callback invoked when the directory is moved.             |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  // move directory from srcPath to destPath
  let srcPath = pathDir + "/srcDir/";
  let destPath = pathDir + "/destDir/";
  fs.moveDir(srcPath, destPath, 1, (err) => {
    if (err && err.code == 13900015) {
      for (let i = 0; i < err.data.length; i++) {
        console.info("move directory failed with conflicting files: " + err.data[i].srcFile +
          " " + err.data[i].destFile);
      }
    } else if (err) {
      console.info("move directory failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("move directory succeed");
    }  
  });
  ```

## fs.moveFile

moveFile(src: string, dest: string, mode?: number): Promise\<void>

Moves a file. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name   | Type    | Mandatory  | Description                         |
  | ------ | ------ | ---- | --------------------------- |
  | src | string | Yes   | Application sandbox path of the source file.|
  | dest | string | Yes   | Application sandbox path of the destination file.|
  | mode | number | No   | Whether to overwrite the file with the same name in the destination directory.<br>The value **0** means to overwrite the file with the same name in the destination directory; the value **1** means to throw an exception.<br>The default value is **0**.|

**Return value**

  | Type                 | Description                          |
  | ------------------- | ---------------------------- |
  | Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let srcPath = pathDir + "/source.txt";
  let destPath = pathDir + "/dest.txt";
  fs.moveFile(srcPath, destPath, 0).then(() => {
      console.info("move file succeed");
  }).catch((err) => {
      console.info("move file failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## fs.moveFile

moveFile(src: string, dest: string, mode?: number, callback: AsyncCallback\<void>): void

Moves a file. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name   | Type    | Mandatory  | Description                         |
  | ------ | ------ | ---- | --------------------------- |
  | src | string | Yes   | Application sandbox path of the source file.|
  | dest | string | Yes   | Application sandbox path of the destination file.|
  | mode | number | No   | Whether to overwrite the file with the same name in the destination directory.<br>The value **0** means to overwrite the file with the same name in the destination directory; the value **1** means to throw an exception.<br>The default value is **0**.|
  | callback | AsyncCallback&lt;void&gt; | Yes   | Callback invoked when the file is moved.             |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let srcPath = pathDir + "/source.txt";
  let destPath = pathDir + "/dest.txt";
  fs.moveFile(srcPath, destPath, 0, (err) => {
    if (err) {
      console.info("move file failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("move file succeed");
    }  
  });
  ```

## fs.moveFileSync

moveFileSync(src: string, dest: string, mode?: number): void

Moves a file synchronously.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name   | Type    | Mandatory  | Description                         |
  | ------ | ------ | ---- | --------------------------- |
  | src | string | Yes   | Application sandbox path of the source file.|
  | dest | string | Yes   | Application sandbox path of the destination file.|
  | mode | number | No   | Whether to overwrite the file with the same name in the destination directory.<br>The value **0** means to overwrite the file with the same name in the destination directory; the value **1** means to throw an exception.<br>The default value is **0**.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let srcPath = pathDir + "/source.txt";
  let destPath = pathDir + "/dest.txt";
  fs.moveFileSync(srcPath, destPath, 0);
  console.info("move file succeed");
  ```

## fs.mkdtemp

mkdtemp(prefix: string): Promise&lt;string&gt;

Creates a temporary directory. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name   | Type    | Mandatory  | Description                         |
  | ------ | ------ | ---- | --------------------------- |
  | prefix | string | Yes   | A randomly generated string used to replace "XXXXXX" in a directory.|

**Return value**

  | Type                  | Description        |
  | --------------------- | ---------- |
  | Promise&lt;string&gt; | Promise used to return the directory created.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  fs.mkdtemp(pathDir + "/XXXXXX").then((pathDir) => {
      console.info("mkdtemp succeed:" + pathDir);
  }).catch((err) => {
      console.info("mkdtemp failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## fs.mkdtemp

mkdtemp(prefix: string, callback: AsyncCallback&lt;string&gt;): void

Creates a temporary directory. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name     | Type                         | Mandatory  | Description                         |
  | -------- | --------------------------- | ---- | --------------------------- |
  | prefix   | string                      | Yes   | A randomly generated string used to replace "XXXXXX" in a directory.|
  | callback | AsyncCallback&lt;string&gt; | Yes   | Callback invoked when a temporary directory is created asynchronously.             |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  fs.mkdtemp(pathDir + "/XXXXXX", (err, res) => {
    if (err) {
      console.info("mkdtemp failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("mkdtemp success");
    }
  });
  ```

## fs.mkdtempSync

mkdtempSync(prefix: string): string

Synchronously creates a temporary directory.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name   | Type    | Mandatory  | Description                         |
  | ------ | ------ | ---- | --------------------------- |
  | prefix | string | Yes   | A randomly generated string used to replace "XXXXXX" in a directory.|

**Return value**

  | Type   | Description        |
  | ------ | ---------- |
  | string | Unique path generated.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let res = fs.mkdtempSync(pathDir + "/XXXXXX");
  ```  


## fs.createRandomAccessFile<sup>10+</sup>

createRandomAccessFile(file: string|File, mode?: string): Promise&lt;RandomAccessFile&gt;

Creates a **RandomAccessFile** instance based on the specified file path or file object. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**
|    Name   | Type    | Mandatory  | Description                         |
| ------------ | ------ | ------ | ------------------------------------------------------------ |
|     file     | string\|[File](#file) | Yes   | Application sandbox path of the file or an opened file object.|
|     mode     | number | No  | [Option](#openmode) for creating the **RandomAccessFile** instance. This parameter is valid only when the application sandbox path of the file is passed in. One of the following options must be specified:<br>- **OpenMode.READ_ONLY(0o0)**: Create the file in read-only mode. This is the default value.<br>- **OpenMode.WRITE_ONLY(0o1)**: Create the file in write-only mode.<br>- **OpenMode.READ_WRITE(0o2)**: Create the file in read/write mode.<br>You can also specify the following options, separated by a bitwise OR operator (&#124;). By default, no additional options are given.<br>- **OpenMode.CREATE(0o100)**: If the file does not exist, create it.<br>- **OpenMode.TRUNC(0o1000)**: If the **RandomAccessFile** object already exists and is created in write-only or read/write mode, truncate the file length to 0.<br>- **OpenMode.APPEND(0o2000)**: Create the file in append mode. New data will be added to the end of the **RandomAccessFile** object. <br>- **OpenMode.NONBLOCK(0o4000)**: If **path** points to a named pipe (also known as a FIFO), block special file, or character special file, perform non-blocking operations on the created file and in subsequent I/Os.<br>- **OpenMode.DIR(0o200000)**: If **path** does not point to a directory, throw an exception.<br>- **OpenMode.NOFOLLOW(0o400000)**: If **path** points to a symbolic link, throw an exception.<br>- **OpenMode.SYNC(0o4010000)**: Create a **RandomAccessFile** instance in synchronous I/O mode.|

**Return value**

  | Type                               | Description       |
  | --------------------------------- | --------- |
  | Promise&lt;[RandomAccessFile](#randomaccessfile)&gt; | Promise used to return the **RandomAccessFile** instance created.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath, fs.OpenMode.CREATE | fs.OpenMode.READ_WRITE);
  fs.createRandomAccessFile(file).then((randomAccessFile) => {
      console.info("randomAccessFile fd: " + randomAccessFile.fd);
  }).catch((err) => {
      console.info("create randomAccessFile failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```


## fs.createRandomAccessFile<sup>10+</sup>

createRandomAccessFile(file: string|File, mode?: string, callback: AsyncCallback&lt;RandomAccessFile&gt;): void

Creates a **RandomAccessFile** instance based on the specified file path or file object. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

|  Name   | Type    | Mandatory  | Description                         |
| ------------ | ------ | ------ | ------------------------------------------------------------ |
|     file     | string\|[File](#file) | Yes   | Application sandbox path of the file or an opened file object.|
|     mode     | number | No  | [Option](#openmode) for creating the **RandomAccessFile** instance. This parameter is valid only when the application sandbox path of the file is passed in. One of the following options must be specified:<br>- **OpenMode.READ_ONLY(0o0)**: Create the file in read-only mode. This is the default value.<br>- **OpenMode.WRITE_ONLY(0o1)**: Create the file in write-only mode.<br>- **OpenMode.READ_WRITE(0o2)**: Create the file in read/write mode.<br>You can also specify the following options, separated by a bitwise OR operator (&#124;). By default, no additional options are given.<br>- **OpenMode.CREATE(0o100)**: If the file does not exist, create it.<br>- **OpenMode.TRUNC(0o1000)**: If the **RandomAccessFile** object already exists and is created in write-only or read/write mode, truncate the file length to 0.<br>- **OpenMode.APPEND(0o2000)**: Create the file in append mode. New data will be added to the end of the **RandomAccessFile** object. <br>- **OpenMode.NONBLOCK(0o4000)**: If **path** points to a named pipe (also known as a FIFO), block special file, or character special file, perform non-blocking operations on the created file and in subsequent I/Os.<br>- **OpenMode.DIR(0o200000)**: If **path** does not point to a directory, throw an exception.<br>- **OpenMode.NOFOLLOW(0o400000)**: If **path** points to a symbolic link, throw an exception.<br>- **OpenMode.SYNC(0o4010000)**: Create a **RandomAccessFile** instance in synchronous I/O mode.|
| callback | AsyncCallback&lt;[RandomAccessFile](#randomaccessfile)&gt; | Yes  | Callback invoked to return the **RandomAccessFile** instance created.                                  |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**
  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath, fs.OpenMode.CREATE | fs.OpenMode.READ_WRITE);
  fs.createRandomAccessFile(file, (err, randomAccessFile) => {
      if (err) {
          console.info("create randomAccessFile failed with error message: " + err.message + ", error code: " + err.code);
      } else {
          console.info("randomAccessFilefile fd: " + randomAccessFile.fd);
      }
  });
  ```


## fs.createRandomAccessFileSync<sup>10+</sup>

createRandomAccessFileSync(file: string|File, , mode?: string): RandomAccessFile

Creates a **RandomAccessFile** instance based on the specified file path or file object.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

|  Name   | Type    | Mandatory  | Description                         |
| ------------ | ------ | ------ | ------------------------------------------------------------ |
|     file     | string\|[File](#file) | Yes   | Application sandbox path of the file or an opened file object.|
|     mode     | number | No  | [Option](#openmode) for creating the **RandomAccessFile** instance. This parameter is valid only when the application sandbox path of the file is passed in. One of the following options must be specified:<br>- **OpenMode.READ_ONLY(0o0)**: Create the file in read-only mode. This is the default value.<br>- **OpenMode.WRITE_ONLY(0o1)**: Create the file in write-only mode.<br>- **OpenMode.READ_WRITE(0o2)**: Create the file in read/write mode.<br>You can also specify the following options, separated by a bitwise OR operator (&#124;). By default, no additional options are given.<br>- **OpenMode.CREATE(0o100)**: If the file does not exist, create it.<br>- **OpenMode.TRUNC(0o1000)**: If the **RandomAccessFile** object already exists and is created in write-only or read/write mode, truncate the file length to 0.<br>- **OpenMode.APPEND(0o2000)**: Create the file in append mode. New data will be added to the end of the **RandomAccessFile** object. <br>- **OpenMode.NONBLOCK(0o4000)**: If **path** points to a named pipe (also known as a FIFO), block special file, or character special file, perform non-blocking operations on the created file and in subsequent I/Os.<br>- **OpenMode.DIR(0o200000)**: If **path** does not point to a directory, throw an exception.<br>- **OpenMode.NOFOLLOW(0o400000)**: If **path** points to a symbolic link, throw an exception.<br>- **OpenMode.SYNC(0o4010000)**: Create a **RandomAccessFile** instance in synchronous I/O mode.|

**Return value**

  | Type               | Description       |
  | ------------------ | --------- |
  | [RandomAccessFile](#randomaccessfile) | **RandomAccessFile** instance created.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath, fileIO.OpenMode.CREATE | fileIO.OpenMode.READ_WRITE);
  let randomaccessfile = fileIO.createRandomAccessFileSync(file);
  ```

## fs.createStream

createStream(path: string, mode: string): Promise&lt;Stream&gt;

Creates a stream based on the file path. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name| Type  | Mandatory| Description                                                        |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| path   | string | Yes  | Application sandbox path of the file.                                  |
| mode   | string | Yes  | - **r**: Open a file for reading. The file must exist.<br>- **r+**: Open a file for both reading and writing. The file must exist.<br>- **w**: Open a file for writing. If the file exists, clear its content. If the file does not exist, create a file.<br>- **w+**: Open a file for both reading and writing. If the file exists, clear its content. If the file does not exist, create a file.<br>- **a**: Open a file in append mode for writing at the end of the file. If the file does not exist, create a file. If the file exists, write data to the end of the file (the original content of the file is reserved).<br>- **a+**: Open a file in append mode for reading or updating at the end of the file. If the file does not exist, create a file. If the file exists, write data to the end of the file (the original content of the file is reserved).|

**Return value**

  | Type                               | Description       |
  | --------------------------------- | --------- |
  | Promise&lt;[Stream](#stream)&gt; | Promise used to return the stream opened.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  fs.createStream(filePath, "r+").then((stream) => {
      console.info("Stream created");
  }).catch((err) => {
      console.info("createStream failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```


## fs.createStream

createStream(path: string, mode: string, callback: AsyncCallback&lt;Stream&gt;): void

Creates a stream based on the file path. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name  | Type                                   | Mandatory| Description                                                        |
| -------- | --------------------------------------- | ---- | ------------------------------------------------------------ |
| path     | string                                  | Yes  | Application sandbox path of the file.                                  |
| mode     | string                                  | Yes  | - **r**: Open a file for reading. The file must exist.<br>- **r+**: Open a file for both reading and writing. The file must exist.<br>- **w**: Open a file for writing. If the file exists, clear its content. If the file does not exist, create a file.<br>- **w+**: Open a file for both reading and writing. If the file exists, clear its content. If the file does not exist, create a file.<br>- **a**: Open a file in append mode for writing at the end of the file. If the file does not exist, create a file. If the file exists, write data to the end of the file (the original content of the file is reserved).<br>- **a+**: Open a file in append mode for reading or updating at the end of the file. If the file does not exist, create a file. If the file exists, write data to the end of the file (the original content of the file is reserved).|
| callback | AsyncCallback&lt;[Stream](#stream)&gt; | Yes  | Callback invoked when the stream is created asynchronously.                                  |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  fs.createStream(filePath, "r+", (err, stream) => {
    if (err) {
      console.info("create stream failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("create stream success");
    }
  });
  ```

## fs.createStreamSync

createStreamSync(path: string, mode: string): Stream

Synchronously creates a stream based on the file path.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name| Type  | Mandatory| Description                                                        |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| path   | string | Yes  | Application sandbox path of the file.                                  |
| mode   | string | Yes  | - **r**: Open a file for reading. The file must exist.<br>- **r+**: Open a file for both reading and writing. The file must exist.<br>- **w**: Open a file for writing. If the file exists, clear its content. If the file does not exist, create a file.<br>- **w+**: Open a file for both reading and writing. If the file exists, clear its content. If the file does not exist, create a file.<br>- **a**: Open a file in append mode for writing at the end of the file. If the file does not exist, create a file. If the file exists, write data to the end of the file (the original content of the file is reserved).<br>- **a+**: Open a file in append mode for reading or updating at the end of the file. If the file does not exist, create a file. If the file exists, write data to the end of the file (the original content of the file is reserved).|

**Return value**

  | Type               | Description       |
  | ------------------ | --------- |
  | [Stream](#stream) | Stream opened.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let ss = fs.createStreamSync(filePath, "r+");
  ```


## fs.fdopenStream

fdopenStream(fd: number, mode: string): Promise&lt;Stream&gt;

Opens a stream based on the file descriptor. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name | Type    | Mandatory  | Description                                      |
  | ---- | ------ | ---- | ---------------------------------------- |
  | fd   | number | Yes   | FD of the file.                            |
  | mode | string | Yes   | - **r**: Open a file for reading. The file must exist.<br>- **r+**: Open a file for both reading and writing. The file must exist.<br>- **w**: Open a file for writing. If the file exists, clear its content. If the file does not exist, create a file.<br>- **w+**: Open a file for both reading and writing. If the file exists, clear its content. If the file does not exist, create a file.<br>- **a**: Open a file in append mode for writing at the end of the file. If the file does not exist, create a file. If the file exists, write data to the end of the file (the original content of the file is reserved).<br>- **a+**: Open a file in append mode for reading or updating at the end of the file. If the file does not exist, create a file. If the file exists, write data to the end of the file (the original content of the file is reserved).|

**Return value**

  | Type                              | Description       |
  | --------------------------------- | --------- |
  | Promise&lt;[Stream](#stream)&gt; | Promise used to return the stream opened.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath);
  fs.fdopenStream(file.fd, "r+").then((stream) => {
      console.info("Stream opened");
      fs.closeSync(file);
  }).catch((err) => {
      console.info("openStream failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## fs.fdopenStream

fdopenStream(fd: number, mode: string, callback: AsyncCallback&lt;Stream&gt;): void

Opens a stream based on the file descriptor. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name     | Type                                      | Mandatory  | Description                                      |
  | -------- | ---------------------------------------- | ---- | ---------------------------------------- |
  | fd       | number                                   | Yes   | FD of the file.                            |
  | mode     | string                                   | Yes   | - **r**: Open a file for reading. The file must exist.<br>- **r+**: Open a file for both reading and writing. The file must exist.<br>- **w**: Open a file for writing. If the file exists, clear its content. If the file does not exist, create a file.<br>- **w+**: Open a file for both reading and writing. If the file exists, clear its content. If the file does not exist, create a file.<br>- **a**: Open a file in append mode for writing at the end of the file. If the file does not exist, create a file. If the file exists, write data to the end of the file (the original content of the file is reserved).<br>- **a+**: Open a file in append mode for reading or updating at the end of the file. If the file does not exist, create a file. If the file exists, write data to the end of the file (the original content of the file is reserved).|
  | callback | AsyncCallback&lt;[Stream](#stream)&gt; | Yes   | Callback invoked when the stream is created asynchronously.                           |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath, fs.OpenMode.READ_ONLY);
  fs.fdopenStream(file.fd, "r+", (err, stream) => {
    if (err) {
      console.info("fdopen stream failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("fdopen stream success");
      fs.closeSync(file);
    }
  });
  ```

## fs.fdopenStreamSync

fdopenStreamSync(fd: number, mode: string): Stream

Synchronously opens a stream based on the file descriptor.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name | Type    | Mandatory  | Description                                      |
  | ---- | ------ | ---- | ---------------------------------------- |
  | fd   | number | Yes   | FD of the file.                            |
  | mode | string | Yes   | - **r**: Open a file for reading. The file must exist.<br>- **r+**: Open a file for both reading and writing. The file must exist.<br>- **w**: Open a file for writing. If the file exists, clear its content. If the file does not exist, create a file.<br>- **w+**: Open a file for both reading and writing. If the file exists, clear its content. If the file does not exist, create a file.<br>- **a**: Open a file in append mode for writing at the end of the file. If the file does not exist, create a file. If the file exists, write data to the end of the file (the original content of the file is reserved).<br>- **a+**: Open a file in append mode for reading or updating at the end of the file. If the file does not exist, create a file. If the file exists, write data to the end of the file (the original content of the file is reserved).|

**Return value**

  | Type               | Description       |
  | ------------------ | --------- |
  | [Stream](#stream) | Stream opened.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath, fs.OpenMode.READ_ONLY | fs.OpenMode.CREATE);
  let ss = fs.fdopenStreamSync(file.fd, "r+");
  fs.closeSync(file);
  ```

## fs.createWatcher<sup>10+</sup>

createWatcher(path: string, events: number, listener: WatchEventListener): Watcher

Creates a **Watcher** object to observe file or directory changes.

**System API**: This is a system API.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name | Type    | Mandatory  | Description                                      |
  | ---- | ------ | ---- | ---------------------------------------- |
  | path   | string | Yes   | Application sandbox path of the file or directory to observe.                            |
  | events | number | Yes   | Events to observe. Multiple events can be separated by a bitwise OR operator (&#124;).<br>- **0x1: IN_ACCESS**: A file is accessed.<br>- **0x2: IN_MODIFY**: The file content is modified.<br>- **0x4: IN_ATTRIB**: Metadata is modified.<br>- **0x8: IN_CLOSE_WRITE**: The file opened for writing is closed.<br>- **0x10: IN_CLOSE_NOWRITE**: The file or directory opened is closed without being written.<br>- **0x20: IN_OPEN**: A file or directory is opened.<br>- **0x40: IN_MOVED_FROM**: A file in the observed directory is moved.<br>- **0x80: IN_MOVED_TO**: A file is moved to the observed directory.<br>- **0x100: IN_CREATE**: A file or directory is created in the observed directory.<br>- **0x200: IN_DELETE**: A file or directory is deleted from the observed directory.<br>- **0x400: IN_DELETE_SELF**: The observed directory is deleted. After the directory is deleted, the listening stops.<br>- **0x800: IN_MOVE_SELF**: The observed file or directory is moved. After the file or directory is moved, the listening continues.<br>- **0xfff: IN_ALL_EVENTS**: All events.|
  | listener   | WatchEventListener | Yes   | Callback invoked when an observed event occurs. The callback will be invoked each time an observed event occurs.                            |

**Return value**

  | Type               | Description       |
  | ------------------ | --------- |
  | [Watcher](#watcher10) | **Watcher** object created.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
  let watcher = fs.createWatcher(filePath, 0x2 | 0x10, (watchEvent) => {
    if (watchEvent.event == 0x2) {
      console.info(watchEvent.fileName + 'was modified');
    } else if (watchEvent.event == 0x10) {
      console.info(watchEvent.fileName + 'was closed');
    }
  });
  watcher.start();
  fs.writeSync(file.fd, 'test');
  fs.closeSync(file);
  watcher.stop();
  ```

## WatchEventListener<sup>10+</sup>

(event: WatchEvent): void

Called when an observed event occurs.

**System API**: This is a system API.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name | Type    | Mandatory  | Description                                      |
  | ---- | ------ | ---- | ---------------------------------------- |
  | event   | WatchEvent | Yes   | Event for the callback to invoke.                            |
 
## WatchEvent<sup>10+</sup>

Defines the event to observe.

**System API**: This is a system API.

**System capability**: SystemCapability.FileManagement.File.FileIO

| Name  | Type  | Readable  | Writable  | Description     |
| ---- | ------ | ---- | ---- | ------- |
| fileName | string | Yes   | No   | Name of the file for which the event occurs.|
| event | number | Yes   | No   | Events to observe. For details, see **events** in [createWatcher](#fscreatewatcher10).|
| cookie | number | Yes   | No   | Cookie bound with the event. Currently, only the **IN_MOVED_FROM** and **IN_MOVED_TO** events are supported. The **IN_MOVED_FROM** and **IN_MOVED_TO** events of the same file have the same **cookie** value.|

## Stat

Represents detailed file information. Before calling any API of the **Stat()** class, use [stat()](#fsstat) to create a **Stat** instance synchronously or asynchronously.

**System capability**: SystemCapability.FileManagement.File.FileIO

### Attributes

| Name    | Type  | Readable  | Writable  | Description                                      |
| ------ | ------ | ---- | ---- | ---------------------------------------- |                        
| ino    | number | Yes   | No   | File ID. Different files on the same device have different **ino**s.|                 |
| mode   | number | Yes   | No   | File permissions. The meaning of each bit is as follows:<br>- **0o400**: The owner has the read permission on a regular file or a directory entry.<br>- **0o200**: The owner has the permission to write a regular file or create and delete a directory entry.<br>- **0o100**: The owner has the permission to execute a regular file or search for the specified path in a directory.<br>- **0o040**: The user group has the read permission on a regular file or a directory entry.<br>- **0o020**: The user group has the permission to write a regular file or create and delete a directory entry.<br>- **0o010**: The user group has the permission to execute a regular file or search for the specified path in a directory.<br>- **0o004**: Other users have the permission to read a regular file or read a directory entry.<br>- **0o002**: Other users have the permission to write a regular file or create and delete a directory entry.<br>- **0o001**: Other users have the permission to execute a regular file or search for the specified path in a directory.|
| uid    | number | Yes   | No   | ID of the file owner.|
| gid    | number | Yes   | No   | ID of the user group of the file.|
| size   | number | Yes   | No   | File size, in bytes. This parameter is valid only for regular files. |
| atime  | number | Yes   | No   | Time of the last access to the file. The value is the number of seconds elapsed since 00:00:00 on January 1, 1970.       |
| mtime  | number | Yes   | No   | Time of the last modification to the file. The value is the number of seconds elapsed since 00:00:00 on January 1, 1970.       |
| ctime  | number | Yes   | No   | Time of the last status change of the file. The value is the number of seconds elapsed since 00:00:00 on January 1, 1970.     |

### isBlockDevice

isBlockDevice(): boolean

Checks whether this file is a block special file. A block special file supports access by block only, and it is cached when accessed.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Return value**

  | Type     | Description              |
  | ------- | ---------------- |
  | boolean | Whether the file is a block special file.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let isBLockDevice = fs.statSync(filePath).isBlockDevice();
  ```

### isCharacterDevice

isCharacterDevice(): boolean

Checks whether this file is a character special file. A character special file supports random access, and it is not cached when accessed.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Return value**

  | Type     | Description               |
  | ------- | ----------------- |
  | boolean | Whether the file is a character special file.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let isCharacterDevice = fs.statSync(filePath).isCharacterDevice();
  ```

### isDirectory

isDirectory(): boolean

Checks whether this file is a directory.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Return value**

  | Type     | Description           |
  | ------- | ------------- |
  | boolean | Whether the file is a directory.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let dirPath = pathDir + "/test";
  let isDirectory = fs.statSync(dirPath).isDirectory(); 
  ```

### isFIFO

isFIFO(): boolean

Checks whether this file is a named pipe (or FIFO). Named pipes are used for inter-process communication.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Return value**

  | Type     | Description                   |
  | ------- | --------------------- |
  | boolean | Whether the file is an FIFO.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let isFIFO = fs.statSync(filePath).isFIFO(); 
  ```

### isFile

isFile(): boolean

Checks whether this file is a regular file.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Return value**

  | Type     | Description             |
  | ------- | --------------- |
  | boolean | Whether the file is a regular file.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let isFile = fs.statSync(filePath).isFile();
  ```

### isSocket

isSocket(): boolean

Checks whether this file is a socket.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Return value**

  | Type     | Description            |
  | ------- | -------------- |
  | boolean | Whether the file is a socket.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let isSocket = fs.statSync(filePath).isSocket(); 
  ```

### isSymbolicLink

isSymbolicLink(): boolean

Checks whether this file is a symbolic link.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Return value**

  | Type     | Description             |
  | ------- | --------------- |
  | boolean | Whether the file is a symbolic link.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test";
  let isSymbolicLink = fs.statSync(filePath).isSymbolicLink(); 
  ```

## Stream

Provides a stream for file operations. Before calling any API of the **Stream** class, use **createStream()** to create a **Stream** instance synchronously or asynchronously.

### close

close(): Promise&lt;void&gt;

Closes the stream. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Return value**

  | Type                 | Description           |
  | ------------------- | ------------- |
  | Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let ss= fs.createStreamSync(filePath, "r+");
  ss.close().then(() => {
      console.info("File stream closed");
  }).catch((err) => {
      console.info("close fileStream  failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

### close

close(callback: AsyncCallback&lt;void&gt;): void

Closes the stream. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name     | Type                       | Mandatory  | Description           |
  | -------- | ------------------------- | ---- | ------------- |
  | callback | AsyncCallback&lt;void&gt; | Yes   | Callback invoked immediately after the stream is closed.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let ss= fs.createStreamSync(filePath, "r+");
  ss.close((err) => {
    if (err) {
      console.info("close stream failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("close stream success");
    }
  });
  ```

### closeSync

closeSync(): void

Synchronously closes the stream.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let ss= fs.createStreamSync(filePath, "r+");
  ss.closeSync();
  ```

### flush

flush(): Promise&lt;void&gt;

Flushes the stream. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Return value**

  | Type                 | Description           |
  | ------------------- | ------------- |
  | Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let ss= fs.createStreamSync(filePath, "r+");
  ss.flush().then(() => {
      console.info("Stream flushed");
  }).catch((err) => {
      console.info("flush failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

### flush

flush(callback: AsyncCallback&lt;void&gt;): void

Flushes the stream. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name     | Type                       | Mandatory  | Description            |
  | -------- | ------------------------- | ---- | -------------- |
  | callback | AsyncCallback&lt;void&gt; | Yes   | Callback invoked when the stream is asynchronously flushed.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let ss= fs.createStreamSync(filePath, "r+");
  ss.flush((err) => {
    if (err) {
      console.info("flush stream failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("flush success");
    }
  });
  ```

### flushSync

flushSync(): void

Synchronously flushes the stream.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let ss= fs.createStreamSync(filePath, "r+");
  ss.flushSync();
  ```

### write

write(buffer: ArrayBuffer|string, options?: { offset?: number; length?: number; encoding?: string; }): Promise&lt;number&gt;

Writes data into the stream. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name    | Type                             | Mandatory  | Description                                      |
  | ------- | ------------------------------- | ---- | ---------------------------------------- |
  | buffer  | ArrayBuffer\|string | Yes   | Data to write. It can be a string or data from a buffer.                    |
  | options | Object                          | No   | The options are as follows:<br>- **length** (number): length of the data to write. The default value is the buffer length.<br>- **offset** (number): start position to write the data in the file. This parameter is optional. By default, data is written from the current position.<br>- **encoding** (string): format of the data to be encoded when the data is a string. The default value is **'utf-8'**, which is the only value supported.|

**Return value**

  | Type                   | Description      |
  | --------------------- | -------- |
  | Promise&lt;number&gt; | Promise used to return the length of the data written.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let ss= fs.createStreamSync(filePath, "r+");
  ss.write("hello, world",{ offset: 5, length: 5, encoding: 'utf-8' }).then((number) => {
      console.info("write succeed and size is:" + number);
  }).catch((err) => {
      console.info("write failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

### write

write(buffer: ArrayBuffer|string, options?: { offset?: number; length?: number; encoding?: string; }, callback: AsyncCallback&lt;number&gt;): void

Writes data into the stream. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name  | Type                           | Mandatory| Description                                                        |
  | -------- | ------------------------------- | ---- | ------------------------------------------------------------ |
  | buffer   | ArrayBuffer\|string | Yes  | Data to write. It can be a string or data from a buffer.                    |
  | options  | Object                          | No  | The options are as follows:<br>- **length** (number): length of the data to write. This parameter is optional. The default value is the buffer length.<br>- **offset** (number): start position to write the data in the file. This parameter is optional. By default, data is written from the current position.<br>- **encoding** (string): format of the data to be encoded when the data is a string. The default value is **'utf-8'**, which is the only value supported.|
  | callback | AsyncCallback&lt;number&gt;     | Yes  | Callback invoked when the data is written asynchronously.                              |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let ss= fs.createStreamSync(filePath, "r+");
  ss.write("hello, world", { offset: 5, length: 5, encoding :'utf-8'}, (err, bytesWritten) => {
    if (err) {
      console.info("write stream failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      if (bytesWritten) {
        console.info("write succeed and size is:" + bytesWritten);
      }
    }
  });
  ```

### writeSync

writeSync(buffer: ArrayBuffer|string, options?: { offset?: number; length?: number; encoding?: string; }): number

Synchronously writes data into the stream.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name    | Type                             | Mandatory  | Description                                      |
  | ------- | ------------------------------- | ---- | ---------------------------------------- |
  | buffer  | ArrayBuffer\|string | Yes   | Data to write. It can be a string or data from a buffer.                    |
  | options | Object                          | No   | The options are as follows:<br>- **length** (number): length of the data to write. This parameter is optional. The default value is the buffer length.<br>- **offset** (number): start position to write the data in the file. This parameter is optional. By default, data is written from the current position.<br>- **encoding** (string): format of the data to be encoded when the data is a string. The default value is **'utf-8'**, which is the only value supported.|

**Return value**

  | Type    | Description      |
  | ------ | -------- |
  | number | Length of the data written in the file.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let ss= fs.createStreamSync(filePath,"r+");
  let num = ss.writeSync("hello, world", {offset: 5, length: 5, encoding :'utf-8'});
  ```

### read

read(buffer: ArrayBuffer, options?: { offset?: number; length?: number; }): Promise&lt;number&gt;

Reads data from the stream. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name    | Type         | Mandatory  | Description                                      |
  | ------- | ----------- | ---- | ---------------------------------------- |
  | buffer  | ArrayBuffer | Yes   | Buffer used to store the file read.                             |
  | options | Object      | No   | The options are as follows:<br>- **length** (number): length of the data to read. This parameter is optional. The default value is the buffer length.<br>- **offset** (number): start position to read the data. This parameter is optional. By default, data is read from the current position.|

**Return value**

  | Type                                | Description    |
  | ---------------------------------- | ------ |
  | Promise&lt;number&gt; | Promise used to return the data read.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let ss = fs.createStreamSync(filePath, "r+");
  let buf = new ArrayBuffer(4096);
  ss.read(buf, {offset: 5, length: 5}).then((readLen) => {
    console.info("Read data successfully");
    console.log(String.fromCharCode.apply(null, new Uint8Array(buf.slice(0, readLen))));
  }).catch((err) => {
      console.info("read data failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

### read

read(buffer: ArrayBuffer, options?: { position?: number; offset?: number; length?: number; }, callback: AsyncCallback&lt;number&gt;): void

Reads data from the stream. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name     | Type                                      | Mandatory  | Description                                      |
  | -------- | ---------------------------------------- | ---- | ---------------------------------------- |
  | buffer   | ArrayBuffer                              | Yes   | Buffer used to store the file read.                             |
  | options  | Object                                   | No   | The options are as follows:<br>- **length** (number): length of the data to read. This parameter is optional. The default value is the buffer length.<br>- **offset** (number): start position to read the data. This parameter is optional. By default, data is read from the current position.|
  | callback | AsyncCallback&lt;number&gt; | Yes   | Callback invoked when data is read asynchronously from the stream.                        |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let ss = fs.createStreamSync(filePath, "r+");
  let buf = new ArrayBuffer(4096)
  ss.read(buf, {offset: 5, length: 5}, (err, readLen) => {
    if (err) {
      console.info("read stream failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("Read data successfully");
      console.log(String.fromCharCode.apply(null, new Uint8Array(buf.slice(0, readLen))));
    }
  });
  ```

### readSync

readSync(buffer: ArrayBuffer, options?: { offset?: number; length?: number; }): number

Synchronously reads data from the stream.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name    | Type         | Mandatory  | Description                                      |
  | ------- | ----------- | ---- | ---------------------------------------- |
  | buffer  | ArrayBuffer | Yes   | Buffer used to store the file read.                             |
  | options | Object      | No   | The options are as follows:<br>- **length** (number): length of the data to read. This parameter is optional. The default value is the buffer length.<br>- **offset** (number): start position to read the data. This parameter is optional. By default, data is read from the current position.<br> |

**Return value**

  | Type    | Description      |
  | ------ | -------- |
  | number | Length of the data read.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let ss = fs.createStreamSync(filePath, "r+");
  let num = ss.readSync(new ArrayBuffer(4096), {offset: 5, length: 5});
  ```

## File

Represents a **File** object opened by **open()**.

**System capability**: SystemCapability.FileManagement.File.FileIO

### Attributes

| Name  | Type  | Readable  | Writable  | Description     |
| ---- | ------ | ---- | ---- | ------- |
| fd | number | Yes   | No   | FD of the file.|

### lock

lock(exclusive?: boolean): Promise\<void>

Applies an exclusive lock or a shared lock on this file in blocking mode. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name    | Type         | Mandatory  | Description                                      |
  | ------- | ----------- | ---- | ---------------------------------------- |
  | exclusive  | boolean | No  | Lock to apply. The value **true** means an exclusive lock, and the value **false** (default) means a shared lock.      |

**Return value**

  | Type                                | Description    |
  | ---------------------------------- | ------ |
  | Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let file = fs.openSync(pathDir + "/test.txt", fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
  file.lock(true).then(() => {
    console.log("lock file successful");
  }).catch((err) => {
      console.info("lock file failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

### lock

lock(exclusive?: boolean, callback: AsyncCallback\<void>): void

Applies an exclusive lock or a shared lock on this file in blocking mode. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name    | Type         | Mandatory  | Description                                      |
  | ------- | ----------- | ---- | ---------------------------------------- |
  | exclusive  | boolean | No  | Lock to apply. The value **true** means an exclusive lock, and the value **false** (default) means a shared lock.      |
  | callback | AsyncCallback&lt;void&gt; | Yes   | Callback invoked when the file is locked.  |     

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let file = fs.openSync(pathDir + "/test.txt", fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
  file.lock(true, (err) => {
    if (err) {
      console.info("lock file failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.log("lock file successful");
    }
  });
  ```

### tryLock

tryLock(exclusive?: boolean): void

Applies an exclusive lock or a shared lock on this file in non-blocking mode.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name    | Type         | Mandatory  | Description                                      |
  | ------- | ----------- | ---- | ---------------------------------------- |
  | exclusive  | boolean | No  | Lock to apply. The value **true** means an exclusive lock, and the value **false** (default) means a shared lock.      |    

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let file = fs.openSync(pathDir + "/test.txt", fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
  file.tryLock(true);
  console.log("lock file successful");
  ```

### unlock

unlock(): void

Unlocks this file synchronously.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let file = fs.openSync(pathDir + "/test.txt", fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
  file.tryLock(true);
  file.unlock();
  console.log("unlock file successful");
  ```


## RandomAccessFile

Randomly reads and writes a stream. Before invoking any API of **RandomAccessFile**, you need to use **createRandomAccess()** to create a **RandomAccessFile** instance synchronously or asynchronously.

**System capability**: SystemCapability.FileManagement.File.FileIO

### Attributes

| Name        | Type  | Readable | Writable | Description             |
| ----------- | ------ | ----  | ----- | ---------------- |
| fd          | number | Yes   | No   | FD of the file.|
| filePointer | number | Yes   | Yes   | Offset pointer to the **RandomAccessFile** instance.|

### setFilePointer<sup>10+</sup>

setFilePointer(): void

Sets the file offset pointer.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let randomAccessFile = fs.createRandomAccessFileSync(filePath, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
  randomAccessFile.setFilePointer(1);
  ```


### close<sup>10+</sup>

close(): void

Closes this **RandomAccessFile** instance synchronously.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let randomAccessFile = fs.createRandomAccessFileSync(filePath, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
  randomAccessFile.closeSync();
  ```

### write<sup>10+</sup>

write(buffer: ArrayBuffer|string, options?: { offset?: number; length?: number; encoding?: string; }): Promise&lt;number&gt;

Writes data into a file. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name    | Type                             | Mandatory  | Description                                      |
  | ------- | ------------------------------- | ---- | ---------------------------------------- |
  | buffer  | ArrayBuffer\|string | Yes   | Data to write. It can be a string or data from a buffer.                    |
  | options | Object                          | No   | The options are as follows:<br>- **length** (number): length of the data to write. The default value is the buffer length.<br>- **offset** (number): start position to write the data (it is determined by **filePointer** plus **offset**). This parameter is optional. By default, data is written from the **filePointer**.<br>- **encoding** (string): format of the data to be encoded when the data is a string. The default value is **'utf-8'**, which is the only value supported.|

**Return value**

  | Type                   | Description      |
  | --------------------- | -------- |
  | Promise&lt;number&gt; | Promise used to return the length of the data written.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(fpath, fs.OpenMode.CREATE | fs.OpenMode.READ_WRITE);
  let randomaccessfile = fs.createRandomAccessFileSync(file);
  let bufferLength = 4096;
  randomaccessfile.write(new ArrayBuffer(bufferLength), { offset: 1, length: 5 }).then((bytesWritten) => {
      console.info("randomAccessFile bytesWritten: " + bytesWritten);
  }).catch((err) => {
      console.info("create randomAccessFile failed with error message: " + err.message + ", error code: " + err.code);
  });

  ```

### write<sup>10+</sup>

write(buffer: ArrayBuffer|string, options?: { offset?: number; length?: number; encoding?: string; }, callback: AsyncCallback&lt;number&gt;): void

Writes data into a file. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name  | Type                           | Mandatory| Description                                                        |
  | -------- | ------------------------------- | ---- | ------------------------------------------------------------ |
  | buffer   | ArrayBuffer\|string | Yes  | Data to write. It can be a string or data from a buffer.                    |
  | options  | Object                          | No  | The options are as follows:<br>- **length** (number): length of the data to write. This parameter is optional. The default value is the buffer length.<br>- **offset** (number): start position to write the data (it is determined by **filePointer** plus **offset**). This parameter is optional. By default, data is written from the **filePointer**.<br>- **encoding** (string): format of the data to be encoded when the data is a string. The default value is **'utf-8'**, which is the only value supported.|
  | callback | AsyncCallback&lt;number&gt;     | Yes  | Callback invoked when the data is written asynchronously.                              |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let randomAccessFile = fs.createRandomAccessFileSync(file);
  let bufferLength = 4096;
  randomAccessFile.write(new ArrayBuffer(bufferLength), { offset: 1 }, function(err, bytesWritten) {
      if (err) {
          console.info("write failed with error message: " + err.message + ", error code: " + err.code);
      } else {
          if (bytesWritten) {
              console.info("write succeed and size is:" + bytesWritten);
          }
      }
  });
  ```

### writeSync<sup>10+</sup>

writeSync(buffer: ArrayBuffer|string, options?: { offset?: number; length?: number; encoding?: string; }): number

Synchronously writes data into a file.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name    | Type                             | Mandatory  | Description                                      |
  | ------- | ------------------------------- | ---- | ---------------------------------------- |
  | buffer  | ArrayBuffer\|string | Yes   | Data to write. It can be a string or data from a buffer.                    |
  | options | Object                          | No   | The options are as follows:<br>- **length** (number): length of the data to write. This parameter is optional. The default value is the buffer length.<br>- **offset** (number): start position to write the data (it is determined by **filePointer** plus **offset**). This parameter is optional. By default, data is written from the **filePointer**.<br>- **encoding** (string): format of the data to be encoded when the data is a string. The default value is **'utf-8'**, which is the only value supported.|

**Return value**

  | Type    | Description      |
  | ------ | -------- |
  | number | Length of the data written in the file.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let randomaccessfile= fs.createRandomAccessFileSync(filePath,"r+");
  let bytesWritten = randomaccessfile.writeSync("hello, world", {offset: 5, length: 5, encoding :'utf-8'});
  ```

### read<sup>10+</sup>

read(buffer: ArrayBuffer, options?: { offset?: number; length?: number; }): Promise&lt;number&gt;

Reads data from a file. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name    | Type         | Mandatory  | Description                                      |
  | ------- | ----------- | ---- | ---------------------------------------- |
  | buffer  | ArrayBuffer | Yes   | Buffer used to store the file read.                             |
  | options | Object      | No   | The options are as follows:<br>- **length** (number): length of the data to read. This parameter is optional. The default value is the buffer length.<br>- **offset** (number): start position to read the data (it is determined by **filePointer** plus **offset**). This parameter is optional. By default, data is read from the **filePointer**.|

**Return value**

  | Type                                | Description    |
  | ---------------------------------- | ------ |
  | Promise&lt;number&gt; | Promise used to return the data read.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath, fs.OpenMode.CREATE | fs.OpenMode.READ_WRITE);
  let randomaccessfile = fs.createRandomAccessFileSync(file);
  let bufferLength = 4096;
  randomaccessfile.read(new ArrayBuffer(bufferLength), { offset: 1, length: 5 }).then((readLength) => {
      console.info("randomAccessFile readLength: " + readLength);
  }).catch((err) => {
      console.info("create randomAccessFile failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

### read<sup>10+</sup>

read(buffer: ArrayBuffer, options?: { position?: number; offset?: number; length?: number; }, callback: AsyncCallback&lt;number&gt;): void

Reads data from a file. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name     | Type                                      | Mandatory  | Description                                      |
  | -------- | ---------------------------------------- | ---- | ---------------------------------------- |
  | buffer   | ArrayBuffer                              | Yes   | Buffer used to store the file read.                             |
  | options  | Object                                   | No   | The options are as follows:<br>- **length** (number): length of the data to read. This parameter is optional. The default value is the buffer length.<br>- **offset** (number): start position to read the data (it is determined by **filePointer** plus **offset**). This parameter is optional. By default, data is read from the **filePointer**.|
  | callback | AsyncCallback&lt;number&gt; | Yes   | Callback invoked when data is read asynchronously from the stream.                        |

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath, fs.OpenMode.CREATE | fs.OpenMode.READ_WRITE);
  let randomaccessfile = await fileIO.createRandomAccessFile(file);
  let length = 20;
  randomaccessfile.read(new ArrayBuffer(length), { offset: 1, length: 5 }, function (err, readLength) {
    if (err) {
      console.info("read failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      if (readLength) {
        console.info("read succeed and size is:" + readLength);
      }
    }
  });
  ```

### readSync<sup>10+</sup>

readSync(buffer: ArrayBuffer, options?: { offset?: number; length?: number; }): number

Synchronously reads data from a file.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name    | Type         | Mandatory  | Description                                      |
  | ------- | ----------- | ---- | ---------------------------------------- |
  | buffer  | ArrayBuffer | Yes   | Buffer used to store the file read.                             |
  | options | Object      | No   | The options are as follows:<br>- **length** (number): length of the data to read. This parameter is optional. The default value is the buffer length.<br>- **offset** (number): start position to read the data (it is determined by **filePointer** plus **offset**). This parameter is optional. By default, data is read from the **filePointer**.<br> |

**Return value**

  | Type    | Description      |
  | ------ | -------- |
  | number | Length of the data read.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let file = fs.openSync(filePath, fileIO.OpenMode.CREATE | fileIO.OpenMode.READ_WRITE);
  let randomaccessfile = fs.createRandomAccessFileSync(file);
  let length = 4096;
  let readLength = randomaccessfile.readSync(new ArrayBuffer(length));
  ```


## Watcher<sup>10+</sup>

Provides APIs for observing the changes of files or folders. Before using the APIs of **Watcher** , call **createWatcher()** to create a **Watcher** object.

### start<sup>10+</sup>

start(): void

Starts listening.

**System API**: This is a system API.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let watcher = fs.createWatcher(filePath, 0xfff, () => {});
  watcher.start();
  watcher.stop();
  ```

### stop<sup>10+</sup>

stop(): void

Stops listening.

**System API**: This is a system API.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](../errorcodes/errorcode-filemanagement.md#basic-file-io-error-codes).

**Example**

  ```js
  let filePath = pathDir + "/test.txt";
  let watcher = fs.createWatcher(filePath, 0xfff, () => {});
  watcher.start();
  watcher.stop();
  ```

## OpenMode

Defines the constants of the **mode** parameter used in **open()**. It specifies the mode for opening a file.

**System capability**: SystemCapability.FileManagement.File.FileIO

| Name  | Type  | Value | Description     |
| ---- | ------ |---- | ------- |
| READ_ONLY | number |  0o0   | Open the file in read-only mode.|
| WRITE_ONLY | number | 0o1    | Open the file in write-only mode.|
| READ_WRITE | number | 0o2    | Open the file in read/write mode.|
| CREATE | number | 0o100    | Create a file if the specified file does not exist.|
| TRUNC | number | 0o1000    | If the file exists and is open in write-only or read/write mode, truncate the file length to 0.|
| APPEND | number | 0o2000   | Open the file in append mode. New data will be written to the end of the file.|
| NONBLOCK | number | 0o4000    | If **path** points to a named pipe (FIFO), block special file, or character special file, perform non-blocking operations on the open file and in subsequent I/Os.|
| DIR | number | 0o200000    | If **path** does not point to a directory, throw an exception.|
| NOFOLLOW | number | 0o400000    | If **path** points to a symbolic link, throw an exception.|
| SYNC | number | 0o4010000    | Open the file in synchronous I/O mode.|

## Filter<sup>10+</sup>

**System capability**: SystemCapability.FileManagement.File.FileIO

Defines the file filtering configuration, which can be used by **listFile()**.

| Name       | Type      | Description               |
| ----------- | --------------- | ------------------ |
| suffix | Array&lt;string&gt;     | Locate files that fully match the specified file name extensions, which are of the OR relationship.          |
| displayName    | Array&lt;string&gt;     | Locate files that fuzzy match the specified file names, which are of the OR relationship.|
| mimeType    | Array&lt;string&gt; | Locate files that fully match the specified MIME types, which are of the OR relationship.      |
| fileSizeOver    | number | Locate files that are greater than or equal to the specified size.      |
| lastModifiedAfter    | number | Locate files whose last modification time is the same or later than the specified time.      |
| excludeMedia    | boolean | Whether to exclude the files already in **Media**.      |

## ConflictFiles<sup>10+</sup>

**System capability**: SystemCapability.FileManagement.File.FileIO

Defines information about the conflicting files. It is used the **copyDir()** and **moveDir()**.

| Name       | Type      | Description               |
| ----------- | --------------- | ------------------ |
| srcFile | string     | Path of the source file.          |
| destFile    | string     | Path of the destination file.|

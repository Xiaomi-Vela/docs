# @ohos.securityLabel (Data Label)

The **secuityLabel** module provides APIs to manage file data security levels, including obtaining and setting file data security levels.

> **NOTE**
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```js
import securityLabel from '@ohos.securityLabel';
```

## Usage

Before using the APIs provided by this module to perform operations on a file or directory, obtain the path of the application sandbox as follows:

```js
import featureAbility from '@ohos.ability.featureAbility';
let context = featureAbility.getContext();
let path = '';
context.getFilesDir().then((data) => {
    path = data;
})
```

## securityLabel.setSecurityLabel

setSecurityLabel(path:string, type:dataLevel):Promise&lt;void&gt;

Sets the security label for a file in asynchronous mode. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name   | Type      | Mandatory| Description                                        |
| --------- | ------    | ---- | -------------------------------------------- |
| path      | string    | Yes  | File path.                                    |
| type      | dataLevel | Yes  | File security level, which can be **s0**, **s1**, **s2**, **s3**, or **s4**.|

**Return value**

  | Type               | Description            |
  | ------------------- | ---------------- |
  | Promise&lt;void&gt; | Promise used to return the result. An empty value will be returned.|

**Example**

  ```js
  securityLabel.setSecurityLabel(path, "s0").then(function(){
      console.info("setSecurityLabel successfully");
  }).catch(function(error){
      console.info("setSecurityLabel failed with error:" + error);
  });
  ```

## securityLabel.setSecurityLabel

setSecurityLabel(path:string, type:dataLevel, callback: AsyncCallback&lt;void&gt;):void

Sets the security label for a file in asynchronous mode. This API uses a callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name   | Type                     | Mandatory| Description                                        |
| --------- | ------------------------- | ---- | -------------------------------------------- |
| path      | string                    | Yes  | File path.                                    |
| type      | dataLevel                 | Yes  | File security level, which can be **s0**, **s1**, **s2**, **s3**, or **s4**.|
| callback  | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.                  |

**Example**

  ```js
  securityLabel.setSecurityLabel(path, "s0", function(error){
      console.info("setSecurityLabel:" + JSON.stringify(error));
  });
  ```
## securityLabel.setSecurityLabelSync

setSecurityLabelSync(path:string, type:dataLevel):void

Sets the security label for a file in synchronous mode.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name   | Type  | Mandatory| Description                                        |
| --------- | ------ | ---- | -------------------------------------------- |
| path      | string | Yes  | File path.                                    |
| type      | dataLevel | Yes  | File security level, which can be **s0**, **s1**, **s2**, **s3**, or **s4**.|

**Example**

```js
securityLabel.setSecurityLabelSync(path, "s0");
```

## securityLabel.getSecurityLabel

getSecurityLabel(path:string):Promise&lt;string&gt;

Obtains the security label of a file in asynchronous mode. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name| Type  | Mandatory| Description    |
  | ------ | ------ | ---- | -------- |
  | path   | string | Yes  | File path.|

**Return value**

  | Type                 | Description        |
  | --------------------- | ------------ |
  | Promise&lt;string&gt; | Promise used to return the security label obtained.|

**Example**

  ```js
  securityLabel.getSecurityLabel(path).then(function(type){
      console.log("getSecurityLabel successfully:" + type);
  }).catch(function(err){
      console.log("getSecurityLabel failed with error:" + err);
  });
  ```

## securityLabel.getSecurityLabel

getSecurityLabel(path:string, callback:AsyncCallback&lt;string&gt;): void

Obtains the security label of a file in asynchronous mode. This API uses a callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

  | Name  | Type                       | Mandatory| Description                      |
  | -------- | --------------------------- | ---- | -------------------------- |
  | path     | string                      | Yes  | File path.                  |
  | callback | AsyncCallback&lt;string&gt; | Yes  | Callback used to return the security label obtained.|

**Example**

  ```js
  securityLabel.getSecurityLabel(path, function(err, type){
      console.log("getSecurityLabel successfully:" + type);
  });
  ```
## securityLabel.getSecurityLabelSync

getSecurityLabelSync(path:string):string

Obtains the security label of a file in synchronous mode.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name| Type  | Mandatory| Description    |
| ------ | ------ | ---- | -------- |
| path   | string | Yes  | File path.|

**Return value**

| Type  | Description        |
| ------ | ------------ |
| string | Security label obtained.|

**Example**

```js
let result = securityLabel.getSecurityLabelSync(path);
console.log("getSecurityLabel successfully:" + result);
```

# @ohos.file.securityLabel (数据标签)

该模块提供文件数据安全等级的相关功能：向应用程序提供查询、设置文件数据安全等级的JS接口。

> **说明：**
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> 本模块支持对错误码进行处理，错误码及其适配方式[参考文档](../errorcodes/errorcode-filemanagement.md#错误码适配指导)。

## 导入模块

```js
import securityLabel from '@ohos.file.securityLabel';
```

## 使用说明

使用该功能模块对文件/目录进行操作前，需要先获取其应用沙箱路径，获取方式及其接口用法请参考：

**Stage模型**

 ```js
import UIAbility from '@ohos.app.ability.UIAbility';

export default class EntryAbility extends UIAbility {
    onWindowStageCreate(windowStage) {
        let context = this.context;
        let pathDir = context.filesDir;
    }
}
 ```

**FA模型**

 ```js
 import featureAbility from '@ohos.ability.featureAbility';
 
 let context = featureAbility.getContext();
 context.getFilesDir().then((data) => {
      let pathDir = data;
 })
 ```

FA模型context的具体获取方法参见[FA模型](js-apis-inner-app-context.md#Context模块)。

## securityLabel.setSecurityLabel

setSecurityLabel(path:string, type:dataLevel):Promise&lt;void&gt;

以异步方法设置数据标签，以promise形式返回结果。

**系统能力**：SystemCapability.FileManagement.File.FileIO

**参数：**

| 参数名    | 类型       | 必填 | 说明                                         |
| --------- | ------    | ---- | -------------------------------------------- |
| path      | string    | 是   | 文件路径                                     |
| type      | dataLevel | 是   | 文件等级属性，只支持"s0","s1","s2","s3","s4" |

**返回值：**

  | 类型                | 说明             |
  | ------------------- | ---------------- |
  | Promise&lt;void&gt; | Promise实例，用于异步获取结果。本调用将返回空值。|

**示例：**

  ```js
  securityLabel.setSecurityLabel(path, "s0").then(function () {
      console.info("setSecurityLabel successfully");
  }).catch(function (err) {
      console.info("setSecurityLabel failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## securityLabel.setSecurityLabel

setSecurityLabel(path:string, type:dataLevel, callback: AsyncCallback&lt;void&gt;):void

以异步方法设置数据标签，以callback形式返回结果。

**系统能力**：SystemCapability.FileManagement.File.FileIO

**参数：**

| 参数名    | 类型                      | 必填 | 说明                                         |
| --------- | ------------------------- | ---- | -------------------------------------------- |
| path      | string                    | 是   | 文件路径                                     |
| type      | dataLevel                 | 是   | 文件等级属性，只支持"s0","s1","s2","s3","s4" |
| callback  | AsyncCallback&lt;void&gt; | 是   | 是否设置数据标签之后的回调                   |

**示例：**

  ```js
  securityLabel.setSecurityLabel(path, "s0", function (err) {
    if (err) {
      console.info("setSecurityLabel failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("setSecurityLabel successfully.");
    }
  });
  ```

## securityLabel.setSecurityLabelSync

setSecurityLabelSync(path:string, type:dataLevel):void

以同步方法设置数据标签。

**系统能力**：SystemCapability.FileManagement.File.FileIO

**参数：**

| 参数名    | 类型   | 必填 | 说明                                         |
| --------- | ------ | ---- | -------------------------------------------- |
| path      | string | 是   | 文件路径                                     |
| type      | dataLevel | 是   | 文件等级属性，只支持"s0","s1","s2","s3","s4" |

**示例：**

```js
securityLabel.setSecurityLabelSync(path, "s0");
```

## securityLabel.getSecurityLabel

getSecurityLabel(path:string):Promise&lt;string&gt;

异步方法获取数据标签，以promise形式返回结果。

**系统能力**：SystemCapability.FileManagement.File.FileIO

**参数：**

  | 参数名 | 类型   | 必填 | 说明     |
  | ------ | ------ | ---- | -------- |
  | path   | string | 是   | 文件路径 |

**返回值：**

  | 类型                  | 说明         |
  | --------------------- | ------------ |
  | Promise&lt;string&gt; | 返回数据标签 |

**示例：**

  ```js
  securityLabel.getSecurityLabel(path).then(function (type) {
      console.log("getSecurityLabel successfully, Label: " + type);
  }).catch(function (err) {
      console.log("getSecurityLabel failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## securityLabel.getSecurityLabel

getSecurityLabel(path:string, callback:AsyncCallback&lt;string&gt;): void

异步方法获取数据标签，以callback形式返回结果。

**系统能力**：SystemCapability.FileManagement.File.FileIO

**参数：**

  | 参数名   | 类型                        | 必填 | 说明                       |
  | -------- | --------------------------- | ---- | -------------------------- |
  | path     | string                      | 是   | 文件路径                   |
  | callback | AsyncCallback&lt;string&gt; | 是   | 异步获取数据标签之后的回调 |

**示例：**

  ```js
  securityLabel.getSecurityLabel(path, function (err, type) {
    if (err) {
      console.log("getSecurityLabel failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.log("getSecurityLabel successfully, Label: " + type);
    }
  });
  ```
## securityLabel.getSecurityLabelSync

getSecurityLabelSync(path:string):string

以同步方法获取数据标签。

**系统能力**：SystemCapability.FileManagement.File.FileIO

**参数：**

| 参数名 | 类型   | 必填 | 说明     |
| ------ | ------ | ---- | -------- |
| path   | string | 是   | 文件路径 |

**返回值：**

| 类型   | 说明         |
| ------ | ------------ |
| string | 返回数据标签 |

**示例：**

```js
let type = securityLabel.getSecurityLabelSync(path);
console.log("getSecurityLabel successfully, Label: " + type);
```

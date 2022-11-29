# Bundle模块(JS端SDK接口)

本模块提供应用信息查询能力，支持BundleInfo、ApplicationInfo、Ability、ExtensionAbility、应用状态等信息的查询

> **说明：**
>
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
## 导入模块

```js
import bundle from '@ohos.bundle';
```

## 权限列表

| 权限                                       | 权限等级     | 描述               |
| ------------------------------------------ | ------------ | ------------------ |
| ohos.permission.GET_BUNDLE_INFO            | normal       | 查询指定应用信息   |
| ohos.permission.GET_BUNDLE_INFO_PRIVILEGED | system_basic | 可查询所有应用信息 |
| ohos.permission.INSTALL_BUNDLE             | system_core  | 可安装、卸载应用   |
| ohos.permission.MANAGE_DISPOSED_APP_STATUS | system_core  | 可设置和查询应用的处置状态   |

权限等级参考[权限等级说明](../../security/accesstoken-overview.md#权限等级说明)。

## bundle.getApplicationInfo<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getApplicationInfo](js-apis-bundleManager.md#bundlemanagergetapplicationinfo)替代。

getApplicationInfo(bundleName: string, bundleFlags: number, userId?: number): Promise\<ApplicationInfo>

以异步方法根据给定的包名获取ApplicationInfo，使用Promise形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED 或 ohos.permission.GET_BUNDLE_INFO

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名      | 类型   | 必填 | 说明                                                         |
| ----------- | ------ | ---- | ------------------------------------------------------------ |
| bundleName  | string | 是   | 要查询的应用程序包名称。                                     |
| bundleFlags | number | 是   | 用于指定返回的应用信息对象中包含信息的标记。默认值：0，取值范围：参考[BundleFlag说明](#bundleflag)中应用信息相关flag |
| userId      | number | 否   | 用户ID。默认值：调用方所在用户，取值范围：大于等于0。        |

**返回值：**

| 类型                        | 说明                 |
| ------------------------- | ------------------ |
| Promise\<[ApplicationInfo](js-apis-bundle-ApplicationInfo.md)> | Promise形式返回应用程序信息。 |

**示例：**

```js
let bundleName = "com.example.myapplication";
let bundleFlags = 0;
let userId = 100;
bundle.getApplicationInfo(bundleName, bundleFlags, userId)
.then((data) => {
    console.info('Operation successful. Data: ' + JSON.stringify(data));
}).catch((error) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
})
```

## bundle.getApplicationInfo<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getApplicationInfo](js-apis-bundleManager.md#bundlemanagergetapplicationinfo)替代。

getApplicationInfo(bundleName: string, bundleFlags: number, userId: number, callback: AsyncCallback\<ApplicationInfo>): void

以异步方法根据给定的包名获取指定用户下的ApplicationInfo，使用callback形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED 或 ohos.permission.GET_BUNDLE_INFO

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名      | 类型                                                         | 必填 | 说明                                                         |
| ----------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| bundleName  | string                                                       | 是   | 要查询的应用程序包名称。                                     |
| bundleFlags | number                                                       | 是   | 用于指定返回的应用信息对象中包含信息的标记。默认值：0，取值范围：参考[BundleFlag说明](#bundleflag)中应用信息相关flag |
| userId      | number                                                       | 是   | 用户ID。默认值：调用方所在用户，取值范围：大于等于0。        |
| callback    | AsyncCallback\<[ApplicationInfo](js-apis-bundle-ApplicationInfo.md)> | 是   | 程序启动作为入参的回调函数，返回应用程序信息。               |

**示例：**

```js
let bundleName = "com.example.myapplication";
let bundleFlags = 0;
let userId = 100;
bundle.getApplicationInfo(bundleName, bundleFlags, userId, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. Data:' + JSON.stringify(data));
 })
```

## bundle.getApplicationInfo<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getApplicationInfo](js-apis-bundleManager.md#bundlemanagergetapplicationinfo)替代。


getApplicationInfo(bundleName: string, bundleFlags: number, callback: AsyncCallback\<ApplicationInfo>): void

以异步方法根据给定的包名获取ApplicationInfo，使用callback形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED 或 ohos.permission.GET_BUNDLE_INFO

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名      | 类型                                                         | 必填 | 说明                                                         |
| ----------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| bundleName  | string                                                       | 是   | 要查询的应用程序包名称。                                     |
| bundleFlags | number                                                       | 是   | 用于指定返回的应用信息对象中包含信息的标记。默认值：0，取值范围：参考[BundleFlag说明](#bundleflag)中应用信息相关flag |
| callback    | AsyncCallback\<[ApplicationInfo](js-apis-bundle-ApplicationInfo.md)> | 是   | 程序启动作为入参的回调函数，返回应用程序信息。               |

**示例：**

```js
let bundleName = "com.example.myapplication";
let bundleFlags = 0;
bundle.getApplicationInfo(bundleName, bundleFlags, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. Data:' + JSON.stringify(data));
 })
```


## bundle.getAllBundleInfo<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getAllBundleInfo](js-apis-bundleManager.md#bundlemanagergetallbundleinfo)替代。

getAllBundleInfo(bundleFlag: BundleFlag, userId?: number): Promise<Array\<BundleInfo>>

以异步方法获取系统中所有可用的BundleInfo，使用Promise形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名     | 类型       | 必填 | 说明                                                         |
| ---------- | ---------- | ---- | ------------------------------------------------------------ |
| bundleFlag | BundleFlag | 是   | 用于指定返回的应用信息对象中包含信息的标记。默认值：0，取值范围：参考[BundleFlag说明](#bundleflag)中包信息相关flag |
| userId     | number     | 否   | 用户ID。默认值：调用方所在用户，取值范围：大于等于0。        |

**返回值：**

| 类型                          | 说明                         |
| --------------------------- | -------------------------- |
| Promise<Array\<[BundleInfo](js-apis-bundle-BundleInfo.md)>> | Promise形式返回所有可用的BundleInfo |

**示例：**

```js
let bundleFlag = 0;
let userId = 100;
bundle.getAllBundleInfo(bundleFlag, userId)
.then((data) => {
    console.info('Operation successful. Data: ' + JSON.stringify(data));
}).catch((error) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
})
```

## bundle.getAllBundleInfo<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getAllBundleInfo](js-apis-bundleManager.md#bundlemanagergetallbundleinfo)替代。


getAllBundleInfo(bundleFlag: BundleFlag, callback: AsyncCallback<Array\<BundleInfo>>): void

以异步方法获取系统中所有可用的BundleInfo，使用callback形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名     | 类型                                                         | 必填 | 说明                                                         |
| ---------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| bundleFlag | BundleFlag                                                   | 是   | 用于指定返回的应用信息对象中包含信息的标记。默认值：0，取值范围：参考[BundleFlag说明](#bundleflag)中包信息相关flag |
| callback   | AsyncCallback<Array\<[BundleInfo](js-apis-bundle-BundleInfo.md)>> | 是   | 程序启动作为入参的回调函数，返回所有可用的BundleInfo。       |

**示例：**

```js
let bundleFlag = 0;
bundle.getAllBundleInfo(bundleFlag, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. Data:' + JSON.stringify(data));
 })
```

## bundle.getAllBundleInfo<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getAllBundleInfo](js-apis-bundleManager.md#bundlemanagergetallbundleinfo)替代。


getAllBundleInfo(bundleFlag: BundleFlag, userId: number, callback: AsyncCallback<Array\<BundleInfo>>): void

以异步方法获取系统中指定用户下所有可用的BundleInfo，使用callback形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名     | 类型                                                         | 必填 | 说明                                                         |
| ---------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| bundleFlag | BundleFlag                                                   | 是   | 用于指定返回的应用信息对象中包含信息的标记。默认值：0，取值范围：参考[BundleFlag说明](#bundleflag)中包信息相关flag |
| userId     | number                                                       | 是   | 用户ID。默认值：调用方所在用户，取值范围：大于等于0。        |
| callback   | AsyncCallback<Array\<[BundleInfo](js-apis-bundle-BundleInfo.md)>> | 是   | 程序启动作为入参的回调函数，返回所有可用的BundleInfo。       |

**示例：**

```js
let bundleFlag = 0;
let userId = 100;
bundle.getAllBundleInfo(bundleFlag, userId, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. Data:' + JSON.stringify(data));
 })
```

## bundle.getBundleInfo<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getBundleInfo](js-apis-bundleManager.md#bundlemanagergetbundleinfo)替代。


getBundleInfo(bundleName: string, bundleFlags: number, options?: BundleOptions): Promise\<BundleInfo>

以异步方法根据给定的包名获取BundleInfo，使用Promise形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED 或 ohos.permission.GET_BUNDLE_INFO

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名         | 类型            | 必填   | 说明                                      |
| ----------- | ------------- | ---- | --------------------------------------- |
| bundleName  | string        | 是    | 包名                                      |
| bundleFlags | number        | 是    | 用于指定返回的应用信息对象中包含信息的标记。默认值：0，取值范围：参考[BundleFlag说明](#bundleflag)中包信息相关flag |
| options     | [BundleOptions](#bundleoptions) | 否    | 包含userid。                               |

**返回值：**

| 类型                   | 说明                           |
| -------------------- | ---------------------------- |
| Promise\<[BundleInfo](js-apis-bundle-BundleInfo.md)> | 返回值为Promise对象，Promise中包含包信息。 |

**示例：**

```js
let bundleName = "com.example.myapplication";
let bundleFlags = 1;
let options = {
  "userId" : 100
};
bundle.getBundleInfo(bundleName, bundleFlags, options)
.then((data) => {
    console.info('Operation successful. Data: ' + JSON.stringify(data));
}).catch((error) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
})
```

## bundle.getBundleInfo<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getBundleInfo](js-apis-bundleManager.md#bundlemanagergetbundleinfo)替代。

getBundleInfo(bundleName: string, bundleFlags: number, callback: AsyncCallback\<BundleInfo>): void

以异步方法根据给定的包名获取BundleInfo，使用callback形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED 或 ohos.permission.GET_BUNDLE_INFO

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名      | 类型                                                       | 必填 | 说明                                                         |
| ----------- | ---------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| bundleName  | string                                                     | 是   | 包名                                                         |
| bundleFlags | number                                                     | 是   | 用于指定返回的应用信息对象中包含信息的标记。默认值：0，取值范围：参考[BundleFlag说明](#bundleflag)中包信息相关flag |
| callback    | AsyncCallback\<[BundleInfo](js-apis-bundle-BundleInfo.md)> | 是   | 程序启动作为入参的回调函数，返回包信息。                     |

**示例：**

```js
let bundleName = "com.example.myapplication";
let bundleFlags = 1;
bundle.getBundleInfo(bundleName, bundleFlags, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. Data:' + JSON.stringify(data));
})
```


## bundle.getBundleInfo<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getBundleInfo](js-apis-bundleManager.md#bundlemanagergetbundleinfo)替代。

getBundleInfo(bundleName: string, bundleFlags: number, options: BundleOptions, callback: AsyncCallback\<BundleInfo>): void

以异步方法根据给定的包名获取BundleInfo，使用callback形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED 或 ohos.permission.GET_BUNDLE_INFO

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名      | 类型                                                       | 必填 | 说明                                                         |
| ----------- | ---------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| bundleName  | string                                                     | 是   | 包名                                                         |
| bundleFlags | number                                                     | 是   | 用于指定返回的应用信息对象中包含信息的标记。默认值：0，取值范围：参考[BundleFlag说明](#bundleflag)中包信息相关flag |
| options     | [BundleOptions](#bundleoptions)                            | 是   | 包含userid。                                                 |
| callback    | AsyncCallback\<[BundleInfo](js-apis-bundle-BundleInfo.md)> | 是   | 程序启动作为入参的回调函数，返回包信息。                     |

**示例：**

```js
let bundleName = "com.example.myapplication";
let bundleFlags = 1;
let options = {
  "userId" : 100
};
bundle.getBundleInfo(bundleName, bundleFlags, options, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. Data:' + JSON.stringify(data));
})
```



## bundle.getBundleInstaller<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[installer.getBundleInstaller](js-apis-installer.md#bundleinstallergetbundleinstaller)替代。

getBundleInstaller(): Promise&lt;BundleInstaller&gt;;

获取用于安装包的接口

**需要权限：**

ohos.permission.INSTALL_BUNDLE

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**系统API：**

此接口为系统接口，三方应用不支持调用

**返回值：**

| 类型                                                         | 说明                                         |
| ------------------------------------------------------------ | -------------------------------------------- |
| Promise<[BundleInstaller](js-apis-bundle-BundleInstaller.md)> | 返回值为Promise对象，Promise中包含安装信息。 |

## bundle.getBundleInstaller<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[installer.getBundleInstaller](js-apis-installer.md#bundleinstallergetbundleinstaller)替代。

getBundleInstaller(callback: AsyncCallback&lt;BundleInstaller&gt;): void;

获取用于安装包的接口

**需要权限：**

ohos.permission.INSTALL_BUNDLE

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**系统API：**

此接口为系统接口，三方应用不支持调用

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明             |
| -------- | ------------------------------------------------------------ | ---- | ---------------- |
| callback | AsyncCallback<[BundleInstaller](js-apis-bundle-BundleInstaller.md)> | 是   | 安装应用程序包。 |

## bundle.cleanBundleCacheFiles<sup>8+</sup> <sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.cleanBundleCacheFiles](js-apis-bundleManager.md#bundlemanagercleanbundlecachefiles)替代。

cleanBundleCacheFiles(bundleName: string, callback: AsyncCallback&lt;void&gt;): void;

清除指定应用程序的缓存数据

**需要权限：**

ohos.permission.REMOVE_CACHE_FILES

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**系统API：**

此接口为系统接口，三方应用不支持调用

**参数：**

| 参数名      | 类型                | 必填 | 说明                                  |
| ---------- | ------------------- | ---- | ------------------------------------- |
| bundleName | string              | 是   | 指示要清除其缓存数据的应用程序包名称. |
| callback   | AsyncCallback\<void> | 是   | 为返回操作结果而调用的回调。          |

## bundle.cleanBundleCacheFiles<sup>8+</sup> <sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.cleanBundleCacheFiles](js-apis-bundleManager.md#bundlemanagercleanbundlecachefiles)替代。

cleanBundleCacheFiles(bundleName: string): Promise&lt;void&gt;

清除指定应用程序的缓存数据

**需要权限：**

ohos.permission.REMOVE_CACHE_FILES

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**系统API：**

此接口为系统接口，三方应用不支持调用

**参数：**

| 参数名     | 类型   | 必填 | 说明                                  |
| ---------- | ------ | ---- | ------------------------------------- |
| bundleName | string | 是   | 指示要清除其缓存数据的应用程序包名称. |

**返回值：**

| 类型          | 说明                                 |
| ------------- | ------------------------------------ |
| Promise\<void> | 返回值为Promise对象，Promise中为空。 |

## bundle.setApplicationEnabled<sup>8+</sup> <sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.setApplicationEnabled](js-apis-bundleManager.md#bundlemanagersetapplicationenabled)替代。

setApplicationEnabled(bundleName: string, isEnable: boolean, callback: AsyncCallback&lt;void&gt;): void;

设置是否启用指定的应用程序

**需要权限：**

ohos.permission.CHANGE_ABILITY_ENABLED_STATE

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**系统API：**

此接口为系统接口，三方应用不支持调用

**参数：**

| 参数名      | 类型                | 必填 | 说明                                            |
| ---------- | ------------------- | ---- | ----------------------------------------------- |
| bundleName | string              | 是   | 应用程序包名称。                                |
| isEnable   | boolean             | 是   | 指定是否启用应用程序。true表示启用，false禁用。 |
| callback   | AsyncCallback\<void> | 是   | 为返回操作结果而调用的回调。                    |

## bundle.setApplicationEnabled<sup>8+</sup> <sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.setApplicationEnabled](js-apis-bundleManager.md#bundlemanagersetapplicationenabled)替代。

setApplicationEnabled(bundleName: string, isEnable: boolean): Promise&lt;void&gt;

设置是否启用指定的应用程序

**需要权限：**

ohos.permission.CHANGE_ABILITY_ENABLED_STATE

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**系统API：**

此接口为系统接口，三方应用不支持调用

**参数：**

| 参数名     | 类型    | 必填 | 说明                                            |
| ---------- | ------- | ---- | ----------------------------------------------- |
| bundleName | string  | 是   | 应用程序包名称。                                |
| isEnable   | boolean | 是   | 指定是否启用应用程序。true表示启用，false禁用。 |

**返回值：**

| 类型          | 说明                                 |
| ------------- | ------------------------------------ |
| Promise\<void> | 返回值为Promise对象，Promise中为空。 |

## bundle.setAbilityEnabled<sup>8+</sup> <sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.setAbilityEnabled](js-apis-bundleManager.md#bundlemanagersetabilityenabled)替代。

setAbilityEnabled(info: AbilityInfo, isEnable: boolean, callback: AsyncCallback&lt;void&gt;): void;

设置是否启用指定的功能

**需要权限：**

ohos.permission.CHANGE_ABILITY_ENABLED_STATE

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**系统API：**

此接口为系统接口，三方应用不支持调用

**参数：**

| 参数名   | 类型                                         | 必填 | 说明                                            |
| -------- | -------------------------------------------- | ---- | ----------------------------------------------- |
| info     | [AbilityInfo](js-apis-bundle-AbilityInfo.md) | 是   | Ability信息。                                   |
| isEnable | boolean                                      | 是   | 指定是否启用应用程序。true表示启用，false禁用。 |
| callback | AsyncCallback\<void>                         | 是   | 为返回操作结果而调用的回调。                    |

## bundle.setAbilityEnabled<sup>8+</sup> <sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.setAbilityEnabled](js-apis-bundleManager.md#bundlemanagersetabilityenabled)替代。

setAbilityEnabled(info: AbilityInfo, isEnable: boolean): Promise&lt;void&gt;

设置是否启用指定的功能

**需要权限：**

ohos.permission.CHANGE_ABILITY_ENABLED_STATE

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**系统API：**

此接口为系统接口，三方应用不支持调用

**参数：**

| 参数名   | 类型                                         | 必填 | 说明                                            |
| -------- | -------------------------------------------- | ---- | ----------------------------------------------- |
| info     | [AbilityInfo](js-apis-bundle-AbilityInfo.md) | 是   | Ability信息。                                   |
| isEnable | boolean                                      | 是   | 指定是否启用应用程序。true表示启用，false禁用。 |

**返回值：**

| 类型          | 说明                                 |
| ------------- | ------------------------------------ |
| Promise\<void> | 返回值为Promise对象，Promise中为空。 |

## bundle.getPermissionDef<sup>8+</sup> <sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getPermissionDef](js-apis-bundleManager.md#bundlemanagergetpermissiondef)替代。

getPermissionDef(permissionName: string, callback: AsyncCallback&lt;PermissionDef&gt;): void;

按权限名称获取权限的详细信息

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**系统API：**

此接口为系统接口，三方应用不支持调用

**参数：**

| 参数名         | 类型                                                         | 必填 | 说明                                             |
| -------------- | ------------------------------------------------------------ | ---- | ------------------------------------------------ |
| permissionName | string                                                       | 是   | 指定权限的名称。                                 |
| callback       | AsyncCallback<[PermissionDef](js-apis-bundle-PermissionDef)> | 是   | 程序启动作为入参的回调函数，返回定义的权限信息。 |

## bundle.getPermissionDef<sup>8+</sup> <sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getPermissionDef](js-apis-bundleManager.md#bundlemanagergetpermissiondef)替代。

getPermissionDef(permissionName: string): Promise&lt;PermissionDef&gt;

按权限名称获取权限的详细信息

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**系统API：**

此接口为系统接口，三方应用不支持调用

**参数：**

| 参数名         | 类型   | 必填 | 说明             |
| -------------- | ------ | ---- | ---------------- |
| permissionName | string | 是   | 指定权限的名称。 |

**返回值：**

| 类型                                                   | 说明                                                   |
| ------------------------------------------------------ | ------------------------------------------------------ |
| Promise<[PermissionDef](js-apis-bundle-PermissionDef)> | 返回值为Promise对象，Promise中包含定义的权限信息对象。 |


## bundle.getAllApplicationInfo<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getAllApplicationInfo](js-apis-bundleManager.md#bundlemanagergetallapplicationinfo)替代。

getAllApplicationInfo(bundleFlags: number, userId?: number): Promise<Array\<ApplicationInfo>>

获取指定用户下所有已安装的应用信息，通过Promise获取返回值。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名      | 类型   | 必填 | 说明                                                         |
| ----------- | ------ | ---- | ------------------------------------------------------------ |
| bundleFlags | number | 是   | 用于指定返回的应用信息对象中包含信息的标记。默认值：0，取值范围：参考[BundleFlag说明](#bundleflag)中应用信息相关flag |
| userId      | number | 否   | 用户ID。默认值：调用方所在用户，取值范围：大于等于0。        |

**返回值：**

| 类型                               | 说明                              |
| -------------------------------- | ------------------------------- |
| Promise<Array\<[ApplicationInfo](js-apis-bundle-ApplicationInfo.md)>> | 返回值为Promise对象，Promise中包含应用信息列表。 |

**示例：**

```js
let bundleFlags = 8;
let userId = 100;
bundle.getAllApplicationInfo(bundleFlags, userId)
.then((data) => {
    console.info('Operation successful. Data: ' + JSON.stringify(data));
}).catch((error) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
})
```

## bundle.getAllApplicationInfo<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getAllApplicationInfo](js-apis-bundleManager.md#bundlemanagergetallapplicationinfo)替代。

getAllApplicationInfo(bundleFlags: number, userId: number, callback: AsyncCallback<Array\<ApplicationInfo>>): void

获取指定用户下所有已安装的应用信息，使用callback形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名      | 类型                                                         | 必填 | 说明                                                         |
| ----------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| bundleFlags | number                                                       | 是   | 用于指定返回的应用信息对象中包含信息的标记。默认值：0，取值范围：参考[BundleFlag说明](#bundleflag)中应用信息相关flag |
| userId      | number                                                       | 是   | 用户ID。默认值：调用方所在用户，取值范围：大于等于0。        |
| callback    | AsyncCallback<Array\<[ApplicationInfo](js-apis-bundle-ApplicationInfo.md)>> | 是   | 程序启动作为入参的回调函数，返回应用信息列表。               |

**示例：**

```js
let bundleFlags = 8;
let userId = 100;
bundle.getAllApplicationInfo(bundleFlags, userId, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. Data:' + JSON.stringify(data));
})
```


## bundle.getAllApplicationInfo<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getAllApplicationInfo](js-apis-bundleManager.md#bundlemanagergetallapplicationinfo)替代。

getAllApplicationInfo(bundleFlags: number, callback: AsyncCallback<Array\<ApplicationInfo>>) : void;

获取所有已安装的应用信息，使用callback形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名      | 类型                                                         | 必填 | 说明                                                         |
| ----------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| bundleFlags | number                                                       | 是   | 用于指定返回的应用信息对象中包含信息的标记。默认值：0，取值范围：参考[BundleFlag说明](#bundleflag)中应用信息相关flag |
| callback    | AsyncCallback<Array\<[ApplicationInfo](js-apis-bundle-ApplicationInfo.md)>> | 是   | 程序启动作为入参的回调函数，返回应用信息列表。               |

**示例：**

```js
let bundleFlags = 8;
bundle.getAllApplicationInfo(bundleFlags, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. Data:' + JSON.stringify(data));
})
```

## bundle.getBundleArchiveInfo<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getBundleArchiveInfo](js-apis-bundleManager.md#bundlemanagergetbundlearchiveinfo)替代。

getBundleArchiveInfo(hapFilePath: string, bundleFlags: number) : Promise\<BundleInfo>

以异步方法获取有关HAP包中包含的应用程序包的信息，使用Promise形式返回结果。

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名        | 类型     | 必填   | 说明           |
| ---------- | ------ | ---- | ------------ |
| hapFilePath | string | 是    | HAP存放路径。路径应指向当前应用程序的数据目录的相对目录。 |
| bundleFlags | number | 是    | 用于指定要返回的BundleInfo对象中包含信息的标记。默认值：0，取值范围：参考[BundleFlag说明](#bundleflag)中包信息相关flag |

**返回值：**
| 类型             | 说明                                     |
| -------------- | -------------------------------------- |
| Promise\<[BundleInfo](js-apis-bundle-BundleInfo.md)> | 返回值为Promise对象，Promise中包含有关hap包中包含的应用程序的信息。 |

**示例：**

```js
let hapFilePath = "/data/xxx/test.hap";
let bundleFlags = 0;
bundle.getBundleArchiveInfo(hapFilePath, bundleFlags)
.then((data) => {
    console.info('Operation successful. Data: ' + JSON.stringify(data));
}).catch((error) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
})
```

## bundle.getBundleArchiveInfo<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getBundleArchiveInfo](js-apis-bundleManager.md#bundlemanagergetbundlearchiveinfo)替代。

getBundleArchiveInfo(hapFilePath: string, bundleFlags: number, callback: AsyncCallback\<BundleInfo>) : void

以异步方法获取有关HAP包中包含的应用程序包的信息，使用callback形式返回结果。

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名        | 类型     | 必填   | 说明           |
| ---------- | ------ | ---- | ------------ |
| hapFilePath | string | 是    | HAP存放路径。路径应指向当前应用程序的数据目录的相对目录。 |
| bundleFlags | number | 是    | 用于指定要返回的BundleInfo对象中包含信息的标记。默认值：0，取值范围：参考[BundleFlag说明](#bundleflag)中包信息相关flag |
| callback| AsyncCallback\<[BundleInfo](js-apis-bundle-BundleInfo.md)> | 是    | 程序启动作为入参的回调函数，返回HAP包中包含的应用程序包的信息。|

**示例：**

```js
let hapFilePath = "/data/xxx/test.hap";
let bundleFlags = 0;
bundle.getBundleArchiveInfo(hapFilePath, bundleFlags, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. Data:' + JSON.stringify(data));
})
```


## bundle.getAbilityInfo<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.queryAbilityInfo](js-apis-bundleManager.md#bundlemanagerqueryabilityinfo)替代。

getAbilityInfo(bundleName: string, abilityName: string): Promise\<AbilityInfo>

通过包名称和abilityName获取Ability信息，使用Promise形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED 或 ohos.permission.GET_BUNDLE_INFO

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名         | 类型     | 必填   | 说明               |
| ----------- | ------ | ---- | ---------------- |
| bundleName  | string | 是    | 应用程序包名。     |
| abilityName | string | 是    | Ability名称。 |

**返回值：**

| 类型                    | 说明                    |
| --------------------- | --------------------- |
| Promise\<[AbilityInfo](js-apis-bundle-AbilityInfo.md)> | Promise形式返回Ability信息。 |

**示例：**

```js
let bundleName = "com.example.myapplication";
let abilityName = "com.example.myapplication.MainAbility";
bundle.getAbilityInfo(bundleName, abilityName)
.then((data) => {
    console.info('Operation successful. Data: ' + JSON.stringify(data));
}).catch((error) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
})
```

## bundle.getAbilityInfo<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.queryAbilityInfo](js-apis-bundleManager.md#bundlemanagerqueryabilityinfo)替代。

getAbilityInfo(bundleName: string, abilityName: string, callback: AsyncCallback\<AbilityInfo>): void;

通过包名称和abilityName获取Ability信息，使用callback形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED 或 ohos.permission.GET_BUNDLE_INFO

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名        | 类型     | 必填   | 说明            |
| ----------- | ------------ | ---- | ---------------- |
| bundleName  | string | 是    | 应用程序包名。     |
| abilityName | string | 是    | Ability名称。 |
| callback    | AsyncCallback\<[AbilityInfo](js-apis-bundle-AbilityInfo.md)> | 是    | 程序启动作为入参的回调函数，返回Ability信息。 |

**示例：**

```js
let bundleName = "com.example.myapplication";
let abilityName = "com.example.myapplication.MainAbility";
bundle.getAbilityInfo(bundleName, abilityName, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. Data:' + JSON.stringify(data));
})
```

## bundle.getAbilityLabel<sup>8+</sup> <sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getAbilityLabel](js-apis-bundleManager.md#bundlemanagergetabilitylabel)替代。

getAbilityLabel(bundleName: string, abilityName: string): Promise\<string>

通过包名称和abilityName获取应用名称，使用Promise形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED 或 ohos.permission.GET_BUNDLE_INFO

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名         | 类型     | 必填   | 说明               |
| ----------- | ------ | ---- | ---------------- |
| bundleName  | string | 是    | 应用程序包名。     |
| abilityName | string | 是    | Ability名称。 |

**返回值：**

| 类型               | 说明                 |
| ---------------- | ------------------ |
| Promise\<string> | Promise形式返回应用名称信息。 |

**示例：**

```js
let bundleName = "com.example.myapplication";
let abilityName = "com.example.myapplication.MainAbility";
bundle.getAbilityLabel(bundleName, abilityName)
.then((data) => {
    console.info('Operation successful. Data: ' + JSON.stringify(data));
}).catch((error) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
})
```

## bundle.getAbilityLabel<sup>8+</sup> <sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getAbilityLabel](js-apis-bundleManager.md#bundlemanagergetabilitylabel)替代。

getAbilityLabel(bundleName: string, abilityName: string, callback : AsyncCallback\<string>): void

通过包名称和abilityName获取应用名称，使用callback形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED 或 ohos.permission.GET_BUNDLE_INFO

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名         | 类型                     | 必填   | 说明               |
| ----------- | ---------------------- | ---- | ---------------- |
| bundleName  | string                 | 是    | 应用程序包名。     |
| abilityName | string                 | 是    | Ability名称。 |
| callback    | AsyncCallback\<string> | 是    | 程序启动作为入参的回调函数，返回应用名称信息。        |

**示例：**

```js
let bundleName = "com.example.myapplication";
let abilityName = "com.example.myapplication.MainAbility";
bundle.getAbilityLabel(bundleName, abilityName, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. Data:' + JSON.stringify(data));
})
```

## bundle.isAbilityEnabled<sup>8+</sup> <sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.isAbilityEnabled](js-apis-bundleManager.md#bundlemanagerisabilityenabled)替代。

isAbilityEnabled(info: AbilityInfo): Promise\<boolean>

以异步方法根据给定的AbilityInfo查询ability是否已经启用，使用Promise形式返回结果。

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名 | 类型                                         | 必填 | 说明              |
| ------ | -------------------------------------------- | ---- | ----------------- |
| info   | [AbilityInfo](js-apis-bundle-AbilityInfo.md) | 是   | Ability的配置信息 |

**返回值：**

| 类型                | 说明                        |
| ----------------- | ------------------------- |
| Promise\<boolean> | Promise形式返回boolean代表是否启用。 |

**示例：**

```js
let bundleName = "com.example.myapplication";
let abilityName = "com.example.myapplication.MainAbility";
bundle.getAbilityInfo(bundleName, abilityName).then((abilityInfo)=>{
    bundle.isAbilityEnabled(abilityInfo).then((data) => {
        console.info('Operation successful. Data: ' + JSON.stringify(data));
    }).catch((error) => {
        console.error('Operation failed. Cause: ' + JSON.stringify(error));
    })
})
```

## bundle.isAbilityEnabled<sup>8+</sup> <sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.isAbilityEnabled](js-apis-bundleManager.md#bundlemanagerisabilityenabled)替代。

isAbilityEnabled(info : AbilityInfo, callback : AsyncCallback\<boolean>): void

以异步方法根据给定的AbilityInfo查询ability是否已经启用，使用callback形式返回结果。

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名   | 类型                                         | 必填 | 说明                    |
| -------- | -------------------------------------------- | ---- | ----------------------- |
| info     | [AbilityInfo](js-apis-bundle-AbilityInfo.md) | 是   | Ability的配置信息       |
| callback | AsyncCallback\<boolean>                      | 是   | 返回boolean代表是否启用 |

**示例：**

```js
let bundleName = "com.example.myapplication";
let abilityName = "com.example.myapplication.MainAbility";
bundle.getAbilityInfo(bundleName, abilityName).then((abilityInfo)=>{
    bundle.isAbilityEnabled(abilityInfo, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. Data:' + JSON.stringify(data));
    })
})
```

## bundle.isApplicationEnabled<sup>8+</sup> <sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.isApplicationEnabled](js-apis-bundleManager.md#bundlemanagerisapplicationenabled)替代。

isApplicationEnabled(bundleName: string): Promise\<boolean>

以异步方法根据给定的bundleName查询指定应用程序是否已经启用，使用Promise形式返回结果。

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名     | 类型   | 必填 | 说明                     |
| ---------- | ------ | ---- | ------------------------ |
| bundleName | string | 是   | 要查询的应用程序包名称。 |

**返回值：**

| 类型                | 说明                        |
| ----------------- | ------------------------- |
| Promise\<boolean> | Promise形式返回boolean代表是否启用。 |

**示例：**

```js
let bundleName = "com.example.myapplication";
bundle.isApplicationEnabled(bundleName)
.then((data) => {
    console.info('Operation successful. Data: ' + JSON.stringify(data));
}).catch((error) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
})
```

## bundle.isApplicationEnabled<sup>8+</sup> <sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.isApplicationEnabled](js-apis-bundleManager.md#bundlemanagerisapplicationenabled)替代。

isApplicationEnabled(bundleName: string, callback : AsyncCallback\<boolean>): void

以异步方法根据给定的bundleName查询指定应用程序是否已经启用，使用callback形式返回结果。

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名     | 类型                    | 必填 | 说明                     |
| ---------- | ----------------------- | ---- | ------------------------ |
| bundleName | string                  | 是   | 要查询的应用程序包名称。 |
| callback   | AsyncCallback\<boolean> | 是   | 返回boolean代表是否启用  |

**示例：**

```js
let bundleName = "com.example.myapplication";
bundle.isApplicationEnabled(bundleName, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. Data:' + JSON.stringify(data));
})
```

## bundle.queryAbilityByWant<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.queryAbilityInfo](js-apis-bundleManager.md#bundlemanagerqueryabilityinfo)替代。

queryAbilityByWant(want: Want, bundleFlags: number, userId?: number): Promise<Array\<AbilityInfo>>

以异步方法根据给定的意图获取Ability信息，使用Promise形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED 或 ohos.permission.GET_BUNDLE_INFO

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名         | 类型     | 必填   | 说明                                    |
| ----------- | ------ | ---- | ------------------------------------- |
| want        | [Want](js-apis-application-Want.md)   | 是    | 包含要查询的应用程序包名称的意图。                     |
| bundleFlags | number | 是    | 用于指定返回abilityInfo信息。默认值：0，取值范围：参考[BundleFlag说明](#bundleflag)中Ability信息相关flag |
| userId      | number | 否    | 用户ID。默认值：调用方所在用户，取值范围：大于等于0           |

**返回值：**

| 类型                           | 说明                    |
| ---------------------------- | --------------------- |
| Promise<Array\<[AbilityInfo](js-apis-bundle-AbilityInfo.md)>> | Promise形式返回Ability信息。 |

**示例：**

```js
let bundleFlags = 0;
let userId = 100;
let want = {
    bundleName : "com.example.myapplication",
    abilityName : "com.example.myapplication.MainAbility"
};
bundle.queryAbilityByWant(want, bundleFlags, userId)
.then((data) => {
    console.info('Operation successful. Data: ' + JSON.stringify(data));
}).catch((error) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
})
```



## bundle.queryAbilityByWant<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.queryAbilityInfo](js-apis-bundleManager.md#bundlemanagerqueryabilityinfo)替代。

queryAbilityByWant(want: Want, bundleFlags: number, userId: number, callback: AsyncCallback<Array\<AbilityInfo>>): void

以异步方法根据给定的意图获取指定用户下Ability信息，使用callback形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED 或 ohos.permission.GET_BUNDLE_INFO

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名      | 类型                                                         | 必填 | 说明                                                         |
| ----------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| want        | [Want](js-apis-application-Want.md)                          | 是   | 指示包含要查询的应用程序包名称的意图。                       |
| bundleFlags | number                                                       | 是   | 用于指定返回abilityInfo信息。默认值：0，取值范围：参考[BundleFlag说明](#bundleflag)中Ability信息相关flag |
| userId      | number                                                       | 是   | 用户ID。默认值：调用方所在用户，取值范围：大于等于0          |
| callback    | AsyncCallback<Array\<[AbilityInfo](js-apis-bundle-AbilityInfo.md)>> | 是   | 程序启动作为入参的回调函数，返回Ability信息。                |

**示例：**

```js
let bundleFlags = 0;
let userId = 100;
let want = {
    bundleName : "com.example.myapplication",
    abilityName : "com.example.myapplication.MainAbility"
};
bundle.queryAbilityByWant(want, bundleFlags, userId, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. Data:' + JSON.stringify(data));
})
```

## bundle.queryAbilityByWant<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.queryAbilityInfo](js-apis-bundleManager.md#bundlemanagerqueryabilityinfo)替代。

queryAbilityByWant(want: Want, bundleFlags: number, callback: AsyncCallback<Array\<AbilityInfo>>): void;

以异步方法根据给定的意图获取Ability信息，使用callback形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED 或 ohos.permission.GET_BUNDLE_INFO

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名      | 类型                                                         | 必填 | 说明                                                         |
| ----------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| want        | [Want](js-apis-application-Want.md)                          | 是   | 指示包含要查询的应用程序包名称的意图。                       |
| bundleFlags | number                                                       | 是   | 用于指定返回abilityInfo信息。默认值：0，取值范围：参考[BundleFlag说明](#bundleflag)中Ability信息相关flag |
| callback    | AsyncCallback<Array\<[AbilityInfo](js-apis-bundle-AbilityInfo.md)>> | 是   | 程序启动作为入参的回调函数，返回Ability信息。                |

**示例：**

```js
let bundleFlags = 0;
let want = {
    bundleName : "com.example.myapplication",
    abilityName : "com.example.myapplication.MainAbility"
};
bundle.queryAbilityByWant(want, bundleFlags, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. Data:' + JSON.stringify(data));
})
```



## bundle.getLaunchWantForBundle<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getLaunchWantForBundle](js-apis-bundleManager.md#bundlemanagergetlaunchwantforbundle)替代。

getLaunchWantForBundle(bundleName: string): Promise\<Want>

以异步方法查询拉起指定应用的want对象，使用Promise形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名     | 类型   | 必填 | 说明                     |
| ---------- | ------ | ---- | ------------------------ |
| bundleName | string | 是   | 要查询的应用程序包名称。 |

**返回值：**
| 类型             | 说明                                     |
| -------------- | -------------------------------------- |
| Promise\<[Want](js-apis-application-Want.md)> | 返回值为Promise对象，Promise中包含拉起指定应用的Want对象。 |

**示例：**

```js
let bundleName = "com.example.myapplication";
bundle.getLaunchWantForBundle(bundleName)
.then((data) => {
    console.info('Operation successful. Data: ' + JSON.stringify(data));
}).catch((error) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
})
```

## bundle.getLaunchWantForBundle<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getLaunchWantForBundle](js-apis-bundleManager.md#bundlemanagergetlaunchwantforbundle)替代。

getLaunchWantForBundle(bundleName: string, callback: AsyncCallback\<Want>): void;

以异步方法查询拉起指定应用的want对象，使用callback形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名     | 类型                                                | 必填 | 说明                                                     |
| ---------- | --------------------------------------------------- | ---- | -------------------------------------------------------- |
| bundleName | string                                              | 是   | 要查询的应用程序包名称。                                 |
| callback   | AsyncCallback\<[Want](js-apis-application-Want.md)> | 是   | 程序启动作为入参的回调函数，返回拉起指定应用的want对象。 |

**示例：**

```js
let bundleName = "com.example.myapplication";
bundle.getLaunchWantForBundle(bundleName, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. Data:' + JSON.stringify(data));
})
```


## bundle.getNameForUid<sup>8+</sup> <sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getBundleNameByUid](js-apis-bundleManager.md#bundlemanagergetbundlenamebyuid)替代。

getNameForUid(uid: number): Promise\<string>

以异步方法通过uid获取对应的包名，使用Promise形式返回结果。

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名 | 类型   | 必填 | 说明          |
| ------ | ------ | ---- | ------------- |
| uid    | number | 是   | 要查询的uid。 |

**返回值：**
| 类型               | 说明                                |
| ---------------- | --------------------------------- |
| Promise\<string> | 返回值为Promise对象，Promise中包含指定uid的包名。 |

**示例：**

```js
let uid = 20010005;
bundle.getNameForUid(uid)
.then((data) => {
    console.info('Operation successful. Data: ' + JSON.stringify(data));
}).catch((error) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
})
```

## bundle.getNameForUid<sup>8+</sup> <sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getBundleNameByUid](js-apis-bundleManager.md#bundlemanagergetbundlenamebyuid)替代。

getNameForUid(uid: number, callback: AsyncCallback\<string>) : void

以异步方法通过uid获取对应的包名，使用callback形式返回结果。

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名   | 类型                   | 必填 | 说明                                            |
| -------- | ---------------------- | ---- | ----------------------------------------------- |
| uid      | number                 | 是   | 要查询的uid。                                   |
| callback | AsyncCallback\<string> | 是   | 程序启动作为入参的回调函数，返回指定uid的包名。 |

**示例：**

```js
let uid = 20010005;
bundle.getNameForUid(uid, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. Data:' + JSON.stringify(data));
})
```


## bundle.getAbilityIcon<sup>8+</sup> <sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getAbilityIcon](js-apis-bundleManager.md#bundlemanagergetabilityicon)替代。

getAbilityIcon(bundleName: string, abilityName: string): Promise\<image.PixelMap>;

以异步方法通过bundleName和abilityName获取对应Icon的[PixelMap](js-apis-image.md)，使用Promise形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED 或 ohos.permission.GET_BUNDLE_INFO

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名      | 类型   | 必填 | 说明                  |
| ----------- | ------ | ---- | --------------------- |
| bundleName  | string | 是   | 要查询的bundleName。  |
| abilityName | string | 是   | 要查询的abilityName。 |

**返回值：**
| 类型                  | 说明                                                         |
| --------------------- | ------------------------------------------------------------ |
| Promise\<image.PixelMap> | 返回值为[PixelMap](js-apis-image.md)。 |

**示例：**

```js
let bundleName = "com.example.myapplication";
let abilityName = "com.example.myapplication.MainAbility";
bundle.getAbilityIcon(bundleName, abilityName)
.then((data) => {
    console.info('Operation successful. Data: ' + JSON.stringify(data));
}).catch((error) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
})
```

## bundle.getAbilityIcon<sup>8+</sup> <sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.getAbilityIcon](js-apis-bundleManager.md#bundlemanagergetabilityicon)替代。

getAbilityIcon(bundleName: string, abilityName: string, callback: AsyncCallback\<image.PixelMap>): void;

以异步方法通过bundleName和abilityName获取对应Icon的[PixelMap](js-apis-image.md)，使用callback形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED 或 ohos.permission.GET_BUNDLE_INFO

**系统能力：**

SystemCapability.BundleManager.BundleFramework

**参数：**

| 参数名         | 类型                                       | 必填   | 说明                                       |
| ----------- | ---------------------------------------- | ---- | ---------------------------------------- |
| bundleName  | string                                   | 是    | 要查询的bundleName。                          |
| abilityName | string                                   | 是    | 要查询的abilityName。                         |
| callback   | AsyncCallback\<image.PixelMap> | 是   | 程序启动作为入参的回调函数，返回指定[PixelMap](js-apis-image.md)。 |

**示例：**

```js
let bundleName = "com.example.myapplication";
let abilityName = "com.example.myapplication.MainAbility";
bundle.getAbilityIcon(bundleName, abilityName, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. Data:' + JSON.stringify(data));
})
```

## InstallErrorCode<sup>deprecated<sup>
> 从API version 9开始不再维护，不推荐使用。

 **系统能力:** SystemCapability.BundleManager.BundleFramework

| 名称                                                 | 值   | 说明                                             |
| ---------------------------------------------------- | ---- | ------------------------------------------------ |
| SUCCESS                                              | 0    | 安装成功                                         |
| STATUS_INSTALL_FAILURE                               | 1    | 安装失败（不存在安装的应用）                     |
| STATUS_INSTALL_FAILURE_ABORTED                       | 2    | 安装中止                                         |
| STATUS_INSTALL_FAILURE_INVALID                       | 3    | 安装参数无效                                     |
| STATUS_INSTALL_FAILURE_CONFLICT                      | 4    | 安装冲突 （常见于升级和已有应用基本信息不一致）  |
| STATUS_INSTALL_FAILURE_STORAGE                       | 5    | 存储包信息失败                                   |
| STATUS_INSTALL_FAILURE_INCOMPATIBLE                  | 6    | 安装不兼容（常见于版本降级安装或者签名信息错误） |
| STATUS_UNINSTALL_FAILURE                             | 7    | 卸载失败 （不存在卸载的应用）                    |
| STATUS_UNINSTALL_FAILURE_BLOCKED                     | 8    | 卸载中止 （没有使用）                            |
| STATUS_UNINSTALL_FAILURE_ABORTED                     | 9    | 卸载中止 （参数无效导致）                        |
| STATUS_UNINSTALL_FAILURE_CONFLICT                    | 10   | 卸载冲突 （卸载系统应用失败， 结束应用进程失败） |
| STATUS_INSTALL_FAILURE_DOWNLOAD_TIMEOUT              | 0x0B | 安装失败 （下载超时）                            |
| STATUS_INSTALL_FAILURE_DOWNLOAD_FAILED               | 0x0C | 安装失败 （下载失败）                            |
| STATUS_RECOVER_FAILURE_INVALID<sup>8+</sup>          | 0x0D | 恢复预置应用失败                                 |
| STATUS_ABILITY_NOT_FOUND                             | 0x40 | Ability未找到                                    |
| STATUS_BMS_SERVICE_ERROR                             | 0x41 | BMS服务错误                                      |
| STATUS_FAILED_NO_SPACE_LEFT<sup>8+</sup>             | 0x42 | 设备空间不足                                     |
| STATUS_GRANT_REQUEST_PERMISSIONS_FAILED<sup>8+</sup> | 0x43 | 应用授权失败                                     |
| STATUS_INSTALL_PERMISSION_DENIED<sup>8+</sup>        | 0x44 | 缺少安装权限                                     |
| STATUS_UNINSTALL_PERMISSION_DENIED<sup>8+</sup>      | 0x45 | 缺少卸载权限                                     |

## BundleFlag<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.BundleFlag](js-apis-bundleManager.md#bundleflag)替代。

包的标志

 **系统能力:** 以下各项对应的系统能力均为SystemCapability.BundleManager.BundleFramework

| 名称                                            | 值         | 说明                            |
| ----------------------------------------------- | ---------- | ------------------------------- |
| GET_BUNDLE_DEFAULT                              | 0x00000000 | 获取默认的应用信息              |
| GET_BUNDLE_WITH_ABILITIES                       | 0x00000001 | 获取包括Ability信息的包信息     |
| GET_ABILITY_INFO_WITH_PERMISSION                | 0x00000002 | 获取包括权限的Ability信息       |
| GET_ABILITY_INFO_WITH_APPLICATION               | 0x00000004 | 获取包括Application的ability信息       |
| GET_APPLICATION_INFO_WITH_PERMISSION            | 0x00000008 | 获取包括权限的应用信息          |
| GET_BUNDLE_WITH_REQUESTED_PERMISSION            | 0x00000010 | 获取包括所需权限的包信息        |
| GET_ABILITY_INFO_WITH_METADATA<sup>8+</sup>     | 0x00000020 | 获取ability的元数据信息         |
| GET_APPLICATION_INFO_WITH_METADATA<sup>8+</sup> | 0x00000040 | 获取应用的元数据信息            |
| GET_ABILITY_INFO_SYSTEMAPP_ONLY<sup>8+</sup>    | 0x00000080 | 获取仅包括系统应用的ability信息 |
| GET_ABILITY_INFO_WITH_DISABLE<sup>8+</sup>      | 0x00000100 | 获取包括被禁用的ability信息     |
| GET_APPLICATION_INFO_WITH_DISABLE<sup>8+</sup>  | 0x00000200 | 获取包括被禁用的应用信息        |
| GET_ALL_APPLICATION_INFO                        | 0xFFFF0000 | 获取应用所有的信息              |

## BundleOptions<sup>deprecated<sup>
> 从API version 9开始不再维护，不推荐使用。

包的选项

 **系统能力:** SystemCapability.BundleManager.BundleFramework

| 名称   | 类型   | 可读 | 可写 | 说明                                                  |
| ------ | ------ | ---- | ---- | ----------------------------------------------------- |
| userId | number | 是   | 是   | 用户ID。默认值：调用方所在用户，取值范围：大于等于0。 |

## AbilityType<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.AbilityType](js-apis-bundleManager.md#abilitytype)替代。

Ability类型

 **系统能力:** 以下各项对应的系统能力均为SystemCapability.BundleManager.BundleFramework

| 名称 | 值 | 说明                        |
| ------- | ---- | --------------------------- |
| UNKNOWN | 无   | 未知Ability类型             |
| PAGE    | 无   | 表示基于Page模板开发的FA，用于提供与用户交互的能力        |
| SERVICE | 无   | 表示基于Service模板开发的PA，用于提供后台运行任务的能力           |
| DATA    | 无   | 表示基于Data模板开发的PA，用于对外部提供统一的数据访问对象 |

## DisplayOrientation<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.DisplayOrientation](js-apis-bundleManager.md#displayorientation)替代。

屏幕显示方向

 **系统能力:** 以下各项对应的系统能力均为SystemCapability.BundleManager.BundleFramework

| 名称          | 值   | 说明                     |
| ------------- | ---- | ------------------------ |
| UNSPECIFIED   | 无   | 屏幕方向--不指定         |
| LANDSCAPE     | 无   | 屏幕方向--横屏           |
| PORTRAIT      | 无   | 屏幕方向--竖屏           |
| FOLLOW_RECENT | 无   | 屏幕方向--紧跟上一个组件 |
## LaunchMode<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.LaunchType](js-apis-bundleManager.md#launchtype)替代。

启动模式

 **系统能力:** 以下各项对应的系统能力均为SystemCapability.BundleManager.BundleFramework

| 名称      | 值   | 说明                |
| --------- | ---- | ------------------- |
| SINGLETON | 0    | Ability只有一个实例 |
| STANDARD  | 1    | Ability有多个实例   |

## AbilitySubType<sup>deprecated<sup>
> 从API version 9开始不再维护，不推荐使用。

Ability的子类型

 **系统能力:** 以下各项对应的系统能力均为SystemCapability.BundleManager.BundleFramework

| 名称        | 值   | 说明                          |
| ----------- | ---- | ----------------------------- |
| UNSPECIFIED | 0    | 未定义Ability子类型           |
| CA          | 1    | Ability子类型是带有 UI 的服务 |

## ColorMode<sup>deprecated<sup>
> 从API version 9开始不再维护，不推荐使用。

颜色模式

 **系统能力:** 以下各项对应的系统能力均为SystemCapability.BundleManager.BundleFramework

| 名称       | 值   | 说明     |
| ---------- | ---- | -------- |
| AUTO_MODE  | -1   | 自动模式 |
| DARK_MODE  | 0    | 黑色模式 |
| LIGHT_MODE | 1    | 亮度模式 |


## GrantStatus<sup>deprecated<sup>

> 从API version 9开始不再维护，建议使用[bundleManager.PermissionGrantState](js-apis-bundleManager.md#permissiongrantstate)替代。

授予状态

 **系统能力:** 以下各项对应的系统能力均为SystemCapability.BundleManager.BundleFramework

| 名称               | 值   | 说明         |
| ------------------ | ---- | ------------ |
| PERMISSION_DENIED  | -1   | 拒绝授予权限 |
| PERMISSION_GRANTED | 0    | 授予权限     |
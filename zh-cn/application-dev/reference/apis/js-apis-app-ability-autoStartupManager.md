# @ohos.app.ability.autoStartupManager(autoStartupManager)

autoStartupManager模块提供注册、注销监听应用开机自启动状态变化的回调函数的能力。

> **说明：**
>
> 本模块首批接口从API version 11开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。  
> 本模块接口均为系统接口，三方应用不支持调用。  
> 本模块接口仅可在Stage模型下使用。

## 导入模块

```ts
import AutoStartupManager from '@ohos.app.ability.autoStartupManager';
```

## on

on(type: 'systemAutoStartup', callback: AutoStartupCallback): void

注册监听应用组件开机自启动状态变化。

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

**参数**：

| 参数名        | 类型                                       | 必填   | 说明             |
| --------- | ---------------------------------------- | ---- | -------------- |
| type | string | 是    | 固定取值“systemAutoStartup”，表示为系统应用所调用。 |
| callback  | [AutoStartupCallback](js-apis-inner-application-autoStartupCallback.md)   | 是    | 监听应用组件开机自启动状态变化的回调对象。      |

**示例**：

```ts
import AutoStartupManager from '@ohos.app.ability.AutoStartupManager';

let autoStartupCallback = {
  onAutoStartupOn(data) {
    console.info('===> onAutoStartupOn data: ' + JSON.stringify(data));
  },
  onAutoStartupOff(data) {
    console.info('===> onAutoStartupOff data: ' + JSON.stringify(data));
  }
}

try {
  AutoStartupManager.on('systemAutoStartup', autoStartupCallback);
} catch (err) {
  console.info('====> autostartupmanager on throw err: ' + JSON.stringify(err));
}
```

## off

off(type: 'systemAutoStartup', callback?: AutoStartupCallback): void

注销监听应用组件开机自启动状态变化。

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

**参数**：

| 参数名        | 类型                                       | 必填   | 说明             |
| --------- | ---------------------------------------- | ---- | -------------- |
| type | string              | 是    | 固定取值“systemAutoStartup”，表示为系统应用所调用。 |
| callback | [AutoStartupCallback](js-apis-inner-application-autoStartupCallback.md)   | 否 | 监听应用组件开机自启动状态变化的回调对象。 |

**示例**：

```ts
import AutoStartupManager from '@ohos.app.ability.AutoStartupManager';

let autoStartupCallback = {
  onAutoStartupOn(data) {
    console.info('===> onAutoStartupOn data: ' + JSON.stringify(data));
  },
  onAutoStartupOff(data) {
    console.info('===> onAutoStartupOff data: ' + JSON.stringify(data));
  }
}

try {
  AutoStartupManager.off('systemAutoStartup', autoStartupCallback);
} catch (err) {
  console.info('====> autostartupmanager off throw err: ' + JSON.stringify(err));
}
```

## setApplicationAutoStartup

setApplicationAutoStartup(info: AutoStartupInfo, callback: AsyncCallback\<void\>): void

设置应用组件开机自启动。使用callback异步回调。

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

**参数**：

| 参数名        | 类型                                       | 必填   | 说明             |
| --------- | ---------------------------------------- | ---- | -------------- |
| info | [AutoStartupInfo](js-apis-inner-application-autoStartupInfo.md) | 是    | 要设置的开机自启动应用组件信息。 |
| callback | AsyncCallback\<void\> | 是 | 回调函数。当设置应用组件开机自启动成功，err为undefined，否则为错误对象。 |

**示例**：

```ts
import AutoStartupManager from '@ohos.app.ability.AutoStartupManager';

try {
  AutoStartupManager.setApplicationAutoStartup({
    bundleName: 'com.example.autostartupapp',
    abilityName: 'EntryAbility'
  }, (err, data) => {
    console.info('====> setApplicationAutoStartup: ' + JSON.stringify(err) + ' data: ' + JSON.stringify(data));
  });
} catch (err) {
  console.info('====> setApplicationAutoStartup throw err: ' + JSON.stringify(err));
}
```

## setApplicationAutoStartup

setApplicationAutoStartup(info: AutoStartupInfo): Promise\<void\>

设置应用组件开机自启动。使用Promise异步回调。

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

**参数**：

| 参数名 | 类型            | 必填 | 说明                         |
| ------ | --------------- | ---- | ---------------------------- |
| info   | [AutoStartupInfo](js-apis-inner-application-autoStartupInfo.md) | 是   | 要设置的开机自启动应用组件信息。 |

**返回值：**

| 类型          | 说明                                                         |
| ------------- | ------------------------------------------------------------ |
| Promise\<void\> | Promise对象。无返回结果的Promise对象。 |

**示例**：

```ts
import AutoStartupManager from '@ohos.app.ability.AutoStartupManager';

try {
  AutoStartupManager.setApplicationAutoStartup({
    bundleName: 'com.example.autostartupapp',
    abilityName: 'EntryAbility'
  }).then((data) => {
    console.info('====> setApplicationAutoStartup data: ' + JSON.stringify(data));
  }).catch((err) => {
    console.info('====> setApplicationAutoStartup err: ' + JSON.stringify(err));
  });
} catch (err) {
  console.info('====> setApplicationAutoStartup throw err: ' + JSON.stringify(err));
}
```

## cancelApplicationAutoStartup

cancelApplicationAutoStartup(info: AutoStartupInfo, callback: AsyncCallback\<void\>): void

取消应用组件开机自启动。使用callback异步回调。

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

**参数**：

| 参数名        | 类型                                       | 必填   | 说明             |
| --------- | ---------------------------------------- | ---- | -------------- |
| info | [AutoStartupInfo](js-apis-inner-application-autoStartupInfo.md)   | 是 | 要取消的开机自启动应用组件信息。 |
| callback | AsyncCallback\<void\> | 是    | 回调函数。当取消应用组件开机自启动成功，err为undefined，否则为错误对象。 |

**示例**：

```ts
import AutoStartupManager from '@ohos.app.ability.AutoStartupManager';

try {
  AutoStartupManager.cancelApplicationAutoStartup({
    bundleName: 'com.example.autostartupapp',
    abilityName: 'EntryAbility'
  }, (err, data) => {
    console.info('====> cancelApplicationAutoStartup err: ' + JSON.stringify(err) + ' data: ' + JSON.stringify(data));
  });
} catch (err) {
  console.info('====> cancelApplicationAutoStartup throw err: ' + JSON.stringify(err));
}
```

## cancelApplicationAutoStartup

cancelApplicationAutoStartup(info: AutoStartupInfo): Promise\<void\>

取消应用组件开机自启动。使用Promise异步回调。

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

**参数**：

| 参数名        | 类型                                       | 必填   | 说明             |
| --------- | ---------------------------------------- | ---- | -------------- |
| info | [AutoStartupInfo](js-apis-inner-application-autoStartupInfo.md)   | 是 | 要取消的开机自启动应用组件信息。 |

**返回值：**

| 类型          | 说明                                                         |
| ------------- | ------------------------------------------------------------ |
| Promise\<void\> | Promise对象。无返回结果的Promise对象。 |

**示例**：

```ts
import AutoStartupManager from '@ohos.app.ability.AutoStartupManager';

try {
  AutoStartupManager.cancelApplicationAutoStartup({
    bundleName: 'com.example.autostartupapp',
    abilityName: 'EntryAbility'
  }).then((data) => {
    console.info('====> cancelApplicationAutoStartup data: ' + JSON.stringify(data));
  }).catch((err) => {
    console.info('====> cancelApplicationAutoStartup err: ' + JSON.stringify(err));
  });
} catch (err) {
  console.info('====> cancelApplicationAutoStartup throw err: ' + JSON.stringify(err));
}
```

## queryAllAutoStartupApplications

queryAllAutoStartupApplications(callback: AsyncCallback\<Array\<AutoStartupInfo\>\>): void

查询自启动应用组件信息。使用callback异步回调。

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

**参数**：

| 参数名        | 类型                                       | 必填   | 说明             |
| --------- | ---------------------------------------- | ---- | -------------- |
| callback  | AsyncCallback\<Array\<[AutoStartupInfo](js-apis-inner-application-autoStartupInfo.md)\>\> | 是    | 回调函数。当查询自启动应用组件信息成功，err为undefined，data为获取到的Array\<[AutoStartupInfo](js-apis-inner-application-autoStartupInfo.md)\>；否则为错误对象。      |

**示例**：

```ts
import AutoStartupManager from '@ohos.app.ability.AutoStartupManager';

try {
  AutoStartupManager.queryAllAutoStartupApplications((err, data) => {
    console.info('====> queryAllAutoStartupApplications err: ' + JSON.stringify(err) + ' data: ' + JSON.stringify(data));
  });
} catch (err) {
  console.info('====> queryAllAutoStartupApplications throw err: ' + JSON.stringify(err));
}
```

## queryAllAutoStartupApplications

 queryAllAutoStartupApplications(): Promise\<Array\<AutoStartupInfo\>\>

查询自启动应用组件信息。使用Promise异步回调。

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

**返回值：**

| 类型                            | 说明                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| Promise\<Array\<[AutoStartupInfo](js-apis-inner-application-autoStartupInfo.md)\>\> | Promise对象，返回自启动应用组件信息。 |

**示例**：

```ts
import AutoStartupManager from '@ohos.app.ability.AutoStartupManager';

try {
  AutoStartupManager.queryAllAutoStartupApplications().then((data) => {
    console.info('====> queryAllAutoStartupApplications OK');
  }).catch((err) => {
    console.info('====> queryAllAutoStartupApplications err: ' + JSON.stringify(err));
  });
} catch (err) {
  console.info('====> queryAllAutoStartupApplications throw err: ' + JSON.stringify(err));
}
```

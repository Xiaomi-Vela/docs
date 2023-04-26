# UIAbilityContext

UIAbilityContext是UIAbility的上下文环境，继承自Context。

UIAbilityContext模块提供允许访问特定UIAbility的资源的能力，包括对UIAbility的启动、停止的设置、获取caller通信接口、拉起弹窗请求用户授权等。

> **说明：**
>
>  - 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>  - 本模块接口仅可在Stage模型下使用。

## 属性

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

| 名称 | 类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| abilityInfo | [AbilityInfo](js-apis-bundleManager-abilityInfo.md) | 是 | 否 | UIAbilityinfo相关信息 |
| currentHapModuleInfo | [HapModuleInfo](js-apis-bundleManager-hapModuleInfo.md) | 是 | 否 | 当前hap包的信息 |
| config | [Configuration](js-apis-app-ability-configuration.md) | 是 | 否 | 表示配置信息。 |

## UIAbilityContext.startAbility

startAbility(want: Want, callback: AsyncCallback&lt;void&gt;): void;

启动UIAbility（callback形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动UIAbility需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 目标UIAbility的visible属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动UIAbility的want信息。 |
| callback | AsyncCallback&lt;void&gt; | 是 | callback形式返回启动结果 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000010 | Can not operation with continue flag.        |
| 16000011 | Context does not exist.        |
| 16000051 | Network error. The network is abnormal. |
| 16000052 | Free install not support. The application does not support freeinstall |
| 16000053 | Not top ability. The application is not top ability. |
| 16000054 | Free install busyness. There are concurrent tasks, waiting for retry. |
| 16000055 | Free install timeout. |
| 16000056 | Can not free install other ability. |
| 16000057 | Not support cross device free install. |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    bundleName: 'com.example.myapp',
    abilityName: 'MyAbility'
  };

  try {
    this.context.startAbility(want, (error) => {
      if (error.code) {
        // 处理业务逻辑错误
        console.log('startAbility failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // 执行正常业务
      console.log('startAbility succeed');
    });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```


## UIAbilityContext.startAbility

startAbility(want: Want, options: StartOptions, callback: AsyncCallback&lt;void&gt;): void;

启动UIAbility（callback形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动UIAbility需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 目标UIAbility的visible属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md)  | 是 | 启动UIAbility的want信息。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 是 | 启动UIAbility所携带的参数。 |
| callback | AsyncCallback&lt;void&gt; | 是 | callback形式返回启动结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000010 | Can not operation with continue flag.        |
| 16000011 | Context does not exist.        |
| 16000051 | Network error. The network is abnormal. |
| 16000052 | Free install not support. The application does not support freeinstall |
| 16000053 | Not top ability. The application is not top ability. |
| 16000054 | Free install busyness. There are concurrent tasks, waiting for retry. |
| 16000055 | Free install timeout. |
| 16000056 | Can not free install other ability. |
| 16000057 | Not support cross device free install. |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.extreme.test',
    abilityName: 'MainAbility'
  };
  let options = {
    windowMode: 0
  };

  try {
    this.context.startAbility(want, options, (error) => {
      if (error.code) {
        // 处理业务逻辑错误
        console.log('startAbility failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // 执行正常业务
      console.log('startAbility succeed');
    });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.startAbility

startAbility(want: Want, options?: StartOptions): Promise&lt;void&gt;;

启动UIAbility（promise形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动UIAbility需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 目标UIAbility的visible属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动UIAbility的want信息。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 否 | 启动UIAbility所携带的参数。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;void&gt; | Promise形式返回启动结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000010 | Can not operation with continue flag.        |
| 16000011 | Context does not exist.        |
| 16000051 | Network error. The network is abnormal. |
| 16000052 | Free install not support. The application does not support freeinstall |
| 16000053 | Not top ability. The application is not top ability. |
| 16000054 | Free install busyness. There are concurrent tasks, waiting for retry. |
| 16000055 | Free install timeout. |
| 16000056 | Can not free install other ability. |
| 16000057 | Not support cross device free install. |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    bundleName: 'com.example.myapp',
    abilityName: 'MyAbility'
  };
  let options = {
  	windowMode: 0,
  };

  try {
    this.context.startAbility(want, options)
      .then((data) => {
        // 执行正常业务
        console.log('startAbility succeed');
      })
      .catch((error) => {
        // 处理业务逻辑错误
        console.log('startAbility failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```


## UIAbilityContext.startAbilityForResult

startAbilityForResult(want: Want, callback: AsyncCallback&lt;AbilityResult&gt;): void;

启动一个UIAbility。UIAbility被启动后，有如下情况(callback形式):
 - 正常情况下可通过调用[terminateSelfWithResult](#uiabilitycontextterminateselfwithresult)接口使之终止并且返回结果给调用方。
 - 异常情况下比如杀死UIAbility会返回异常信息给调用方, 异常信息中resultCode为-1。
 - 如果被启动的UIAbility模式是单实例模式, 不同应用多次调用该接口启动这个UIAbility，当这个UIAbility调用[terminateSelfWithResult](#uiabilitycontextterminateselfwithresult)接口使之终止时，只将正常结果返回给最后一个调用方, 其它调用方返回异常信息, 异常信息中resultCode为-1。

使用规则：
 - 调用方应用位于后台时，使用该接口启动UIAbility需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 目标UIAbility的visible属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want |[Want](js-apis-application-want.md) | 是 | 启动UIAbility的want信息。 |
| callback | AsyncCallback&lt;[AbilityResult](js-apis-inner-ability-abilityResult.md)&gt; | 是 | 执行结果回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000010 | Can not operation with continue flag.        |
| 16000011 | Context does not exist.        |
| 16000051 | Network error. The network is abnormal. |
| 16000052 | Free install not support. The application does not support freeinstall |
| 16000053 | Not top ability. The application is not top ability. |
| 16000054 | Free install busyness. There are concurrent tasks, waiting for retry. |
| 16000055 | Free install timeout. |
| 16000056 | Can not free install other ability. |
| 16000057 | Not support cross device free install. |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.extreme.test',
    abilityName: 'MainAbility'
  };

  try {
    this.context.startAbilityForResult(want, (error, result) => {
      if (error.code) {
        // 处理业务逻辑错误
        console.log('startAbilityForResult failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // 执行正常业务
      console.log('startAbilityForResult succeed, result.resultCode = ' +
        result.resultCode)
    });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.startAbilityForResult

startAbilityForResult(want: Want, options: StartOptions, callback: AsyncCallback&lt;AbilityResult&gt;): void;

启动一个UIAbility。UIAbility被启动后，有如下情况(callback形式):
 - 正常情况下可通过调用[terminateSelfWithResult](#uiabilitycontextterminateselfwithresult)接口使之终止并且返回结果给调用方。
 - 异常情况下比如杀死UIAbility会返回异常信息给调用方, 异常信息中resultCode为-1。
 - 如果被启动的UIAbility模式是单实例模式, 不同应用多次调用该接口启动这个UIAbility，当这个UIAbility调用[terminateSelfWithResult](#uiabilitycontextterminateselfwithresult)接口使之终止时，只将正常结果返回给最后一个调用方, 其它调用方返回异常信息, 异常信息中resultCode为-1。

使用规则：
 - 调用方应用位于后台时，使用该接口启动UIAbility需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 目标UIAbility的visible属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want |[Want](js-apis-application-want.md) | 是 | 启动UIAbility的want信息。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 是 | 启动UIAbility所携带的参数。 |
| callback | AsyncCallback&lt;[AbilityResult](js-apis-inner-ability-abilityResult.md)&gt; | 是 | 执行结果回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000010 | Can not operation with continue flag.        |
| 16000011 | Context does not exist.        |
| 16000051 | Network error. The network is abnormal. |
| 16000052 | Free install not support. The application does not support freeinstall |
| 16000053 | Not top ability. The application is not top ability. |
| 16000054 | Free install busyness. There are concurrent tasks, waiting for retry. |
| 16000055 | Free install timeout. |
| 16000056 | Can not free install other ability. |
| 16000057 | Not support cross device free install. |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.extreme.test',
    abilityName: 'MainAbility'
  };
  let options = {
    windowMode: 0,
  };

  try {
    this.context.startAbilityForResult(want, options, (error, result) => {
      if (error.code) {
        // 处理业务逻辑错误
        console.log('startAbilityForResult failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // 执行正常业务
      console.log('startAbilityForResult succeed, result.resultCode = ' +
        result.resultCode)
    });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```


## UIAbilityContext.startAbilityForResult

startAbilityForResult(want: Want, options?: StartOptions): Promise&lt;AbilityResult&gt;;

启动一个UIAbility。UIAbility被启动后，有如下情况(promise形式):
 - 正常情况下可通过调用[terminateSelfWithResult](#uiabilitycontextterminateselfwithresult)接口使之终止并且返回结果给调用方。
 - 异常情况下比如杀死UIAbility会返回异常信息给调用方, 异常信息中resultCode为-1。
 - 如果被启动的UIAbility模式是单实例模式, 不同应用多次调用该接口启动这个UIAbility，当这个UIAbility调用[terminateSelfWithResult](#uiabilitycontextterminateselfwithresult)接口使之终止时，只将正常结果返回给最后一个调用方, 其它调用方返回异常信息, 异常信息中resultCode为-1。

使用规则：
 - 调用方应用位于后台时，使用该接口启动UIAbility需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 目标UIAbility的visible属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动UIAbility的want信息。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 否 | 启动UIAbility所携带的参数。 |


**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;[AbilityResult](js-apis-inner-ability-abilityResult.md)&gt; | Promise形式返回执行结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000010 | Can not operation with continue flag.        |
| 16000011 | Context does not exist.        |
| 16000051 | Network error. The network is abnormal. |
| 16000052 | Free install not support. The application does not support freeinstall |
| 16000053 | Not top ability. The application is not top ability. |
| 16000054 | Free install busyness. There are concurrent tasks, waiting for retry. |
| 16000055 | Free install timeout. |
| 16000056 | Can not free install other ability. |
| 16000057 | Not support cross device free install. |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    bundleName: 'com.example.myapp',
    abilityName: 'MyAbility'
  };
  let options = {
  	windowMode: 0,
  };

  try {
    this.context.startAbilityForResult(want, options)
      .then((result) => {
        // 执行正常业务
        console.log('startAbilityForResult succeed, result.resultCode = ' + result.resultCode);
      })
      .catch((error) => {
        // 处理业务逻辑错误
        console.log('startAbilityForResult failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.startAbilityForResultWithAccount

startAbilityForResultWithAccount(want: Want, accountId: number, callback: AsyncCallback\<AbilityResult>): void;

启动一个UIAbility并在该UIAbility帐号销毁时返回执行结果（callback形式）。

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动UIAbility的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess)。 |
| callback | AsyncCallback\<AbilityResult\> | 是 | 启动UIAbility的回调函数，返回UIAbility结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000006 | Can not cross user operations. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000010 | Can not operation with continue flag.        |
| 16000011 | Context does not exist.        |
| 16000051 | Network error. The network is abnormal. |
| 16000052 | Free install not support. The application does not support freeinstall |
| 16000053 | Not top ability. The application is not top ability. |
| 16000054 | Free install busyness. There are concurrent tasks, waiting for retry. |
| 16000055 | Free install timeout. |
| 16000056 | Can not free install other ability. |
| 16000057 | Not support cross device free install. |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.extreme.test',
    abilityName: 'MainAbility'
  };
  let accountId = 100;

  try {
    this.context.startAbilityForResultWithAccount(want, accountId, (error, result) => {
      if (error.code) {
        // 处理业务逻辑错误
        console.log('startAbilityForResultWithAccount failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // 执行正常业务
      console.log('startAbilityForResultWithAccount succeed, result.resultCode = ' +
        result.resultCode)
    });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```


## UIAbilityContext.startAbilityForResultWithAccount

startAbilityForResultWithAccount(want: Want, accountId: number, options: StartOptions, callback: AsyncCallback\<void\>): void;

启动一个UIAbility并在该UIAbility帐号销毁时返回执行结果（callback形式）。

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动UIAbility的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess)。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 是 | 启动UIAbility所携带的参数。 |
| callback | AsyncCallback\<void\> | 是 | 启动UIAbility的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000006 | Can not cross user operations. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000010 | Can not operation with continue flag.        |
| 16000011 | Context does not exist.        |
| 16000051 | Network error. The network is abnormal. |
| 16000052 | Free install not support. The application does not support freeinstall |
| 16000053 | Not top ability. The application is not top ability. |
| 16000054 | Free install busyness. There are concurrent tasks, waiting for retry. |
| 16000055 | Free install timeout. |
| 16000056 | Can not free install other ability. |
| 16000057 | Not support cross device free install. |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.extreme.test',
    abilityName: 'MainAbility'
  };
  let accountId = 100;
  let options = {
    windowMode: 0
  };

  try {
    this.context.startAbilityForResultWithAccount(want, accountId, options, (error, result) => {
      if (error.code) {
        // 处理业务逻辑错误
        console.log('startAbilityForResultWithAccount failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // 执行正常业务
      console.log('startAbilityForResultWithAccount succeed, result.resultCode = ' +
        result.resultCode)
    });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```


## UIAbilityContext.startAbilityForResultWithAccount

startAbilityForResultWithAccount(want: Want, accountId: number, options?: StartOptions): Promise\<AbilityResult\>;

启动一个UIAbility并在该UIAbility帐号销毁时返回执行结果（promise形式）。

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动UIAbility的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess)。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 否 | 启动UIAbility所携带的参数。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;AbilityResult&gt; | 返回一个Promise，包含UIAbility结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000006 | Can not cross user operations. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000010 | Can not operation with continue flag.        |
| 16000011 | Context does not exist.        |
| 16000051 | Network error. The network is abnormal. |
| 16000052 | Free install not support. The application does not support freeinstall |
| 16000053 | Not top ability. The application is not top ability. |
| 16000054 | Free install busyness. There are concurrent tasks, waiting for retry. |
| 16000055 | Free install timeout. |
| 16000056 | Can not free install other ability. |
| 16000057 | Not support cross device free install. |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.extreme.test',
    abilityName: 'MainAbility'
  };
  let accountId = 100;
  let options = {
    windowMode: 0
  };

  try {
    this.context.startAbilityForResultWithAccount(want, accountId, options)
      .then((result) => {
        // 执行正常业务
        console.log('startAbilityForResultWithAccount succeed, result.resultCode = ' +
          result.resultCode)
      })
      .catch((error) => {
        // 处理业务逻辑错误
        console.log('startAbilityForResultWithAccount failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```
## UIAbilityContext.startServiceExtensionAbility

startServiceExtensionAbility(want: Want, callback: AsyncCallback\<void>): void;

启动一个新的ServiceExtensionAbility（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动UIAbility的want信息。 |
| callback | AsyncCallback\<void\> | 是 | 启动UIAbility的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000002 | Ability type error. The specified ability type is wrong. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000011 | Context does not exist.        |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.extreme.test',
    abilityName: 'MainAbility'
  };

  try {
    this.context.startServiceExtensionAbility(want, (error) => {
      if (error.code) {
        // 处理业务逻辑错误
        console.log('startServiceExtensionAbility failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // 执行正常业务
      console.log('startServiceExtensionAbility succeed');
    });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.startServiceExtensionAbility

startServiceExtensionAbility(want: Want): Promise\<void>;

启动一个新的ServiceExtensionAbility（Promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动UIAbility的want信息。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000002 | Ability type error. The specified ability type is wrong. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000011 | Context does not exist.        |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.extreme.test',
    abilityName: 'MainAbility'
  };

  try {
    this.context.startServiceExtensionAbility(want)
      .then((data) => {
        // 执行正常业务
        console.log('startServiceExtensionAbility succeed');
      })
      .catch((error) => {
        // 处理业务逻辑错误
        console.log('startServiceExtensionAbility failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.startServiceExtensionAbilityWithAccount

startServiceExtensionAbilityWithAccount(want: Want, accountId: number, callback: AsyncCallback\<void>): void;

启动一个新的ServiceExtensionAbility（callback形式）。

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动UIAbility的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess)。 |
| callback | AsyncCallback\<void\> | 是 | 启动UIAbility的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000002 | Ability type error. The specified ability type is wrong. |
| 16000004 | Visibility verification failed. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000011 | Context does not exist.        |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.extreme.test',
    abilityName: 'MainAbility'
  };
  let accountId = 100;

  try {
    this.context.startServiceExtensionAbilityWithAccount(want, accountId, (error) => {
      if (error.code) {
        // 处理业务逻辑错误
        console.log('startServiceExtensionAbilityWithAccount failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // 执行正常业务
      console.log('startServiceExtensionAbilityWithAccount succeed');
    });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.startServiceExtensionAbilityWithAccount

startServiceExtensionAbilityWithAccount(want: Want, accountId: number): Promise\<void>;

启动一个新的ServiceExtensionAbility（Promise形式）。

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动UIAbility的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess)。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000002 | Ability type error. The specified ability type is wrong. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000006 | Can not cross user operations. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000011 | Context does not exist.        |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.extreme.test',
    abilityName: 'MainAbility'
  };
  let accountId = 100;

  try {
    this.context.startServiceExtensionAbilityWithAccount(want, accountId)
      .then((data) => {
        // 执行正常业务
        console.log('startServiceExtensionAbilityWithAccount succeed');
      })
      .catch((error) => {
        // 处理业务逻辑错误
        console.log('startServiceExtensionAbilityWithAccount failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```
## UIAbilityContext.stopServiceExtensionAbility

stopServiceExtensionAbility(want: Want, callback: AsyncCallback\<void>): void;

停止同一应用程序内的服务（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动UIAbility的want信息。 |
| callback | AsyncCallback\<void\> | 是 | 启动UIAbility的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000002 | Ability type error. The specified ability type is wrong. |
| 16000004 | Visibility verification failed. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000011 | Context does not exist.        |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.extreme.test',
    abilityName: 'MainAbility'
  };

  try {
    this.context.stopServiceExtensionAbility(want, (error) => {
      if (error.code) {
        // 处理业务逻辑错误
        console.log('stopServiceExtensionAbility failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // 执行正常业务
      console.log('stopServiceExtensionAbility succeed');
    });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.stopServiceExtensionAbility

stopServiceExtensionAbility(want: Want): Promise\<void>;

停止同一应用程序内的服务（Promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动UIAbility的want信息。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000002 | Ability type error. The specified ability type is wrong. |
| 16000004 | Visibility verification failed. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000011 | Context does not exist.        |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.extreme.test',
    abilityName: 'MainAbility'
  };

  try {
    this.context.stopServiceExtensionAbility(want)
      .then((data) => {
        // 执行正常业务
        console.log('stopServiceExtensionAbility succeed');
      })
      .catch((error) => {
        // 处理业务逻辑错误
        console.log('stopServiceExtensionAbility failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.stopServiceExtensionAbilityWithAccount

stopServiceExtensionAbilityWithAccount(want: Want, accountId: number, callback: AsyncCallback\<void>): void;

使用帐户停止同一应用程序内的服务（callback形式）。

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动UIAbility的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess)。 |
| callback | AsyncCallback\<void\> | 是 | 启动UIAbility的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000002 | Ability type error. The specified ability type is wrong. |
| 16000004 | Visibility verification failed. |
| 16000006 | Can not cross user operations. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000011 | Context does not exist.        |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.extreme.test',
    abilityName: 'MainAbility'
  };
  let accountId = 100;

  try {
    this.context.stopServiceExtensionAbilityWithAccount(want, accountId, (error) => {
      if (error.code) {
        // 处理业务逻辑错误
        console.log('stopServiceExtensionAbilityWithAccount failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // 执行正常业务
      console.log('stopServiceExtensionAbilityWithAccount succeed');
    });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.stopServiceExtensionAbilityWithAccount

stopServiceExtensionAbilityWithAccount(want: Want, accountId: number): Promise\<void>;

使用帐户停止同一应用程序内的服务（Promise形式）。

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动UIAbility的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess)。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000002 | Ability type error. The specified ability type is wrong. |
| 16000004 | Visibility verification failed. |
| 16000006 | Can not cross user operations. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000011 | Context does not exist.        |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.extreme.test',
    abilityName: 'MainAbility'
  };
  let accountId = 100;

  try {
    this.context.stopServiceExtensionAbilityWithAccount(want, accountId)
      .then((data) => {
        // 执行正常业务
        console.log('stopServiceExtensionAbilityWithAccount succeed');
      })
      .catch((error) => {
        // 处理业务逻辑错误
        console.log('stopServiceExtensionAbilityWithAccount failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.terminateSelf

terminateSelf(callback: AsyncCallback&lt;void&gt;): void;

停止UIAbility自身（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;void&gt; | 是 | 回调函数，返回接口调用是否成功的结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000011 | Context does not exist.        |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  this.context.terminateSelf((error) => {
    if (error.code) {
      // 处理业务逻辑错误
      console.log('terminateSelf failed, error.code: ' + JSON.stringify(error.code) +
        ' error.message: ' + JSON.stringify(error.message));
      return;
    }
    // 执行正常业务
    console.log('terminateSelf succeed');
  });
  ```


## UIAbilityContext.terminateSelf

terminateSelf(): Promise&lt;void&gt;;

停止UIAbility自身（promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;void&gt; | 返回一个Promise，包含接口的结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000011 | Context does not exist.        |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  this.context.terminateSelf().then((data) => {
    // 执行正常业务
    console.log('terminateSelf succeed');
  }).catch((error) => {
    // 处理业务逻辑错误
    console.log('terminateSelf failed, error.code: ' + JSON.stringify(error.code) +
      ' error.message: ' + JSON.stringify(error.message));
  });
  ```


## UIAbilityContext.terminateSelfWithResult

terminateSelfWithResult(parameter: AbilityResult, callback: AsyncCallback&lt;void&gt;): void;

停止当前的UIAbility。如果该UIAbility是通过调用[startAbilityForResult](#uiabilitycontextstartabilityforresult)接口被拉起的，调用terminateSelfWithResult接口时会将结果返回给调用者，如果该UIAbility不是通过调用[startAbilityForResult](#uiabilitycontextstartabilityforresult)接口被拉起的，调用terminateSelfWithResult接口时不会有结果返回给调用者（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| parameter | [AbilityResult](js-apis-inner-ability-abilityResult.md) | 是 | 返回给调用startAbilityForResult&nbsp;接口调用方的相关信息。 |
| callback | AsyncCallback&lt;void&gt; | 是 | callback形式返回停止结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000011 | Context does not exist.        |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    bundleName: 'com.extreme.myapplication',
    abilityName: 'SecondAbility'
  }
  let resultCode = 100;
  // 返回给接口调用方AbilityResult信息
  let abilityResult = {
    want,
    resultCode
  }

  try {
    this.context.terminateSelfWithResult(abilityResult, (error) => {
      if (error.code) {
        // 处理业务逻辑错误
        console.log('terminateSelfWithResult failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // 执行正常业务
      console.log('terminateSelfWithResult succeed');
    });
  } catch (paramError) {
      // 处理入参错误异常
      console.log('error.code: ' + JSON.stringify(paramError.code) +
        ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```


## UIAbilityContext.terminateSelfWithResult

terminateSelfWithResult(parameter: AbilityResult): Promise&lt;void&gt;;

停止当前的UIAbility。如果该UIAbility是通过调用[startAbilityForResult](#uiabilitycontextstartabilityforresult)接口被拉起的，调用terminateSelfWithResult接口时会将结果返回给调用者，如果该UIAbility不是通过调用[startAbilityForResult](#uiabilitycontextstartabilityforresult)接口被拉起的，调用terminateSelfWithResult接口时不会有结果返回给调用者（promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| parameter | [AbilityResult](js-apis-inner-ability-abilityResult.md) | 是 | 返回给startAbilityForResult&nbsp;调用方的信息。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;void&gt; | promise形式返回停止结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000011 | Context does not exist.        |
| 16000050 | Internal Error. |


**示例：**

  ```ts
  let want = {
    bundleName: 'com.extreme.myapplication',
    abilityName: 'SecondAbility'
  }
  let resultCode = 100;
  // 返回给接口调用方AbilityResult信息
  let abilityResult = {
    want,
    resultCode
  }

  try {
    this.context.terminateSelfWithResult(abilityResult)
      .then((data) => {
        // 执行正常业务
        console.log('terminateSelfWithResult succeed');
      })
      .catch((error) => {
        // 处理业务逻辑错误
        console.log('terminateSelfWithResult failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.connectServiceExtensionAbility

connectServiceExtensionAbility(want: Want, options: ConnectOptions): number;

使用AbilityInfo.AbilityType.SERVICE模板将当前UIAbility连接到一个UIAbility。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动UIAbility的want信息。 |
| options | [ConnectOptions](js-apis-inner-ability-connectOptions.md) | 否 | 远端对象实例。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回UIAbility连接的结果code。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000002 | Ability type error. The specified ability type is wrong. |
| 16000004 | Visibility verification failed. |
| 16000011 | Context does not exist.        |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.extreme.test',
    abilityName: 'MainAbility'
  };
  let options = {
    onConnect(elementName, remote) { console.log('----------- onConnect -----------') },
    onDisconnect(elementName) { console.log('----------- onDisconnect -----------') },
    onFailed(code) { console.log('----------- onFailed -----------') }
  }

  let connection = null;
  try {
    connection = this.context.connectServiceExtensionAbility(want, options);
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```


## UIAbilityContext.connectServiceExtensionAbilityWithAccount

connectServiceExtensionAbilityWithAccount(want: Want, accountId: number, options: ConnectOptions): number;

使用AbilityInfo.AbilityType.SERVICE模板和account将当前UIAbility连接到一个UIAbility。

**需要权限：** ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动UIAbility的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess)。 |
| options | [ConnectOptions](js-apis-inner-ability-connectOptions.md) | 否 | 远端对象实例。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回UIAbility连接的结果code。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000002 | Ability type error. The specified ability type is wrong. |
| 16000004 | Visibility verification failed. |
| 16000006 | Can not cross user operations. |
| 16000011 | Context does not exist.        |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.extreme.test',
    abilityName: 'MainAbility'
  };
  let accountId = 100;
  let options = {
    onConnect(elementName, remote) { console.log('----------- onConnect -----------') },
    onDisconnect(elementName) { console.log('----------- onDisconnect -----------') },
    onFailed(code) { console.log('----------- onFailed -----------') }
  }

  let connection = null;
  try {
    connection = this.context.connectServiceExtensionAbilityWithAccount(want, accountId, options);
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.disconnectServiceExtensionAbility

disconnectServiceExtensionAbility(connection: number): Promise\<void>;

断开连接（promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| connection | number | 是 | 连接的UIAbility的数字代码。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise\<void> | 返回执行结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000003 | Input error. The specified id does not exist. |
| 16000011 | Context does not exist.        |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  // connection为connectServiceExtensionAbility中的返回值
  let connection = 1;

  try {
    this.context.disconnectServiceExtensionAbility(connection)
      .then((data) => {
        // 执行正常业务
        console.log('disconnectServiceExtensionAbility succeed');
      })
      .catch((error) => {
        // 处理业务逻辑错误
        console.log('disconnectServiceExtensionAbility failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.disconnectServiceExtensionAbility

disconnectServiceExtensionAbility(connection: number, callback:AsyncCallback\<void>): void;

断开连接（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| connection | number | 是 | 连接的UIAbility的数字代码。 |
| callback | AsyncCallback\<void> | 是 | 表示指定的回调方法。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000003 | Input error. The specified id does not exist. |
| 16000011 | Context does not exist.        |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  // connection为connectServiceExtensionAbility中的返回值
  let connection = 1;

  try {
    this.context.disconnectServiceExtensionAbility(connection, (error) => {
      if (error.code) {
        // 处理业务逻辑错误
        console.log('disconnectServiceExtensionAbility failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // 执行正常业务
      console.log('disconnectServiceExtensionAbility succeed');
    });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.startAbilityByCall

startAbilityByCall(want: Want): Promise&lt;Caller&gt;;

启动指定UIAbility至前台或后台，同时获取其Caller通信接口，调用方可使用Caller与被启动的UIAbility进行通信。

使用规则：
 - 调用方应用位于后台时，使用该接口启动UIAbility需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 目标UIAbility的visible属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 传入需要启动的UIAbility的信息，包含abilityName、moduleName、bundleName、deviceId(可选)、parameters(可选)，其中deviceId缺省或为空表示启动本地UIAbility，parameters缺省或为空表示后台启动UIAbility。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;Caller&gt; | 获取要通讯的caller对象。 |

**示例：**

  后台启动：

  ```ts
  let caller = undefined;

  // 后台启动Ability，不配置parameters
  let wantBackground = {
      bundleName: 'com.example.myservice',
      moduleName: 'entry',
      abilityName: 'MainAbility',
      deviceId: ''
  };

  try {
    this.context.startAbilityByCall(wantBackground)
      .then((obj) => {
        // 执行正常业务
        caller = obj;
        console.log('startAbilityByCall succeed');
      }).catch((error) => {
        // 处理业务逻辑错误
        console.log('startAbilityByCall failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

  前台启动：

  ```ts
  let caller = undefined;

  // 前台启动Ability，将parameters中的'ohos.aafwk.param.callAbilityToForeground'配置为true
  let wantForeground = {
      bundleName: 'com.example.myservice',
      moduleName: 'entry',
      abilityName: 'MainAbility',
      deviceId: '',
      parameters: {
        'ohos.aafwk.param.callAbilityToForeground': true
      }
  };

  try {
    this.context.startAbilityByCall(wantForeground)
      .then((obj) => {
        // 执行正常业务
        caller = obj;
        console.log('startAbilityByCall succeed');
      }).catch((error) => {
        // 处理业务逻辑错误
        console.log('startAbilityByCall failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.startAbilityWithAccount

startAbilityWithAccount(want: Want, accountId: number, callback: AsyncCallback\<void\>): void;

根据account启动UIAbility（callback形式）。

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动UIAbility的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess)。 |
| callback | AsyncCallback\<void\> | 是 | 启动UIAbility的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000006 | Can not cross user operations. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000010 | Can not operation with continue flag.        |
| 16000011 | Context does not exist.        |
| 16000051 | Network error. The network is abnormal. |
| 16000052 | Free install not support. The application does not support freeinstall |
| 16000053 | Not top ability. The application is not top ability. |
| 16000054 | Free install busyness. There are concurrent tasks, waiting for retry. |
| 16000055 | Free install timeout. |
| 16000056 | Can not free install other ability. |
| 16000057 | Not support cross device free install. |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.extreme.test',
    abilityName: 'MainAbility'
  };
  let accountId = 100;

  try {
    this.context.startAbilityWithAccount(want, accountId, (error) => {
      if (error.code) {
        // 处理业务逻辑错误
        console.log('startAbilityWithAccount failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // 执行正常业务
      console.log('startAbilityWithAccount succeed');
    });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```


## UIAbilityContext.startAbilityWithAccount

startAbilityWithAccount(want: Want, accountId: number, options: StartOptions, callback: AsyncCallback\<void\>): void;

根据account启动UIAbility（callback形式）。

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动UIAbility的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess)。|
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 否 | 启动UIAbility所携带的参数。 |
| callback | AsyncCallback\<void\> | 是 | 启动UIAbility的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000006 | Can not cross user operations. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000010 | Can not operation with continue flag.        |
| 16000011 | Context does not exist.        |
| 16000051 | Network error. The network is abnormal. |
| 16000052 | Free install not support. The application does not support freeinstall |
| 16000053 | Not top ability. The application is not top ability. |
| 16000054 | Free install busyness. There are concurrent tasks, waiting for retry. |
| 16000055 | Free install timeout. |
| 16000056 | Can not free install other ability. |
| 16000057 | Not support cross device free install. |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.extreme.test',
    abilityName: 'MainAbility'
  };
  let accountId = 100;
  let options = {
    windowMode: 0
  };

  try {
    this.context.startAbilityWithAccount(want, accountId, options, (error) => {
      if (error.code) {
        // 处理业务逻辑错误
        console.log('startAbilityWithAccount failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // 执行正常业务
      console.log('startAbilityWithAccount succeed');
    });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```


## UIAbilityContext.startAbilityWithAccount

startAbilityWithAccount(want: Want, accountId: number, options?: StartOptions): Promise\<void\>;

根据account启动UIAbility（Promise形式）。

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动UIAbility的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess)。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 否 | 启动UIAbility所携带的参数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 201 | The application does not have permission to call the interface. |
| 401 | Invalid input parameter. |
| 16000001 | Input error. The specified ability name does not exist. |
| 16000004 | Visibility verification failed. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000006 | Can not cross user operations. |
| 16000007 | Service busyness. There are concurrent tasks, waiting for retry. |
| 16000008 | Crowdtest App Expiration. |
| 16000009 | Can not start ability in wukong mode. |
| 16000010 | Can not operation with continue flag.        |
| 16000011 | Context does not exist.        |
| 16000051 | Network error. The network is abnormal. |
| 16000052 | Free install not support. The application does not support freeinstall |
| 16000053 | Not top ability. The application is not top ability. |
| 16000054 | Free install busyness. There are concurrent tasks, waiting for retry. |
| 16000055 | Free install timeout. |
| 16000056 | Can not free install other ability. |
| 16000057 | Not support cross device free install. |
| 16200001 | Caller released. The caller has been released. |
| 16000050 | Internal Error. |

**示例：**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.extreme.test',
    abilityName: 'MainAbility'
  };
  let accountId = 100;
  let options = {
    windowMode: 0
  };

  try {
    this.context.startAbilityWithAccount(want, accountId, options)
      .then((data) => {
        // 执行正常业务
        console.log('startAbilityWithAccount succeed');
      })
      .catch((error) => {
        // 处理业务逻辑错误
        console.log('startAbilityWithAccount failed, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('error.code: ' + JSON.stringify(paramError.code) +
      ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.requestPermissionsFromUser

requestPermissionsFromUser(permissions: Array&lt;string&gt;, requestCallback: AsyncCallback&lt;PermissionRequestResult&gt;) : void;

拉起弹窗请求用户授权（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| permissions | Array&lt;string&gt; | 是 | 权限列表。 |
| callback | AsyncCallback&lt;[PermissionRequestResult](js-apis-inner-application-permissionRequestResult.md)&gt; | 是 | 回调函数，返回接口调用是否成功的结果。 |

**示例：**

  ```ts
       let permissions=['com.example.permission']
       this.context.requestPermissionsFromUser(permissions,(result) => {
       console.log('requestPermissionsFromUserresult:' + JSON.stringify(result));
  });

  ```


## UIAbilityContext.requestPermissionsFromUser

requestPermissionsFromUser(permissions: Array&lt;string&gt;) : Promise&lt;PermissionRequestResult&gt;;

拉起弹窗请求用户授权（promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| permissions | Array&lt;string&gt; | 是 | 权限列表。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;[PermissionRequestResult](js-apis-inner-application-permissionRequestResult.md)&gt; | 返回一个Promise，包含接口的结果。 |

**示例：**

  ```ts
   let permissions=['com.example.permission']
       this.context.requestPermissionsFromUser(permissions).then((data) => {
      console.log('success:' + JSON.stringify(data));
  }).catch((error) => {
      console.log('failed:' + JSON.stringify(error));
  });

  ```


## UIAbilityContext.setMissionLabel

setMissionLabel(label: string, callback:AsyncCallback&lt;void&gt;): void;

设置UIAbility在任务中显示的名称（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| label | string | 是 | 显示名称。 |
| callback | AsyncCallback&lt;void&gt; | 是 | 回调函数，返回接口调用是否成功的结果。 |

**示例：**

  ```ts
  this.context.setMissionLabel('test',(result) => {
      console.log('requestPermissionsFromUserresult:' + JSON.stringify(result));
  });
  ```


## UIAbilityContext.setMissionLabel

setMissionLabel(label: string): Promise&lt;void&gt;;

设置UIAbility在任务中显示的名称（promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| label | string | 是 | 显示名称。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;void&gt; | 返回一个Promise，包含接口的结果。 |

**示例：**

  ```ts
  this.context.setMissionLabel('test').then(() => {
      console.log('success');
  }).catch((error) => {
      console.log('failed:' + JSON.stringify(error));
  });
  ```
## UIAbilityContext.setMissionIcon

setMissionIcon(icon: image.PixelMap, callback:AsyncCallback\<void>): void;

设置当前UIAbility在任务中显示的图标（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| icon | image.PixelMap | 是 | 在最近的任务中显示的UIAbility图标。 |
| callback | AsyncCallback\<void> | 是 | 指定的回调函数的结果。 |

**示例：**

  ```ts
    import image from '@ohos.multimedia.image';
    let imagePixelMap;
    let color = new ArrayBuffer(0);
    let initializationOptions = {
       size: {
           height: 100,
           width: 100
       }
    };
    image.createPixelMap(color, initializationOptions)
       .then((data) => {
           imagePixelMap = data;
       })
       .catch((err) => {
           console.log('--------- createPixelMap fail, err: ---------', err)
       });
    this.context.setMissionIcon(imagePixelMap, (err) => {
       console.log('---------- setMissionIcon fail, err: -----------', err);
    })
  ```


## UIAbilityContext.setMissionIcon

setMissionIcon(icon: image.PixelMap): Promise\<void>;

设置当前UIAbility在任务中显示的图标（promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| icon | image.PixelMap | 是 | 在最近的任务中显示的UIAbility图标。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;void&gt; | 返回一个Promise，包含接口的结果。 |

**示例：**

  ```ts
    import image from '@ohos.multimedia.image';
    let imagePixelMap;
    let color = new ArrayBuffer(0);
    let initializationOptions = {
      size: {
          height: 100,
          width: 100
      }
    };
    image.createPixelMap(color, initializationOptions)
      .then((data) => {
          imagePixelMap = data;
      })
      .catch((err) => {
          console.log('--------- createPixelMap fail, err: ---------', err)
      });
    this.context.setMissionIcon(imagePixelMap)
      .then(() => {
          console.log('-------------- setMissionIcon success -------------');
      })
      .catch((err) => {
          console.log('-------------- setMissionIcon fail, err: -------------', err);
      });
  ```
## UIAbilityContext.restoreWindowStage

restoreWindowStage(localStorage: LocalStorage) : void;

恢复UIAbility中的window stage数据。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| localStorage | image.LocalStorage | 是 | 用于恢复window stage的存储数据。 |

**示例：**

  ```ts
    let storage = new LocalStorage();
    this.context.restoreWindowStage(storage);
  ```

## UIAbilityContext.isTerminating

isTerminating(): boolean;

查询UIAbility是否在terminating状态。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| bool | true：UIAbility当前处于terminating状态；false：不处于terminating状态。 |

**示例：**

  ```ts
  let isTerminating = this.context.isTerminating();
  console.log('ability state :' + isTerminating);
  ```
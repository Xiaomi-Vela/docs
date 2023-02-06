# UIAbilityContext

UIAbilityContext是[UIAbility](js-apis-app-ability-uiAbility.md)的上下文环境，继承自[Context](js-apis-inner-application-context.md)，提供UIAbility的相关配置信息以及操作UIAbility和ServiceExtensionAbility的方法，如启动UIAbility，停止当前UIAbilityContext所属的UIAbility，启动、停止、连接、断开连接ServiceExtensionAbility等。

> **说明：**
>
>  - 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>  - 本模块接口仅可在Stage模型下使用。

## 属性

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

| 名称 | 类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| abilityInfo | [AbilityInfo](js-apis-bundleManager-abilityInfo.md) | 是 | 否 | UIAbility的相关信息。 |
| currentHapModuleInfo | [HapModuleInfo](js-apis-bundleManager-hapModuleInfo.md) | 是 | 否 | 当前HAP的信息。 |
| config | [Configuration](js-apis-app-ability-configuration.md) | 是 | 否 | 与UIAbility相关的配置信息，如语言、颜色模式等。 |

> **关于示例代码的说明：**
> - 本文档中的示例，通过this.context获取UIAbilityContext，this代表的是继承自UIAbility的UIAbility实例，若需要在页面中使用UIAbilityContext的能力，请参照[获取UIAbility的上下文信息](../../application-models/uiability-usage.md#获取uiability的上下文信息)

## UIAbilityContext.startAbility

startAbility(want: Want, callback: AsyncCallback&lt;void&gt;): void;

启动Ability（callback形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的visible属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| callback | AsyncCallback&lt;void&gt; | 是 | callback形式返回启动结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
  let want = {
    bundleName: "com.example.myapp",
    abilityName: "MyAbility"
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
    console.log('startAbility failed, error.code: ' + JSON.stringify(paramError.code) +
    ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.startAbility

startAbility(want: Want, options: StartOptions, callback: AsyncCallback&lt;void&gt;): void;

启动Ability（callback形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的visible属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md)  | 是 | 启动Ability的want信息。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 是 | 启动Ability所携带的参数。 |
| callback | AsyncCallback&lt;void&gt; | 是 | callback形式返回启动结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
  let want = {
    deviceId: "",
    bundleName: "com.example.myapplication",
    abilityName: "EntryAbility"
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
    console.log('startAbility failed, error.code: ' + JSON.stringify(paramError.code) +
    ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.startAbility

startAbility(want: Want, options?: StartOptions): Promise&lt;void&gt;;

启动Ability（promise形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的visible属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 否 | 启动Ability所携带的参数。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;void&gt; | Promise形式返回启动结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
  let want = {
    bundleName: "com.example.myapp",
    abilityName: "MyAbility"
  };
  let options = {
    windowMode: 0,
  };

  try {
    this.context.startAbility(want, options)
      .then(() => {
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
    console.log('startAbility failed, error.code: ' + JSON.stringify(paramError.code) +
    ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.startAbilityForResult

startAbilityForResult(want: Want, callback: AsyncCallback&lt;AbilityResult&gt;): void;

启动一个Ability。Ability被启动后，正常情况下可通过调用[terminateSelfWithResult](#uiabilitycontextterminateselfwithresult)接口使之终止并且返回结果给调用者。如果被启动的Ability模式是单实例模式, 不同应用多次调用该接口, 返回正常结果给最后一个调用方, 其它调用方返回错误信息, 错误信息中resultCode为-1（callback形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的visible属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want |[Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| callback | AsyncCallback&lt;[AbilityResult](js-apis-inner-ability-abilityResult.md)&gt; | 是 | 执行结果回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
  let want = {
    deviceId: "",
    bundleName: "com.example.myapplication",
    abilityName: "EntryAbility"
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
      console.log("startAbilityForResult succeed, result.resultCode = " + result.resultCode)
    });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('startAbilityForResult failed, error.code: ' + JSON.stringify(paramError.code) +
    ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.startAbilityForResult

startAbilityForResult(want: Want, options: StartOptions, callback: AsyncCallback&lt;AbilityResult&gt;): void;

启动一个Ability。Ability被启动后，正常情况下可通过调用[terminateSelfWithResult](#uiabilitycontextterminateselfwithresult)接口使之终止并且返回结果给调用者。如果被启动的Ability模式是单实例模式, 不同应用多次调用该接口, 返回正常结果给最后一个调用方, 其它调用方返回错误信息, 错误信息中resultCode为-1（callback形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的visible属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want |[Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 是 | 启动Ability所携带的参数。 |
| callback | AsyncCallback&lt;[AbilityResult](js-apis-inner-ability-abilityResult.md)&gt; | 是 | 执行结果回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
  let want = {
    deviceId: "",
    bundleName: "com.example.myapplication",
    abilityName: "EntryAbility"
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
      console.log("startAbilityForResult succeed, result.resultCode = " + result.resultCode)
    });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('startAbilityForResult failed, error.code: ' + JSON.stringify(paramError.code) +
    ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```


## UIAbilityContext.startAbilityForResult

startAbilityForResult(want: Want, options?: StartOptions): Promise&lt;AbilityResult&gt;;

启动一个Ability。Ability被启动后，正常情况下可通过调用[terminateSelfWithResult](#uiabilitycontextterminateselfwithresult)接口使之终止并且返回结果给调用者。如果被启动的Ability模式是单实例模式, 不同应用多次调用该接口, 返回正常结果给最后一个调用方, 其它调用方返回错误信息, 错误信息中resultCode为-1（promise形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的visible属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 否 | 启动Ability所携带的参数。 |


**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;[AbilityResult](js-apis-inner-ability-abilityResult.md)&gt; | Promise形式返回执行结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
let want = {
    bundleName: "com.example.myapplication",
    abilityName: "EntryAbility"
};
let options = {
    windowMode: 0,
};

try {
    this.context.startAbilityForResult(want, options)
        .then((result) => {
        // 执行正常业务
        console.log("startAbilityForResult succeed, result.resultCode = " + result.resultCode);
    })
        .catch((error) => {
        // 处理业务逻辑错误
        console.log('startAbilityForResult failed, error.code: ' + JSON.stringify(error.code) +
                    ' error.message: ' + JSON.stringify(error.message));
    });
} catch (paramError) {
    // 处理入参错误异常
    console.log('startAbilityForResult failed, error.code: ' + JSON.stringify(paramError.code) +
                ' error.message: ' + JSON.stringify(paramError.message));
}
  ```

## UIAbilityContext.startAbilityForResultWithAccount

startAbilityForResultWithAccount(want: Want, accountId: number, callback: AsyncCallback\<AbilityResult>): void;

启动一个Ability并在该Ability销毁时返回执行结果（callback形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的visible属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS，当accountId为当前用户时，不需要校验该权限。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getCreatedOsAccountsCount)。 |
| callback | AsyncCallback&lt;[AbilityResult](js-apis-inner-ability-abilityResult.md)&gt; | 是 | 启动Ability的回调函数，返回Ability结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
  let want = {
    deviceId: "",
    bundleName: "com.example.myapplication",
    abilityName: "EntryAbility"
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
      console.log("startAbilityForResultWithAccount succeed, result.resultCode = " +
      result.resultCode + ' result.want = ' + JSON.stringify(result.want))
    });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('startAbilityForResultWithAccount failed, error.code: ' + JSON.stringify(paramError.code) +
    ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```


## UIAbilityContext.startAbilityForResultWithAccount

startAbilityForResultWithAccount(want: Want, accountId: number, options: StartOptions, callback: AsyncCallback\<void\>): void;

启动一个Ability并在该Ability销毁时返回执行结果（callback形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的visible属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS，当accountId为当前用户时，不需要校验该权限。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getCreatedOsAccountsCount)。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 是 | 启动Ability所携带的参数。 |
| callback | AsyncCallback\<void\> | 是 | 启动Ability后，Ability被销毁时的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
  let want = {
    deviceId: "",
    bundleName: "com.example.myapplication",
    abilityName: "EntryAbility"
  };
  let accountId = 100;
  let options = {
    windowMode: 0
  };

  try {
    this.context.startAbilityForResultWithAccount(want, accountId, options, (error) => {
      if (error.code) {
        // 处理业务逻辑错误
        console.log('startAbilityForResultWithAccount failed, error.code: ' + JSON.stringify(error.code) +
        ' error.message: ' + JSON.stringify(error.message));
        return;
      }
      // 执行正常业务
      console.log("startAbilityForResultWithAccount succeed")
    });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('startAbilityForResultWithAccount failed, error.code: ' + JSON.stringify(paramError.code) +
    ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```


## UIAbilityContext.startAbilityForResultWithAccount

startAbilityForResultWithAccount(want: Want, accountId: number, options?: StartOptions): Promise\<AbilityResult\>;

启动一个Ability并在该Ability销毁时返回执行结果（promise形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的visible属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS，当accountId为当前用户时，不需要校验该权限。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getCreatedOsAccountsCount)。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 否 | 启动Ability所携带的参数。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;[AbilityResult](js-apis-inner-ability-abilityResult.md)&gt; | Ability被销毁时的回调函数，包含AbilityResult参数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
  let want = {
    deviceId: "",
    bundleName: "com.example.myapplication",
    abilityName: "EntryAbility"
  };
  let accountId = 100;
  let options = {
    windowMode: 0
  };

  try {
    this.context.startAbilityForResultWithAccount(want, accountId, options)
      .then((result) => {
        // 执行正常业务
        console.log("startAbilityForResultWithAccount succeed, result.resultCode = " +
        result.resultCode)
      })
      .catch((error) => {
        // 处理业务逻辑错误
        console.log('startAbilityForResultWithAccount failed, error.code: ' + JSON.stringify(error.code) +
        ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (paramError) {
    // 处理入参错误异常
    console.log('startAbilityForResultWithAccount failed, error.code: ' + JSON.stringify(paramError.code) +
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
| want | [Want](js-apis-application-want.md) | 是 | 启动ServiceExtensionAbility的want信息。 |
| callback | AsyncCallback\<void\> | 是 | 启动ServiceExtensionAbility的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
  let want = {
    deviceId: "",
    bundleName: "com.example.myapplication",
    abilityName: "ServiceExtensionAbility"
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
    console.log('startServiceExtensionAbility failed, error.code: ' + JSON.stringify(paramError.code) +
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
| want | [Want](js-apis-application-want.md) | 是 | 启动ServiceExtensionAbility的want信息。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
  let want = {
    deviceId: "",
    bundleName: "com.example.myapplication",
    abilityName: "ServiceExtensionAbility"
  };

  try {
    this.context.startServiceExtensionAbility(want)
      .then(() => {
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
    console.log('startServiceExtensionAbility failed, error.code: ' + JSON.stringify(paramError.code) +
    ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.startServiceExtensionAbilityWithAccount

startServiceExtensionAbilityWithAccount(want: Want, accountId: number, callback: AsyncCallback\<void>): void;

启动一个新的ServiceExtensionAbility（callback形式）。

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS，当accountId为当前用户时，不需要校验该权限。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动ServiceExtensionAbility的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getCreatedOsAccountsCount)。 |
| callback | AsyncCallback\<void\> | 是 | 启动ServiceExtensionAbility的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
  let want = {
    deviceId: "",
    bundleName: "com.example.myapplication",
    abilityName: "ServiceExtensionAbility"
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
    console.log('startServiceExtensionAbilityWithAccount failed, error.code: ' + JSON.stringify(paramError.code) +
    ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.startServiceExtensionAbilityWithAccount

startServiceExtensionAbilityWithAccount(want: Want, accountId: number): Promise\<void>;

启动一个新的ServiceExtensionAbility（Promise形式）。

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS，当accountId为当前用户时，不需要校验该权限。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getCreatedOsAccountsCount)。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
  let want = {
    deviceId: "",
    bundleName: "com.example.myapplication",
    abilityName: "ServiceExtensionAbility"
  };
  let accountId = 100;

  try {
    this.context.startServiceExtensionAbilityWithAccount(want, accountId)
      .then(() => {
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
    console.log('startServiceExtensionAbilityWithAccount failed, error.code: ' + JSON.stringify(paramError.code) +
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
| want | [Want](js-apis-application-want.md) | 是 | 停止ServiceExtensionAbility的want信息。 |
| callback | AsyncCallback\<void\> | 是 | 停止ServiceExtensionAbility的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
  let want = {
    deviceId: "",
    bundleName: "com.example.myapplication",
    abilityName: "ServiceExtensionAbility"
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
    console.log('stopServiceExtensionAbility failed, error.code: ' + JSON.stringify(paramError.code) +
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
| want | [Want](js-apis-application-want.md) | 是 | 停止ServiceExtensionAbility的want信息。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
  let want = {
    deviceId: "",
    bundleName: "com.example.myapplication",
    abilityName: "ServiceExtensionAbility"
  };

  try {
    this.context.stopServiceExtensionAbility(want)
      .then(() => {
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
    console.log('stopServiceExtensionAbility failed, error.code: ' + JSON.stringify(paramError.code) +
    ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.stopServiceExtensionAbilityWithAccount

stopServiceExtensionAbilityWithAccount(want: Want, accountId: number, callback: AsyncCallback\<void>): void;

停止同一应用程序内指定账户的服务（callback形式）。

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS，当accountId为当前用户时，不需要校验该权限。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 停止ServiceExtensionAbility的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getCreatedOsAccountsCount)。 |
| callback | AsyncCallback\<void\> | 是 | 停止ServiceExtensionAbility的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
  let want = {
    deviceId: "",
    bundleName: "com.example.myapplication",
    abilityName: "ServiceExtensionAbility"
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
    console.log('stopServiceExtensionAbilityWithAccount failed, error.code: ' + JSON.stringify(paramError.code) +
    ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.stopServiceExtensionAbilityWithAccount

stopServiceExtensionAbilityWithAccount(want: Want, accountId: number): Promise\<void>;

停止同一应用程序内指定账户的服务（Promise形式）。

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS，当accountId为当前用户时，不需要校验该权限。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 停止ServiceExtensionAbility的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getCreatedOsAccountsCount)。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
  let want = {
    deviceId: "",
    bundleName: "com.example.myapplication",
    abilityName: "ServiceExtensionAbility"
  };
  let accountId = 100;

  try {
    this.context.stopServiceExtensionAbilityWithAccount(want, accountId)
      .then(() => {
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
    console.log('stopServiceExtensionAbilityWithAccount failed, error.code: ' + JSON.stringify(paramError.code) +
    ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.terminateSelf

terminateSelf(callback: AsyncCallback&lt;void&gt;): void;

停止Ability自身（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;void&gt; | 是 | 停止Ability自身的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

**示例：**

  ```ts
  try {
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
  } catch (error) {
    // 捕获同步的参数错误
    console.log('terminateSelf failed, error.code: ' + JSON.stringify(error.code) +
      ' error.message: ' + JSON.stringify(error.message));
  }
  ```


## UIAbilityContext.terminateSelf

terminateSelf(): Promise&lt;void&gt;;

停止Ability自身（promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;void&gt; | 停止Ability自身的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

**示例：**

  ```ts
  try {
    this.context.terminateSelf()
      .then(() => {
        // 执行正常业务
        console.log('terminateSelf succeed');
      })
      .catch((error) => {
        // 处理业务逻辑错误
        console.log('terminateSelf failed, error.code: ' + JSON.stringify(error.code) +
        ' error.message: ' + JSON.stringify(error.message));
      });
  } catch (error) {
    // 捕获同步的参数错误
    console.log('terminateSelf failed, error.code: ' + JSON.stringify(error.code) +
    ' error.message: ' + JSON.stringify(error.message));
  }
  ```


## UIAbilityContext.terminateSelfWithResult

terminateSelfWithResult(parameter: AbilityResult, callback: AsyncCallback&lt;void&gt;): void;

停止当前的Ability。如果该Ability是通过调用[startAbilityForResult](#uiabilitycontextstartabilityforresult)接口被拉起的，调用terminateSelfWithResult接口时会将结果返回给调用者，如果该Ability不是通过调用[startAbilityForResult](#uiabilitycontextstartabilityforresult)接口被拉起的，调用terminateSelfWithResult接口时不会有结果返回给调用者（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| parameter | [AbilityResult](js-apis-inner-ability-abilityResult.md) | 是 | 返回给调用startAbilityForResult&nbsp;接口调用方的相关信息。 |
| callback | AsyncCallback&lt;void&gt; | 是 | callback形式返回停止结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

**示例：**

  ```ts
  let want = {
    bundleName: "com.example.myapplication",
    abilityName: "EntryAbility"
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
    console.log('terminateSelfWithResult failed, error.code: ' + JSON.stringify(paramError.code) +
    ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```


## UIAbilityContext.terminateSelfWithResult

terminateSelfWithResult(parameter: AbilityResult): Promise&lt;void&gt;;

停止当前的Ability。如果该Ability是通过调用[startAbilityForResult](#uiabilitycontextstartabilityforresult)接口被拉起的，调用terminateSelfWithResult接口时会将结果返回给调用者，如果该Ability不是通过调用[startAbilityForResult](#uiabilitycontextstartabilityforresult)接口被拉起的，调用terminateSelfWithResult接口时不会有结果返回给调用者（promise形式）。

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
| 16000001 | The specified ability does not exist. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

**示例：**

  ```ts
  let want = {
    bundleName: "com.example.myapplication",
    abilityName: "EntryAbility"
  }
  let resultCode = 100;
  // 返回给接口调用方AbilityResult信息
  let abilityResult = {
    want,
    resultCode
  }

  try {
    this.context.terminateSelfWithResult(abilityResult)
      .then(() => {
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
    console.log('terminateSelfWithResult failed, error.code: ' + JSON.stringify(paramError.code) +
    ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.connectServiceExtensionAbility

connectServiceExtensionAbility(want: Want, options: ConnectOptions): number;

将当前Ability连接到一个使用AbilityInfo.AbilityType.SERVICE模板的Ability。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 连接ServiceExtensionAbility的want信息。 |
| options | [ConnectOptions](js-apis-inner-ability-connectOptions.md) | 是 | 与ServiceExtensionAbility建立连接后回调函数的实例。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回Ability连接的结果code。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000005 | The specified process does not have the permission. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

**示例：**

  ```ts
  let want = {
    deviceId: "",
    bundleName: "com.example.myapplication",
    abilityName: "ServiceExtensionAbility"
  };
  let options = {
    onConnect(elementName, remote) {
      console.log('----------- onConnect -----------')
    },
    onDisconnect(elementName) {
      console.log('----------- onDisconnect -----------')
    },
    onFailed(code) {
      console.log('----------- onFailed -----------')
    }
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

将当前Ability连接到一个使用AbilityInfo.AbilityType.SERVICE模板的指定account的Ability。

**需要权限：** ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS，当accountId为当前用户时，不需要校验该权限。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getCreatedOsAccountsCount)。 |
| options | [ConnectOptions](js-apis-inner-ability-connectOptions.md) | 是 | 与ServiceExtensionAbility建立连接后回调函数的实例。。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回Ability连接的结果code。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000005 | The specified process does not have the permission. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

**示例：**

  ```ts
  let want = {
    deviceId: "",
    bundleName: "com.example.myapplication",
    abilityName: "ServiceExtensionAbility"
  };
  let accountId = 100;
  let options = {
    onConnect(elementName, remote) {
      console.log('----------- onConnect -----------')
    },
    onDisconnect(elementName) {
      console.log('----------- onDisconnect -----------')
    },
    onFailed(code) {
      console.log('----------- onFailed -----------')
    }
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

断开与ServiceExtensionAbility的连接（promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| connection | number | 是 | 连接的ServiceExtensionAbility的数字代码，即connectServiceExtensionAbility返回的connectionId。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise\<void> | 返回执行结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000005 | The specified process does not have the permission. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

**示例：**

  ```ts
  // connection为connectServiceExtensionAbility中的返回值
  let connection = 1;

  try {
    this.context.disconnectServiceExtensionAbility(connection)
      .then(() => {
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

断开与ServiceExtensionAbility的连接（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| connection | number | 是 | 连接的ServiceExtensionAbility的数字代码，即connectServiceExtensionAbility返回的connectionId。 |
| callback | AsyncCallback\<void> | 是 | callback形式返回断开连接的结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000005 | The specified process does not have the permission. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

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

启动指定Ability至前台或后台，同时获取其Caller通信接口，调用方可使用Caller与被启动的Ability进行通信。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的visible属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 同设备与跨设备场景下，该接口的使用规则存在差异，详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 传入需要启动的Ability的信息，包含abilityName、moduleName、bundleName、deviceId(可选)、parameters(可选)，其中deviceId缺省或为空表示启动本地Ability，parameters缺省或为空表示后台启动Ability。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;Caller&gt; | 获取要通讯的caller对象。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

**示例：**

  后台启动：

  ```ts
  let caller = undefined;

  // 后台启动Ability，不配置parameters
  let wantBackground = {
    bundleName: "com.example.myservice",
    moduleName: "entry",
    abilityName: "EntryAbility",
    deviceId: ""
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

  // 前台启动Ability，将parameters中的"ohos.aafwk.param.callAbilityToForeground"配置为true
  let wantForeground = {
    bundleName: "com.example.myservice",
    moduleName: "entry",
    abilityName: "EntryAbility",
    deviceId: "",
    parameters: {
      "ohos.aafwk.param.callAbilityToForeground": true
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

根据want和accountId启动Ability（callback形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的visible属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS，当accountId为当前用户时，不需要校验该权限。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getCreatedOsAccountsCount)。 |
| callback | AsyncCallback\<void\> | 是 | 启动Ability的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
  let want = {
    deviceId: "",
    bundleName: "com.example.myapplication",
    abilityName: "EntryAbility"
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

根据want、accountId及startOptions启动Ability（callback形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的visible属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS，当accountId为当前用户时，不需要校验该权限。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getCreatedOsAccountsCount)。|
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 是 | 启动Ability所携带的参数。 |
| callback | AsyncCallback\<void\> | 是 | 启动Ability的回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
  let want = {
    deviceId: "",
    bundleName: "com.example.myapplication",
    abilityName: "EntryAbility"
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
    console.log('startAbilityWithAccount failed, error.code: ' + JSON.stringify(paramError.code) +
    ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```


## UIAbilityContext.startAbilityWithAccount

startAbilityWithAccount(want: Want, accountId: number, options?: StartOptions): Promise\<void\>;

根据want、accountId和startOptions启动Ability（Promise形式）。

使用规则：
 - 调用方应用位于后台时，使用该接口启动Ability需申请`ohos.permission.START_ABILITIES_FROM_BACKGROUND`权限
 - 跨应用场景下，目标Ability的visible属性若配置为false，调用方应用需申请`ohos.permission.START_INVISIBLE_ABILITY`权限
 - 组件启动规则详见：[组件启动规则（Stage模型）](../../application-models/component-startup-rules.md)

**需要权限**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS，当accountId为当前用户时，不需要校验该权限。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | 是 | 启动Ability的want信息。 |
| accountId | number | 是 | 系统帐号的帐号ID，详情参考[getCreatedOsAccountsCount](js-apis-osAccount.md#getCreatedOsAccountsCount)。 |
| options | [StartOptions](js-apis-app-ability-startOptions.md) | 否 | 启动Ability所携带的参数。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

**示例：**

  ```ts
  let want = {
    deviceId: "",
    bundleName: "com.example.myapplication",
    abilityName: "EntryAbility"
  };
  let accountId = 100;
  let options = {
    windowMode: 0
  };

  try {
    this.context.startAbilityWithAccount(want, accountId, options)
      .then(() => {
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
    console.log('startAbilityWithAccount failed, error.code: ' + JSON.stringify(paramError.code) +
    ' error.message: ' + JSON.stringify(paramError.message));
  }
  ```

## UIAbilityContext.setMissionLabel

setMissionLabel(label: string, callback:AsyncCallback&lt;void&gt;): void;

设置ability在任务中显示的名称（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| label | string | 是 | 显示名称。 |
| callback | AsyncCallback&lt;void&gt; | 是 | 回调函数，返回接口调用是否成功的结果。 |

**示例：**

  ```ts
  this.context.setMissionLabel("test", (result) => {
    console.log('setMissionLabel:' + JSON.stringify(result));
  });
  ```

## UIAbilityContext.setMissionLabel

setMissionLabel(label: string): Promise&lt;void&gt;;

设置ability在任务中显示的名称（promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| label | string | 是 | 显示名称。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;void&gt; | 返回一个Promise，包含接口的结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

**示例：**

  ```ts
  this.context.setMissionLabel("test").then(() => {
    console.log('success');
  }).catch((error) => {
    console.log('failed:' + JSON.stringify(error));
  });
  ```
## UIAbilityContext.setMissionIcon

setMissionIcon(icon: image.PixelMap, callback:AsyncCallback\<void>): void;

设置当前ability在任务中显示的图标（callback形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| icon | image.PixelMap | 是 | 在最近的任务中显示的ability图标。 |
| callback | AsyncCallback\<void> | 是 | 指定的回调函数的结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

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

设置当前ability在任务中显示的图标（promise形式）。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| icon | image.PixelMap | 是 | 在最近的任务中显示的ability图标。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;void&gt; | 返回一个Promise，包含接口的结果。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

**示例：**

  ```ts
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

恢复ability中的window stage数据。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| localStorage | image.LocalStorage | 是 | 用于恢复window stage的存储数据。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

**示例：**

  ```ts
  let storage = new LocalStorage();
  this.context.restoreWindowStage(storage);
  ```

## UIAbilityContext.isTerminating

isTerminating(): boolean;

查询ability是否在terminating状态。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| bool | true：ability当前处于terminating状态；false：不处于terminating状态。 |

**错误码：**

| 错误码ID | 错误信息 |
| ------- | -------------------------------- |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |

**示例：**

  ```ts
  let isTerminating = this.context.isTerminating();
  console.log('ability state :' + isTerminating);
  ```

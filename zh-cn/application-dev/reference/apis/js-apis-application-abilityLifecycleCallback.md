# @ohos.application.AbilityLifecycleCallback (AbilityLifecycleCallback)

AbilityLifecycleCallback模块提供应用上下文ApplicationContext的生命周期监听方法的回调类的能力，包括onAbilityCreate、onWindowStageCreate、onWindowStageDestroy等方法，可以作为[on(type: 'abilityLifecycle', callback: AbilityLifecycleCallback)](js-apis-inner-application-applicationContext.md#applicationcontextontype-abilitylifecycle-callback-abilitylifecyclecallback)的入参。

> **说明：**
> 
> 本模块首批接口从API version 9 开始支持，从API version 9后续版本废弃，替换模块为[@ohos.app.ability.AbilityLifecycleCallback](js-apis-app-ability-abilityLifecycleCallback.md)。后续版本的新增接口，采用上角标单独标记接口的起始版本。  
> 本模块接口仅可在Stage模型下使用。


## 导入模块

```ts
import AbilityLifecycleCallback from '@ohos.application.AbilityLifecycleCallback';
```


## AbilityLifecycleCallback.onAbilityCreate

onAbilityCreate(ability: Ability): void;

注册监听应用上下文的生命周期后，在ability创建时触发回调。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| ability | [Ability](js-apis-application-ability.md#Ability) | 是 | 当前Ability对象 |


## AbilityLifecycleCallback.onWindowStageCreate

onWindowStageCreate(ability: Ability, windowStage: window.WindowStage): void;

注册监听应用上下文的生命周期后，在windowStage创建时触发回调。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| ability | [Ability](js-apis-application-ability.md#Ability) | 是 | 当前Ability对象 |
| windowStage | [window.WindowStage](js-apis-window.md#windowstage9) | 是 | 当前WindowStage对象 |


## AbilityLifecycleCallback.onWindowStageActive

onWindowStageActive(ability: Ability, windowStage: window.WindowStage): void;

注册监听应用上下文的生命周期后，在windowStage获焦时触发回调。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| ability | [Ability](js-apis-application-ability.md#Ability) | 是 | 当前Ability对象 |
| windowStage | [window.WindowStage](js-apis-window.md#windowstage9) | 是 | 当前WindowStage对象 |


## AbilityLifecycleCallback.onWindowStageInactive

onWindowStageInactive(ability: Ability, windowStage: window.WindowStage): void;

注册监听应用上下文的生命周期后，在windowStage失焦时触发回调。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| ability | [Ability](js-apis-application-ability.md#Ability) | 是 | 当前Ability对象 |
| windowStage | [window.WindowStage](js-apis-window.md#windowstage9) | 是 | 当前WindowStage对象 |


## AbilityLifecycleCallback.onWindowStageDestroy

onWindowStageDestroy(ability: Ability, windowStage: window.WindowStage): void;

注册监听应用上下文的生命周期后，在windowStage销毁时触发回调。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| ability | [Ability](js-apis-application-ability.md#Ability) | 是 | 当前Ability对象 |
| windowStage | [window.WindowStage](js-apis-window.md#windowstage9) | 是 | 当前WindowStage对象 |


## AbilityLifecycleCallback.onAbilityDestroy

onAbilityDestroy(ability: Ability): void;

注册监听应用上下文的生命周期后，在ability销毁时触发回调。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| ability | [Ability](js-apis-application-ability.md#Ability) | 是 | 当前Ability对象 |


## AbilityLifecycleCallback.onAbilityForeground

onAbilityForeground(ability: Ability): void;

注册监听应用上下文的生命周期后，在ability的状态从后台转到前台时触发回调。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| ability | [Ability](js-apis-application-ability.md#Ability) | 是 | 当前Ability对象 |


## AbilityLifecycleCallback.onAbilityBackground

onAbilityBackground(ability: Ability): void;

注册监听应用上下文的生命周期后，在ability的状态从前台转到后台时触发回调。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| ability | [Ability](js-apis-application-ability.md#Ability) | 是 | 当前Ability对象 |


## AbilityLifecycleCallback.onAbilityContinue

onAbilityContinue(ability: Ability): void;

注册监听应用上下文的生命周期后，在ability迁移时触发回调。

**系统能力**：SystemCapability.Ability.AbilityRuntime.AbilityCore

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| ability | [Ability](js-apis-application-ability.md#Ability) | 是 | 当前Ability对象 |

**示例：**

```ts
import AbilityStage from '@ohos.app.ability.AbilityStage';

let lifecycleId;

export default class MyAbilityStage extends AbilityStage {
    onCreate() {
        console.log('MyAbilityStage onCreate')
        let AbilityLifecycleCallback = {
            onAbilityCreate(ability) {
                console.log('onAbilityCreate ability:' + JSON.stringify(ability));
            },
            onWindowStageCreate(ability, windowStage) {
                console.log('onWindowStageCreate ability:' + JSON.stringify(ability));
                console.log('onWindowStageCreate windowStage:' + JSON.stringify(windowStage));
            },
            onWindowStageActive(ability, windowStage) {
                console.log('onWindowStageActive ability:' + JSON.stringify(ability));
                console.log('onWindowStageActive windowStage:' + JSON.stringify(windowStage));
            },
            onWindowStageInactive(ability, windowStage) {
                console.log('onWindowStageInactive ability:' + JSON.stringify(ability));
                console.log('onWindowStageInactive windowStage:' + JSON.stringify(windowStage));
            },
            onWindowStageDestroy(ability, windowStage) {
                console.log('onWindowStageDestroy ability:' + JSON.stringify(ability));
                console.log('onWindowStageDestroy windowStage:' + JSON.stringify(windowStage));
            },
            onAbilityDestroy(ability) {
                console.log('onAbilityDestroy ability:' + JSON.stringify(ability));
            },
            onAbilityForeground(ability) {
                console.log('onAbilityForeground ability:' + JSON.stringify(ability));
            },
            onAbilityBackground(ability) {
                console.log('onAbilityBackground ability:' + JSON.stringify(ability));
            },
            onAbilityContinue(ability) {
                console.log('onAbilityContinue ability:' + JSON.stringify(ability));
            }
        }
        // 1.通过context属性获取applicationContext
        let applicationContext = this.context.getApplicationContext();
        // 2.通过applicationContext注册监听应用内生命周期
        lifecycleId = applicationContext.registerAbilityLifecycleCallback(AbilityLifecycleCallback);
        console.log('registerAbilityLifecycleCallback number: ' + JSON.stringify(lifecycleId));
    }

    onDestroy() {
        let applicationContext = this.context.getApplicationContext();
        applicationContext.unregisterAbilityLifecycleCallback(lifecycleId, (error, data) => {
            console.log('unregisterAbilityLifecycleCallback success, err: ' + JSON.stringify(error));
        });
    }
}
```
<!--no_check-->
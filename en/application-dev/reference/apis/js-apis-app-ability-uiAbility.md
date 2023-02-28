# @ohos.app.ability.UIAbility (UIAbility)

The **Ability** module manages the ability lifecycle and context, such as creating and destroying an ability, and dumping client information.

This module provides the following common ability-related functions:
- [Caller](#caller): implements sending of sequenceable data to the target ability when an ability (caller ability) invokes the target ability (callee ability).
- [Callee](#callee): implements callbacks for registration and deregistration of caller notifications.

> **NOTE**
> 
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version. 
> The APIs of this module can be used only in the stage model.

## Modules to Import

```ts
import Ability from '@ohos.app.ability.UIAbility';
```

## Attributes

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

| Name| Type| Readable| Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| context | [UIAbilityContext](js-apis-inner-application-uiAbilityContext.md) | Yes| No| Context of the ability.|
| launchWant | [Want](js-apis-app-ability-want.md) | Yes| No| Parameters for starting the ability.|
| lastRequestWant | [Want](js-apis-app-ability-want.md) | Yes| No| Parameters used when the ability was started last time.|
| callee | [Callee](#callee) | Yes| No| Object that invokes the stub service.|

## Ability.onCreate

onCreate(want: Want, param: AbilityConstant.LaunchParam): void;

Called to initialize the service logic when an ability is created.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-app-ability-want.md) | Yes| Information related to this ability, including the ability name and bundle name.|
| param | [AbilityConstant.LaunchParam](js-apis-app-ability-abilityConstant.md#abilityconstantlaunchparam) | Yes| Parameters for starting the ability, and the reason for the last abnormal exit.|

**Example**

  ```ts
  class myAbility extends Ability {
      onCreate(want, param) {
          console.log('onCreate, want:' + want.abilityName);
      }
  }
  ```


## Ability.onWindowStageCreate

onWindowStageCreate(windowStage: window.WindowStage): void

Called when a **WindowStage** is created for this ability.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| windowStage | [window.WindowStage](js-apis-window.md#windowstage9) | Yes| **WindowStage** information.|

**Example**
    
  ```ts
  class myAbility extends Ability {
      onWindowStageCreate(windowStage) {
          console.log('onWindowStageCreate');
      }
  }
  ```


## Ability.onWindowStageDestroy

onWindowStageDestroy(): void

Called when the **WindowStage** is destroyed for this ability.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Example**
    
  ```ts
  class myAbility extends Ability {
      onWindowStageDestroy() {
          console.log('onWindowStageDestroy');
      }
  }
  ```


## Ability.onWindowStageRestore

onWindowStageRestore(windowStage: window.WindowStage): void

Called when the **WindowStage** is restored during the migration of this ability, which is a multi-instance ability.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| windowStage | [window.WindowStage](js-apis-window.md#windowstage9) | Yes| **WindowStage** information.|

**Example**
    
  ```ts
  class myAbility extends Ability {
      onWindowStageRestore(windowStage) {
          console.log('onWindowStageRestore');
      }
  }
  ```


## Ability.onDestroy

onDestroy(): void;

Called when this ability is destroyed to clear resources.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Example**
    
  ```ts
  class myAbility extends Ability {
      onDestroy() {
          console.log('onDestroy');
      }
  }
  ```


## Ability.onForeground

onForeground(): void;

Called when this ability is switched from the background to the foreground.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Example**
    
  ```ts
  class myAbility extends Ability {
      onForeground() {
          console.log('onForeground');
      }
  }
  ```


## Ability.onBackground

onBackground(): void;

Called when this ability is switched from the foreground to the background.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Example**
    
  ```ts
  class myAbility extends Ability {
      onBackground() {
          console.log('onBackground');
      }
  }
  ```


## Ability.onContinue

onContinue(wantParam : {[key: string]: any}): AbilityConstant.OnContinueResult;

Called to save data during the ability migration preparation process.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| wantParam | {[key:&nbsp;string]:&nbsp;any} | Yes| **want** parameter.|

**Return value**

| Type| Description|
| -------- | -------- |
| [AbilityConstant.OnContinueResult](js-apis-app-ability-abilityConstant.md#abilityconstantoncontinueresult) | Continuation result.|

**Example**
    
  ```ts
  import AbilityConstant from '@ohos.app.ability.AbilityConstant';
  class MyUIAbility extends UIAbility {
      onContinue(wantParams) {
          console.log('onContinue');
          wantParams['myData'] = 'my1234567';
          return AbilityConstant.OnContinueResult.AGREE;
      }
  }
  ```


## Ability.onNewWant

onNewWant(want: Want, launchParams: AbilityConstant.LaunchParam): void;

Called when a new Want is passed in and this ability is started again.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-app-ability-want.md) | Yes| Want information, such as the ability name and bundle name.|
| launchParams | [AbilityConstant.LaunchParam](js-apis-app-ability-abilityConstant.md#abilityconstantlaunchparam) | Yes| Reason for the ability startup and the last abnormal exit.|

**Example**
    
  ```ts
   class MyUIAbility extends UIAbility {
      onNewWant(want, launchParams) {
          console.log('onNewWant, want:' + want.abilityName);
          console.log('onNewWant, launchParams:' + JSON.stringify(launchParams));
       }
   }
  ```

## Ability.onDump

onDump(params: Array\<string>): Array\<string>;

Dumps client information.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| params | Array\<string> | Yes| Parameters in the form of a command.|

**Example**
    
  ```ts
  class myAbility extends Ability {
      onDump(params) {
          console.log('dump, params:' + JSON.stringify(params));
          return ['params'];
      }
  }
  ```


## Ability.onSaveState

onSaveState(reason: AbilityConstant.StateType, wantParam : {[key: string]: any}): AbilityConstant.OnSaveResult;

Called when the framework automatically saves the ability state in the case of an application fault. This API is used together with [appRecovery](js-apis-app-ability-appRecovery.md). If automatic state saving is enabled, **onSaveState** is called to save the state of this ability.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| reason | [AbilityConstant.StateType](js-apis-application-abilityConstant.md#abilityconstantstatetype) | Yes| Reason for triggering the callback to save the ability state.|
| wantParam | {[key:&nbsp;string]:&nbsp;any} | Yes| **want** parameter.|

**Return value**

| Type| Description|
| -------- | -------- |
| AbilityConstant.OnSaveResult | Whether the ability state is saved.|

**Example**

  ```ts
import AbilityConstant from '@ohos.app.ability.AbilityConstant';

class MyUIAbility extends UIAbility {
    onSaveState(reason, wantParam) {
        console.log('onSaveState');
        wantParam['myData'] = 'my1234567';
        return AbilityConstant.OnSaveResult.RECOVERY_AGREE;
    }
}
  ```



## Caller

Implements sending of sequenceable data to the target ability when the CallerAbility invokes the target ability (CalleeAbility).

## Caller.call

call(method: string, data: rpc.Sequenceable): Promise&lt;void&gt;;

Sends sequenceable data to the target ability.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| method | string | Yes| Notification message string negotiated between the two abilities. The message is used to instruct the callee to register a function to receive the sequenceable data.|
| data | [rpc.Sequenceable](js-apis-rpc.md#sequenceabledeprecated) | Yes| Sequenceable data. You need to customize the data.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise used to return a response.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | If the input parameter is not valid parameter. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**
    
  ```ts
  import Ability from '@ohos.app.ability.UIAbility';
  class MyMessageAble{ // �Զ����Sequenceable���ݽṹ
    name:''
    str:''
    num: 1
    constructor(name, str) {
      this.name = name;
      this.str = str;
    }
    marshalling(messageParcel) {
      messageParcel.writeInt(this.num);
      messageParcel.writeString(this.str);
      console.log('MyMessageAble marshalling num[' + this.num + '] str[' + this.str + ']');
      return true;
    }
    unmarshalling(messageParcel) {
      this.num = messageParcel.readInt();
      this.str = messageParcel.readString();
      console.log('MyMessageAble unmarshalling num[' + this.num + '] str[' + this.str + ']');
      return true;
    }
  };
  let method = 'call_Function'; // Notification message string negotiated by the two abilities.
  let caller;
  export default class MainAbility extends Ability {
    onWindowStageCreate(windowStage) {
      this.context.startAbilityByCall({
        bundleName: 'com.example.myservice',
        abilityName: 'MainAbility',
        deviceId: ''
      }).then((obj) => {
        caller = obj;
        let msg = new MyMessageAble('msg', 'world'); // See the definition of Sequenceable.

        caller.call(method, msg)
          .then(() => {
            console.log('Caller call() called');
          })
          .catch((callErr) => {
            console.log('Caller.call catch error, error.code: ' + JSON.stringify(callErr.code) +
              ' error.message: ' + JSON.stringify(callErr.message));
          });
      }).catch((err) => {
        console.log('Caller GetCaller error, error.code: ' + JSON.stringify(err.code) +
          ' error.message: ' + JSON.stringify(err.message));
      });
    }
  }
  ```


## Caller.callWithResult

callWithResult(method: string, data: rpc.Sequenceable): Promise&lt;rpc.MessageParcel&gt;;

Sends sequenceable data to the target ability and obtains the sequenceable data returned by the target ability.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| method | string | Yes| Notification message string negotiated between the two abilities. The message is used to instruct the callee to register a function to receive the sequenceable data.|
| data | [rpc.Sequenceable](js-apis-rpc.md#sequenceabledeprecated) | Yes| Sequenceable data. You need to customize the data.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;[rpc.MessageParcel](js-apis-rpc.md#sequenceabledeprecated)&gt; | Promise used to return the sequenceable data from the target ability.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | If the input parameter is not valid parameter. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**

  ```ts
  import Ability from '@ohos.app.ability.UIAbility';
  class MyMessageAble{
    name:''
    str:''
    num: 1
    constructor(name, str) {
      this.name = name;
      this.str = str;
    }
    marshalling(messageParcel) {
      messageParcel.writeInt(this.num);
      messageParcel.writeString(this.str);
      console.log('MyMessageAble marshalling num[' + this.num + '] str[' + this.str + ']');
      return true;
    }
    unmarshalling(messageParcel) {
      this.num = messageParcel.readInt();
      this.str = messageParcel.readString();
      console.log('MyMessageAble unmarshalling num[' + this.num + '] str[' + this.str + ']');
      return true;
    }
  };
  let method = 'call_Function';
  let caller;
  export default class MainAbility extends Ability {
    onWindowStageCreate(windowStage) {
      this.context.startAbilityByCall({
        bundleName: 'com.example.myservice',
        abilityName: 'MainAbility',
        deviceId: ''
      }).then((obj) => {
        caller = obj;
        let msg = new MyMessageAble(1, 'world');
        caller.callWithResult(method, msg)
          .then((data) => {
            console.log('Caller callWithResult() called');
            let retmsg = new MyMessageAble(0, '');
            data.readSequenceable(retmsg);
          })
          .catch((callErr) => {
            console.log('Caller.callWithResult catch error, error.code: ' + JSON.stringify(callErr.code) +
              ' error.message: ' + JSON.stringify(callErr.message));
          });
      }).catch((err) => {
        console.log('Caller GetCaller error, error.code: ' + JSON.stringify(err.code) +
          ' error.message: ' + JSON.stringify(err.message));
      });
    }
  }
  ```


## Caller.release

release(): void;

Releases the caller interface of the target ability.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | Invalid input parameter. |
| 16200001 | Caller released. The caller has been released. |
| 16200002 | Callee invalid. The callee does not exist. |
| 16000050 | Internal Error. |

**Example**
    
  ```ts
  import Ability from '@ohos.app.ability.UIAbility';
  let caller;
  export default class MainAbility extends Ability {
    onWindowStageCreate(windowStage) {
      this.context.startAbilityByCall({
        bundleName: 'com.example.myservice',
        abilityName: 'MainAbility',
        deviceId: ''
      }).then((obj) => {
        caller = obj;
        try {
          caller.release();
        } catch (releaseErr) {
          console.log('Caller.release catch error, error.code: ' + JSON.stringify(releaseErr.code) +
            ' error.message: ' + JSON.stringify(releaseErr.message));
        }
      }).catch((err) => {
        console.log('Caller GetCaller error, error.code: ' + JSON.stringify(err.code) +
          ' error.message: ' + JSON.stringify(err.message));
      });
    }
  }
  ```

## Caller.onRelease

 onRelease(callback: OnReleaseCallBack): void;

Registers a callback that is invoked when the stub on the target ability is disconnected.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| callback | [OnReleaseCallBack](#onreleasecallback) | Yes| Callback used to return the result.|

**Example**
    
  ```ts
  import Ability from '@ohos.application.Ability';
  let caller;
  export default class MainAbility extends Ability {
    onWindowStageCreate(windowStage) {
      this.context.startAbilityByCall({
        bundleName: 'com.example.myservice',
        abilityName: 'MainAbility',
        deviceId: ''
      }).then((obj) => {
          caller = obj;
          try {
            caller.onRelease((str) => {
                console.log(' Caller OnRelease CallBack is called ' + str);
            });
          } catch (error) {
            console.log('Caller.onRelease catch error, error.code: ' + JSON.stringify(error.code) +
              ' error.message: ' + JSON.stringify(error.message));
          }
      }).catch((err) => {
        console.log('Caller GetCaller error, error.code: ' + JSON.stringify(err.code) +
          ' error.message: ' + JSON.stringify(err.message));
      });
    }
  }
  ```

## Caller.on

 on(type: 'release', callback: OnReleaseCallback): void;

Registers a callback that is invoked when the stub on the target ability is disconnected.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type. The value is fixed at **release**.|
| callback | [OnReleaseCallBack](#onreleasecallback) | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | If the input parameter is not valid parameter. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**
    
  ```ts
  import Ability from '@ohos.app.ability.UIAbility';
  let caller;
  export default class MainAbility extends Ability {
    onWindowStageCreate(windowStage) {
      this.context.startAbilityByCall({
        bundleName: 'com.example.myservice',
        abilityName: 'MainAbility',
        deviceId: ''
      }).then((obj) => {
          caller = obj;
          try {
            caller.on('release', (str) => {
                console.log(' Caller OnRelease CallBack is called ' + str);
            });
          } catch (error) {
            console.log('Caller.on catch error, error.code: ' + JSON.stringify(error.code) +
              ' error.message: ' + JSON.stringify(error.message));
          }
      }).catch((err) => {
        console.log('Caller GetCaller error, error.code: ' + JSON.stringify(err.code) +
          ' error.message: ' + JSON.stringify(err.message));
      });
    }
  }
  ```

## Caller.off

off(type: 'release', callback: OnReleaseCallback): void;

Deregisters a callback that is invoked when the stub on the target ability is disconnected. This capability is reserved.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type. The value is fixed at **release**.|
| callback | [OnReleaseCallBack](#onreleasecallback) | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | If the input parameter is not valid parameter. |
For other IDs, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**
    
  ```ts
  let caller;
  export default class MainUIAbility extends UIAbility {
    onWindowStageCreate(windowStage) {
      this.context.startAbilityByCall({
        bundleName: 'com.example.myservice',
        abilityName: 'MainUIAbility',
        deviceId: ''
      }).then((obj) => {
          caller = obj;
          try {
            let onReleaseCallBack = (str) => {
                console.log(' Caller OnRelease CallBack is called ' + str);
            };
            caller.on('release', onReleaseCallBack);
            caller.off('release', onReleaseCallBack);
          } catch (error) {
            console.log('Caller.on or Caller.off catch error, error.code: ' + JSON.stringify(error.code) +
              ' error.message: ' + JSON.stringify(error.message));
          }
      }).catch((err) => {
        console.log('Caller GetCaller error, error.code: ' + JSON.stringify(err.code) +
          ' error.message: ' + JSON.stringify(err.message));
      });
    }
  }
  ```

## Caller.off

off(type: 'release'): void;

Deregisters a callback that is invoked when the stub on the target ability is disconnected. This capability is reserved.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type. The value is fixed at **release**.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | If the input parameter is not valid parameter. |
For other IDs, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**
    
  ```ts
  let caller;
  export default class MainUIAbility extends UIAbility {
    onWindowStageCreate(windowStage) {
      this.context.startAbilityByCall({
        bundleName: 'com.example.myservice',
        abilityName: 'MainUIAbility',
        deviceId: ''
      }).then((obj) => {
          caller = obj;
          try {
            let onReleaseCallBack = (str) => {
                console.log(' Caller OnRelease CallBack is called ' + str);
            };
            caller.on('release', onReleaseCallBack);
            caller.off('release');
          } catch (error) {  
            console.error('Caller.on or Caller.off catch error, error.code: ' + JSON.stringify(error.code) +
              ' error.message: ' + JSON.stringify(error.message));
          }
      }).catch((err) => {
        console.error('Caller GetCaller error, error.code: ' + JSON.stringify(err.code) +
          ' error.message: ' + JSON.stringify(err.message));
      });
    }
  }
  ```

## Callee

Implements callbacks for caller notification registration and deregistration.

## Callee.on

on(method: string, callback: CalleeCallback): void;

Registers a caller notification callback, which is invoked when the target ability registers a function.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| method | string | Yes| Notification message string negotiated between the two abilities.|
| callback | [CalleeCallback](#calleecallback) | Yes| JS notification synchronization callback of the [rpc.MessageParcel](js-apis-rpc.md#sequenceabledeprecated) type. The callback must return at least one empty [rpc.Sequenceable](js-apis-rpc.md#sequenceabledeprecated) object. Otherwise, the function execution fails.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | If the input parameter is not valid parameter. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**

  ```ts
  import Ability from '@ohos.app.ability.UIAbility';
  class MyMessageAble{
      name:''
      str:''
      num: 1
      constructor(name, str) {
        this.name = name;
        this.str = str;
      }
      marshalling(messageParcel) {
          messageParcel.writeInt(this.num);
          messageParcel.writeString(this.str);
          console.log('MyMessageAble marshalling num[' + this.num + '] str[' + this.str + ']');
          return true;
      }
      unmarshalling(messageParcel) {
          this.num = messageParcel.readInt();
          this.str = messageParcel.readString();
          console.log('MyMessageAble unmarshalling num[' + this.num + '] str[' + this.str + ']');
          return true;
      }
  };
  let method = 'call_Function';
  function funcCallBack(pdata) {
      console.log('Callee funcCallBack is called ' + pdata);
      let msg = new MyMessageAble('test', '');
      pdata.readSequenceable(msg);
      return new MyMessageAble('test1', 'Callee test');
  }
  export default class MainAbility extends Ability {
    onCreate(want, launchParam) {
      console.log('Callee onCreate is called');
      try {
        this.callee.on(method, funcCallBack);
      } catch (error) {
        console.log('Callee.on catch error, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      }
    }
  }
  ```

## Callee.off

off(method: string): void;

Deregisters a caller notification callback, which is invoked when the target ability registers a function.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| method | string | Yes| Registered notification message string.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | If the input parameter is not valid parameter. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).


**Example**
    
  ```ts
  import Ability from '@ohos.app.ability.UIAbility';
  let method = 'call_Function';
  export default class MainAbility extends Ability {
    onCreate(want, launchParam) {
      console.log('Callee onCreate is called');
      try {
        this.callee.off(method);
      } catch (error) {
        console.log('Callee.off catch error, error.code: ' + JSON.stringify(error.code) +
          ' error.message: ' + JSON.stringify(error.message));
      }
    }
  }
  ```

## OnReleaseCallback

(msg: string): void;

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

| Name| Readable| Writable| Type| Description|
| -------- | -------- | -------- | -------- | -------- |
| (msg: string) | Yes| No| function | Prototype of the listener function registered by the caller.|

## CalleeCallback

(indata: rpc.MessageParcel): rpc.Sequenceable;

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

| Name| Readable| Writable| Type| Description|
| -------- | -------- | -------- | -------- | -------- |
| (indata: [rpc.MessageParcel](js-apis-rpc.md#sequenceabledeprecated)) | Yes| No| [rpc.Sequenceable](js-apis-rpc.md#sequenceabledeprecated) | Prototype of the listener function registered by the callee.|

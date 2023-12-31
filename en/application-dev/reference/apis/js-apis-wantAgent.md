# @ohos.wantAgent (WantAgent)

The **WantAgent** module provides APIs for creating and comparing **WantAgent** objects, and obtaining the user ID and bundle name of a **WantAgent** object.

> **NOTE**
> 
> The APIs of this module are supported since API version 7 and deprecated since API version 9. You are advised to use [@ohos.app.ability.wantAgent](js-apis-app-ability-wantAgent.md) instead. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```ts
import WantAgent from '@ohos.wantAgent';
```

## WantAgent.getWant

getWant(agent: WantAgent, callback: AsyncCallback\<Want\>): void

Obtains the Want in a **WantAgent** object. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                      | Mandatory| Description                   |
| -------- | -------------------------- | ---- | ----------------------- |
| agent     | [WantAgent](js-apis-wantAgent.md)              | Yes  | **WantAgent** object.          |
| callback | AsyncCallback\<Want\> | Yes  | Callback used to return the Want.|

**Example**

```ts
import WantAgent, { WantAgent as _WantAgent} from '@ohos.wantAgent';
import Want from '@ohos.app.ability.Want';
import { BusinessError } from '@ohos.base';

// WantAgent object
let wantAgent: _WantAgent;

// getWantAgent callback
function getWantAgentCallback(err: BusinessError, data: _WantAgent) {
	console.info('==========================>getWantAgentCallback=======================>');
    if (err.code == 0) {
    	wantAgent = data;
    } else {
        console.error('getWantAgent failed, error: ' + JSON.stringify(err));
        return;
    }

    // getWant callback
    let getWantCallback = (err: BusinessError, data: Want) => {
        console.info('==========================>getWantCallback=======================>');
    }
    WantAgent.getWant(wantAgent, getWantCallback);
}

WantAgent.getWantAgent({
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.EntryAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
}, getWantAgentCallback);
```

## WantAgent.getWant

getWant(agent: WantAgent): Promise\<Want\>

Obtains the Want in a **WantAgent** object. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type         | Mandatory| Description         |
| ---- | ------------- | ---- | ------------- |
| agent | [WantAgent](js-apis-wantAgent.md) | Yes  | **WantAgent** object.|

**Return value**

| Type                                                       | Description                                                        |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<Want\> | Promise used to return the Want.|

**Example**

```ts
import WantAgent, { WantAgent as _WantAgent} from '@ohos.wantAgent';
import { BusinessError } from '@ohos.base';

// WantAgent object
let wantAgent: _WantAgent;

WantAgent.getWantAgent({
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.EntryAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
}).then((data) => {
	console.info('==========================>getWantAgentCallback=======================>');
    wantAgent = data;
    if (wantAgent) {        
        WantAgent.getWant(wantAgent).then((data) => {
            console.info('==========================>getWantCallback=======================>');
        });
    }
});
```

## WantAgent.getWantAgent

getWantAgent(info: WantAgentInfo, callback: AsyncCallback\<WantAgent\>): void

Creates a **WantAgent** object. This API uses an asynchronous callback to return the result. If the creation fails, a null **WantAgent** object is returned.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

| Name    | Type                      | Mandatory| Description                   |
| -------- | -------------------------- | ---- | ----------------------- |
| info     | [WantAgentInfo](js-apis-inner-wantAgent-wantAgentInfo.md)              | Yes  | **WantAgent** object.          |
| callback | AsyncCallback\<WantAgent\> | Yes  | Callback used to return the **WantAgent** object.|

**Example**

```ts
import WantAgent, { WantAgent as _WantAgent} from '@ohos.wantAgent';
import { BusinessError } from '@ohos.base';

// getWantAgent callback
function getWantAgentCallback(err: BusinessError, data: _WantAgent) {
    if (err.code) {
        console.info('getWantAgent Callback err:' + JSON.stringify(err))
    } else { 
        console.info('getWantAgent Callback success')
    }
}

WantAgent.getWantAgent({
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.EntryAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
}, getWantAgentCallback);
```

## WantAgent.getWantAgent

getWantAgent(info: WantAgentInfo): Promise\<WantAgent\>

Creates a **WantAgent** object. This API uses a promise to return the result. If the creation fails, a null **WantAgent** object is returned.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

| Name| Type         | Mandatory| Description         |
| ---- | ------------- | ---- | ------------- |
| info | [WantAgentInfo](js-apis-inner-wantAgent-wantAgentInfo.md) | Yes  | **WantAgent** object.|

**Return value**

| Type                                                       | Description                                                        |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<WantAgent\> | Promise used to return the **WantAgent** object.|

**Example**

```ts
import WantAgent, { WantAgent as _WantAgent} from '@ohos.wantAgent';

WantAgent.getWantAgent({
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.EntryAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
}).then((data: _WantAgent) => {
	console.info('==========================>getWantAgentCallback=======================>');
});
```

## WantAgent.getBundleName

getBundleName(agent: WantAgent, callback: AsyncCallback\<string\>): void

Obtains the bundle name of a **WantAgent** object. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

| Name    | Type                   | Mandatory| Description                             |
| -------- | ----------------------- | ---- | --------------------------------- |
| agent    | WantAgent               | Yes  | **WantAgent** object.                    |
| callback | AsyncCallback\<string\> | Yes  | Callback used to return the bundle name.|

**Example**

```ts
import WantAgent, { WantAgent as _WantAgent} from '@ohos.wantAgent';
import { BusinessError } from '@ohos.base';

// WantAgent object
let wantAgent: _WantAgent;

// getWantAgent callback
function getWantAgentCallback(err: BusinessError, data: _WantAgent) {
	console.info('==========================>getWantAgentCallback=======================>');
    if (err.code == 0) {
    	wantAgent = data;
    } else {
        console.error('getWantAgent failed, error: ' + JSON.stringify(err));
        return;
    }

    // getBundleName callback
    let getBundleNameCallback = (err: BusinessError, data: string) => {
        console.info('==========================>getBundleNameCallback=======================>');
    }
    WantAgent.getBundleName(wantAgent, getBundleNameCallback);
}

WantAgent.getWantAgent({
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.EntryAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
}, getWantAgentCallback)
```



## WantAgent.getBundleName

getBundleName(agent: WantAgent): Promise\<string\>

Obtains the bundle name of a **WantAgent** object. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

| Name | Type     | Mandatory| Description         |
| ----- | --------- | ---- | ------------- |
| agent | WantAgent | Yes  | **WantAgent** object.|

**Return value**

| Type             | Description                                            |
| ----------------- | ------------------------------------------------ |
| Promise\<string\> | Promise used to return the bundle name.|

**Example**

```ts
import WantAgent, { WantAgent as _WantAgent} from '@ohos.wantAgent';

// WantAgent object
let wantAgent: _WantAgent;

WantAgent.getWantAgent({
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.EntryAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
}).then((data: _WantAgent) => {
	console.info('==========================>getWantAgentCallback=======================>');
    wantAgent = data;
    if (wantAgent) {
        WantAgent.getBundleName(wantAgent).then((data) => {
            console.info('==========================>getBundleNameCallback=======================>');
        });
    }
});
```



## WantAgent.getUid

getUid(agent: WantAgent, callback: AsyncCallback\<number\>): void

Obtains the user ID of a **WantAgent** object. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

| Name    | Type                   | Mandatory| Description                               |
| -------- | ----------------------- | ---- | ----------------------------------- |
| agent    | WantAgent               | Yes  | **WantAgent** object.                      |
| callback | AsyncCallback\<number\> | Yes  | Callback used to return the user ID.|

**Example**

```ts
import WantAgent, { WantAgent as _WantAgent} from '@ohos.wantAgent';
import { BusinessError } from '@ohos.base';

// WantAgent object
let wantAgent: _WantAgent;

// getWantAgent callback
function getWantAgentCallback(err: BusinessError, data: _WantAgent) {
	console.info('==========================>getWantAgentCallback=======================>');
    if (err.code == 0) {
    	wantAgent = data;
    } else {
        console.error('getWantAgent failed, error: ' + JSON.stringify(err));
        return;
    }

    // getUid callback
    let getUidCallback = (err: BusinessError, data: number) => {
        console.info('==========================>getUidCallback=======================>');
    }
    WantAgent.getUid(wantAgent, getUidCallback);
}

WantAgent.getWantAgent({
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.EntryAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
}, getWantAgentCallback)
```



## WantAgent.getUid

getUid(agent: WantAgent): Promise\<number\>

Obtains the user ID of a **WantAgent** object. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

| Name | Type     | Mandatory| Description         |
| ----- | --------- | ---- | ------------- |
| agent | WantAgent | Yes  | **WantAgent** object.|

**Return value**

| Type                                                       | Description                                                        |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<number\> | Promise used to return the user ID.|

**Example**

```ts
import WantAgent, { WantAgent as _WantAgent} from '@ohos.wantAgent';

// WantAgent object
let wantAgent: _WantAgent;

WantAgent.getWantAgent({
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.EntryAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
}).then((data) => {
	console.info('==========================>getWantAgentCallback=======================>');
    wantAgent = data;
    if (wantAgent) {
        WantAgent.getUid(wantAgent).then((data) => {
        console.info('==========================>getUidCallback=======================>');
    });
    }
});
```


## WantAgent.cancel

cancel(agent: WantAgent, callback: AsyncCallback\<void\>): void

Cancels a **WantAgent** object. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

| Name    | Type                 | Mandatory| Description                       |
| -------- | --------------------- | ---- | --------------------------- |
| agent    | WantAgent             | Yes  | **WantAgent** object.              |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```ts
import WantAgent, { WantAgent as _WantAgent} from '@ohos.wantAgent';
import { BusinessError } from '@ohos.base';

// WantAgent object
let wantAgent: _WantAgent;

// getWantAgent callback
function getWantAgentCallback(err: BusinessError, data: _WantAgent) {
	console.info('==========================>getWantAgentCallback=======================>');
    if (err.code == 0) {
    	wantAgent = data;
    } else {
        console.error('getWantAgent failed, error: ' + JSON.stringify(err));
        return;
    }

    // cancel callback
    let cancelCallback = (err: BusinessError) => {
        console.info('==========================>cancelCallback=======================>');
    }
    WantAgent.cancel(wantAgent, cancelCallback);
}

WantAgent.getWantAgent({
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.EntryAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
}, getWantAgentCallback)
```



## WantAgent.cancel

cancel(agent: WantAgent): Promise\<void\>

Cancels a **WantAgent** object. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

| Name | Type     | Mandatory| Description         |
| ----- | --------- | ---- | ------------- |
| agent | WantAgent | Yes  | **WantAgent** object.|

**Return value**

| Type           | Description                           |
| --------------- | ------------------------------- |
| Promise\<void\> | Promise used to return the result.|

**Example**

```ts
import WantAgent, { WantAgent as _WantAgent} from '@ohos.wantAgent';
import { BusinessError } from '@ohos.base';

// WantAgent object
let wantAgent: _WantAgent;

WantAgent.getWantAgent({
    wants: [
    {
        deviceId: 'deviceId',
        bundleName: 'com.neu.setResultOnAbilityResultTest1',
        abilityName: 'com.example.test.EntryAbility',
        action: 'action1',
        entities: ['entity1'],
        type: 'MIMETYPE',
        uri: 'key={true,true,false}',
        parameters:
        {
            mykey0: 2222,
            mykey1: [1, 2, 3],
            mykey2: '[1, 2, 3]',
            mykey3: 'ssssssssssssssssssssssssss',
            mykey4: [false, true, false],
            mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
            mykey6: true,
        }
    }
],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
}).then((data) => {
	console.info('==========================>getWantAgentCallback=======================>');
    wantAgent = data;
    if (wantAgent) {        
        WantAgent.cancel(wantAgent).then((data) => {
            console.info('==========================>cancelCallback=======================>');
        });
    }
});
```



## WantAgent.trigger

trigger(agent: WantAgent, triggerInfo: TriggerInfo, callback?: Callback\<CompleteData\>): void

Triggers a **WantAgent** object. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

| Name       | Type                         | Mandatory| Description                           |
| ----------- | ----------------------------- | ---- | ------------------------------- |
| agent       | WantAgent                     | Yes  | **WantAgent** object.                  |
| triggerInfo | [TriggerInfo](js-apis-inner-wantAgent-triggerInfo.md)                     | Yes  | **TriggerInfo** object.                |
| callback    | Callback\<CompleteData\> | No  | Callback used to return the result.|

**Example**

```ts
import WantAgent, { WantAgent as _WantAgent} from '@ohos.wantAgent';
import { BusinessError } from '@ohos.base';

// WantAgent object
let wantAgent: _WantAgent;

// getWantAgent callback
function getWantAgentCallback(err: BusinessError, data: _WantAgent) {
	console.info('==========================>getWantAgentCallback=======================>');
    if (err.code == 0) {
    	wantAgent = data;
    } else {
        console.error('getWantAgent failed, error: ' + JSON.stringify(err));
        return;
    }

    // trigger callback
    let triggerCallback = (data: WantAgent.CompleteData) => {
        console.info('==========================>triggerCallback=======================>');
    }

    WantAgent.trigger(wantAgent, {code:0}, triggerCallback)
}

WantAgent.getWantAgent({
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.EntryAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
}, getWantAgentCallback)
```



## WantAgent.equal

equal(agent: WantAgent, otherAgent: WantAgent, callback: AsyncCallback\<boolean\>): void

Checks whether two **WantAgent** objects are equal to determine whether the same operation is from the same application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

| Name      | Type                    | Mandatory| Description                                   |
| ---------- | ------------------------ | ---- | --------------------------------------- |
| agent      | WantAgent                | Yes  | The first **WantAgent** object.                          |
| otherAgent | WantAgent                | Yes  | The second **WantAgent** object.                          |
| callback   | AsyncCallback\<boolean\> | Yes  | Callback used to return the result.|

**Example**

```ts
import WantAgent, { WantAgent as _WantAgent} from '@ohos.wantAgent';
import { BusinessError } from '@ohos.base';

// WantAgent object
let wantAgent1: _WantAgent;
let wantAgent2: _WantAgent;

// getWantAgent callback
function getWantAgentCallback(err: BusinessError, data: _WantAgent) {
	console.info('==========================>getWantAgentCallback=======================>');
    if (err.code == 0) {
    	wantAgent1 = data;
        wantAgent2 = data;
    } else {
        console.error('getWantAgent failed, error: ' + JSON.stringify(err));
        return;
    }

    // equal callback
    let equalCallback = (err: BusinessError, data: boolean) => {
        console.info('==========================>equalCallback=======================>');
    }
    WantAgent.equal(wantAgent1, wantAgent2, equalCallback)
}

WantAgent.getWantAgent({
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.EntryAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
}, getWantAgentCallback)
```



## WantAgent.equal

equal(agent: WantAgent, otherAgent: WantAgent): Promise\<boolean\>

Checks whether two **WantAgent** objects are equal to determine whether the same operation is from the same application. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

| Name      | Type     | Mandatory| Description         |
| ---------- | --------- | ---- | ------------- |
| agent      | WantAgent | Yes  | The first **WantAgent** object.|
| otherAgent | WantAgent | Yes  | The second **WantAgent** object.|

**Return value**

| Type                                                       | Description                                                        |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<boolean\> | Promise used to return the result.|

**Example**

```ts
import WantAgent, { WantAgent as _WantAgent} from '@ohos.wantAgent';
import { BusinessError } from '@ohos.base';


// WantAgent object
let wantAgent1: _WantAgent;
let wantAgent2: _WantAgent;

WantAgent.getWantAgent({
    wants: [
        {
            deviceId: 'deviceId',
            bundleName: 'com.neu.setResultOnAbilityResultTest1',
            abilityName: 'com.example.test.EntryAbility',
            action: 'action1',
            entities: ['entity1'],
            type: 'MIMETYPE',
            uri: 'key={true,true,false}',
            parameters:
            {
                mykey0: 2222,
                mykey1: [1, 2, 3],
                mykey2: '[1, 2, 3]',
                mykey3: 'ssssssssssssssssssssssssss',
                mykey4: [false, true, false],
                mykey5: ['qqqqq', 'wwwwww', 'aaaaaaaaaaaaaaaaa'],
                mykey6: true,
            }
        }
    ],
    operationType: WantAgent.OperationType.START_ABILITIES,
    requestCode: 0,
    wantAgentFlags:[WantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
}).then((data) => {
	console.info('==========================>getWantAgentCallback=======================>');
    wantAgent1 = data;
    wantAgent2 = data;
    if (data) {
        WantAgent.equal(wantAgent1, wantAgent2).then((data) => {
            console.info('==========================>equalCallback=======================>');
        });
    }
});
```

## WantAgentFlags

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name               | Value            | Description                                                        |
| ------------------- | -------------- | ------------------------------------------------------------ |
| ONE_TIME_FLAG       | 0 | The **WantAgent** object can be used only once.                                     |
| NO_BUILD_FLAG       | 1 | The **WantAgent** object does not exist and hence it is not created. In this case, **null** is returned.     |
| CANCEL_PRESENT_FLAG | 2 | The existing **WantAgent** object should be canceled before a new object is generated.|
| UPDATE_PRESENT_FLAG | 3 | Extra information of the existing **WantAgent** object is replaced with that of the new object.|
| CONSTANT_FLAG       | 4 | The **WantAgent** object is immutable.                                       |
| REPLACE_ELEMENT     | 5 | The **element** attribute of the current **Want** can be replaced by the **element** attribute of the **Want** in **WantAgent.trigger()**.|
| REPLACE_ACTION      | 6 | The **action** attribute of the current **Want** can be replaced by the **action** attribute of the **Want** in **WantAgent.trigger()**.|
| REPLACE_URI         | 7 | The **uri** attribute of the current **Want** can be replaced by the **uri** attribute of the **Want** in **WantAgent.trigger()**.|
| REPLACE_ENTITIES    | 8 | The **entities** attribute of the current **Want** can be replaced by the **entities** attribute of the **Want** in **WantAgent.trigger()**.|
| REPLACE_BUNDLE      | 9 | The **bundleName** attribute of the current **Want** can be replaced by the **bundleName** attribute of **Want** in **WantAgent.trigger()**.|

## OperationType

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name             | Value           | Description                     |
| ----------------- | ------------- | ------------------------- |
| UNKNOWN_TYPE      | 0 | Unknown operation type.           |
| START_ABILITY     | 1 | Starts an ability with a UI.|
| START_ABILITIES   | 2 | Starts multiple abilities with a UI.|
| START_SERVICE     | 3 | Starts an ability without a UI.|
| SEND_COMMON_EVENT | 4 | Sends a common event.       |

## CompleteData 

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name          | Type                          | Mandatory| Description                   |
| -------------- | ------------------------------ | ---- | ---------------------- |
| info           | WantAgent                       | Yes  | A triggered **WantAgent** object.      |
| want           | Want                            | Yes  | An existing triggered **want**.    |
| finalCode      | number                          | Yes  | Request code that triggers the **WantAgent** object.|
| finalData      | string                          | Yes  | Final data collected by the common event. |
| extraInfo      | {[key: string]: any}            | No  | Extra information.              |

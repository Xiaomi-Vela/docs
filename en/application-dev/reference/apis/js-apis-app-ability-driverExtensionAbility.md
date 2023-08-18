# @ohos.app.ability.DriverExtensionAbility (DriverExtensionAbility)

The **DriverExtensionAbility** module provides the ExtensionAbility related to drivers. It provides lifecycle callbacks to be invoked when a driver is created, destroyed, connected, or disconnected.

> **NOTE**
> 
> The initial APIs of this module are supported since API version 10. Newly added APIs will be marked with a superscript to indicate their earliest API version. 
> The APIs of this module can be used only in the stage model.

## Modules to Import

```ts
import DriverExtension from '@ohos.app.ability.DriverExtensionAbility';
```

## Required Permissions

None.

## Attributes

**System capability**: SystemCapability.Driver.ExternalDevice


| Name| Type| Readable| Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| context | [DriverExtensionContext](js-apis-inner-application-driverExtensionContext.md)  | Yes| No| Context of the **DriverExtension**. This context is inherited from **ExtensionContext**.|


## DriverExtensionAbility.onInit

onInit(want: Want): void;

Called when a DriverExtensionAbility is created to initialize the service logic.

**System capability**: SystemCapability.Driver.ExternalDevice

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want |  [Want](js-apis-app-ability-want.md) | Yes| Want information related to this DriverExtensionAbility, including the ability name and bundle name.|

**Example**

  ```ts
  class DriverExt extends DriverExtension {
    onInit(want) {
      console.log('onInit, want: ${want.abilityName}');
    }
  }
  ```


## DriverExtensionAbility.onRelease

onRelease(): void;

Called when this DriverExtensionAbility is destroyed to clear resources.

**System capability**: SystemCapability.Driver.ExternalDevice

**Example**

  ```ts
  class DriverExt extends DriverExtension {
    onRelease() {
      console.log('onRelease');
    }
  }
  ```


## DriverExtensionAbility.onConnect

onConnect(want: Want): rpc.RemoteObject | Promise<rpc.RemoteObject>;

Called following **onCreate()** when a DriverExtensionAbility is started by calling **connectAbility()**. A **RemoteObject** object is returned for communication between the server and client.

**System capability**: SystemCapability.Driver.ExternalDevice

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want |  [Want](js-apis-app-ability-want.md)| Yes| Want information related to this DriverExtensionAbility, including the ability name and bundle name.|

**Return value**

| Type| Description|
| -------- | -------- |
| rpc.RemoteObject | A **RemoteObject** object used for communication between the server and client.|

**Example**

  ```ts
  import rpc from '@ohos.rpc';
  class StubTest extends rpc.RemoteObject{
      constructor(des) {
          super(des);
      }
      onRemoteMessageRequest(code, data, reply, option) {
      }
  }
  class DriverExt extends DriverExtension {
    onConnect(want) {
      console.log('onConnect , want: ${want.abilityName}');
      return new StubTest('test');
    }
  }
  ```

If the returned **RemoteObject** object depends on an asynchronous API, you can use the asynchronous lifecycle.

  ```ts
import rpc from '@ohos.rpc';
class StubTest extends rpc.RemoteObject{
    constructor(des) {
        super(des);
    }
    onRemoteMessageRequest(code, data, reply, option) {
    }
}
async function getDescriptor() {
    // Call the asynchronous function.
    return "asyncTest"
}
class DriverExt extends DriverExtension {
  async onConnect(want) {
    console.log(`onConnect , want: ${want.abilityName}`);
    let descriptor = await getDescriptor();
    return new StubTest(descriptor);
  }
}
  ```

## DriverExtensionAbility.onDisconnect

onDisconnect(want: Want): void | Promise\<void>;

Called when a client is disconnected from this DriverExtensionAbility.

**System capability**: SystemCapability.Driver.ExternalDevice

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want |[Want](js-apis-app-ability-want.md)| Yes| Want information related to this DriverExtensionAbility, including the ability name and bundle name.|

**Example**

  ```ts
  class DriverExt extends DriverExtension {
    onDisconnect(want) {
      console.log('onDisconnect, want: ${want.abilityName}');
    }
  }
  ```

After the **onDisconnect** lifecycle callback is executed, the application may exit. As a result, the asynchronous function in **onDisconnect** may fail to be executed correctly, for example, asynchronously writing data to the database. The asynchronous lifecycle can be used to ensure that the subsequent lifecycle continues after the asynchronous **onDisconnect** is complete.

  ```ts
class DriverExt extends DriverExtension {
  async onDisconnect(want) {
    console.log('onDisconnect, want: ${want.abilityName}');
    // Call the asynchronous function.
  }
}
  ```


## DriverExtensionAbility.onDump

onDump(params: Array\<string>): Array\<string>;

Dumps client information.

**System capability**: SystemCapability.Driver.ExternalDevice

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| params | Array\<string> | Yes| Parameters in the form of a command.|

**Example**
    
  ```ts
  class DriverExt extends DriverExtension {
      onDump(params) {
          console.log('dump, params: ${JSON.stringify(params)}');
          return ['params'];
      }
  }
  ```

# DriverExtensionAbility

[DriverExtensionAbility](../reference/apis/js-apis-app-ability-driverExtensionAbility.md) is an ExtensionAbility of the driver type that provides driver-related extension framework. If the capabilities of a device can be expanded by inserting an external hardware module, you can install the driver of the hardware module through an application. DriverExtensionAbility can be used to develop such applications.


The [DriverExtensionAbility](../reference/apis/js-apis-app-ability-driverExtensionAbility.md) can be bound to an application through the DriverExtensionManager and process related transactions in the background based on the application request information.
Each type of ExtensionAbility has its own context. The DriverExtensionAbility provides related capabilities through the [DriverExtensionContext](../reference/apis/js-apis-inner-application-driverExtensionContext.md).
         
This topic describes how to use DriverExtensionAbility in the following scenarios:

- [DriverExtensionAbility](#driverextensionability)
  - [How to Develop](#how-to-develop)

## How to Develop

To implement a driver, create a DriverExtensionAbility in the DevEco Studio project. The procedure is as follows:

1. In the **ets** directory of a module in the project, right-click and choose **New > Directory** to create a directory named **driverextability**.

2. In the **driverextability** directory, right-click and choose **New > TypeScript File** to create a file named **DriverExtAbility.ts**.

3. Open the **DriverExtAbility.ts** file, import the [RPC module](../reference/apis/js-apis-rpc.md), and overload the **onRemoteMessageRequest()** method to receive messages from the application and return the processing result to the application. **REQUEST_VALUE** is used to verify the service request code sent by the application.
   
   ```ts
   import rpc from '@ohos.rpc';
   
   const REQUEST_CODE = 99;
   
   class StubTest extends rpc.RemoteObject {
     constructor(des) {
       super(des);
     }
     
     // Receive the message sent from the application and return the processing result to the application.
     onRemoteMessageRequest(code, data, reply, option) {
       if (code === REQUEST_CODE) {
         // Receive the data sent from the application.
         // When the application calls data.writeInt() multiple times to write data, the driver can receive the corresponding data by calling data.readInt() for multiple times.
         let optFir = data.readInt();
         let optSec = data.readInt();
         // The driver returns the data processing result to the application.
         // In the example, two pieces of data are received, and the sum of the two pieces of data is returned to the application.
         reply.writeInt(optFir + optSec);
       }
       return true;
     }
   }
   ```


4. In the **DriverExtAbility.ts** file, import the dependency package [DriverExtensionAbility](../reference/apis/js-apis-app-ability-driverExtensionAbility.md), which provides the **onInit()**, **onRelease()**, **onConnect()**, and **onDisconnect()** lifecycle callbacks. Then, customize a class to inherit from [DriverExtensionAbility](../reference/apis/js-apis-app-ability-driverExtensionAbility.md) and override the lifecycle callbacks as required.
   
   ```ts
   import DriverExtensionAbility from '@ohos.app.ability.DriverExtensionAbility';
   import rpc from '@ohos.rpc';
   
   const TAG: string = '[Example].[Entry].[DriverExtAbility]';
   const REQUEST_CODE = 99;
   
   class StubTest extends rpc.RemoteObject {
     // ...
   }
   
   export default class DriverExtAbility extends DriverExtensionAbility {
     onInit(want) {
       console.info(TAG, `onInit, want: ${want.abilityName}`);
     }
   
     onRelease() {
       console.info(TAG, `onRelease, want: ${want.abilityName}`);
     }
   
     onConnect(want) {
       console.info(TAG, `onConnect, want: ${want.abilityName}`);
       return new StubTest("test");
     }
   
     onDisconnect(want) {
       console.info(TAG, `onDisconnect, want: ${want.abilityName}`);
     }
   
     onDump() {
       console.info(TAG, `onDump, params:` + JSON.stringify(params));
       return ['params'];
     }
   }
   ```

5. Register the DriverExtensionAbility in the [**module.json5** file](../quick-start/module-configuration-file.md) of the module in the project. Set **type** to **service** and **srcEntry** to the code path of the DriverExtensionAbility component.
   
   ```json
   {
     "module": {
       // ...
       "extensionAbilities": [
         {
           "name": "DriverExtAbility",
           "icon": "$media:icon",
           "description": "driver",
           "type": "driver",
           "exported": true,
           "srcEntry": "./ets/driverextability/DriverExtAbility.ts",
           "metadata": [
            {
              "name": "bus", // The bus is mandatory.
              "value": "USB",
            },
            {
              "name": "desc", // Description of the driver, which is mandatory.
              "value": "the sample of driverExtensionAbility",
            },
            {
              "name": "vendor", // Driver vendor name, which is mandatory.
              "value": "string",
            },
            {
              "name": "vid", // List of supported USB vendor IDs, separated by commas (,). The value cannot be empty.
              "value": "string, string",
            },
            {
              "name": "pid", // List of supported USB product IDs, separated by commas (,). The value cannot be empty.
              "value": "string, string",
            }
           ]
         }
       ]
     }
   }
   ```

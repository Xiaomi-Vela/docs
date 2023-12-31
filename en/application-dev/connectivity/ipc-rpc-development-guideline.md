# IPC & RPC Development Guidelines

## When to Use

IPC/RPC enables a proxy and a stub that run on different processes to communicate with each other, regardless of whether they run on the same or different devices.


## Available APIs

Table 1 Native IPC APIs

| Class| API| Description|
| -------- | -------- | -------- |
| IRemoteBroker | sptr&lt;IRemoteObject&gt; AsObject() | Obtains the holder of a remote proxy object. If you call this API on the stub, the **RemoteObject** is returned; if you call this API on the proxy, the proxy object is returned.|
| IRemoteStub | virtual int OnRemoteRequest(uint32_t code, MessageParcel &amp;data, MessageParcel &amp;reply, MessageOption &amp;option) | Called to process a request from the proxy and return the result. Derived classes need to override this API.|
| IRemoteProxy | Remote()->SendRequest(code, data, reply, option)             | Sends a request to the peer end. Service proxy classes are derived from the **IRemoteProxy** class.|


## How to Develop

### **Using Native APIs**

1. Add dependencies.

   SDK dependency:

   ```
   #IPC scenario
   external_deps = [
     "ipc:ipc_single",
   ]

   #RPC scenario
   external_deps = [
     "ipc:ipc_core",
   ]
   ```

   In addition, the refbase implementation on which IPC/RPC depends is stored in **//utils**. Add the dependency on the Utils source code.

   ```
   external_deps = [
     "c_utils:utils",
   ]
   ```

2. Define the IPC interface **ITestAbility**.

   **ITestAbility** inherits the IPC base class **IRemoteBroker** and defines descriptors, functions, and message code. The functions need to be implemented on both the proxy and stub.

   ```c++
   #include "iremote_broker.h"

   // Define message codes.
   const int TRANS_ID_PING_ABILITY = 5;

   const std::string DESCRIPTOR = "test.ITestAbility";

   class ITestAbility : public IRemoteBroker {
   public:
       // DECLARE_INTERFACE_DESCRIPTOR is mandatory, and the input parameter is std::u16string.
       DECLARE_INTERFACE_DESCRIPTOR(to_utf16(DESCRIPTOR));
       virtual int TestPingAbility(const std::u16string &dummy) = 0; // Define functions.
   };
   ```

3. Define and implement service provider **TestAbilityStub**.

   This class is related to the IPC framework and needs to inherit **IRemoteStub&lt;ITestAbility&gt;**. You need to override **OnRemoteRequest** on the stub to receive requests from the proxy.

   ```c++
   #include "iability_test.h"
   #include "iremote_stub.h"

   class TestAbilityStub : public IRemoteStub<ITestAbility> {
   public:
       virtual int OnRemoteRequest(uint32_t code, MessageParcel &data, MessageParcel &reply, MessageOption &option) override;
       int TestPingAbility(const std::u16string &dummy) override;
    };

   int TestAbilityStub::OnRemoteRequest(uint32_t code,
       MessageParcel &data, MessageParcel &reply, MessageOption &option)
   {
       switch (code) {
           case TRANS_ID_PING_ABILITY: {
               std::u16string dummy = data.ReadString16();
               int result = TestPingAbility(dummy);
               reply.WriteInt32(result);
               return 0;
           }
           default:
               return IPCObjectStub::OnRemoteRequest(code, data, reply, option);
       }
   }
   ```

4. Define the **TestAbility** class that implements functions for the stub.

   ```c++
   #include "iability_server_test.h"

   class TestAbility : public TestAbilityStub {
   public:
       int TestPingAbility(const std::u16string &dummy);
   }

   int TestAbility::TestPingAbility(const std::u16string &dummy) {
       return 0;
   }
   ```

5. Define and implement **TestAbilityProxy**.

   This class is implemented on the proxy and inherits **IRemoteProxy&lt;ITestAbility&gt;**. You can call **SendRequest** to send a request to the stub and expose the capabilities provided by the stub.

   ```c++
   #include "iability_test.h"
   #include "iremote_proxy.h"
   #include "iremote_object.h"

   class TestAbilityProxy : public IRemoteProxy<ITestAbility> {
   public:
       explicit TestAbilityProxy(const sptr<IRemoteObject> &impl);
       int TestPingAbility(const std::u16string &dummy) override;
   private:
       static inline BrokerDelegator<TestAbilityProxy> delegator_; // For use of the iface_cast macro at a later time
   }

   TestAbilityProxy::TestAbilityProxy(const sptr<IRemoteObject> &impl)
       : IRemoteProxy<ITestAbility>(impl)
   {
   }

   int TestAbilityProxy::TestPingAbility(const std::u16string &dummy){
       MessageOption option;
       MessageParcel dataParcel, replyParcel;
       dataParcel.WriteString16(dummy);
       int error = Remote()->SendRequest(TRANS_ID_PING_ABILITY, dataParcel, replyParcel, option);
       int result = (error == ERR_NONE) ? replyParcel.ReadInt32() : -1;
       return result;
   }
   ```

6. Register and start an SA.

   Call **AddSystemAbility** to register the **TestAbilityStub** instance of the SA with **SystemAbilityManager**. The registration parameters vary depending on whether the **SystemAbilityManager** resides on the same device as the SA.

   ```c++
   // Register the TestAbilityStub instance with the SystemAbilityManager on the same device as the SA.
   auto samgr = SystemAbilityManagerClient::GetInstance().GetSystemAbilityManager();
   samgr->AddSystemAbility(saId, new TestAbility());

   // Register the TestAbilityStub instance with the SystemAbilityManager on a different device.
   auto samgr = SystemAbilityManagerClient::GetInstance().GetSystemAbilityManager();
   ISystemAbilityManager::SAExtraProp saExtra;
   saExtra.isDistributed = true; // Set a distributed SA.
   int result = samgr->AddSystemAbility(saId, new TestAbility(), saExtra);
   ```

7. Obtain the SA.

   Call the **GetSystemAbility** function of the **SystemAbilityManager** class to obtain the **IRemoteObject** for the SA, and create a **TestAbilityProxy** instance.

   ```c++
   // Obtain the proxy of the SA registered on the local device.
   sptr<ISystemAbilityManager> samgr = SystemAbilityManagerClient::GetInstance().GetSystemAbilityManager();
   sptr<IRemoteObject> remoteObject = samgr->GetSystemAbility(saId);
   sptr<ITestAbility> testAbility = iface_cast<ITestAbility>(remoteObject); // Use the iface_cast macro to convert the proxy to a specific type.
   
   // Obtain the proxy of the SA registered with any other devices.
   sptr<ISystemAbilityManager> samgr = SystemAbilityManagerClient::GetInstance().GetSystemAbilityManager();
   
   // networkId is the device identifier and can be obtained through GetLocalNodeDeviceInfo.
   sptr<IRemoteObject> remoteObject = samgr->GetSystemAbility(saId, networkId);
   sptr<TestAbilityProxy> proxy(new TestAbilityProxy(remoteObject)); // Construct a proxy.
   ```

### **Using JS APIs**

1. Add dependencies.

   ```ts
    import rpc from '@ohos.rpc';
    // Import @ohos.ability.featureAbility only for the application developed based on the FA model.
    // import featureAbility from '@ohos.ability.featureAbility';
    ```

    If you use the stage model, you need to obtain the context. The sample code is as follows:

    ```ts
    import UIAbility from '@ohos.app.ability.UIAbility';
    import Want from '@ohos.app.ability.Want';
    import hilog from '@ohos.hilog';
    import AbilityConstant from '@ohos.app.ability.AbilityConstant';
    import window from '@ohos.window';

    export default class MainAbility extends UIAbility {
      onCreate(want: Want, launchParam: AbilityConstant.LaunchParam) {
        hilog.info(0x0000, 'testTag', '%{public}s', 'UIAbility onCreate');
        let context = this.context;
      }
      onDestroy() {
        hilog.info(0x0000, 'testTag', '%{public}s', 'UIAbility onDestroy');
      }
      onWindowStageCreate(windowStage: window.WindowStage) {
        // Main window is created, set main page for this ability
	  	hilog.info(0x0000, 'testTag', '%{public}s', 'UIAbility onWindowStageCreate');
      }
      onWindowStageDestroy() {
        // Main window is destroyed, release UI related resources
	  	hilog.info(0x0000, 'testTag', '%{public}s', 'UIAbility onWindowStageDestroy');
      }
      onForeground() {
        // Ability has brought to foreground
        hilog.info(0x0000, 'testTag', '%{public}s', 'UIAbility onForeground');
      }
      onBackground() {
        // Ability has back to background
        hilog.info(0x0000, 'testTag', '%{public}s', 'UIAbility onBackground');
      }
    }
   ```

2. Bind the desired ability.

   Construct the **want** variable, and specify the bundle name and component name of the application where the ability is located. If cross-device communication is involved, also specify the network ID of the target device, which can be obtained through **deviceManager**. Then, construct the **connect** variable, and specify the callback that is called when the binding is successful, the binding fails, or the ability is disconnected. If you use the FA model, call the API provided by **featureAbility** to bind an ability. If you use the stage model, obtain a service instance through **Context**, and then call the API provided by **featureAbility** to bind an ability.

   ```ts
    // Import @ohos.ability.featureAbility only for the application developed based on the FA model.
    // import featureAbility from "@ohos.ability.featureAbility";
    import rpc from '@ohos.rpc';
    import Want from '@ohos.app.ability.Want';
    import common from '@ohos.app.ability.common';
    import hilog from '@ohos.hilog';
    import deviceManager from '@ohos.distributedHardware.deviceManager';
    import { BusinessError } from '@ohos.base';

    let dmInstance: deviceManager.DeviceManager | undefined;
    let proxy: rpc.IRemoteObject | undefined = undefined;
    let connectId: number;

    // Bind the ability on a single device.
    let want: Want = {
      // Enter the bundle name and ability name.
      bundleName: "ohos.rpc.test.server",
      abilityName: "ohos.rpc.test.server.ServiceAbility",
    };
    let connect: common.ConnectOptions = {
      onConnect: (elementName, remoteProxy) => {
        hilog.info(0x0000, 'testTag', 'RpcClient: js onConnect called');
        proxy = remoteProxy;
      },
      onDisconnect: (elementName) => {
        hilog.info(0x0000, 'testTag', 'RpcClient: onDisconnect');
      },
      onFailed: () => {
        hilog.info(0x0000, 'testTag', 'RpcClient: onFailed');
      }
    };
    // Use this method to connect to the ability in the FA model.
    // connectId = featureAbility.connectAbility(want, connect);

    connectId = this.context.connectServiceExtensionAbility(want,connect);

    // Cross-device binding
    let deviceManagerCallback = (err: BusinessError, data: deviceManager.DeviceManager) => {
      if (err) {
        hilog.error(0x0000, 'testTag', 'createDeviceManager errCode:' + err.code + ', errMessage:' + err.message);
        return;
      }
      hilog.info(0x0000, 'testTag', 'createDeviceManager success');
      dmInstance = data;
    }
    try{
      deviceManager.createDeviceManager("ohos.rpc.test", deviceManagerCallback);
    } catch(error) {
      let err: BusinessError = error as BusinessError;
      hilog.error(0x0000, 'testTag', 'createDeviceManager errCode:' + err.code + ', errMessage:' + err.message);
    }

    // Use deviceManager to obtain the network ID of the target device.
    if (dmInstance != undefined) {
      let deviceList: Array<deviceManager.DeviceInfo> = dmInstance.getTrustedDeviceListSync();
      let networkId: string = deviceList[0].networkId;
      let want: Want = {
        bundleName: "ohos.rpc.test.server",
        abilityName: "ohos.rpc.test.service.ServiceAbility",
        deviceId: networkId,
        flags: 256
      };
      // The ID returned after the connection is set up must be saved. The ID will be passed for service disconnection.
      // Use this method to connect to the ability in the FA model.
      // connectId = featureAbility.connectAbility(want, connect);
      
      // The first parameter specifies the bundle name of the application, and the second parameter specifies the callback used to return the device ID obtained by using DeviceManager.
      connectId = this.context.connectServiceExtensionAbility(want,connect);
    }
   ```

3. Process requests sent from the client.

   Call the **onConnect** API to return a proxy object inherited from **rpc.RemoteObject** after the ability is successfully bound. Implement the **onRemoteMessageRequest** API for the proxy object to process requests sent from the client.

   ```ts
    import rpc from '@ohos.rpc';
    import Want from '@ohos.app.ability.Want';
    class Stub extends rpc.RemoteObject {
      constructor(descriptor: string) {
        super(descriptor);
      }
      onRemoteMessageRequest(code: number, data: rpc.MessageSequence, reply: rpc.MessageSequence, option: rpc.MessageOption): boolean | Promise<boolean> {
        // Process requests sent from the client based on the code.
        return true;
      }

      onConnect(want: Want) {
        const robj: rpc.RemoteObject = new Stub("rpcTestAbility");
        return robj;
      }
    } 
   ```

4. Process responses sent from the server.

   Obtain the proxy object from the **onConnect** callback, call **sendRequest** to send a request, and receive the response using a callback or a promise (an object representing the eventual completion or failure of an asynchronous operation and its result value).

   ```ts
    import rpc from '@ohos.rpc';
    import hilog from '@ohos.hilog';

    // Use a promise.
    let option = new rpc.MessageOption();
    let data = rpc.MessageSequence.create();
    let reply = rpc.MessageSequence.create();
    // Write parameters to data.
    let proxy: rpc.IRemoteObject | undefined = undefined;
    proxy.sendMessageRequest(1, data, reply, option)
      .then((result: rpc.RequestResult) => {
        if (result.errCode != 0) {
          hilog.error(0x0000, 'testTag', 'sendMessageRequest failed, errCode: ' + result.errCode);
          return;
        }
        // Read the result from result.reply.
      })
      .catch((e: Error) => {
        hilog.error(0x0000, 'testTag', 'sendMessageRequest got exception: ' + e);
      })
      .finally(() => {
        data.reclaim();
        reply.reclaim();
      })
 
    // Use a callback.
    function sendRequestCallback(err: Error, result: rpc.SendRequestResult) {
      try {
        if (result.errCode != 0) {
          hilog.error(0x0000, 'testTag', 'sendMessageRequest failed, errCode: ' + result.errCode);
          return;
        }
        // Read the result from result.reply.
      } finally {
          result.data.reclaim();
          result.reply.reclaim();
      }
    }
    let options = new rpc.MessageOption();
    let datas = rpc.MessageSequence.create();
    let replys = rpc.MessageSequence.create();
    // Write parameters to data.
    proxy.sendMessageRequest(1, datas, replys, options, sendRequestCallback);
   ```

5. Tear down the connection.

   If you use the FA model, call the API provided by **featureAbility** to tear down the connection when the communication is over. If you use the stage model, obtain a service instance through **Context**, and then call the API provided by **featureAbility** to tear down the connection.

   ```ts
    import rpc from '@ohos.rpc';
    import Want from '@ohos.app.ability.Want';
    import hilog from '@ohos.hilog';
    import common from '@ohos.app.ability.common';
    // Import @ohos.ability.featureAbility only for the application developed based on the FA model.
    // import featureAbility from "@ohos.ability.featureAbility";

    function disconnectCallback() {
      hilog.info(0x0000, 'testTag', 'disconnect ability done');
    }
    // Use this method to disconnect from the ability in the FA model.
    // featureAbility.disconnectAbility(connectId, disconnectCallback);

    let proxy: rpc.IRemoteObject | undefined = undefined;
    let connectId: number;

    // Bind the ability on a single device.
    let want: Want = {
      // Enter the bundle name and ability name.
      bundleName: "ohos.rpc.test.server",
      abilityName: "ohos.rpc.test.server.ServiceAbility",
    };
    let connect: common.ConnectOptions = {
      onConnect: (elementName, remote) => {
        proxy = remote;
      },
      onDisconnect: (elementName) => {
      },
      onFailed: () => {
        proxy;
      }
    };
    // Use this method to connect to the ability in the FA model.
    // connectId = featureAbility.connectAbility(want, connect);

    connectId = this.context.connectServiceExtensionAbility(want,connect);

    this.context.disconnectServiceExtensionAbility(connectId);
   ```


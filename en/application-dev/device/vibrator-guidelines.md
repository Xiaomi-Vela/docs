# Vibrator Development


## When to Use

You can set different vibration effects as needed, for example, customizing the vibration intensity, frequency, and duration for button touches, alarm clocks, and incoming calls.

For details about the APIs, see [Vibrator](../reference/apis/js-apis-vibrator.md).


## Available APIs

| Module         | API                                                      | Description                                                        |
| ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ohos.vibrator | startVibration(effect: VibrateEffect, attribute: VibrateAttribute): Promise&lt;void&gt; | Starts vibration with the specified effect and attribute. This API uses a promise to return the result.|
| ohos.vibrator | startVibration(effect: VibrateEffect, attribute: VibrateAttribute, callback: AsyncCallback&lt;void&gt;): void | Starts vibration with the specified effect and attribute. This API uses an asynchronous callback to return the result.|
| ohos.vibrator | stopVibration(stopMode: VibratorStopMode): Promise&lt;void&gt; | Stops vibration in the specified mode. This API uses a promise to return the result.                                |
| ohos.vibrator | stopVibration(stopMode: VibratorStopMode, callback: AsyncCallback&lt;void&gt;): void | Stops vibration in the specified mode. This API uses an asynchronous callback to return the result.                                |
| ohos.vibrator | stopVibration(): Promise&lt;void&gt;                         | Stops vibration in all modes. This API uses a promise to return the result.                                    |
| ohos.vibrator | stopVibration(callback: AsyncCallback&lt;void&gt;): void     | Stops vibration in all modes. This API uses an asynchronous callback to return the result.                                    |
| ohos.vibrator | isSupportEffect(effectId: string): Promise&lt;boolean&gt;    | Checks whether the passed effect ID is supported. This API uses a promise to return the result. The value **true** means that the passed effect ID is supported, and **false** means the opposite.|
| ohos.vibrator | isSupportEffect(effectId: string, callback: AsyncCallback&lt;boolean&gt;): void | Checks whether the passed effect ID is supported. This API uses an asynchronous callback to return the result. The value **true** means that the passed effect ID is supported, and **false** means the opposite.|


## Custom Vibration Format

Custom vibration enables you to design desired vibration effects by customizing a vibration configuration file and orchestrating vibration forms based on the corresponding rules.

The custom vibration configuration file is in JSON format. An example file is as follows:

```json
{
    "MetaData": {
        "Create": "2023-01-09",
        "Description": "a haptic case",
        "Version": 1.0,
        "ChannelNumber": 1
    },
    "Channels": [
        {
            "Parameters": {
                "Index": 1
            },
            "Pattern": [
                {
                    "Event": {
                        "Type": "transient",
                        "StartTime": 0,
                        "Parameters": {
                            "Intensity": 100,
                            "Frequency": 31
                        }
                    }
                },
                {
                    "Event": {
                        "Type": "continuous",
                        "StartTime": 100,
                        "Duration": 54,
                        "Parameters": {
                            "Intensity": 38,
                            "Frequency": 30
                        }
                    }
                }
            ]
        }
    ]
}
```

This JSON file contains two attributes: **MetaData** and **Channels**.
- **MetaData** contains information about the file header. You can add the following attributes under **MetaData**:
  - **Version**: version number of the file format, which is forward compatible. Currently, only version 1.0 is supported. This parameter is mandatory.
  - **ChannelNumber**: number of channels for vibration. Currently, only one channel is supported, and the value is fixed at **1**. This parameter is mandatory.
  - **Create**: time when the file was created. This parameter is optional.
  - **Description**: additional information such as the vibration effect and creation information. This parameter is optional.
- **Channels** provides information about the vibration channel. It is a JSON array that holds information about each channel. It contains two attributes: **Parameters** and **Pattern**.
- **Parameters** provides parameters related to the channel. Under it, **Index** indicates the channel ID. The value is fixed at **1** for a single channel. This parameter is mandatory.
  - **Pattern** indicates the vibration sequence. It is a JSON array. Under it, **Event** indicates a vibration event, which can be either of the following types:
  - **transient**: short vibration
  - **continuous**: long vibration

The table below describes the parameters under **Event**.

| Parameter| Description| Value or Value Range|
| --- | ------------------------ | ---|
| Type | Type of the vibration event. This parameter is mandatory.| **transient** or **continuous**|
| StartTime | Start time of the vibration. This parameter is mandatory.| [0, 1800 000], in ms, without overlapping|
| Duration | Duration of the vibration. This parameter is valid only when **Type** is **continuous**.| (10, 1600), in ms|
| Intensity | Intensity of the vibration. This parameter is mandatory.| [0, 100], a relative value that does not represent the actual vibration strength.|
| Frequency | Frequency of the vibration. This parameter is mandatory.| [0, 100], a relative value that does not represent the actual vibration frequency|

The following requirements must be met:

| Item| Description                |
| -------- | ------------------------ |
| Number of vibration events| No more than 128|
| Length of the vibration configuration file| Not greater than 64 KB|


## How to Develop

1. Before using the vibrator on a device, you must declare the **ohos.permission.VIBRATE** permission. For details about how to configure a permission, see [Declaring Permissions](../security/accesstoken-guidelines.md).

2. Start vibration with the specified effect and attribute.

   ```js
   import vibrator from '@ohos.vibrator';
   try {
       vibrator.startVibration({ // To use startVibration, you must configure the ohos.permission.VIBRATE permission.
           type: 'time',
           duration: 1000,
       }, {
           id: 0,
           usage: 'alarm'
       }, (error) => {
           if (error) {
               console.error('vibrate fail, error.code: ' + error.code + 'error.message: ', + error.message);
               return;
           }
           console.log('Callback returned to indicate a successful vibration.');
       });
   } catch (err) {
       console.error('errCode: ' + err.code + ' ,msg: ' + err.message);
   }
   ```

3. Stop vibration in the specified mode.

   ```js
   import vibrator from '@ohos.vibrator';
   try {
       // Stop vibration in VIBRATOR_STOP_MODE_TIME mode. To use stopVibration, you must configure the ohos.permission.VIBRATE permission.
       vibrator.stopVibration(vibrator.VibratorStopMode.VIBRATOR_STOP_MODE_TIME, function (error) {
           if (error) {
               console.log('error.code' + error.code + 'error.message' + error.message);
               return;
           }
           console.log('Callback returned to indicate successful.');
       })
   } catch (err) {
       console.info('errCode: ' + err.code + ' ,msg: ' + err.message);
   }
   ```

4. Stop vibration in all modes.

   ```js
   import vibrator from '@ohos.vibrator';
   // To use startVibration and stopVibration, you must configure the ohos.permission.VIBRATE permission.
   try {
       vibrator.startVibration({
           type: 'time',
           duration: 1000,
       }, {
           id: 0,
           usage: 'alarm'
       }, (error) => {
           if (error) {
               console.error('vibrate fail, error.code: ' + error.code + 'error.message: ', + error.message);
               return;
           }
           console.log('Callback returned to indicate a successful vibration.');
       });
       // Stop vibration in all modes.
       vibrator.stopVibration(function (error) {
           if (error) {
               console.log('error.code' + error.code + 'error.message' + error.message);
               return;
           }
           console.log('Callback returned to indicate successful.');
       })
   } catch (error) {
       console.info('errCode: ' + error.code + ' ,msg: ' + error.message);
   }
   ```

5. Check whether the passed effect ID is supported.

   ```js
   import vibrator from '@ohos.vibrator';
   try {
       // Check whether 'haptic.clock.timer' is supported.
       vibrator.isSupportEffect('haptic.clock.timer', function (err, state) {
           if (err) {
               console.error('isSupportEffect failed, error:' + JSON.stringify(err));
               return;
           }
           console.log('The effectId is ' + (state ? 'supported' : 'unsupported'));
           if (state) {
               try {
                   vibrator.startVibration({ // To use startVibration, you must configure the ohos.permission.VIBRATE permission.
                       type: 'preset',
                       effectId: 'haptic.clock.timer',
                       count: 1,
                   }, {
                       usage: 'unknown'
                   }, (error) => {
                       if(error) {
                           console.error('haptic.clock.timer vibrator error:'  + JSON.stringify(error));
                       } else {
                           console.log('haptic.clock.timer vibrator success');
                       }
                   });
               } catch (error) {
                   console.error('Exception in, error:' + JSON.stringify(error));
               }
           }
       })
   } catch (error) {
       console.error('Exception in, error:' + JSON.stringify(error));
   }
   ```

6. Start and stop custom vibration.

   ```js
   import vibrator from '@ohos.vibrator';
   import resourceManager from '@ohos.resourceManager';
   
   const FILE_NAME = "xxx.json";
   
   async function openResource(fileName) {
       let fileDescriptor = undefined;
       let mgr = await resourceManager.getResourceManager();
       await mgr.getRawFd(fileName).then(value => {
           fileDescriptor = {fd: value.fd, offset: value.offset, length: value.length};
           console.log('openResource success fileName: ' + fileName);
       }).catch(error => {
           console.log('openResource err: ' + error);
       });
       return fileDescriptor;
   }
   
   async function closeResource(fileName) {
       let mgr = await resourceManager.getResourceManager();
       await mgr.closeRawFd(fileName).then(()=> {
           console.log('closeResource success fileName: ' + fileName);
       }).catch(error => {
           console.log('closeResource err: ' + error);
       });
   }
   
   // Obtain the file descriptor of the vibration configuration file.
   let rawFd = openResource(FILE_NAME);
   // To use startVibration and stopVibration, you must configure the ohos.permission.VIBRATE permission.
   try {
       // Start custom vibration.
       vibrator.startVibration({
           type: "file",
           hapticFd: { fd: rawFd.fd, offset: rawFd.offset, length: rawFd.length }
       }, {
           usage: "alarm"
       }).then(() => {
           console.info('startVibration success');
       }, (error) => {
           console.info('startVibration error');
       });
       // Stop vibration in all modes.
       vibrator.stopVibration(function (error) {
           if (error) {
               console.log('error.code' + error.code + 'error.message' + error.message);
               return;
           }
           console.log('Callback returned to indicate successful.');
       })
   } catch (error) {
       console.info('errCode: ' + error.code + ' ,msg: ' + error.message);
   }
   // Close the vibration configuration file.
   closeResource(FILE_NAME);
   ```


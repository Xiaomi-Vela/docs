# Call Service Development

## Scenario Description

You can implement the call service in either of the following ways:
- For a system application, use the **dial** API to make a voice or video call. The call will be displayed on the application page.
- For a third-party application, use the **makecall** API to start the system call application. Users can then make calls as needed.

## Basic Concepts

- Call status code
  A code used to report the current call status to the application, so that the application can then take appropriate logic processing. For example, if there is no ongoing call, the application allows you to make a new call.

  | Name              | Value  | Description                                                        |
  | ------------------ | ---- | ------------------------------------------------------------ |
  | CALL_STATE_UNKNOWN | -1   | The call status fails to be obtained and is unknown.                        |
  | CALL_STATE_IDLE    | 0    | No call is in progress.                                    |
  | CALL_STATE_RINGING | 1    | The call is in the ringing or waiting state.                                    |
  | CALL_STATE_OFFHOOK | 2    | At least one call is in dialing, active, or on hold, and no new incoming call is ringing or waiting.|

## Constraints

1. The call service is available only on standard-system devices.
2. An available SIM card must be present on the device.


## Available APIs

> **NOTE**
> To maximize the application running efficiency, most API calls are called asynchronously in callback or promise mode. The following code examples use the callback mode. For details about the APIs, see [call API Reference](../reference/apis/js-apis-call.md).

|                                  Name                                            | Description                                                        |
| ----------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| hasVoiceCapability(): boolean;                                                      | Checks whether the voice function is available.                                       |
| dial(phoneNumber: string, callback: AsyncCallback<boolean>): void                   | Makes a call. This is a system API.                                     |
| makeCall(phoneNumber: string, callback: AsyncCallback<void>): void                  | Redirects to the dial screen and displays the called number.                                 |

The **observer** module provides the functions of subscribing to and unsubscribing from the call service status. For details about the APIs, see [observer API Reference](../reference/apis/js-apis-observer.md).

| Name                                                      | Description              |
| ------------------------------------------------------------ | ------------------ |
| on(type: 'callStateChange', options: { slotId: number }, callback: Callback<{ state: CallState, number: string }>): void | Listens to call status changes.|

## How to Develop

### Making a Call by Using the **dial** API (for System Applications Only)

1. Declare the required permission: **ohos.permission.PLACE_CALL**.
This permission is of the **system\_basic** level. Before applying for the permission, ensure that the [basic principles for permission management](../security/accesstoken-overview.md#basic-principles-for-permission-management) are met. Then, declare the corresponding permission by following instructions in [Declaring Permissions in the Configuration File](../security/accesstoken-guidelines.md#declaring-permissions-in-the-configuration-file).
2. Import the **call** and **observer** modules.
3. Invoke the **hasVoiceCapability** API to check whether the device supports the voice call function.
   If the voice call function is supported, the user will be redirected to the dial screen and the dialed number is displayed.
4. Invoke the **dial** API to make a call.
5. (Optional) Register the observer for call status changes.
   ```js
    // Import the required modules.
    import call from '@ohos.telephony.call'
    import observer from '@ohos.telephony.observer'

    // Check whether the voice call function is supported.
    let isSupport = call.hasVoiceCapability();
    if (!isSupport) {
        console.log("not support voice capability, return.");
        return;
    }
    // If the device supports the voice call function, call the following API to make a call.
    call.dial("13xxxx", (err, data) => {
        this.output = this.output + `dial: ${JSON.stringify(data)}\n`
        console.log(`callback: dial err->${JSON.stringify(err)} data->${JSON.stringify(data)}`)
    })

    // (Optional) Register the observer for call service status changes.
    observer.on("callStateChange", {slotId: 0}, (data) => {
        console.log("call state change, data is:" + JSON.stringify(data));
    });
   ```

### Making a Call by Using the makecall API

1. Import the **call** and **observer** modules.
2. Invoke the **hasVoiceCapability** API to check whether the device supports the voice call function.
   If the voice call function is supported, the user will be redirected to the dial screen and the dialed number is displayed.
3. Invoke the **makecall** API to start the system call application and make a call.
4. (Optional) Register the observer for call status changes.

   ```js
    // Import the required modules.
    import call from '@ohos.telephony.call'
    import observer from '@ohos.telephony.observer' 
   
    // Check whether the voice call function is supported.
    let isSupport = call.hasVoiceCapability();
    if (!isSupport) {
        console.log("not support voice capability, return.");
        return;
    }
    // If the voice call function is supported, the user will be redirected to the dial screen and the dialed number is displayed.
    call.makeCall("13xxxx", (err)=> {
        if (!err) {
            console.log("make call success.");
        } else {
            console.log("make call fail, err is:" + JSON.stringify(err));
        }
    });

    // (Optional) Register the observer for call service status changes.
    observer.on("callStateChange", {slotId: 0}, (data) => {
        console.log("call state change, data is:" + JSON.stringify(data));
    });
   ```

## Samples

The following sample is provided to help you better understand how to develop the call service:

- [Call](https://gitee.com/openharmony/applications_app_samples/tree/master/Telephony/Call)

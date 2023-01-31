# Battery Level

> **NOTE**
> - The APIs of this module are no longer maintained since API version 6. You are advised to use [`@ohos.batteryInfo`](js-apis-battery-info.md).
> 
> - The initial APIs of this module are supported since API version 3. Newly added APIs will be marked with a superscript to indicate their earliest API version.


## Modules to Import


```js
import battery from '@system.battery';
```


## battery.getStatus

getStatus(Object): void

Obtains the current charging state and battery level.

**System capability**: SystemCapability.PowerManager.BatteryManager.Core

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| success | (data: [BatteryResponse](#batteryresponse)) => void | No| Called when API call is successful.|
| fail | (data: string, code: number) => void | No| Called when API call has failed.|
| complete | () => void | No| Called when API call is complete.|

**Example**

```js
export default {    
  getStatus() {       
    battery.getStatus({           
      success: function(data) {               
        console.log('success get battery level:' + data.level);           
      },            
      fail: function(data, code) {                
        console.log('fail to get battery level code:' + code + ', data: ' + data);            
      },        
    });    
  },
}
```

## BatteryResponse

| Name| Type| Description|
| -------- | -------- | -------- |
| charging | boolean | Whether the battery is being charged.|
| level | number | Current battery level, which ranges from **0.00** to **1.00**.|

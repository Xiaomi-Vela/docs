# 位置服务


> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块


```
import geolocation from '@ohos.geolocation';
```

## geolocation.on('locationChange')

on(type: 'locationChange', request: LocationRequest, callback: Callback&lt;Location&gt;) : void

开启位置变化订阅，并发起定位请求。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“locationChange”，表示位置变化。 |
  | request | LocationRequest | 是 | 设置位置请求参数。 |
  | callback | Callback&lt;[Location](#location)&gt; | 是 | 接收位置变化状态变化监听。 |


- 示例：
  
  ```
  var requestInfo = {'priority': 0x203, 'scenario': 0x300, 'timeInterval': 0, 'distanceInterval': 0, 'maxAccuracy': 0};
  var locationChange = (location) => {
      console.log('locationChanger: data: ' + JSON.stringify(location));
  };
  geolocation.on('locationChange', requestInfo, locationChange);
  ```


## geolocation.off('locationChange')

off(type: 'locationChange', callback?: Callback&lt;Location&gt;) : void

关闭位置变化订阅，并删除对应的定位请求。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“locationChange”，表示位置变化。 |
  | callback | Callback&lt;[Location](#location)&gt; | 否 | 接收位置变化状态变化监听。 |


- 示例：
  
  ```
  var requestInfo = {'priority': 0x203, 'scenario': 0x300, 'timeInterval': 0, 'distanceInterval': 0, 'maxAccuracy': 0};
  var locationChange = (location) => {
      console.log('locationChanger: data: ' + JSON.stringify(location));
  };
  geolocation.on('locationChange', requestInfo, locationChange);
  geolocation.off('locationChange', locationChange);
  ```


## geolocation.on('locationServiceState')

on(type: 'locationServiceState', callback: Callback&lt;boolean&gt;) : void

订阅位置服务状态变化。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“locationServiceState”，表示位置服务状态。 |
  | callback | Callback&lt;boolean&gt; | 是 | 接收位置服务状态变化监听。 |


- 示例：
  
  ```
  var locationServiceState = (state) => {
      console.log('locationServiceState: ' + state);
  }
  geolocation.on('locationServiceState', locationServiceState);
  ```


## geolocation.off('locationServiceState')

off(type: 'locationServiceState', callback?: Callback&lt;boolean&gt;) : void;

取消订阅位置服务状态变化。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“locationServiceState”，表示位置服务状态。 |
  | callback | Callback&lt;boolean&gt; | 否 | 接收位置服务状态变化监听。 |


- 示例：
  
  ```
  var locationServiceState = (state) => {
      console.log('locationServiceState: state: ' + state);
  }
  geolocation.on('locationServiceState', locationServiceState);
  geolocation.off('locationServiceState', locationServiceState);
  ```


## geolocation.on('cachedGnssLocationsReporting')<sup>8+</sup>

on(type: 'cachedGnssLocationsReporting', request: CachedGnssLocationsRequest, callback: Callback&lt;Array&lt;Location&gt;&gt;) : void;

订阅缓存GNSS定位结果上报事件。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“cachedGnssLocationsReporting”，表示GNSS缓存定位结果上报。 |
  | request | CachedGnssLocationsRequest | 是 | GNSS缓存功能配置参数 |
  | callback | Callback&lt;boolean&gt; | 是 | 接收GNSS缓存位置上报。 |


- 示例：
  
  ```
  var cachedLocationsCb = (locations) => {
      console.log('cachedGnssLocationsReporting: locations: ' + locations);
  }
  var requestInfo = {'reportingPeriodSec': 10, 'wakeUpCacheQueueFull': true};
  geolocation.on('cachedGnssLocationsReporting', requestInfo, cachedLocationsCb);
  ```


## geolocation.off('cachedGnssLocationsReporting')<sup>8+</sup>

off(type: 'cachedGnssLocationsReporting', callback?: Callback&lt;Array&lt;Location&gt;&gt;) : void;

取消订阅缓存GNSS定位结果上报事件。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“cachedGnssLocationsReporting”，表示GNSS缓存定位结果上报。 |
  | callback | Callback&lt;boolean&gt; | 否 | 接收GNSS缓存位置上报。 |


- 示例：
  
  ```
  var cachedLocationsCb = (locations) => {
      console.log('cachedGnssLocationsReporting: locations: ' + locations);
  }
  var requestInfo = {'reportingPeriodSec': 10, 'wakeUpCacheQueueFull': true};
  geolocation.on('cachedGnssLocationsReporting', requestInfo, cachedLocationsCb);
  geolocation.off('cachedGnssLocationsReporting');
  ```


## geolocation.on('gnssStatusChange')<sup>8+</sup>

on(type: 'gnssStatusChange', callback: Callback&lt;SatelliteStatusInfo&gt;) : void;

订阅GNSS卫星状态信息上报事件。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“gnssStatusChange”，表示订阅GNSS卫星状态信息上报。 |
  | callback | Callback&lt;SatelliteStatusInfo&gt; | 是 | 接收GNSS卫星状态信息上报。 |


- 示例：
  
  ```
  var gnssStatusCb = (satelliteStatusInfo) => {
      console.log('gnssStatusChange: ' + satelliteStatusInfo);
  }
  geolocation.on('gnssStatusChange', gnssStatusCb);
  ```


## geolocation.off('gnssStatusChange')<sup>8+</sup>

off(type: 'gnssStatusChange', callback?: Callback&lt;SatelliteStatusInfo&gt;) : void;

取消订阅GNSS卫星状态信息上报事件。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“gnssStatusChange”，表示订阅GNSS卫星状态信息上报。 |
  | callback | Callback&lt;SatelliteStatusInfo&gt; | 否 | 接收GNSS卫星状态信息上报。 |

- 示例：
  
  ```
  var gnssStatusCb = (satelliteStatusInfo) => {
      console.log('gnssStatusChange: ' + satelliteStatusInfo);
  }
  geolocation.on('gnssStatusChange', gnssStatusCb);
  geolocation.off('gnssStatusChange', gnssStatusCb);
  ```


## geolocation.on('nmeaMessageChange')<sup>8+</sup>

on(type: 'nmeaMessageChange', callback: Callback&lt;string&gt;) : void;

订阅GNSS NMEA信息上报事件。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“nmeaMessageChange”，表示订阅GNSS&nbsp;NMEA信息上报。 |
  | callback | Callback&lt;string&gt; | 是 | 接收GNSS&nbsp;NMEA信息上报。 |


- 示例：
  
  ```
  var nmeaCb = (str) => {
      console.log('nmeaMessageChange: ' + str);
  }
  geolocation.on('nmeaMessageChange', nmeaCb );
  ```


## geolocation.off('nmeaMessageChange')<sup>8+</sup>

off(type: 'nmeaMessageChange', callback?: Callback&lt;string&gt;) : void;

取消订阅GNSS NMEA信息上报事件。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“nmeaMessageChange”，表示订阅GNSS&nbsp;NMEA信息上报。 |
  | callback | Callback&lt;string&gt; | 否 | 接收GNSS&nbsp;NMEA信息上报。 |


- 示例：
  
  ```
  var nmeaCb = (str) => {
      console.log('nmeaMessageChange: ' + str);
  }
  geolocation.on('nmeaMessageChange', nmeaCb);
  geolocation.off('nmeaMessageChange', nmeaCb);
  ```


## geolocation.on('fenceStatusChange')<sup>8+</sup>

on(type: 'fenceStatusChange', request: GeofenceRequest, want: WantAgent) : void;

添加一个围栏，并订阅地理围栏事件。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geofence

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“fenceStatusChange”，表示订阅围栏事件上报。 |
  | request | GeofenceRequest | 是 | 围栏的配置参数。 |
  | want | WantAgent | 是 | 用于接收地理围栏事件上报（进出围栏）。 |


- 示例：
  
  ```
  import WantAgent from '@ohos.wantAgent';
  import { OperationType, WantAgentFlags } from '@ohos.wantagent';
  //wantAgent对象
  var wantAgent;
  //getWantAgent回调
  function getWantAgentCallback(err, data) {
  	console.info("==========================>getWantAgentCallback=======================>");
      if (err.code == 0) {
  	wantAgent = data;
      } else {
          console.info('----getWantAgent failed!----');
      }
  }
  //WantAgentInfo对象
  var wantAgentInfo = {
      wants: [
          {
              deviceId: "deviceId",
              bundleName: "com.neu.setResultOnAbilityResultTest1",
              abilityName: "com.example.test.MainAbility",
              action: "action1",
              entities: ["entity1"],
              type: "MIMETYPE",
              uri: "key={true,true,false}",
              parameters:
              {
                  mykey0: 2222,
                  mykey1: [1, 2, 3],
                  mykey2: "[1, 2, 3]",
                  mykey3: "ssssssssssssssssssssssssss",
                  mykey4: [false, true, false],
                  mykey5: ["qqqqq", "wwwwww", "aaaaaaaaaaaaaaaaa"],
                  mykey6: true,
              }
          }
      ],
      operationType: OperationType.START_ABILITIES,
      requestCode: 0,
      wantAgentFlags:[WantAgentFlags.UPDATE_PRESENT_FLAG]
  }
  WantAgent.getWantAgent(wantAgentInfo, getWantAgentCallback)
  var requestInfo = {'priority': 0x201, 'scenario': 0x301, "geofence": {"latitude": 121, "longitude": 26, "radius": 100, "expiration": 10000}};
  geolocation.on('fenceStatusChange', requestInfo, wantAgent);
  ```


## geolocation.off('fenceStatusChange')<sup>8+</sup>

off(type: 'fenceStatusChange', request: GeofenceRequest, want: WantAgent) : void;

删除一个围栏，并取消订阅该围栏事件。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geofence

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“fenceStatusChange”，表示订阅围栏事件上报。 |
  | request | GeofenceRequest | 是 | 围栏的配置参数。 |
  | want | WantAgent | 是 | 用于接收地理围栏事件上报（进出围栏）。 |

- 示例：
  
  ```
  import WantAgent from '@ohos.wantAgent';
  import { OperationType, WantAgentFlags } from '@ohos.wantagent';
  //wantAgent对象
  var wantAgent;
  //getWantAgent回调
  function getWantAgentCallback(err, data) {
  	console.info("==========================>getWantAgentCallback=======================>");
      if (err.code == 0) {
  	wantAgent = data;
      } else {
          console.info('----getWantAgent failed!----');
      }
  }
  //WantAgentInfo对象
  var wantAgentInfo = {
      wants: [
          {
              deviceId: "deviceId",
              bundleName: "com.neu.setResultOnAbilityResultTest1",
              abilityName: "com.example.test.MainAbility",
              action: "action1",
              entities: ["entity1"],
              type: "MIMETYPE",
              uri: "key={true,true,false}",
              parameters:
              {
                  mykey0: 2222,
                  mykey1: [1, 2, 3],
                  mykey2: "[1, 2, 3]",
                  mykey3: "ssssssssssssssssssssssssss",
                  mykey4: [false, true, false],
                  mykey5: ["qqqqq", "wwwwww", "aaaaaaaaaaaaaaaaa"],
                  mykey6: true,
              }
          }
      ],
      operationType: OperationType.START_ABILITIES,
      requestCode: 0,
      wantAgentFlags:[WantAgentFlags.UPDATE_PRESENT_FLAG]
  }
  WantAgent.getWantAgent(wantAgentInfo, getWantAgentCallback)
  var requestInfo = {'priority': 0x201, 'scenario': 0x301, "geofence": {"latitude": 121, "longitude": 26, "radius": 100, "expiration": 10000}};
  geolocation.on('fenceStatusChange', requestInfo, wantAgent);
  geolocation.off('fenceStatusChange', requestInfo, wantAgent);
  ```


## geolocation.getCurrentLocation

getCurrentLocation(request: CurrentLocationRequest, callback: AsyncCallback&lt;Location&gt;) : void


获取当前位置，使用callback回调异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | request | [CurrentLocationRequest](#currentlocationrequest) | 否 | 设置位置请求参数。 |
  | callback | AsyncCallback&lt;[Location](#location)&gt; | 是 | 用来接收位置信息的回调。 |

- 示例：
  
  ```
  var requestInfo = {'priority': 0x203, 'scenario': 0x300,'maxAccuracy': 0};
  var locationChange = (err, location) => {
      console.log('locationChanger: ' + err + 'data: ' + location);
  };
  geolocation.getCurrentLocation(requestInfo, locationChange);
  geolocation.getCurrentLocation(locationChange);
  ```


## geolocation.getCurrentLocation

getCurrentLocation(request?: CurrentLocationRequest) : Promise&lt;Location&gt;


获取当前位置，使用Promise方式异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | request | [CurrentLocationRequest](#currentlocationrequest) | 否 | 设置位置请求参数。 |

- 返回值：
    | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;[Location](#location)&gt; | 返回位置信息。 |


- 示例：
  
  ```
  var requestInfo = {'priority': 0x203, 'scenario': 0x300,'maxAccuracy': 0};
  geolocation.getCurrentLocation(requestInfo).then((result) => {
      console.log('current location: ' + JSON.stringify(result));
  });
  ```


## geolocation.getLastLocation

getLastLocation(callback: AsyncCallback&lt;Location&gt;) : void

获取上一次位置，使用callback回调异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;[Location](#location)&gt; | 是 | 用来接收上次位置的回调。 |


- 示例：
  
  ```
  geolocation.getLastLocation((err, data) => {
      console.log('getLastLocation: ' + err + " data: " + JSON.stringify(data));
  });
  ```


## geolocation.getLastLocation

getLastLocation() : Promise&lt;Location&gt;

获取上一次位置，使用Promise方式异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

- 返回值：
    | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;[Location](#location)&gt; | 返回上次位置信息。 |


- 示例：
  
  ```
  geolocation.getLastLocation().then((result) => {
      console.log('getLastLocation: result: ' + JSON.stringify(result));
  });
  ```


## geolocation.isLocationEnabled

isLocationEnabled(callback: AsyncCallback&lt;boolean&gt;) : void


判断位置服务是否已经打开，使用callback回调异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 用来接收位置服务状态的回调。 |


- 示例：
  
  ```
  geolocation.isLocationEnabled((err, data) => {
      console.log('isLocationEnabled: ' + err + " data: " + data);
  });
  ```


## geolocation.isLocationEnabled

isLocationEnabled() : Promise&lt;boolean&gt;

判断位置服务是否已经开启，使用Promise方式异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

- 返回值：
    | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 返回位置服务是否可用的状态。 |

- 示例：
  
  ```
  geolocation.isLocationEnabled().then((result) => {
      console.log('promise, isLocationEnabled: ' + result);
  });
  ```


## geolocation.requestEnableLocation

requestEnableLocation(callback: AsyncCallback&lt;boolean&gt;) : void


请求打开位置服务，使用callback回调异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 用来接收位置服务状态的回调。 |


- 示例：
  
  ```
  geolocation.requestEnableLocation((err, data) => {
      console.log('requestEnableLocation: ' + err + " data: " + data);
  });
  ```


## geolocation.requestEnableLocation

requestEnableLocation() : Promise&lt;boolean&gt;

请求打开位置服务，使用Promise方式异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

- 返回值：
    | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 返回位置服务是否可用。 |


- 示例：
  
  ```
  geolocation.requestEnableLocation().then((result) => {
      console.log('promise, requestEnableLocation: ' + result);
  });
  ```


## geolocation.enableLocation

enableLocation(callback: AsyncCallback&lt;boolean&gt;) : void;

打开位置服务，使用callback回调异步返回结果。

**系统API**：此接口为系统接口，三方应用不支持调用。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 用来接收位置服务状态的回调。 |


- 示例：
  
  ```
  geolocation.enableLocation((err, data) => {
      console.log('enableLocation: ' + err + " data: " + data);
  });
  ```


## geolocation.enableLocation

enableLocation() : Promise&lt;boolean&gt;

打开位置服务，使用Promise方式异步返回结果。

**系统API**：此接口为系统接口，三方应用不支持调用。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

- 返回值：
    | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 返回位置服务是否可用。 |


- 示例：
  
  ```
  geolocation.enableLocation().then((result) => {
      console.log('promise, enableLocation: ' + result);
  });
  ```

## geolocation.disableLocation

disableLocation(callback: AsyncCallback&lt;boolean&gt;) : void;

打开位置服务，使用callback回调异步返回结果。

**系统API**：此接口为系统接口，三方应用不支持调用。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 用来接收位置服务状态的回调。 |


- 示例：
  
  ```
  geolocation.disableLocation((err, data) => {
      console.log('disableLocation: ' + err + " data: " + data);
  });
  ```


## geolocation.disableLocation

disableLocation() : Promise&lt;boolean&gt;

打开位置服务，使用Promise方式异步返回结果。

**系统API**：此接口为系统接口，三方应用不支持调用。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

- 返回值：
    | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 返回位置服务是否可用。 |


- 示例：
  
  ```
  geolocation.disableLocation().then((result) => {
      console.log('promise, disableLocation: ' + result);
  });
  ```

## geolocation.isGeoServiceAvailable

isGeoServiceAvailable(callback: AsyncCallback&lt;boolean&gt;) : void

判断（逆）地理编码服务状态，使用callback回调异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 用来接收地理编码服务状态的回调。 |


- 示例：
  
  ```
  geolocation.isGeoServiceAvailable((err, data) => {
      console.log('isGeoServiceAvailable: ' + err + " data: " + data);
  });
  ```


## geolocation.isGeoServiceAvailable

isGeoServiceAvailable() : Promise&lt;boolean&gt;

判断（逆）地理编码服务状态，使用Promise方式异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

- 返回值：
    | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 返回地理编码服务是否可用的状态。 |


- 示例：
  
  ```
  geolocation.isGeoServiceAvailable().then((result) => {
      console.log('promise, isGeoServiceAvailable: ' + result);
  });
  ```



## geolocation.getAddressesFromLocation

getAddressesFromLocation(request: ReverseGeoCodeRequest, callback: AsyncCallback&lt;Array&lt;GeoAddress&gt;&gt;) : void

调用逆地理编码服务，将坐标转换为地理描述，使用callback回调异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | request | [ReverseGeoCodeRequest](#reversegeocoderequest) | 是 | 设置逆地理编码请求的相关参数。 |
  | callback | AsyncCallback&lt;Array&lt;[GeoAddress](#geoaddress)&gt;&gt; | 是 | 设置接收逆地理编码请求的回调参数。 |

- 示例：
  
  ```
  var reverseGeocodeRequest = {"latitude": 31.12, "longitude": 121.11, "maxItems": 1};
  geolocation.getAddressesFromLocation(reverseGeocodeRequest, (err, data) => {
      console.log('getAddressesFromLocation: ' + err + " data: " + JSON.stringify(data));
  });
  ```


## geolocation.getAddressesFromLocation

getAddressesFromLocation(request: ReverseGeoCodeRequest) : Promise&lt;Array&lt;GeoAddress&gt;&gt;;

调用逆地理编码服务，将坐标转换为地理描述，使用Promise方式异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | request | [ReverseGeoCodeRequest](#reversegeocoderequest) | 是 | 设置逆地理编码请求的相关参数。 |

- 返回值：
    | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;Array&lt;[GeoAddress](#geoaddress)&gt;&gt; | 返回地理描述信息。 |

- 示例：
  
  ```
  var reverseGeocodeRequest = {"latitude": 31.12, "longitude": 121.11, "maxItems": 1};
  geolocation.getAddressesFromLocation(reverseGeocodeRequest).then((data) => {
      console.log('getAddressesFromLocation: ' + JSON.stringify(data));
  });
  ```


## geolocation.getAddressesFromLocationName

getAddressesFromLocationName(request: GeoCodeRequest, callback: AsyncCallback&lt;Array&lt;GeoAddress&gt;&gt;) : void

调用地理编码服务，将地理描述转换为具体坐标，使用callback回调异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | request | [GeoCodeRequest](#geocoderequest) | 是 | 设置地理编码请求的相关参数。 |
  | callback | AsyncCallback&lt;Array&lt;[GeoAddress](#geoaddress)&gt;&gt; | 是 | 设置接收地理编码请求的回调参数。 |


- 示例：
  
  ```
  var geocodeRequest = {"description": "上海市浦东新区xx路xx号", "maxItems": 1};
  geolocation.getAddressesFromLocationName(geocodeRequest, (err, data) => {
      console.log('getAddressesFromLocationName: ' + err + " data: " + JSON.stringify(data));
  });
  ```


## geolocation.getAddressesFromLocationName

getAddressesFromLocationName(request: GeoCodeRequest) : Promise&lt;Array&lt;GeoAddress&gt;&gt;

调用地理编码服务，将地理描述转换为具体坐标，使用Promise方式异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | request | [GeoCodeRequest](#geocoderequest) | 是 | 设置地理编码请求的相关参数。 |

- 返回值：
    | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;Array&lt;[GeoAddress](#geoaddress)&gt;&gt; | 设置接收地理编码请求的回调参数。 |

- 示例：
  
  ```
  var geocodeRequest = {"description": "上海市浦东新区xx路xx号", "maxItems": 1};
  geolocation.getAddressesFromLocationName(geocodeRequest).then((result) => {
      console.log('getAddressesFromLocationName: ' + JSON.stringify(result));
  });
  ```



## geolocation.getCachedGnssLocationsSize<sup>8+</sup>

getCachedGnssLocationsSize(callback: AsyncCallback&lt;number&gt;) : void;

获取GNSS芯片缓存位置的个数。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;number&gt; | 是 | 用来接收GNSS芯片缓存位置个数的回调。 |

- 示例：
  
  ```
  geolocation.getCachedGnssLocationsSize((err, size) => {
      console.log('getCachedGnssLocationsSize: err:' + err + " size: " + size);
  });
  ```


## geolocation.getCachedGnssLocationsSize<sup>8+</sup>

getCachedGnssLocationsSize() : Promise&lt;number&gt;;

获取GNSS芯片缓存位置的个数。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

- 返回值：
    | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;number&gt; | 返回GNSS缓存位置的个数。 |

- 示例：
  
  ```
  geolocation.getCachedGnssLocationsSize().then((result) => {
      console.log('promise, getCachedGnssLocationsSize: ' + result);
  });
  ```


## geolocation.flushCachedGnssLocations<sup>8+</sup>

flushCachedGnssLocations(callback: AsyncCallback&lt;boolean&gt;) : void;

读取并清空GNSS芯片所有缓存位置。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 用来接收清空GNSS芯片缓存位置操作的结果。 |

- 示例：
  
  ```
  geolocation.flushCachedGnssLocations((err, result) => {
      console.log('flushCachedGnssLocations: err:' + err + " result: " + result);
  });
  ```


## geolocation.flushCachedGnssLocations<sup>8+</sup>

flushCachedGnssLocations() : Promise&lt;boolean&gt;;

读取并清空GNSS芯片所有缓存位置。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

- 返回值：
    | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 清空所有GNSS缓存位置是否成功。 |

- 示例：
  
  ```
  geolocation.flushCachedGnssLocations().then((result) => {
      console.log('promise, flushCachedGnssLocations: ' + result);
  });
  ```


## geolocation.sendCommand<sup>8+</sup>

sendCommand(command: LocationCommand, callback: AsyncCallback&lt;boolean&gt;) : void;

给位置服务子系统的各个部件发送扩展命令。只有系统应用才能调用。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | command | LocationCommand | 是 | 指定目标场景，和将要发送的命令（字符串）。 |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 用来接收命令发送的结果。 |

- 示例：
  
  ```
  var requestInfo = {'scenario': 0x301, 'command': "command_1"};
  geolocation.sendCommand(requestInfo, (err, result) => {
      console.log('sendCommand: err:' + err + " result: " + result);
  });
  ```


## geolocation.sendCommand<sup>8+</sup>

sendCommand(command: LocationCommand) : Promise&lt;boolean&gt;;

给位置服务子系统的各个部件发送扩展命令。只有系统应用才能调用。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | command | LocationCommand | 是 | 指定目标场景，和将要发送的命令（字符串）。 |

- 返回值：
    | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 表示命令发送成功或失败。 |

- 示例：
  
  ```
  var requestInfo = {'scenario': 0x301, 'command': "command_1"};
  geolocation.sendCommand(requestInfo).then((result) => {
      console.log('promise, sendCommand: ' + result);
  });
  ```


## geolocation.isLocationPrivacyConfirmed<sup>8+</sup>

isLocationPrivacyConfirmed(type : LocationPrivacyType, callback: AsyncCallback&lt;boolean&gt;) : void;

查询用户是否同意定位服务隐私申明，是否同意启用定位服务。只有系统应用才能调用。

**系统API**：此接口为系统接口，三方应用不支持调用。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | LocationPrivacyType | 是 | 指定隐私申明场景，例如开机向导中的隐私申明、开启网络定位功能时弹出的隐私申明等。 |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 表示用户是否同意定位服务隐私申明。 |

- 示例：
  
  ```
  geolocation.isLocationPrivacyConfirmed(1, (err, result) => {
      console.log('isLocationPrivacyConfirmed: err:' + err + " result: " + result);
  });
  ```


## geolocation.isLocationPrivacyConfirmed<sup>8+</sup>

isLocationPrivacyConfirmed(type : LocationPrivacyType,) : Promise&lt;boolean&gt;;

查询用户是否同意定位服务隐私申明，是否同意启用定位服务。只有系统应用才能调用。

**系统API**：此接口为系统接口，三方应用不支持调用。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | LocationPrivacyType | 是 | 指定隐私申明场景，例如开机向导中的隐私申明、开启网络定位功能时弹出的隐私申明等。 |

- 返回值：
    | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 表示用户是否同意定位服务隐私申明。 |

- 示例：
  
  ```
  geolocation.isLocationPrivacyConfirmed(1).then((result) => {
      console.log('promise, isLocationPrivacyConfirmed: ' + result);
  });
  ```


## geolocation.setLocationPrivacyConfirmStatus<sup>8+</sup>

setLocationPrivacyConfirmStatus(type : LocationPrivacyType, isConfirmed: boolean, callback: AsyncCallback&lt;boolean&gt;) : void;

设置用户勾选定位服务隐私申明的状态，记录用户是否同意启用定位服务。只有系统应用才能调用。

**系统API**：此接口为系统接口，三方应用不支持调用。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | LocationPrivacyType | 是 | 指定隐私申明场景，例如开机向导中的隐私申明、开启网络定位功能时弹出的隐私申明等。 |
  | isConfirmed | boolean | 是 | 表示用户是否同意定位服务隐私申明。 |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 表示操作是否成功。 |

- 示例：
  
  ```
  geolocation.setLocationPrivacyConfirmStatus(1, true, (err, result) => {
      console.log('isLocationPrivacyConfirmed: err:' + err + " result: " + result);
  });
  ```


## geolocation.setLocationPrivacyConfirmStatus<sup>8+</sup>

setLocationPrivacyConfirmStatus(type : LocationPrivacyType, isConfirmed : boolean) : Promise&lt;boolean&gt;;

设置用户勾选定位服务隐私申明的状态，记录用户是否同意启用定位服务。只有系统应用才能调用。

**系统API**：此接口为系统接口，三方应用不支持调用。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

- 参数：
    | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | LocationPrivacyType | 是 | 指定隐私申明场景，例如开机向导中的隐私申明、开启网络定位功能时弹出的隐私申明等。 |
  | isConfirmed | boolean | 是 | 表示用户是否同意定位服务隐私申明。 |

- 返回值：
    | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 表示操作是否成功。 |

- 示例：
  
  ```
  geolocation.setLocationPrivacyConfirmStatus(1, true).then((result) => {
      console.log('promise, setLocationPrivacyConfirmStatus: ' + result);
  });
  ```



## LocationRequestPriority

位置请求中位置信息优先级设置。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 默认值 | 说明 |
| -------- | -------- | -------- |
| UNSET | 0x200 | 表示未设置优先级。 |
| ACCURACY | 0x201 | 表示精度优先。 |
| LOW_POWER | 0x202 | 表示低功耗优先。 |
| FIRST_FIX | 0x203 | 表示快速获取位置优先，如果应用希望快速拿到1个位置，可以将优先级设置为该字段。 |


## LocationRequestScenario

  位置请求中定位场景设置。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 默认值 | 说明 |
| -------- | -------- | -------- |
| UNSET | 0x300 | 表示未设置场景信息。 |
| NAVIGATION | 0x301 | 表示导航场景。 |
| TRAJECTORY_TRACKING | 0x302 | 表示运动轨迹记录场景。 |
| CAR_HAILING | 0x303 | 表示打车场景。 |
| DAILY_LIFE_SERVICE | 0x304 | 表示日常服务使用场景。 |
| NO_POWER | 0x305 | 表示无功耗功场景，这种场景下不会主动触发定位，会在其他应用定位时，才给当前应用返回位置。 |


## GeoLocationErrorCode

位置服务中的错误码信息。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 默认值 | 说明 |
| -------- | -------- | -------- |
| INPUT_PARAMS_ERROR | 101 | 表示输入参数错误。 |
| REVERSE_GEOCODE_ERROR | 102 | 表示逆地理编码接口调用失败。 |
| GEOCODE_ERROR | 103 | 表示地理编码接口调用失败。 |
| LOCATOR_ERROR | 104 | 表示定位失败。 |
| LOCATION_SWITCH_ERROR | 105 | 表示定位开关。 |
| LAST_KNOWN_LOCATION_ERROR | 106 | 表示获取上次位置失败。 |
| LOCATION_REQUEST_TIMEOUT_ERROR | 107 | 表示单次定位，没有在指定时间内返回位置。 |


## ReverseGeoCodeRequest

逆地理编码请求接口。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| locale | string | 否 | 指定位置描述信息的语言，“zh”代表中文，“en”代表英文。 |
| latitude | number | 是 | 表示纬度信息，正值表示北纬，负值表示南纬。 |
| longitude | number | 是 | 表示经度信息，正值表示东经，负值表示西经。 |
| maxItems | number | 否 | 指定返回位置信息的最大个数。 |


## GeoCodeRequest

地理编码请求接口。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| locale | string | 否 | 表示位置描述信息的语言，“zh”代表中文，“en”代表英文。 |
| description | number | 是 | 表示位置信息描述，如“上海市浦东新区xx路xx号”。 |
| maxItems | number | 否 | 表示返回位置信息的最大个数。 |
| minLatitude | number | 否 | 表示最小纬度信息，与下面三个参数一起，表示一个经纬度范围。 |
| minLongitude | number | 否 | 表示最小经度信息。 |
| maxLatitude | number | 否 | 表示最大纬度信息。 |
| maxLongitude | number | 否 | 表示最大经度信息。 |


## GeoAddress

地理编码类型。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| latitude | number | 否 | 表示纬度信息，正值表示北纬，负值表示南纬。 |
| longitude | number | 否 | 表示经度信息，正值表示东经，负值表是西经。 |
| locale | string | 否 | 表示位置描述信息的语言，“zh”代表中文，“en”代表英文。 |
| placeName | string | 否 | 表示地区信息。 |
| countryCode | string | 否 | 表示国家码信息。 |
| countryName | string | 否 | 表示国家信息。 |
| administrativeArea | string | 否 | 表示省份区域信息。 |
| subAdministrativeArea | string | 否 | 表示表示子区域信息。 |
| locality | string | 否 | 表示城市信息。 |
| subLocality | string | 否 | 表示子城市信息。 |
| roadName | string | 否 | 表示路名信息。 |
| subRoadName | string | 否 | 表示子路名信息。 |
| premises | string | 否 | 表示门牌号信息。 |
| postalCode | string | 否 | 表示邮政编码信息。 |
| phoneNumber | string | 否 | 表示联系方式信息。 |
| addressUrl | string | 否 | 表示位置信息附件的网址信息。 |
| descriptions | Array&lt;string&gt; | 否 | 表示附加的描述信息。 |
| descriptionsSize | number | 否 | 表示附加的描述信息数量。 |


## LocationRequest

位置信息请求类型。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| priority | [LocationRequestPriority](#locationrequestpriority) | 否 | 表示优先级信息。 |
| scenario | [LocationRequestScenario](#locationrequestscenario) | 是 | 表示场景信息。 |
| timeInterval | number | 否 | 表示上报位置信息的时间间隔。 |
| distanceInterval | number | 否 | 表示上报位置信息的距离间隔。 |
| maxAccuracy | number | 否 | 表示精度信息。 |


## CurrentLocationRequest

当前位置信息请求类型。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| priority | [LocationRequestPriority](#locationrequestpriority) | 否 | 表示优先级信息。 |
| scenario | [LocationRequestScenario](#locationrequestscenario) | 否 | 表示场景信息。 |
| maxAccuracy | number | 否 | 表示精度信息，单位是米。 |
| timeoutMs | number | 否 | 表示超时时间，单位是毫秒，最小为1000毫秒。 |


## SatelliteStatusInfo<sup>8+</sup>

卫星状态信息。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| satellitesNumber | number | 是 | 表示卫星个数。 |
| satelliteIds | Array&lt;number&gt; | 是 | 表示每个卫星的ID，数组类型。 |
| carrierToNoiseDensitys | Array&lt;number&gt; | 是 | 表示载波噪声功率谱密度比，即cn0。 |
| altitudes | Array&lt;number&gt; | 是 | 表示高程信息。 |
| azimuths | Array&lt;number&gt; | 是 | 表示方位角。 |
| carrierFrequencies | Array&lt;number&gt; | 是 | 表示载波频率。 |


## CachedGnssLocationsRequest<sup>8+</sup>

请求订阅GNSS缓存位置上报功能接口的配置参数。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| reportingPeriodSec | number | 是 | 表示GNSS缓存位置上报的周期，单位是毫秒。 |
| wakeUpCacheQueueFull | boolean | 是 | true表示GNSS芯片底层缓存队列满之后会主动唤醒AP芯片，并把缓存位置上报给应用。<br/>false表示GNSS芯片底层缓存队列满之后不会主动唤醒AP芯片，会把缓存位置直接丢弃。 |


## Geofence<sup>8+</sup>

GNSS围栏的配置参数。目前只支持圆形围栏。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geofence

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| latitude | number | 是 | 表示纬度。 |
| longitude | number | 是 | 表示经度。 |
| radius | number | 是 | 表示圆形围栏的半径。 |
| expiration | number | 是 | 围栏存活的时间，单位是毫秒。 |


## GeofenceRequest<sup>8+</sup>

请求添加GNSS围栏消息中携带的参数，包括定位优先级、定位场景和围栏信息。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geofence

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| priority | LocationRequestPriority | 是 | 表示位置信息优先级。 |
| scenario | LocationRequestScenario | 是 | 表示定位场景。 |
| geofence | Geofence | 是 | 表示围栏信息。 |


## LocationPrivacyType<sup>8+</sup>

定位服务隐私协议类型。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 默认值 | 说明 |
| -------- | -------- | -------- |
| OTHERS | 0 | 其他场景。 |
| STARTUP | 1 | 开机向导场景下的隐私协议。 |
| CORE_LOCATION | 2 | 开启网络定位时弹出的隐私协议。 |


## LocationCommand<sup>8+</sup>

扩展命令结构体。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| scenario | LocationRequestScenario | 是 | 表示定位场景。 |
| command | string | 是 | 扩展命令字符串。 |


## Location

位置信息类型。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| latitude | number | 是 | 表示纬度信息，正值表示北纬，负值表示南纬。 |
| longitude | number | 是 | 表示经度信息，正值表示东经，负值表是西经。 |
| altitude | number | 是 | 表示高度信息，单位米。 |
| accuracy | number | 是 | 表示精度信息，单位米。 |
| speed | number | 是 | 表示速度信息，单位米每秒。 |
| timeStamp | number | 是 | 表示位置时间戳，UTC格式。 |
| direction | number | 是 | 表示航向信息。 |
| timeSinceBoot | number | 是 | 表示位置时间戳，开机时间格式。 |
| additions | Array&lt;string&gt; | 否 | 附加信息。 |
| additionSize | number | 否 | 附加信息数量。 |

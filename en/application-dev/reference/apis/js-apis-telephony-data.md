# Cellular Data

> **NOTE**<br>
> The initial APIs of this module are supported since API version 7. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```
import data from '@ohos.telephony.data';
```

## data.getDefaultCellularDataSlotId

getDefaultCellularDataSlotId(callback: AsyncCallback\<number\>): void 

Obtains the default SIM card used for mobile data. This API uses an asynchronous callback to return the result. 

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Telephony.CellularData

**Parameters**

| Name  | Type                   | Mandatory| Description                                      |
| -------- | ----------------------- | ---- | ------------------------------------------ |
| callback | AsyncCallback\<number\> | Yes  | Callback used to return the result.<br>**0**: card slot 1<br>**1**: card slot 2|

**Example**

```
data.getDefaultCellularDataSlotId((err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```

## data.getDefaultCellularDataSlotId

getDefaultCellularDataSlotId(): Promise\<number\> 

Obtains the default SIM card used for mobile data. This API uses a promise to return the result. 

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Telephony.CellularData

**Return Value**

| Type             | Description                                                        |
| ----------------- | ------------------------------------------------------------ |
| Promise\<number\> | Promise used to return the result.<br>**0**: card slot 1<br>**1**: card slot 2|

**Example**

```
let promise = data.getDefaultCellularDataSlotId();
promise.then((data) => {
    console.log(`test success, promise: data->${JSON.stringify(data)}`);
}).catch((err) => {
    console.error(`test fail, promise: err->${JSON.stringify(err)}`);
});
```

## data.getCellularDataFlowType

getCellularDataFlowType(callback: AsyncCallback\<DataFlowType\>): void

Obtains the cellular data flow type, which can be uplink or downlink. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Telephony.CellularData

**Parameters**

| Name  | Type                                          | Mandatory| Description      |
| -------- | ---------------------------------------------- | ---- | ---------- |
| callback | AsyncCallback\<[DataFlowType](#dataflowtype)\> | Yes  | Callback used to return the result.|

**Example**

```
data.getCellularDataFlowType((err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```

## data.getCellularDataFlowType

getCellularDataFlowType(): Promise\<DataFlowType\>

Obtains the cellular data flow type, which can be uplink or downlink. This API uses a promise to return the result.

**System capability**: SystemCapability.Telephony.CellularData

**Return Value**

| Type                                    | Description                                           |
| ---------------------------------------- | ----------------------------------------------- |
| Promise\<[DataFlowType](#dataflowtype)\> | Promise used to return the result. |

**Example**

```
let promise = data.getCellularDataFlowType();
promise.then((data) => {
    console.log(`test success, promise: data->${JSON.stringify(data)}`);
}).catch((err) => {
    console.error(`test fail, promise: err->${JSON.stringify(err)}`);
});
```

## data.getCellularDataState

getCellularDataState(callback: AsyncCallback\<DataConnectState\>): void

Obtains the connection status of the packet switched (PS) domain. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Telephony.CellularData

**Parameters**

| Name  | Type                                                  | Mandatory| Description      |
| -------- | ------------------------------------------------------ | ---- | ---------- |
| callback | AsyncCallback\<[DataConnectState](#dataconnectstate)\> | Yes  | Callback used to return the result.|

**Example**

```
data.getCellularDataState((err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```

## data.getCellularDataState

getCellularDataState(): Promise\<DataConnectState\>

Obtains the connection status of the PS domain. This API uses a promise to return the result.

**System capability**: SystemCapability.Telephony.CellularData

**Return Value**

| Type                                            | Description                                 |
| ------------------------------------------------ | ------------------------------------- |
| Promise\<[DataConnectState](#dataconnectstate)\> | Promise used to return the result.|

**Example**

```
let promise = data.getCellularDataState();
promise.then((data) => {
    console.log(`test success, promise: data->${JSON.stringify(data)}`);
}).catch((err) => {
    console.error(`test fail, promise: err->${JSON.stringify(err)}`);
});
```

## data.isCellularDataEnabled

isCellularDataEnabled(callback: AsyncCallback\<boolean\>): void

Checks whether the cellular data service is enabled. This API uses an asynchronous callback to return the result.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Telephony.CellularData

**Parameters**

| Name  | Type                    | Mandatory| Description                                                        |
| -------- | ------------------------ | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback\<boolean\> | Yes  | Callback used to return the result.<br>**true**: The cellular data service is enabled.<br>**false**: The cellular data service is disabled.|

**Example**

```
data.isCellularDataEnabled((err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```

## data.isCellularDataEnabled

isCellularDataEnabled(): Promise\<boolean\>

Checks whether the cellular data service is enabled. This API uses a promise to return the result.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Telephony.CellularData

**Return Value**

| Type              | Description                                                        |
| ------------------ | ------------------------------------------------------------ |
| Promise\<boolean\> | Promise used to return the result.<br>**true**: The cellular data service is enabled.<br>**false**: The cellular data service is disabled.|

**Example**

```
let promise = data.isCellularDataEnabled();
promise.then((data) => {
    console.log(`test success, promise: data->${JSON.stringify(data)}`);
}).catch((err) => {
    console.error(`test fail, promise: err->${JSON.stringify(err)}`);
});
```

## data.isCellularDataRoamingEnabled

isCellularDataRoamingEnabled(slotId: number, callback: AsyncCallback\<boolean\>): void

Checks whether roaming is enabled for the cellular data service. This API uses an asynchronous callback to return the result.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Telephony.CellularData

**Parameters**

| Name  | Type                    | Mandatory| Description                                                        |
| -------- | ------------------------ | ---- | ------------------------------------------------------------ |
| slotId   | number                   | Yes  | Card slot ID. <br>**0**: card slot 1<br>**1**: card slot 2                    |
| callback | AsyncCallback\<boolean\> | Yes  | Callback used to return the result.<br>**true**: Roaming is enabled for the cellular data service.<br>**false**: Roaming is disabled for the cellular data service.|

**Example**

```
data.isCellularDataRoamingEnabled(0,(err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```

## data.isCellularDataRoamingEnabled

isCellularDataRoamingEnabled(slotId: number): Promise\<boolean\>

Checks whether roaming is enabled for the cellular data service. This API uses a promise to return the result.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Telephony.CellularData

**Parameters**

| Name| Type  | Mandatory| Description                                    |
| ------ | ------ | ---- | ---------------------------------------- |
| slotId | number | Yes  | Card slot ID. <br>**0**: card slot 1<br>**1**: card slot 2|

**Return Value**

| Type              | Description                                                        |
| ------------------ | ------------------------------------------------------------ |
| Promise\<boolean\> | Promise used to return the result.<br>**true**: Roaming is enabled for the cellular data service.<br>**false**: Roaming is disabled for the cellular data service.|

**Example**

```
let promise = data.isCellularDataRoamingEnabled(0);
promise.then((data) => {
    console.log(`test success, promise: data->${JSON.stringify(data)}`);
}).catch((err) => {
    console.error(`test fail, promise: err->${JSON.stringify(err)}`);
});
```

## DataFlowType

Defines the cellular data flow type.

**System capability**: SystemCapability.Telephony.CellularData

| Name                  | Value  | Description                                      |
| ---------------------- | ---- | ------------------------------------------ |
| DATA_FLOW_TYPE_NONE    | 0    | No uplink or downlink data is available.                  |
| DATA_FLOW_TYPE_DOWN    | 1    | Only the downlink data is available.                        |
| DATA_FLOW_TYPE_UP      | 2    | Only the uplink data is available.                        |
| DATA_FLOW_TYPE_UP_DOWN | 3    | Both uplink data and downlink data are available.                        |
| DATA_FLOW_TYPE_DORMANT | 4    | No uplink or downlink data is available because the lower-layer link is in the dormant state.|

## DataConnectState

Describes the connection status of a cellular data link.

**System capability**: SystemCapability.Telephony.CellularData

| Name                   | Value  | Description                      |
| ----------------------- | ---- | -------------------------- |
| DATA_STATE_UNKNOWN     | -1   | The status of the cellular data link is unknown.    |
| DATA_STATE_DISCONNECTED | 0    | The cellular data link is disconnected.    |
| DATA_STATE_CONNECTING   | 1    | The cellular data link is being connected.|
| DATA_STATE_CONNECTED    | 2    | The cellular data link is connected.  |
| DATA_STATE_SUSPENDED    | 3    | The cellular data link is suspended.  |

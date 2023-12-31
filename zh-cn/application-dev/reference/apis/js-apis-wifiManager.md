# @ohos.wifiManager (WLAN)
该模块主要提供WLAN基础功能、P2P（peer-to-peer）功能和WLAN消息通知的相应服务，让应用可以通过WLAN和其他设备互联互通。

> **说明：**
> 本模块首批接口从API version 6开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```ts
import wifiManager from '@ohos.wifiManager';
```

## wifiManager.enableWifi<sup>9+</sup>

enableWifi(): void

使能WLAN，异步接口，需要通过注册"wifiStateChange"事件的回调来监听是否打开成功。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.SET_WIFI_INFO 和 ohos.permission.MANAGE_WIFI_CONNECTION  仅系统应用可用。

**系统能力：** SystemCapability.Communication.WiFi.STA

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|
| 2501003  | Failed for wifi is closing.|

**示例：**

```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		wifiManager.enableWifi();
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.disableWifi<sup>9+</sup>

disableWifi(): void

去使能WLAN，异步接口，需要通过注册"wifiStateChange"事件的回调来监听是否关闭成功。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.SET_WIFI_INFO 和 ohos.permission.MANAGE_WIFI_CONNECTION，仅系统应用可用。

**系统能力：** SystemCapability.Communication.WiFi.STA

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|
| 2501004  | Failed for wifi is opening.|

**示例：**

```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		wifiManager.disableWifi();
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.isWifiActive<sup>9+</sup>

isWifiActive(): boolean

查询WLAN是否已使能。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**返回值：**

  | **类型** | **说明** |
  | -------- | -------- |
  | boolean | true:已使能，&nbsp;false:未使能。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**

```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let isWifiActive = wifiManager.isWifiActive();
		console.info("isWifiActive:" + isWifiActive);
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.scan<sup>9+</sup>

scan(): void

启动WLAN扫描。

**需要权限：** ohos.permission.SET_WIFI_INFO、ohos.permission.LOCATION 和 ohos.permission.APPROXIMATELY_LOCATION

**系统能力：** SystemCapability.Communication.WiFi.STA

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**

```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		wifiManager.scan();
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.startScan<sup>10+</sup>

startScan(): void

**系统接口：** 此接口为系统接口。

启动WLAN扫描。

**需要权限：** ohos.permission.SET_WIFI_INFO 和ohos.permission.MANAGE_WIFI_CONNECTION

**系统能力：** SystemCapability.Communication.WiFi.STA

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**

```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		wifiManager.startScan();
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```
## wifiManager.getScanResults<sup>9+</sup>

getScanResults(): Promise&lt;Array&lt;WifiScanInfo&gt;&gt;

获取扫描结果，使用Promise异步回调。

**需要权限：** ohos.permission.GET_WIFI_INFO 和 (ohos.permission.GET_WIFI_PEERS_MAC 或(ohos.permission.LOCATION 和 ohos.permission.APPROXIMATELY_LOCATION))

**系统能力：** SystemCapability.Communication.WiFi.STA

**返回值：**

| **类型** | **说明** |
| -------- | -------- |
| Promise&lt;&nbsp;Array&lt;[WifiScanInfo](#wifiscaninfo9)&gt;&nbsp;&gt; | Promise对象。返回扫描到的热点列表。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.getScanResults<sup>9+</sup>

getScanResults(callback: AsyncCallback&lt;Array&lt;WifiScanInfo&gt;&gt;): void

获取扫描结果，使用callback异步回调。

**需要权限：** ohos.permission.GET_WIFI_INFO 和 (ohos.permission.GET_WIFI_PEERS_MAC 或 (ohos.permission.LOCATION 和 ohos.permission.APPROXIMATELY_LOCATION))

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**
| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;&nbsp;Array&lt;[WifiScanInfo](#wifiscaninfo9)&gt;&gt; | 是 | 回调函数。当成功时，err为0，data为扫描到的热点；否则err为非0值，data为空。 |
  | Array&lt;[WifiScanInfo](#wifiscaninfo9)&gt; | 返回扫描到的热点列表。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
| -------- | -------- |
| 2501000  | Operation failed.|

**示例：**
```ts
  import wifiManager from '@ohos.wifiManager';
  
  wifiManager.getScanResults((err, result) => {
      if (err) {
          console.error("get scan info error");
          return;
      }
  
      let len = result.length;
      console.log("wifi received scan info: " + len);
      for (let i = 0; i < len; ++i) {
          console.info("ssid: " + result[i].ssid);
          console.info("bssid: " + result[i].bssid);
          console.info("capabilities: " + result[i].capabilities);
          console.info("securityType: " + result[i].securityType);
          console.info("rssi: " + result[i].rssi);
          console.info("band: " + result[i].band);
          console.info("frequency: " + result[i].frequency);
          console.info("channelWidth: " + result[i].channelWidth);
          console.info("timestamp: " + result[i].timestamp);
      }
  });
  
  wifiManager.getScanResults().then(result => {
      let len = result.length;
      console.log("wifi received scan info: " + len);
      for (let i = 0; i < len; ++i) {
          console.info("ssid: " + result[i].ssid);
          console.info("bssid: " + result[i].bssid);
          console.info("capabilities: " + result[i].capabilities);
          console.info("securityType: " + result[i].securityType);
          console.info("rssi: " + result[i].rssi);
          console.info("band: " + result[i].band);
          console.info("frequency: " + result[i].frequency);
          console.info("channelWidth: " + result[i].channelWidth);
          console.info("timestamp: " + result[i].timestamp);
      }
  }).catch(err => {
      console.error("failed:" + JSON.stringify(err));
  });
```

## wifiManager.getScanResultsSync<sup>9+</sup>

getScanResultsSync(): &nbsp;Array&lt;[WifiScanInfo](#wifiscaninfo9)&gt;

获取扫描结果，使用同步方式返回结果。

**需要权限：** ohos.permission.GET_WIFI_INFO 和 (ohos.permission.GET_WIFI_PEERS_MAC 或 (ohos.permission.LOCATION 和 ohos.permission.APPROXIMATELY_LOCATION))

**系统能力：** SystemCapability.Communication.WiFi.STA

**返回值：**

| **类型** | **说明** |
| -------- | -------- |
| &nbsp;Array&lt;[WifiScanInfo](#wifiscaninfo9)&gt; | 扫描结果数组。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**

```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let scanInfoList = wifiManager.getScanResultsSync();
		console.info("scanInfoList:" + JSON.stringify(scanInfoList));
		let len = scanInfoList.length;
        console.log("wifi received scan info: " + len);
		if(len > 0){
			for (let i = 0; i < len; ++i) {
				console.info("ssid: " + scanInfoList[i].ssid);
				console.info("bssid: " + scanInfoList[i].bssid);
				console.info("capabilities: " + scanInfoList[i].capabilities);
				console.info("securityType: " + scanInfoList[i].securityType);
				console.info("rssi: " + scanInfoList[i].rssi);
				console.info("band: " + scanInfoList[i].band);
				console.info("frequency: " + scanInfoList[i].frequency);
				console.info("channelWidth: " + scanInfoList[i].channelWidth);
				console.info("timestamp: " + scanInfoList[i].timestamp);
			}
		}	
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
	
```

## wifiManager.getScanInfoList<sup>10+</sup>

getScanInfoList(): Array&lt;WifiScanInfo&gt;;

获取扫描结果。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**返回值：**

| **类型** | **说明** |
| -------- | -------- |
| Array&lt;[WifiScanInfo](#wifiscaninfo9)&gt; | 返回扫描到的热点列表。如果应用申请了ohos.permission.GET_WIFI_PEERS_MAC权限，则返回结果中的bssid为真实设备地址，否则为随机设备地址。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**

```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let scanInfoList = wifiManager.getScanInfoList();
		console.info("scanInfoList:" + JSON.stringify(scanInfoList));
		let len = scanInfoList.length;
        console.log("wifi received scan info: " + len);
		if(len > 0){
			for (let i = 0; i < len; ++i) {
				console.info("ssid: " + scanInfoList[i].ssid);
				console.info("bssid: " + scanInfoList[i].bssid);
				console.info("capabilities: " + scanInfoList[i].capabilities);
				console.info("securityType: " + scanInfoList[i].securityType);
				console.info("rssi: " + scanInfoList[i].rssi);
				console.info("band: " + scanInfoList[i].band);
				console.info("frequency: " + scanInfoList[i].frequency);
				console.info("channelWidth: " + scanInfoList[i].channelWidth);
				console.info("timestamp: " + scanInfoList[i].timestamp);
			}
		}	
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
	
```

## WifiScanInfo<sup>9+</sup>

WLAN热点信息。

**系统能力：** SystemCapability.Communication.WiFi.STA


| **名称** | **类型** | **可读** | **可写** | **说明** |
| -------- | -------- | -------- | -------- | -------- |
| ssid | string | 是 | 否 | 热点的SSID，最大长度为32字节，编码格式为UTF-8。 |
| bssid | string | 是 | 否 | 热点的BSSID，例如：00:11:22:33:44:55。 |
| bssidType<sup>10+</sup>| DeviceAddressType | 是 | 否 | 热点的BSSID类型。 |
| capabilities | string | 是 | 否 | 热点能力。 |
| securityType | [WifiSecurityType](#wifisecuritytype9) | 是 | 否 | WLAN加密类型。 |
| rssi | number | 是 | 否 | 热点的信号强度(dBm)。 |
| band | number | 是 | 否 | WLAN接入点的频段。 |
| frequency | number | 是 | 否 | WLAN接入点的频率。 |
| channelWidth | number | 是 | 否 | WLAN接入点的带宽。 |
| centerFrequency0 | number | 是 | 否 | 热点的中心频率。 |
| centerFrequency1 | number | 是 | 否 | 热点的中心频率。如果热点使用两个不重叠的WLAN信道，则返回两个中心频率，分别用centerFrequency0和centerFrequency1表示。 |
| infoElems | Array&lt;[WifiInfoElem](#wifiinfoelem9)&gt; | 是 | 否 | 信息元素。 |
| timestamp | number | 是 | 否 | 时间戳。 |

## DeviceAddressType <sup>10+</sup>

wifi 设备地址（mac/bssid）类型。

**系统能力：** SystemCapability.Communication.WiFi.Core

| **名称** | **值** | **说明** |
| -------- | -------- | -------- |
| RANDOM_DEVICE_ADDRESS | 0 | 随机设备地址。 |
| REAL_DEVICE_ADDRESS | 1 | 真实设备地址。 |

## WifiSecurityType<sup>9+</sup>

表示加密类型的枚举。

**系统能力：** SystemCapability.Communication.WiFi.Core


| **名称** | **值** | **说明** |
| -------- | -------- | -------- |
| WIFI_SEC_TYPE_INVALID | 0 | 无效加密类型。 |
| WIFI_SEC_TYPE_OPEN | 1 | 开放加密类型。 |
| WIFI_SEC_TYPE_WEP | 2 | Wired&nbsp;Equivalent&nbsp;Privacy&nbsp;(WEP)加密类型。 |
| WIFI_SEC_TYPE_PSK | 3 | Pre-shared&nbsp;key&nbsp;(PSK)加密类型。 |
| WIFI_SEC_TYPE_SAE | 4 | Simultaneous&nbsp;Authentication&nbsp;of&nbsp;Equals&nbsp;(SAE)加密类型。 |
| WIFI_SEC_TYPE_EAP | 5 | EAP加密类型。 |
| WIFI_SEC_TYPE_EAP_SUITE_B | 6 | Suite-B 192位加密类型。 |
| WIFI_SEC_TYPE_OWE | 7 | 机会性无线加密类型。 |
| WIFI_SEC_TYPE_WAPI_CERT | 8 | WAPI-Cert加密类型。 |
| WIFI_SEC_TYPE_WAPI_PSK | 9 | WAPI-PSK加密类型。 |


## WifiBandType<sup>10+</sup>

表示WIFI频段类型的枚举。

**系统能力：** SystemCapability.Communication.WiFi.STA

| **名称** | **值** | **说明** |
| -------- | -------- | -------- |
| WIFI_BAND_NONE | 0 | 无效频段类型。 |
| WIFI_BAND_2G | 1 | 2.4G频段类型。 |
| WIFI_BAND_5G | 2 | 5G频段类型。 |
| WIFI_BAND_6G | 3 | 6G频段类型。 |
| WIFI_BAND_60G | 4 | 60G频段类型。 |

## WifiStandard<sup>10+</sup>

表示WIFI标准的枚举。

**系统能力：** SystemCapability.Communication.WiFi.STA

| **名称** | **值** | **说明** |
| -------- | -------- | -------- |
| WIFI_STANDARD_UNDEFINED | 0 | 无效WIFI标准类型。 |
| WIFI_STANDARD_11A | 1 | 802.11a WiFi标准类型。 |
| WIFI_STANDARD_11B | 2 | 802.11b WiFi标准类型。 |
| WIFI_STANDARD_11G | 3 | 802.11g WiFi标准类型。 |
| WIFI_STANDARD_11N | 4 | 802.11n WiFi标准类型。 |
| WIFI_STANDARD_11AC | 5 | 802.11ac WiFi标准类型。 |
| WIFI_STANDARD_11AX | 6 | 802.11ax WiFi标准类型。 |
| WIFI_STANDARD_11AD | 7 | 802.11ad WiFi标准类型。 |

## WifiInfoElem<sup>9+</sup>

WLAN热点信息。

**系统能力：** SystemCapability.Communication.WiFi.STA


| **名称** | **类型** | **可读** | **可写** | **说明** |
| -------- | -------- | -------- | -------- | -------- |
| eid | number | 是 | 否 | 元素ID。 |
| content | Uint8Array | 是 | 否 | 元素内容。 |


## WifiChannelWidth<sup>9+</sup>

表示带宽类型的枚举。

**系统能力：** SystemCapability.Communication.WiFi.STA


| **名称** | **值** | **说明** |
| -------- | -------- | -------- |
| WIDTH_20MHZ | 0 | 20MHZ。 |
| WIDTH_40MHZ | 1 | 40MHZ。 |
| WIDTH_80MHZ | 2 | 80MHZ。 |
| WIDTH_160MHZ | 3 | 160MHZ。 |
| WIDTH_80MHZ_PLUS | 4 | 80MHZ<sup>+</sup>。 |
| WIDTH_INVALID | 5 | 无效值 |

## wifiManager.setScanAlwaysAllowed<sup>10+</sup>

setScanAlwaysAllowed(isScanAlwaysAllowed: boolean): void

设置是否始终允许扫描。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.SET_WIFI_INFO 和 ohos.permission.SET_WIFI_CONFIG

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| isScanAlwaysAllowed | boolean | 是 | 是否始终允许扫描。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let isScanAlwaysAllowed = true;
		wifiManager.setScanAlwaysAllowed(isScanAlwaysAllowed);
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.getScanAlwaysAllowed<sup>10+</sup>

getScanAlwaysAllowed(): boolean

获取是否始终允许扫描。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.GET_WIFI_INFO 和 ohos.permission.GET_WIFI_CONFIG

**系统能力：** SystemCapability.Communication.WiFi.STA

**返回值：**

| **类型** | **说明** |
| -------- | -------- |
| boolean| 是否始终允许扫描。 true 表示允许触发扫描，false表示在禁用wifi时不允许触发扫描|

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**

```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let isScanAlwaysAllowed = wifiManager.getScanAlwaysAllowed();
		console.info("isScanAlwaysAllowed:" + isScanAlwaysAllowed);
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.addDeviceConfig<sup>9+</sup>

addDeviceConfig(config: WifiDeviceConfig): Promise&lt;number&gt;

添加网络配置，使用Promise异步回调。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.SET_WIFI_INFO 和 ohos.permission.SET_WIFI_CONFIG

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| config | [WifiDeviceConfig](#wifideviceconfig9) | 是 | WLAN配置信息。如果bssidType未指定值，则bssidType默认为随机设备地址类型。 |

**返回值：**

  | **类型** | **说明** |
  | -------- | -------- |
  | Promise&lt;number&gt; | Promise对象。返回添加的网络配置ID，如果值为-1表示添加失败。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**

```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let config:wifiManager.WifiDeviceConfig = {
			ssid : "****",
			preSharedKey : "****",
			securityType : 0
		}
		wifiManager.addDeviceConfig(config).then(result => {
			console.info("result:" + JSON.stringify(result));
		}).catch(err => {
			console.error("failed:" + JSON.stringify(err));
		});
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## WifiDeviceConfig<sup>9+</sup>

WLAN配置信息。

**系统能力：** SystemCapability.Communication.WiFi.STA


| **名称** | **类型** | **可读** | **可写** | **说明** |
| -------- | -------- | -------- | -------- | -------- |
| ssid | string | 是 | 否 | 热点的SSID，最大长度为32字节，编码格式为UTF-8。 |
| bssid | string | 是 | 否 | 热点的BSSID，例如：00:11:22:33:44:55。 |
| bssidType<sup>10+</sup> | DeviceAddressType | 是 | 否 | 热点的BSSID类型。 |
| preSharedKey | string | 是 | 否 | 热点的密钥，最大长度为64字节。 |
| isHiddenSsid | boolean | 是 | 否 | 是否是隐藏网络。 |
| securityType | [WifiSecurityType](#wifisecuritytype9)| 是 | 否 | 加密类型。 |
| creatorUid | number | 是 | 否 | 创建用户的ID。 <br /> **系统接口：** 此接口为系统接口。 |
| disableReason | number | 是 | 否 | 禁用原因。 <br /> **系统接口：** 此接口为系统接口。 |
| netId | number | 是 | 否 | 分配的网络ID。 <br /> **系统接口：** 此接口为系统接口。 |
| randomMacType | number | 是 | 否 | MAC地址类型。0 - 随机MAC地址，1 - 设备MAC地址 <br /> **系统接口：** 此接口为系统接口。 |
| randomMacAddr | string | 是 | 否 | MAC地址。<br /> **系统接口：** 此接口为系统接口。 |
| ipType | [IpType](#iptype9) | 是 | 否 | IP地址类型。 <br /> **系统接口：** 此接口为系统接口。 |
| staticIp | [IpConfig](#ipconfig9) | 是 | 否 | 静态IP配置信息。 <br /> **系统接口：** 此接口为系统接口。 |
| eapConfig<sup>10+</sup> | [WifiEapConfig](#wifieapconfig10) | 是 | 否 | 可扩展身份验证协议配置。 |
| proxyConfig<sup>10+</sup> | WifiProxyConfig | 是 | 否 | 代理配置。  <br /> **系统接口：** 此接口为系统接口。|

## IpType<sup>9+</sup>

表示IP类型的枚举。

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.Communication.WiFi.STA


| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| STATIC | 0 | 静态IP。 |
| DHCP | 1 | 通过DHCP获取。 |
| UNKNOWN | 2 | 未指定。 |


## IpConfig<sup>9+</sup>

IP配置信息。

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.Communication.WiFi.STA

| **名称** | **类型** | **可读** | **可写** | **说明** |
| -------- | -------- | -------- | -------- | -------- |
| ipAddress | number | 是 | 否 | IP地址。 |
| gateway | number | 是 | 否 | 网关。 |
| prefixLength | number | 是 | 否 | 掩码。 |
| dnsServers | number[] | 是 | 否 | DNS服务器。 |
| domains | Array&lt;string&gt; | 是 | 否 | 域信息。 |


## WifiEapConfig<sup>10+</sup>

可扩展身份验证协议配置信息。

**系统能力：** SystemCapability.Communication.WiFi.STA

| **名称** | **类型** | **可读** | **可写** | **说明** |
| -------- | -------- | -------- | -------- | -------- |
| eapMethod | [EapMethod](#eapmethod10) | 是 | 否 | EAP认证方式。 |
| phase2Method | [Phase2Method](#phase2method10) | 是 | 否 | 第二阶段认证方式。 |
| identity | string | 是 | 否 | 身份信息。 |
| anonymousIdentity | string | 是 | 否 | 匿名身份。 |
| password | string | 是 | 否 | 密码。 |
| caCertAlias | string | 是 | 否 | CA 证书别名。 |
| caPath | string | 是 | 否 | CA 证书路径。 |
| clientCertAlias | string | 是 | 否 | 客户端证书别名。 |
| certEntry | Uint8Array | 是 | 是 | CA 证书内容。 |
| certPassword | string | 是 | 是 | CA证书密码。 |
| altSubjectMatch | string | 是 | 否 | 替代主题匹配。 |
| domainSuffixMatch | string | 是 | 否 | 域后缀匹配。 |
| realm | string | 是 | 否 | 通行证凭证的领域。 |
| plmn | string | 是 | 否 | 公共陆地移动网的直通凭证提供商。 |
| eapSubId | number | 是 | 否 | SIM卡的子ID。 |


## EapMethod<sup>10+</sup>

表示EAP认证方式的枚举。

**系统能力：** SystemCapability.Communication.WiFi.STA

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| EAP_NONE | 0 | 不指定。 |
| EAP_PEAP | 1 | PEAP类型。 |
| EAP_TLS | 2 | TLS类型。 |
| EAP_TTLS | 3 | TTLS类型。 |
| EAP_PWD | 4 | PWD类型。 |
| EAP_SIM | 5 | SIM类型。 |
| EAP_AKA | 6 | AKA类型。 |
| EAP_AKA_PRIME | 7 | AKA Prime类型。 |
| EAP_UNAUTH_TLS | 8 | UNAUTH TLS类型。 |


## Phase2Method<sup>10+</sup>

表示第二阶段认证方式的枚举。

**系统能力：** SystemCapability.Communication.WiFi.STA

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| PHASE2_NONE | 0 | 不指定。 |
| PHASE2_PAP | 1 | PAP类型。 |
| PHASE2_MSCHAP | 2 | MSCHAP类型。 |
| PHASE2_MSCHAPV2 | 3 | MSCHAPV2类型。 |
| PHASE2_GTC | 4 | GTC类型。 |
| PHASE2_SIM | 5 | SIM类型。 |
| PHASE2_AKA | 6 | AKA类型。 |
| PHASE2_AKA_PRIME | 7 | AKA Prime类型。 |


## WifiProxyConfig <sup>10+</sup>

Wifi 代理配置。

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.Communication.WiFi.STA

| **名称** | **类型** | **可读** | **可写** | **说明** |
| -------- | -------- | -------- | -------- | -------- |
| proxyMethod | ProxyMethod | 是 | 否 | 代理方法 |
| pacWebAddress | string | 是 | 否 | 自动配置代理的PAC web 地址。 |
| serverHostName | string | 是 | 否 | 手动配置代理的服务器主机名。 |
| serverPort | string | 是 | 否 | 手动配置代理的服务器端口。 |
| exclusionObjects | string | 是 | 否 | 手动配置代理的排除对象，对象用“,”分隔。|

## ProxyMethod<sup>10+</sup>

表示WiFi代理方法的枚举。

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.Communication.WiFi.STA

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| METHOD_NONE  | 0 | 不使用代理。 |
| METHOD_AUTO  | 1 | 使用自动配置的代理。 |
| METHOD_MANUAL  | 2 | 使用手动配置的代理。 |

## wifiManager.addDeviceConfig<sup>9+</sup>

addDeviceConfig(config: WifiDeviceConfig, callback: AsyncCallback&lt;number&gt;): void

添加网络配置，使用callback异步回调。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.SET_WIFI_INFO 和 ohos.permission.SET_WIFI_CONFIG

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| config | [WifiDeviceConfig](#wifideviceconfig9) | 是 | WLAN配置信息。如果bssidType未指定值，则bssidType默认为随机设备地址类型。 |
| callback | AsyncCallback&lt;number&gt; | 是 | 回调函数。当操作成功时，err为0，data为添加的网络配置ID，如果data值为-1，表示添加失败。当error为非0，表示处理出现错误。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**

```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let config:wifiManager.WifiDeviceConfig = {
			ssid : "****",
			preSharedKey : "****",
			securityType : 0
		}
		wifiManager.addDeviceConfig(config,(error,result) => {
			console.info("result:" + JSON.stringify(result));
		});	
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.addCandidateConfig<sup>9+</sup>

addCandidateConfig(config: WifiDeviceConfig): Promise&lt;number&gt;

添加候选网络配置，使用Promise异步回调。

**需要权限：** ohos.permission.SET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| config | [WifiDeviceConfig](#wifideviceconfig9) | 是 | WLAN配置信息。如果bssidType未指定值，则bssidType默认为随机设备地址类型。 |

**返回值：**

  | **类型** | **说明** |
  | -------- | -------- |
  | Promise&lt;number&gt; | Promise对象。表示网络配置ID。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**
`````ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let config:wifiManager.WifiDeviceConfig = {
			ssid : "****",
			preSharedKey : "****",
			securityType : 0
		}
		wifiManager.addCandidateConfig(config).then(result => {
			console.info("result:" + JSON.stringify(result));
		}).catch(err => {
			console.error("failed:" + JSON.stringify(err));
		});
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
`````

## wifiManager.addCandidateConfig<sup>9+</sup>

addCandidateConfig(config: WifiDeviceConfig, callback: AsyncCallback&lt;number&gt;): void

添加候选网络配置，使用callback异步回调。

**需要权限：** ohos.permission.SET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| config | [WifiDeviceConfig](#wifideviceconfig9) | 是 | WLAN配置信息。如果bssidType未指定值，则bssidType默认为随机设备地址类型。 |
| callback | AsyncCallback&lt;number&gt; | 是 | 回调函数。当操作成功时，err为0，data为添加的网络配置ID，如果data值为-1，表示添加失败。如果操作出现错误，err为非0值。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**
`````ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let config:wifiManager.WifiDeviceConfig = {
			ssid : "****",
			preSharedKey : "****",
			securityType : 0
		}
		wifiManager.addCandidateConfig(config,(error,result) => {
			console.info("result:" + JSON.stringify(result));
		});	
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
`````

## wifiManager.removeCandidateConfig<sup>9+</sup>

removeCandidateConfig(networkId: number): Promise&lt;void&gt;

移除候选网络配置，使用Promise异步回调。

**需要权限：** ohos.permission.SET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | networkId | number | 是 | 网络配置ID。 |

**返回值：**

  | **类型** | **说明** |
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**

```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let networkId = 0;
		wifiManager.removeCandidateConfig(networkId).then(result => {
			console.info("result:" + JSON.stringify(result));
		}).catch(err => {
			console.error("failed:" + JSON.stringify(err));
		});
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.removeCandidateConfig<sup>9+</sup>

removeCandidateConfig(networkId: number, callback: AsyncCallback&lt;void&gt;): void

移除候选网络配置，使用callback异步回调。

**需要权限：** ohos.permission.SET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | networkId | number | 是 | 网络配置ID。 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 回调函数。当操作成功时，err为0。如果error为非0，表示处理出现错误。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let networkId = 0;
		wifiManager.removeCandidateConfig(networkId,(error,result) => {
		console.info("result:" + JSON.stringify(result));
		});	
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.getCandidateConfigs<sup>9+</sup>

getCandidateConfigs(): &nbsp;Array&lt;WifiDeviceConfig&gt;

获取候选网络配置。

**需要权限：**

API 9：ohos.permission.GET_WIFI_INFO、ohos.permission.LOCATION 和 ohos.permission.APPROXIMATELY_LOCATION

API 10起：ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**返回值：**

  | **类型** | **说明** |
  | -------- | -------- |
  | &nbsp;Array&lt;[WifiDeviceConfig](#wifideviceconfig9)&gt; | 候选网络配置数组。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.| 

**示例：**

`````ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let configs = wifiManager.getCandidateConfigs();
		console.info("configs:" + JSON.stringify(configs));
		let len = configs.length;
        console.log("result len: " + len);
		if(len > 0){
			for (let i = 0; i < len; ++i) {
				console.info("ssid: " + configs[i].ssid);
				console.info("bssid: " + configs[i].bssid);
			}
		}	
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
	
`````

## wifiManager.connectToCandidateConfig<sup>9+</sup>

connectToCandidateConfig(networkId: number): void

应用使用该接口连接到自己添加的候选网络（如果当前已经连接到热点，需要先断开连接）。

**需要权限：** ohos.permission.SET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | networkId | number | 是 | 候选网络配置的ID。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|
| 2501001  | Wifi is closed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let networkId = 0; // 实际的候选网络ID，在添加候选网络时生成，取自WifiDeviceConfig.netId
		wifiManager.connectToCandidateConfig(networkId);
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
	
```

## wifiManager.connectToNetwork<sup>9+</sup>

connectToNetwork(networkId: number): void

连接到指定网络（如果当前已经连接到热点，请先使用disconnet（）接口断开连接）。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.MANAGE_WIFI_CONNECTION，仅系统应用可用。

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | networkId | number | 是 | 待连接的网络配置ID。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|
| 2501001  | Wifi is closed.|

**示例：**

```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let networkId = 0;
		wifiManager.connectToNetwork(networkId);
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}	
```

## wifiManager.connectToDevice<sup>9+</sup>

connectToDevice(config: WifiDeviceConfig): void

连接到指定网络（如果当前已经连接到热点，请先使用disconnet（）接口断开连接）。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.SET_WIFI_INFO 和 ohos.permission.SET_WIFI_CONFIG 和 ohos.permission.MANAGE_WIFI_CONNECTION，仅系统应用可用。

**系统能力：**
  SystemCapability.Communication.WiFi.STA

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| config | [WifiDeviceConfig](#wifideviceconfig9) | 是 | WLAN配置信息。如果bssidType未指定值，则bssidType默认为随机设备地址类型。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|
| 2501001  | Wifi is closed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let config:wifiManager.WifiDeviceConfig = {
			ssid : "****",
			preSharedKey : "****",
			securityType : 3
		}
		wifiManager.connectToDevice(config);
				
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.disconnect<sup>9+</sup>

disconnect(): void

断开连接的网络。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.SET_WIFI_INFO 和 ohos.permission.MANAGE_WIFI_CONNECTION，仅系统应用可用。

**系统能力：**
  SystemCapability.Communication.WiFi.STA

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		wifiManager.disconnect();
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.getSignalLevel<sup>9+</sup>

getSignalLevel(rssi: number, band: number): number

查询WLAN信号强度。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | rssi | number | 是 | 热点的信号强度(dBm)。 |
  | band | number | 是 | WLAN接入点的频段。 |

**返回值：**

  | **类型** | **说明** |
  | -------- | -------- |
  | number | 信号强度，取值范围为[0,&nbsp;4]。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let rssi = 0;
		let band = 0;
		let level = wifiManager.getSignalLevel(rssi,band);
		console.info("level:" + JSON.stringify(level));
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}

```

## wifiManager.getLinkedInfo<sup>9+</sup>

getLinkedInfo(): Promise&lt;WifiLinkedInfo&gt;

获取WLAN连接信息，使用Promise异步回调。

**需要权限：** ohos.permission.GET_WIFI_INFO 。 

 获取 macAddress 还需申请ohos.permission.GET_WIFI_LOCAL_MAC权限，无该权限时，macAddress 返回空字符串。

**系统能力：** SystemCapability.Communication.WiFi.STA

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;[WifiLinkedInfo](#wifilinkedinfo9)&gt; | Promise对象。表示WLAN连接信息。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|
| 2501001  | Wifi is closed.|

## wifiManager.getLinkedInfo<sup>9+</sup>

getLinkedInfo(callback: AsyncCallback&lt;WifiLinkedInfo&gt;): void

获取WLAN连接信息，使用callback异步回调。

**需要权限：** ohos.permission.GET_WIFI_INFO 。 

获取 macAddress 还需申请ohos.permission.GET_WIFI_LOCAL_MAC权限，无该权限时，macAddress 返回空字符串。

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;[WifiLinkedInfo](#wifilinkedinfo9)&gt; | 是 | 回调函数。当获取成功时，err为0，data表示WLAN连接信息。如果err为非0，表示处理出现错误。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|
| 2501001  | Wifi is closed.|

**示例：**
```ts
  import wifiManager from '@ohos.wifiManager';
  
  wifiManager.getLinkedInfo((err, data) => {
      if (err) {
          console.error("get linked info error");
          return;
      }
      console.info("get wifi linked info: " + JSON.stringify(data));
  });
  
  wifiManager.getLinkedInfo().then(data => {
      console.info("get wifi linked info: " + JSON.stringify(data));
  }).catch((error:number) => {
      console.info("get linked info error");
  });
```


## WifiLinkedInfo<sup>9+</sup>

提供WLAN连接的相关信息。

**系统能力：** SystemCapability.Communication.WiFi.STA

| 名称 | 类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| ssid | string | 是 | 否 | 热点的SSID，编码格式为UTF-8。 |
| bssid | string | 是 | 否 | 热点的BSSID。 |
| networkId | number | 是 | 否 | 网络配置ID。 <br /> **系统接口：** 此接口为系统接口。 |
| rssi | number | 是 | 否 | 热点的信号强度(dBm)。 |
| band | number | 是 | 否 | WLAN接入点的频段。 |
| linkSpeed | number | 是 | 否 | WLAN接入点的上行速度。 |
| rxLinkSpeed<sup>10+</sup> | number | 是 | 否 | WLAN接入点的下行速度。 |
| maxSupportedTxLinkSpeed<sup>10+</sup> | number | 是 | 否 | 当前支持的最大上行速率。 |
| maxSupportedRxLinkSpeed<sup>10+</sup> | number | 是 | 否 | 当前支持的最大下行速率。 |
| frequency | number | 是 | 否 | WLAN接入点的频率。 |
| isHidden | boolean | 是 | 否 | WLAN接入点是否是隐藏网络。 |
| isRestricted | boolean | 是 | 否 | WLAN接入点是否限制数据量。 |
| chload | number | 是 | 否 | 连接负载，值越大表示负载约高。 <br /> **系统接口：** 此接口为系统接口。 |
| snr | number | 是 | 否 | 信噪比。 <br /> **系统接口：** 此接口为系统接口。 |
| macType | number | 是 | 否 | MAC地址类型。0 - 随机MAC地址，1 - 设备MAC地址。 |
| macAddress | string | 是 | 否 | 设备的MAC地址。 |
| ipAddress | number | 是 | 否 | WLAN连接的IP地址。 |
| suppState | [SuppState](#suppstate9) | 是 | 否 | 请求状态。 <br /> **系统接口：** 此接口为系统接口。 |
| connState | [ConnState](#connstate9) | 是 | 否 | WLAN连接状态。 |
| channelWidth<sup>10+</sup> | [WifiChannelWidth](#wifichannelwidth9) | 是 | 否 | 当前连接热点的信道带宽。 |
| wifiStandard<sup>10+</sup> | [WifiStandard](#wifistandard10) | 是 | 否 | 当前连接热点的WiFi标准。 |

## ConnState<sup>9+</sup>

表示WLAN连接状态的枚举。

**系统能力：** SystemCapability.Communication.WiFi.STA

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| SCANNING | 0 | 设备正在搜索可用的AP。 |
| CONNECTING | 1 | 正在建立WLAN连接。 |
| AUTHENTICATING | 2 | WLAN连接正在认证中。 |
| OBTAINING_IPADDR | 3 | 正在获取WLAN连接的IP地址。 |
| CONNECTED | 4 | WLAN连接已建立。 |
| DISCONNECTING | 5 | WLAN连接正在断开。 |
| DISCONNECTED | 6 | WLAN连接已断开。 |
| UNKNOWN | 7 | WLAN连接建立失败。 |


## SuppState<sup>9+</sup>

表示请求状态的枚举。

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.Communication.WiFi.STA

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| DISCONNECTED | 0 | 已断开。 |
| INTERFACE_DISABLED | 1 | 接口禁用。 |
| INACTIVE | 2 | 未激活。 |
| SCANNING | 3 | 扫描中。 |
| AUTHENTICATING | 4 | 认证中。 |
| ASSOCIATING | 5 | 关联中。 |
| ASSOCIATED | 6 | 已关联。 |
| FOUR_WAY_HANDSHAKE | 7 | 四次握手。 |
| GROUP_HANDSHAKE | 8 | 组握手。 |
| COMPLETED | 9 | 所有认证已完成。 |
| UNINITIALIZED | 10 | 连接建立失败。 |
| INVALID | 11 | 无效值。 |

## wifiManager.isConnected<sup>9+</sup>

isConnected(): boolean

查询WLAN是否已连接。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**返回值：**

  | **类型** | **说明** |
  | -------- | -------- |
  | boolean | true:已连接，&nbsp;false:未连接。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let ret = wifiManager.isConnected();
		console.info("isConnected:" + ret);
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}

```

## wifiManager.getSupportedFeatures<sup>9+</sup>

getSupportedFeatures(): number

查询设备支持的特性。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.Core

**返回值：**

  | **类型** | **说明** |
  | -------- | -------- |
  | number | 支持的特性值。 |

**特性ID值枚举：**

| 枚举值 | 说明 |
| -------- | -------- |
| 0x0001 | 基础结构模式特性。 |
| 0x0002 | 5&nbsp;GHz带宽特性。 |
| 0x0004 | GAS/ANQP特性。 |
| 0x0008 | Wifi-Direct特性。 |
| 0x0010 | Soft&nbsp;AP特性。 |
| 0x0040 | Wi-Fi&nbsp;AWare组网特性。 |
| 0x8000 | AP&nbsp;STA共存特性。 |
| 0x8000000 | WPA3-Personal&nbsp;SAE特性。 |
| 0x10000000 | WPA3-Enterprise&nbsp;Suite-B |
| 0x20000000 | 增强开放特性。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2401000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let ret = wifiManager.getSupportedFeatures();
		console.info("supportedFeatures:" + ret);
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}

```

## wifiManager.isFeatureSupported<sup>9+</sup>

isFeatureSupported(featureId: number): boolean

判断设备是否支持相关WLAN特性。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.Core

**参数：**


  | **参数名** | **类型** | 必填 | **说明** |
  | -------- | -------- | -------- | -------- |
  | featureId | number | 是 | 特性ID值。 |

**返回值：**

  | **类型** | **说明** |
  | -------- | -------- |
  | boolean | true:支持，&nbsp;false:不支持。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2401000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let featureId = 0;
		let ret = wifiManager.isFeatureSupported(featureId);
		console.info("isFeatureSupported:" + ret);
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}

```

## wifiManager.getDeviceMacAddress<sup>9+</sup>

getDeviceMacAddress(): string[]

获取设备的MAC地址。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.GET_WIFI_LOCAL_MAC 和 ohos.permission.GET_WIFI_INFO，仅系统应用可用。

**系统能力：** SystemCapability.Communication.WiFi.STA

**返回值：**

  | **类型** | **说明** |
  | -------- | -------- |
  | string[] | MAC地址。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|
| 2501001  | wifi is closed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let ret = wifiManager.getDeviceMacAddress();
		console.info("deviceMacAddress:" + JSON.stringify(ret));
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}

```

## wifiManager.getIpInfo<sup>9+</sup>

getIpInfo(): IpInfo

获取IP信息。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**返回值：**

  | **类型** | **说明** |
  | -------- | -------- |
  | [IpInfo](#ipinfo9) | IP信息。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let info = wifiManager.getIpInfo();
		console.info("info:" + JSON.stringify(info));
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## IpInfo<sup>9+</sup>

IP信息。

**系统能力：** SystemCapability.Communication.WiFi.STA

| **名称** | **类型** | **可读** | **可写** | **说明** |
| -------- | -------- | -------- | -------- | -------- |
| ipAddress | number | 是 | 否 | IP地址。 |
| gateway | number | 是 | 否 | 网关。 |
| netmask | number | 是 | 否 | 掩码。 |
| primaryDns | number | 是 | 否 | 主DNS服务器IP地址。 |
| secondDns | number | 是 | 否 | 备DNS服务器IP地址。 |
| serverIp | number | 是 | 否 | DHCP服务端IP地址。 |
| leaseDuration | number | 是 | 否 | IP地址租用时长。 |


## wifiManager.getIpv6Info<sup>10+</sup>

getIpv6Info(): Ipv6Info

获取IP信息。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**返回值：**

| **类型** | **说明** |
| -------- | -------- |
| Ipv6Info | Ipv6信息。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let info = wifiManager.getIpv6Info();
		console.info("info:" + JSON.stringify(info));
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```
## Ipv6Info <sup>10+</sup>

Ipv6信息。

**系统能力：** SystemCapability.Communication.WiFi.STA

| **名称** | **类型** | **可读** | **可写** | **说明** |
| -------- | -------- | -------- | -------- | -------- |
| linkIpv6Address | string | 是 | 否 | 链路Ipv6地址。 |
| globalIpv6Address | string | 是 | 否 | 全局Ipv6地址。 |
| randomGlobalIpv6Address | string | 是 | 否 | 随机全局Ipv6地址。 |
| gateway | string | 是 | 否 | 网关。 |
| netmask | string | 是 | 否 | 网络掩码。 |
| primaryDNS | string | 是 | 否 | 主DNS服务器Ipv6地址。 |
| secondDNS | string | 是 | 否 | 备DNS服务器Ipv6地址。 |


## wifiManager.getCountryCode<sup>9+</sup>

getCountryCode(): string

获取国家码信息。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.Core

**返回值：**

  | **类型** | **说明** |
  | -------- | -------- |
  | string | 国家码。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2401000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let code = wifiManager.getCountryCode();
		console.info("code:" + code);
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.reassociate<sup>9+</sup>

reassociate(): void

重新关联网络。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.SET_WIFI_INFO 和 ohos.permission.MANAGE_WIFI_CONNECTION，仅系统应用可用。

**系统能力：** SystemCapability.Communication.WiFi.STA

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|
| 2501001  | Wifi is closed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		wifiManager.reassociate();
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.reconnect<sup>9+</sup>

reconnect(): void

重新连接网络。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.SET_WIFI_INFO 和 ohos.permission.MANAGE_WIFI_CONNECTION，仅系统应用可用。

**系统能力：** SystemCapability.Communication.WiFi.STA

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|
| 2501001  | Wifi is closed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		wifiManager.reconnect();
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.getDeviceConfigs<sup>9+</sup>

getDeviceConfigs(): &nbsp;Array&lt;[WifiDeviceConfig](#wifideviceconfig9)&gt;

获取网络配置。

**系统接口：** 此接口为系统接口。

**需要权限：**

API 9：ohos.permission.GET_WIFI_INFO、ohos.permission.LOCATION、ohos.permission.APPROXIMATELY_LOCATION 和 ohos.permission.GET_WIFI_CONFIG

API 10起：ohos.permission.GET_WIFI_INFO 和 ohos.permission.GET_WIFI_CONFIG

**系统能力：** SystemCapability.Communication.WiFi.STA

**返回值：**

  | **类型** | **说明** |
  | -------- | -------- |
  | &nbsp;Array&lt;[WifiDeviceConfig](#wifideviceconfig9)&gt; | 网络配置信息的数组。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let configs = wifiManager.getDeviceConfigs();
		console.info("configs:" + JSON.stringify(configs));
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.updateNetwork<sup>9+</sup>

updateNetwork(config: WifiDeviceConfig): number

更新网络配置。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.SET_WIFI_INFO 和 ohos.permission.SET_WIFI_CONFIG

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | config | [WifiDeviceConfig](#wifideviceconfig9) | 是 | WLAN配置信息。 |

**返回值：**

  | **类型** | **说明** |
  | -------- | -------- |
  | number | 返回更新的网络配置ID，如果值为-1表示更新失败。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let config:wifiManager.WifiDeviceConfig = {
			ssid : "****",
			preSharedKey : "****",
			securityType : 3
		}
		let ret = wifiManager.updateNetwork(config);
		console.info("ret:" + ret);
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.disableNetwork<sup>9+</sup>

disableNetwork(netId: number): void

去使能网络配置。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.SET_WIFI_INFO 和 ohos.permission.MANAGE_WIFI_CONNECTION，仅系统应用可用。

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | netId | number | 是 | 网络配置ID。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let netId = 0;
		wifiManager.disableNetwork(netId);		
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.removeAllNetwork<sup>9+</sup>

removeAllNetwork(): void

移除所有网络配置。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.SET_WIFI_INFO 和 ohos.permission.MANAGE_WIFI_CONNECTION，仅系统应用可用。

**系统能力：** SystemCapability.Communication.WiFi.STA

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		wifiManager.removeAllNetwork();		
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.removeDevice<sup>9+</sup>

removeDevice(id: number): void

移除指定的网络配置。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.SET_WIFI_INFO 和 ohos.permission.MANAGE_WIFI_CONNECTION，仅系统应用可用。

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | id | number | 是 | 网络配置ID。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let id = 0;
		wifiManager.removeDevice(id);		
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.isBandTypeSupported<sup>10+</sup>

isBandTypeSupported(bandType: WifiBandType): boolean

判断当前频段是否支持。

**需要权限：** ohos.permission.GET_WIFI_INFO。

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | bandType | WifiBandType | 是 | Wifi 频段类型。 |

**返回值：**

  | **类型** | **说明** |
  | -------- | -------- |
  | boolean | true:支持，&nbsp;false:不支持。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let type = 0;
		let isBandTypeSupported = wifiManager.isBandTypeSupported(type);
		console.info("isBandTypeSupported:" + isBandTypeSupported);		
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.get5GChannelList<sup>10+</sup>

get5GChannelList(): Array&lt;number&gt;

获取当前设备支持的5G信道列表。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.GET_WIFI_INFO 和 ohos.permission.GET_WIFI_CONFIG

**系统能力：** SystemCapability.Communication.WiFi.STA

**返回值：**

  | **类型** | **说明** |
  | -------- | -------- |
  | &nbsp;Array&lt;number&gt; | 设备支持的5G信道列表。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let channelList = wifiManager.get5GChannelList();
		console.info("channelList:" + JSON.stringify(channelList));		
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```
## wifiManager.getDisconnectedReason<sup>10+</sup>

getDisconnectedReason(): DisconnectedReason

获取最近一次断连原因。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.GET_WIFI_INFO 和 ohos.permission.GET_WIFI_CONFIG

**系统能力：** SystemCapability.Communication.WiFi.STA

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**返回值：**

| **类型** | **说明** |
| -------- | -------- |
| DisconnectedReason | 最近断开的原因 |

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let disconnectedReason = wifiManager.getDisconnectedReason();	
        console.info("disconnectedReason:" + disconnectedReason);
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## DisconnectedReason <sup>10+</sup>

表示wifi断开原因的枚举。

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.Communication.WiFi.STA

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| DISC_REASON_DEFAULT  | 0 | 默认原因。 |
| DISC_REASON_WRONG_PWD  | 1 | 密码错误。 |
| DISC_REASON_CONNECTION_FULL  | 2 | 路由器的连接数已达到最大数量限制。 |

## wifiManager.enableHotspot<sup>9+</sup>

enableHotspot(): void

使能热点，异步接口，是否打开成功需要注册并监听hotspotStateChange的回调。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.MANAGE_WIFI_HOTSPOT，仅系统应用可用。

**系统能力：** SystemCapability.Communication.WiFi.AP.Core

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2601000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		wifiManager.enableHotspot();	
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.disableHotspot<sup>9+</sup>

disableHotspot(): void

去使能热点 ，异步接口，是否关闭成功需要注册并监听hotspotStateChange的回调。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.MANAGE_WIFI_HOTSPOT，仅系统应用可用。

**系统能力：** SystemCapability.Communication.WiFi.AP.Core

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2601000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		wifiManager.disableHotspot();	
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.isHotspotDualBandSupported<sup>9+</sup>

isHotspotDualBandSupported(): boolean

热点是否支持双频。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.GET_WIFI_INFO 和 ohos.permission.MANAGE_WIFI_HOTSPOT，仅系统应用可用。

**系统能力：** SystemCapability.Communication.WiFi.AP.Core

**返回值：**

  | **类型** | **说明** |
  | -------- | -------- |
  | boolean | true:支持，&nbsp;false:不支持.|

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2601000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let ret = wifiManager.isHotspotDualBandSupported();
		console.info("result:" + ret);		
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.isHotspotActive<sup>9+</sup>

isHotspotActive(): boolean

热点是否已使能。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.AP.Core

**返回值：**

  | **类型** | **说明** |
  | -------- | -------- |
  | boolean | true:已使能，&nbsp;false:未使能.|

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2601000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let ret = wifiManager.isHotspotActive();
		console.info("result:" + ret);		
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.setHotspotConfig<sup>9+</sup>

setHotspotConfig(config: HotspotConfig): void

设置热点配置信息。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.SET_WIFI_INFO 和 ohos.permission.GET_WIFI_CONFIG

**系统能力：** SystemCapability.Communication.WiFi.AP.Core

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | config | [HotspotConfig](#hotspotconfig9) | 是 | 热点配置信息。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2601000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let config:wifiManager.HotspotConfig = {
			ssid: "****",
			securityType: 3,
			band: 0,
			channel: 0,
			preSharedKey: "****",
			maxConn: 0
		}
		let ret = wifiManager.setHotspotConfig(config);
		console.info("result:" + ret);		
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## HotspotConfig<sup>9+</sup>

热点配置信息。

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.Communication.WiFi.AP.Core

| **名称** | **类型** | **可读** | **可写** | **说明** |
| -------- | -------- | -------- | -------- | -------- |
| ssid | string | 是 | 是 | 热点的SSID，编码格式为UTF-8。 |
| securityType | [WifiSecurityType](#wifisecuritytype9)| 是 | 是 | 加密类型。 |
| band | number | 是 | 是 | 热点的带宽。1: 2.4G, 2: 5G, 3: 双模频段 |
| channel<sup>10+</sup> | number | 是 | 是 | 热点的信道（2.4G：1~14,5G：7~196，双模频段：暂不支持）。 |
| preSharedKey | string | 是 | 是 | 热点的密钥。 |
| maxConn | number | 是 | 是 | 最大设备连接数。 |

## wifiManager.getHotspotConfig<sup>9+</sup>

getHotspotConfig(): HotspotConfig

获取热点配置信息。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.GET_WIFI_INFO 和 ohos.permission.GET_WIFI_CONFIG

**系统能力：** SystemCapability.Communication.WiFi.AP.Core

**返回值：**

  | **类型** | **说明** |
  | -------- | -------- |
  | [HotspotConfig](#hotspotconfig9) | 热点的配置信息。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2601000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let config = wifiManager.getHotspotConfig();
		console.info("result:" + JSON.stringify(config));		
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.getStations<sup>9+</sup>

getStations(): &nbsp;Array&lt;StationInfo&gt;

获取连接的设备。

**系统接口：** 此接口为系统接口。

**需要权限：**

API 9：ohos.permission.GET_WIFI_INFO、ohos.permission.LOCATION、ohos.permission.APPROXIMATELY_LOCATION 和 ohos.permission.MANAGE_WIFI_HOTSPOT，仅系统应用可用。

API 10起：ohos.permission.GET_WIFI_INFO 和 ohos.permission.MANAGE_WIFI_HOTSPOT，仅系统应用可用。

**系统能力：** SystemCapability.Communication.WiFi.AP.Core

**返回值：**

| **类型** | **说明** |
| -------- | -------- |
| &nbsp;Array&lt;[StationInfo](#stationinfo9)&gt; | 连接的设备数组。如果应用申请了ohos.permission.GET_WIFI_PEERS_MAC权限，则返回结果中的macAddress为真实设备地址，否则为随机设备地址。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2601000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let stations = wifiManager.getStations();
		console.info("result:" + JSON.stringify(stations));		
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## StationInfo<sup>9+</sup>

接入的设备信息。

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.Communication.WiFi.AP.Core

| **名称** | **类型** | **可读** | **可写** | **说明** |
| -------- | -------- | -------- | -------- | -------- |
| name | string | 是 | 否 | 设备名称。 |
| macAddress | string | 是 | 否 | MAC地址。 |
| macAddressType<sup>10+</sup> | DeviceAddressType | 是 | 否 | MAC地址类型。 |
| ipAddress | string | 是 | 否 | IP地址。 |


## wifiManager.getP2pLinkedInfo<sup>9+</sup>

getP2pLinkedInfo(): Promise&lt;WifiP2pLinkedInfo&gt;

获取P2P连接信息，使用Promise异步回调。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;[WifiP2pLinkedInfo](#wifip2plinkedinfo9)&gt; | Promise对象。表示P2P连接信息。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|


## wifiManager.getP2pLinkedInfo<sup>9+</sup>

getP2pLinkedInfo(callback: AsyncCallback&lt;WifiP2pLinkedInfo&gt;): void

获取P2P连接信息，使用callback异步回调。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;[WifiP2pLinkedInfo](#wifip2plinkedinfo9)&gt; | 是 | 回调函数。当操作成功时，err为0，data表示P2P连接信息。如果err为非0，表示处理出现错误。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	wifiManager.getP2pLinkedInfo((err, data) => {
    if (err) {
        console.error("get p2p linked info error");
        return;
    }
		console.info("get wifi p2p linked info: " + JSON.stringify(data));
	});

	wifiManager.getP2pLinkedInfo().then(data => {
		console.info("get wifi p2p linked info: " + JSON.stringify(data));
	});
```


## WifiP2pLinkedInfo<sup>9+</sup>

提供WLAN连接的相关信息。

**系统能力：** SystemCapability.Communication.WiFi.P2P

| 名称 | 类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| connectState | [P2pConnectState](#p2pconnectstate9) | 是 | 否 | P2P连接状态。 |
| isGroupOwner | boolean | 是 | 否 | 是否是群主。 |
| groupOwnerAddr | string | 是 | 否 | 群组MAC地址。 


## P2pConnectState<sup>9+</sup>

表示P2P连接状态的枚举。

**系统能力：** SystemCapability.Communication.WiFi.P2P

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| DISCONNECTED | 0 | 断开状态。 |
| CONNECTED | 1 | 连接状态。 |

## wifiManager.getCurrentGroup<sup>9+</sup>

getCurrentGroup(): Promise&lt;WifiP2pGroupInfo&gt;

获取P2P当前组信息，使用Promise异步回调。

**需要权限：**

API 9：ohos.permission.GET_WIFI_INFO、ohos.permission.LOCATION 和 ohos.permission.APPROXIMATELY_LOCATION

API 10起：ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;[WifiP2pGroupInfo](#wifip2pgroupinfo9)&gt; | Promise对象。表示当前组信息。如果应用申请了ohos.permission.GET_WIFI_PEERS_MAC权限，则返回结果中的deviceAddress为真实设备地址，否则为随机设备地址。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.getCurrentGroup<sup>9+</sup>

getCurrentGroup(callback: AsyncCallback&lt;WifiP2pGroupInfo&gt;): void

获取P2P当前组信息，使用callback异步回调。

**需要权限：**

API 9：ohos.permission.GET_WIFI_INFO、ohos.permission.LOCATION 和 ohos.permission.APPROXIMATELY_LOCATION

API 10起：ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;[WifiP2pGroupInfo](#wifip2pgroupinfo9)&gt; | 是 | 回调函数。当操作成功时，err为0，data表示当前组信息。如果error为非0，表示处理出现错误。如果应用申请了ohos.permission.GET_WIFI_PEERS_MAC权限，则返回结果中的deviceAddress为真实设备地址，否则为随机设备地址。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';
	// p2p处于连接状态，才能正常获取到当前组信息
	wifiManager.getCurrentGroup((err, data) => {
    if (err) {
        console.error("get current P2P group error");
        return;
    }
		console.info("get current P2P group: " + JSON.stringify(data));
	});

	wifiManager.getCurrentGroup().then(data => {
		console.info("get current P2P group: " + JSON.stringify(data));
	});
```

## wifiManager.getP2pPeerDevices<sup>9+</sup>

getP2pPeerDevices(): Promise&lt;WifiP2pDevice[]&gt;

获取P2P对端设备列表信息，使用Promise异步回调。

**需要权限：**

API 9：ohos.permission.GET_WIFI_INFO、ohos.permission.LOCATION 和 ohos.permission.APPROXIMATELY_LOCATION

API 10起：ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;[WifiP2pDevice[]](#wifip2pdevice9)&gt; | Promise对象。表示对端设备列表信息。如果应用申请了ohos.permission.GET_WIFI_PEERS_MAC权限，则返回结果中的deviceAddress为真实设备地址，否则为随机设备地址。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.getP2pPeerDevices<sup>9+</sup>

getP2pPeerDevices(callback: AsyncCallback&lt;WifiP2pDevice[]&gt;): void

获取P2P对端设备列表信息，使用callback异步回调。

**需要权限：**

API 9：ohos.permission.GET_WIFI_INFO、ohos.permission.LOCATION 和 ohos.permission.APPROXIMATELY_LOCATION

API 10起：ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;[WifiP2pDevice[]](#wifip2pdevice9)&gt; | 是 | 回调函数。当操作成功时，err为0，data表示对端设备列表信息。如果err为非0，表示处理出现错误。如果应用申请了ohos.permission.GET_WIFI_PEERS_MAC权限，则返回结果中的deviceAddress为真实设备地址，否则为随机设备地址。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';
	// p2p处于连接状态，才能正常获取到对端设备列表信息
	wifiManager.getP2pPeerDevices((err, data) => {
    if (err) {
        console.error("get P2P peer devices error");
        return;
    }
		console.info("get P2P peer devices: " + JSON.stringify(data));
	});

	wifiManager.getP2pPeerDevices().then(data => {
		console.info("get P2P peer devices: " + JSON.stringify(data));
	});
```

## WifiP2pDevice<sup>9+</sup>

表示P2P设备信息。

**系统能力：** SystemCapability.Communication.WiFi.P2P

| 名称 | 类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| deviceName | string | 是 | 否 | 设备名称。 |
| deviceAddress | string | 是 | 否 | 设备MAC地址。 |
| deviceAddressType<sup>10+</sup> | DeviceAddressType | 是 | 否 | 设备MAC地址类型。 |
| primaryDeviceType | string | 是 | 否 | 主设备类型。 |
| deviceStatus | [P2pDeviceStatus](#p2pdevicestatus9) | 是 | 否 | 设备状态。 |
| groupCapabilities | number | 是 | 否 | 群组能力。 |


## P2pDeviceStatus<sup>9+</sup>

表示设备状态的枚举。

**系统能力：** SystemCapability.Communication.WiFi.P2P

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| CONNECTED | 0 | 连接状态。 |
| INVITED | 1 | 邀请状态。 |
| FAILED | 2 | 失败状态。 |
| AVAILABLE | 3 | 可用状态。 |
| UNAVAILABLE | 4 | 不可用状态。 |


## wifiManager.getP2pLocalDevice<sup>9+</sup>

getP2pLocalDevice(): Promise&lt;WifiP2pDevice&gt;

获取P2P本端设备信息，使用Promise异步回调。

**需要权限：** ohos.permission.GET_WIFI_INFO 和 ohos.permission.GET_WIFI_CONFIG

**系统能力：** SystemCapability.Communication.WiFi.P2P

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;[WifiP2pDevice](#wifip2pdevice9)&gt; | Promise对象。表示本端设备信息。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.getP2pLocalDevice<sup>9+</sup>

getP2pLocalDevice(callback: AsyncCallback&lt;WifiP2pDevice&gt;): void

获取P2P本端设备信息，使用callback异步回调。

**需要权限：** ohos.permission.GET_WIFI_INFO 和 ohos.permission.GET_WIFI_CONFIG

**系统能力：** SystemCapability.Communication.WiFi.P2P

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;[WifiP2pDevice](#wifip2pdevice9)&gt; | 是 | 回调函数。当操作成功时，err为0，data表示本端设备信息。如果error为非0，表示处理出现错误。 |

**错误码：**

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';
	// p2p处于连接状态，才能正常获取到本端设备信息
	wifiManager.getP2pLocalDevice((err, data) => {
    if (err) {
        console.error("get P2P local device error");
        return;
    }
		console.info("get P2P local device: " + JSON.stringify(data));
	});

	wifiManager.getP2pLocalDevice().then(data => {
		console.info("get P2P local device: " + JSON.stringify(data));
	});
```

## wifiManager.createGroup<sup>9+</sup>

createGroup(config: WifiP2PConfig): void

创建群组。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**参数：**

| **参数名** | **类型** | 必填 | **说明** |
| -------- | -------- | -------- | -------- |
| config | [WifiP2PConfig](#wifip2pconfig9) | 是 | 群组配置信息。如果DeviceAddressType未指定值，则DeviceAddressType默认为随机设备地址类型。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let config:wifiManager.WifiP2PConfig = {
			deviceAddress: "****",
			netId: 0,
			passphrase: "*****",
			groupName: "****",
			goBand: 0
		}
		wifiManager.createGroup(config);	
		
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## WifiP2PConfig<sup>9+</sup>

表示P2P配置信息。

**系统能力：** SystemCapability.Communication.WiFi.P2P

| 名称 | 类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| deviceAddress | string | 是 | 否 | 设备地址。 |
| deviceAddressType<sup>10+</sup>| DeviceAddressType | 是 | 否 | 设备地址类型。 |
| netId | number | 是 | 否 | 网络ID。创建群组时-1表示创建临时组，-2表示创建永久组。 |
| passphrase | string | 是 | 否 | 群组密钥。 |
| groupName | string | 是 | 否 | 群组名称。 |
| goBand | [GroupOwnerBand](#groupownerband9) | 是 | 否 | 群组带宽。 |


## GroupOwnerBand<sup>9+</sup>

表示群组带宽的枚举。

**系统能力：** SystemCapability.Communication.WiFi.P2P

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| GO_BAND_AUTO | 0 | 自动模式。 |
| GO_BAND_2GHZ | 1 | 2.4GHZ。 |
| GO_BAND_5GHZ | 2 | 5GHZ。 |


## wifiManager.removeGroup<sup>9+</sup>

removeGroup(): void

移除群组。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		wifiManager.removeGroup();	
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.p2pConnect<sup>9+</sup>

p2pConnect(config: WifiP2PConfig): void

执行P2P连接。

**需要权限：**

API 9：ohos.permission.GET_WIFI_INFO、ohos.permission.LOCATION 和 ohos.permission.APPROXIMATELY_LOCATION

API 10起：ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**参数：**

| **参数名** | **类型** | 必填 | **说明** |
| -------- | -------- | -------- | -------- |
| config | [WifiP2PConfig](#wifip2pconfig9) | 是 | 连接配置信息。如果DeviceAddressType未指定值，则DeviceAddressType默认为随机设备地址类型。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

**示例：**
```ts
  import wifiManager from '@ohos.wifiManager';
  
  let recvP2pConnectionChangeFunc = (result:wifiManager.WifiP2pLinkedInfo) => {
      console.info("p2p connection change receive event: " + JSON.stringify(result));
      wifiManager.getP2pLinkedInfo((err, data) => {
          if (err) {
              console.error('failed to get getP2pLinkedInfo: ' + JSON.stringify(err));
              return;
          }
          console.info("get getP2pLinkedInfo: " + JSON.stringify(data));
      });
  }
  wifiManager.on("p2pConnectionChange", recvP2pConnectionChangeFunc);
  
  let recvP2pDeviceChangeFunc = (result:wifiManager.WifiP2pDevice) => {
      console.info("p2p device change receive event: " + JSON.stringify(result));
  }
  wifiManager.on("p2pDeviceChange", recvP2pDeviceChangeFunc);
  
  let recvP2pPeerDeviceChangeFunc = (result:wifiManager.WifiP2pDevice[]) => {
      console.info("p2p peer device change receive event: " + JSON.stringify(result));
      wifiManager.getP2pPeerDevices((err, data) => {
          if (err) {
              console.error('failed to get peer devices: ' + JSON.stringify(err));
              return;
          }
          console.info("get peer devices: " + JSON.stringify(data));
          let len = data.length;
          for (let i = 0; i < len; ++i) {
              if (data[i].deviceName === "my_test_device") {
                  console.info("p2p connect to test device: " + data[i].deviceAddress);
                  let config:wifiManager.WifiP2PConfig = {
                      deviceAddress:data[i].deviceAddress,
                      netId:-2,
                      passphrase:"",
                      groupName:"",
                      goBand:0,
                  }
                  wifiManager.p2pConnect(config);
              }
          }
      });
  }
  wifiManager.on("p2pPeerDeviceChange", recvP2pPeerDeviceChangeFunc);
  
  let recvP2pPersistentGroupChangeFunc = () => {
      console.info("p2p persistent group change receive event");
  
      wifiManager.getCurrentGroup((err, data) => {
          if (err) {
              console.error('failed to get current group: ' + JSON.stringify(err));
              return;
          }
          console.info("get current group: " + JSON.stringify(data));
      });
  }
  wifiManager.on("p2pPersistentGroupChange", recvP2pPersistentGroupChangeFunc);
  
  setTimeout(() => {wifiManager.off("p2pConnectionChange", recvP2pConnectionChangeFunc);}, 125 * 1000);
  setTimeout(() =>  {wifiManager.off("p2pDeviceChange", recvP2pDeviceChangeFunc);}, 125 * 1000);
  setTimeout(() =>  {wifiManager.off("p2pPeerDeviceChange", recvP2pPeerDeviceChangeFunc);}, 125 * 1000);
  setTimeout(() =>  {wifiManager.off("p2pPersistentGroupChange", recvP2pPersistentGroupChangeFunc);}, 125 * 1000);
  console.info("start discover devices -> " + wifiManager.startDiscoverDevices());
```

## wifiManager.p2pCancelConnect<sup>9+</sup>

p2pCancelConnect(): void

取消P2P连接。

**需要权限：** ohos.permission.GET_WIFI_INFO 

**系统能力：** SystemCapability.Communication.WiFi.P2P

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		wifiManager.p2pCancelConnect();	
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.startDiscoverDevices<sup>9+</sup>

startDiscoverDevices(): void

开始发现设备。

**需要权限：**

API 9：ohos.permission.GET_WIFI_INFO 和 ohos.permission.LOCATION 和 ohos.permission.APPROXIMATELY_LOCATION

API 10起：ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		wifiManager.startDiscoverDevices();	
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.stopDiscoverDevices<sup>9+</sup>

stopDiscoverDevices(): void

停止发现设备。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		wifiManager.stopDiscoverDevices();	
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.deletePersistentGroup<sup>9+</sup>

deletePersistentGroup(netId: number): void

删除永久组。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.SET_WIFI_INFO 和 ohos.permission.MANAGE_WIFI_CONNECTION

**系统能力：** SystemCapability.Communication.WiFi.P2P

**参数：**


  | **参数名** | **类型** | 必填 | **说明** |
  | -------- | -------- | -------- | -------- |
  | netId | number | 是 | 组的ID。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let netId = 0;
		wifiManager.deletePersistentGroup(netId);	
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.getP2pGroups<sup>9+</sup>

getP2pGroups(): Promise&lt;Array&lt;WifiP2pGroupInfo&gt;&gt;

获取创建的所有P2P群组信息，使用Promise异步回调。

**系统接口：** 此接口为系统接口。

**需要权限：**

API 9：ohos.permission.GET_WIFI_INFO、ohos.permission.LOCATION 和 ohos.permission.APPROXIMATELY_LOCATION

API 10起：ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;&nbsp;Array&lt;[WifiP2pGroupInfo](#wifip2pgroupinfo9)&gt;&nbsp;&gt; | Promise对象。表示所有群组信息。如果应用申请了ohos.permission.GET_WIFI_PEERS_MAC权限，则返回结果中的deviceAddress为真实设备地址，否则为随机设备地址。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	wifiManager.getP2pGroups((err, data) => {
    if (err) {
        console.error("get P2P groups error");
        return;
    }
		console.info("get P2P groups: " + JSON.stringify(data));
	});

	wifiManager.getP2pGroups().then(data => {
		console.info("get P2P groups: " + JSON.stringify(data));
	});
	
```

## WifiP2pGroupInfo<sup>9+</sup>

表示P2P群组相关信息。

**系统能力：** SystemCapability.Communication.WiFi.P2P

| 名称 | 类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| isP2pGo | boolean | 是 | 否 | 是否是群主。 |
| ownerInfo | [WifiP2pDevice](#wifip2pdevice9) | 是 | 否 | 群组的设备信息。 |
| passphrase | string | 是 | 否 | 群组密钥。 |
| interface | string | 是 | 否 | 接口名称。 |
| groupName | string | 是 | 否 | 群组名称。 |
| networkId | number | 是 | 否 | 网络ID。 |
| frequency | number | 是 | 否 | 群组的频率。 |
| clientDevices | [WifiP2pDevice[]](#wifip2pdevice9) | 是 | 否 | 接入的设备列表信息。 |
| goIpAddress | string | 是 | 否 | 群组IP地址。 |


## wifiManager.getP2pGroups<sup>9+</sup>

getP2pGroups(callback: AsyncCallback&lt;Array&lt;WifiP2pGroupInfo&gt;&gt;): void

获取创建的所有P2P群组信息，使用callback方式作为异步方法。

**系统接口：** 此接口为系统接口。

**需要权限：**

API 9：ohos.permission.GET_WIFI_INFO、ohos.permission.LOCATION 和 ohos.permission.APPROXIMATELY_LOCATION

API 10起：ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;&nbsp;Array&lt;[WifiP2pGroupInfo](#wifip2pgroupinfo9)&gt;&gt; | 是 | 回调函数。当操作成功时，err为0，data表示所有群组信息。如果error为非0，表示处理出现错误。如果应用申请了ohos.permission.GET_WIFI_PEERS_MAC权限，则返回结果中的deviceAddress为真实设备地址，否则为随机设备地址。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.setDeviceName<sup>9+</sup>

setDeviceName(devName: string): void

设置设备名称。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.SET_WIFI_INFO 和 ohos.permission.MANAGE_WIFI_CONNECTION，仅系统应用可用。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | devName | string | 是 | 设备名称。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

**示例：**
```ts
	import wifiManager from '@ohos.wifiManager';

	try {
		let name = "****";
		wifiManager.setDeviceName(name);	
	}catch(error){
		console.error("failed:" + JSON.stringify(error));
	}
```

## wifiManager.on('wifiStateChange')<sup>9+</sup>

on(type: "wifiStateChange", callback: Callback&lt;number&gt;): void

注册WLAN状态改变事件。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 固定填"wifiStateChange"字符串。 |
  | callback | Callback&lt;number&gt; | 是 | 状态改变回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**状态改变事件的枚举：**

| **枚举值** | **说明** |
| -------- | -------- |
| 0 | 未激活。 |
| 1 | 已激活。 |
| 2 | 激活中。 |
| 3 | 去激活中。 |


## wifiManager.off('wifiStateChange')<sup>9+</sup>

off(type: "wifiStateChange", callback?: Callback&lt;number&gt;): void

取消注册WLAN状态改变事件。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 固定填"wifiStateChange"字符串。 |
  | callback | Callback&lt;number&gt; | 否 | 状态改变回调函数。如果callback不填，将取消注册该事件关联的所有回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**
```ts
  import wifiManager from '@ohos.wifiManager';
  
  let recvPowerNotifyFunc = (result:number) => {
      console.info("Receive power state change event: " + result);
  }
  
  // Register event
  wifiManager.on("wifiStateChange", recvPowerNotifyFunc);
  
  // Unregister event
  wifiManager.off("wifiStateChange", recvPowerNotifyFunc);
```


## wifiManager.on('wifiConnectionChange')<sup>9+</sup>

on(type: "wifiConnectionChange", callback: Callback&lt;number&gt;): void

注册WLAN连接状态改变事件。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 固定填"wifiConnectionChange"字符串。 |
  | callback | Callback&lt;number&gt; | 是 | 状态改变回调函数。 |

**连接状态改变事件的枚举：**

| **枚举值** | **说明** |
| -------- | -------- |
| 0 | 已断开。 |
| 1 | 已连接。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.off('wifiConnectionChange')<sup>9+</sup>

off(type: "wifiConnectionChange", callback?: Callback&lt;number&gt;): void

取消注册WLAN连接状态改变事件。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 固定填"wifiConnectionChange"字符串。 |
  | callback | Callback&lt;number&gt; | 否 | 连接状态改变回调函数。如果callback不填，将取消注册该事件关联的所有回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**
```ts
  import wifiManager from '@ohos.wifiManager';
  
  let recvWifiConnectionChangeFunc = (result:number) => {
      console.info("Receive wifi connection change event: " + result);
  }
  
  // Register event
  wifiManager.on("wifiConnectionChange", recvWifiConnectionChangeFunc);
  
  // Unregister event
  wifiManager.off("wifiConnectionChange", recvWifiConnectionChangeFunc);
```

## wifiManager.on('wifiScanStateChange')<sup>9+</sup>

on(type: "wifiScanStateChange", callback: Callback&lt;number&gt;): void

注册扫描状态改变事件。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 固定填"wifiScanStateChange"字符串。 |
  | callback | Callback&lt;number&gt; | 是 | 状态改变回调函数。 |

**扫描状态改变事件的枚举：**

| **枚举值** | **说明** |
| -------- | -------- |
| 0 | 扫描失败。 |
| 1 | 扫描成功。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.off('wifiScanStateChange')<sup>9+</sup>

off(type: "wifiScanStateChange", callback?: Callback&lt;number&gt;): void

取消注册扫描状态改变事件。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 固定填"wifiScanStateChange"字符串。 |
| callback | Callback&lt;number&gt; | 否 | 状态改变回调函数。如果callback不填，将取消注册该事件关联的所有回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**
```ts
  import wifiManager from '@ohos.wifiManager';
  
  let recvWifiScanStateChangeFunc = (result:number) => {
      console.info("Receive Wifi scan state change event: " + result);
  }
  
  // Register event
  wifiManager.on("wifiScanStateChange", recvWifiScanStateChangeFunc);
  
  // Unregister event
  wifiManager.off("wifiScanStateChange", recvWifiScanStateChangeFunc);
```

## wifiManager.on('wifiRssiChange')<sup>9+</sup>

on(type: "wifiRssiChange", callback: Callback&lt;number&gt;): void

注册RSSI状态改变事件。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 固定填"wifiRssiChange"字符串。 |
  | callback | Callback&lt;number&gt; | 是 | 状态改变回调函数，返回以dBm为单位的RSSI值。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.off('wifiRssiChange')<sup>9+</sup>

off(type: "wifiRssiChange", callback?: Callback&lt;number&gt;): void

取消注册RSSI状态改变事件。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 固定填"wifiRssiChange"字符串。 |
| callback | Callback&lt;number&gt; | 否 | 状态改变回调函数。如果callback不填，将取消注册该事件关联的所有回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**
```ts
  import wifiManager from '@ohos.wifiManager';
  
  let recvWifiRssiChangeFunc = (result:number) => {
      console.info("Receive wifi rssi change event: " + result);
  }
  
  // Register event
  wifiManager.on("wifiRssiChange", recvWifiRssiChangeFunc);
  
  // Unregister event
  wifiManager.off("wifiRssiChange", recvWifiRssiChangeFunc);
```
 ## wifiManager.on('streamChange')<sup>9+</sup>

on(type: "streamChange", callback: Callback&lt;number&gt;): void

注册WIFI流变更事件，当前版本不支持，抛出通用错误码801。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.MANAGE_WIFI_CONNECTION

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 固定填"streamChange"字符串。 |
| callback | Callback&lt;number&gt; | 是 | 状态改变回调函数，返回0:无，1：向下，2：向上，3：双向。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.off('streamChange')<sup>9+</sup>

off(type: "streamChange", callback?: Callback&lt;number&gt;): void

取消注册WIFI流变更事件，当前版本不支持，抛出通用错误码801。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.MANAGE_WIFI_CONNECTION

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 固定填"streamChange"字符串。 |
| callback | Callback&lt;number&gt; | 否 | 状态改变回调函数，返回0:无，1：向下，2：向上，3：双向。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**
```ts
import wifi from '@ohos.wifi';

let recvStreamChangeFunc = (result:number) => {
    console.info("Receive stream change event: " + result);
}

// Register event
wifi.on("streamChange", recvStreamChangeFunc);

// Unregister event
wifi.off("streamChange", recvStreamChangeFunc);

```
## wifiManager.on('deviceConfigChange')<sup>9+</sup>

on(type: "deviceConfigChange", callback: Callback&lt;number&gt;): void

注册WIFI设备配置更改事件。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 固定填"streamChange"字符串。 |
| callback | Callback&lt;number&gt; | 是 | 状态改变回调函数，返回0: 添加配置, 1: 更改配置, 2: 删除配置. |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.off('deviceConfigChange')<sup>9+</sup>

off(type: "deviceConfigChange", callback?: Callback&lt;number&gt;): void

取消注册WIFI设备配置更改事件。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 固定填"streamChange"字符串。 |
| callback | Callback&lt;number&gt; | 否 | 状态改变回调函数，返回0: 添加配置, 1: 更改配置, 2: 删除配置.|

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2501000  | Operation failed.|

**示例：**
```ts
import wifi from '@ohos.wifiManager';

let recvDeviceConfigChangeFunc = (result:number) => {
    console.info("Receive device config change event: " + result);
}

// Register event
wifi.on("deviceConfigChange", recvDeviceConfigChangeFunc);

// Unregister event
wifi.off("deviceConfigChange", recvDeviceConfigChangeFunc);

```

## wifiManager.on('hotspotStateChange')<sup>9+</sup>

on(type: "hotspotStateChange", callback: Callback&lt;number&gt;): void

注册热点状态改变事件。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.AP.Core

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 固定填"hotspotStateChange"字符串。 |
| callback | Callback&lt;number&gt; | 是 | 状态改变回调函数。 |

**热点状态改变事件的枚举：**

| **枚举值** | **说明** |
| -------- | -------- |
| 0 | 未激活。 |
| 1 | 已激活。 |
| 2 | 激活中。 |
| 3 | 去激活中。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2601000  | Operation failed.|

## wifiManager.off('hotspotStateChange')<sup>9+</sup>

off(type: "hotspotStateChange", callback?: Callback&lt;number&gt;): void

取消注册热点状态改变事件。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.AP.Core

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 固定填"hotspotStateChange"字符串。 |
| callback | Callback&lt;number&gt; | 否 | 状态改变回调函数。如果callback不填，将取消注册该事件关联的所有回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2601000  | Operation failed.|

**示例：**
```ts
  import wifiManager from '@ohos.wifiManager';
  
  let recvHotspotStateChangeFunc = (result:number) => {
      console.info("Receive hotspot state change event: " + result);
  }
  
  // Register event
  wifiManager.on("hotspotStateChange", recvHotspotStateChangeFunc);
  
  // Unregister event
  wifiManager.off("hotspotStateChange", recvHotspotStateChangeFunc);
```

## wifiManager.on('hotspotStaJoin')<sup>9+</sup>

on(type: "hotspotStaJoin", callback: Callback&lt;StationInfo&gt;): void

注册wifi热点sta加入事件。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.MANAGE_WIFI_HOTSPOT

**系统能力：** SystemCapability.Communication.WiFi.AP.Core

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 固定填"hotspotStaJoin"字符串。 |
| callback | Callback&lt;StationInfo&gt; | 是 | 状态改变回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2601000  | Operation failed.|

## wifiManager.off('hotspotStaJoin')<sup>9+</sup>

off(type: "hotspotStaJoin", callback?: Callback&lt;StationInfo&gt;): void

取消注册wifi热点sta加入事件。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.MANAGE_WIFI_HOTSPOT

**系统能力：** SystemCapability.Communication.WiFi.AP.Core

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 固定填"hotspotStaJoin"字符串。 |
| callback | Callback&lt;StationInfo&gt; | 否 | 状态改变回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2601000  | Operation failed.|

**示例：**
```ts
import wifiManager from '@ohos.wifiManager';

let recvHotspotStaJoinFunc = (result:wifiManager.StationInfo) => {
    console.info("Receive hotspot sta join event: " + result);
}

// Register event
wifiManager.on("hotspotStaJoin", recvHotspotStaJoinFunc);

// Unregister event
wifiManager.off("hotspotStaJoin", recvHotspotStaJoinFunc);

```

## wifiManager.on('hotspotStaLeave')<sup>9+</sup>

on(type: "hotspotStaLeave", callback: Callback&lt;StationInfo&gt;): void

注册wifi热点sta离开事件。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.MANAGE_WIFI_HOTSPOT

**系统能力：** SystemCapability.Communication.WiFi.AP.Core

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 固定填"hotspotStaLeave"字符串。 |
  | callback | Callback&lt;StationInf]&gt; | 是 | 状态改变回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2601000  | Operation failed.|

## wifiManager.off('hotspotStaLeave')<sup>9+</sup>

off(type: "hotspotStaLeave", callback?: Callback&lt;StationInfo&gt;): void

取消注册wifi热点sta离开事件。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.MANAGE_WIFI_HOTSPOT

**系统能力：** SystemCapability.Communication.WiFi.AP.Core

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 固定填"hotspotStaLeave"字符串。 |
| callback | Callback&lt;StationInf]&gt; | 否 | 状态改变回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2601000  | Operation failed.|

**示例：**
```ts
import wifiManager from '@ohos.wifiManager';

let recvHotspotStaLeaveFunc = (result:wifiManager.StationInfo) => {
    console.info("Receive hotspot sta leave event: " + result);
}

// Register event
wifiManager.on("hotspotStaLeave", recvHotspotStaLeaveFunc);

// Unregister event
wifiManager.off("hotspotStaLeave", recvHotspotStaLeaveFunc);

```

## wifiManager.on('p2pStateChange')<sup>9+</sup>

on(type: "p2pStateChange", callback: Callback&lt;number&gt;): void

注册P2P开关状态改变事件。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 固定填"p2pStateChange"字符串。 |
| callback | Callback&lt;number&gt; | 是 | 状态改变回调函数。 |

** P2P状态改变事件的枚举：**

| **枚举值** | **说明** |
| -------- | -------- |
| 1 | 空闲。 |
| 2 | 打开中。 |
| 3 | 已打开。 |
| 4 | 关闭中。 |
| 5 | 已关闭。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.off('p2pStateChange')<sup>9+</sup>

off(type: "p2pStateChange", callback?: Callback&lt;number&gt;): void

取消注册P2P开关状态改变事件。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 固定填"p2pStateChange"字符串。 |
  | callback | Callback&lt;number&gt; | 否 | 状态改变回调函数。如果callback不填，将取消注册该事件关联的所有回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

**示例：**
```ts
  import wifiManager from '@ohos.wifiManager';
  
  let recvP2pStateChangeFunc = (result:number) => {
      console.info("Receive p2p state change event: " + result);
  }
  
  // Register event
  wifiManager.on("p2pStateChange", recvP2pStateChangeFunc);
  
  // Unregister event
  wifiManager.off("p2pStateChange", recvP2pStateChangeFunc);
```

## wifiManager.on('p2pConnectionChange')<sup>9+</sup>

on(type: "p2pConnectionChange", callback: Callback&lt;WifiP2pLinkedInfo&gt;): void

注册P2P连接状态改变事件。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 固定填"p2pConnectionChange"字符串。 |
  | callback | Callback&lt;[WifiP2pLinkedInfo](#wifip2plinkedinfo9)&gt; | 是 | 状态改变回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.off('p2pConnectionChange')<sup>9+</sup>

off(type: "p2pConnectionChange", callback?: Callback&lt;WifiP2pLinkedInfo&gt;): void

取消注册P2P连接状态改变事件。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 固定填"p2pConnectionChange"字符串。 |
  | callback | Callback&lt;[WifiP2pLinkedInfo](#wifip2plinkedinfo9)&gt; | 否 | 状态改变回调函数。如果callback不填，将取消注册该事件关联的所有回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

**示例：**
```ts
  import wifiManager from '@ohos.wifiManager';
  
  let recvP2pConnectionChangeFunc = (result:wifiManager.WifiP2pLinkedInfo) => {
      console.info("Receive p2p connection change event: " + result);
  }
  
  // Register event
  wifiManager.on("p2pConnectionChange", recvP2pConnectionChangeFunc);
  
  // Unregister event
  wifiManager.off("p2pConnectionChange", recvP2pConnectionChangeFunc);
```

## wifiManager.on('p2pDeviceChange')<sup>9+</sup>

on(type: "p2pDeviceChange", callback: Callback&lt;WifiP2pDevice&gt;): void

注册P2P设备状态改变事件。

**需要权限：**

API 9：ohos.permission.GET_WIFI_INFO、ohos.permission.LOCATION 和 ohos.permission.APPROXIMATELY_LOCATION

API 10起：ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 固定填"p2pDeviceChange"字符串。 |
  | callback | Callback&lt;[WifiP2pDevice](#wifip2pdevice9)&gt; | 是 | 状态改变回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.off('p2pDeviceChange')<sup>9+</sup>

off(type: "p2pDeviceChange", callback?: Callback&lt;WifiP2pDevice&gt;): void

取消注册P2P设备状态改变事件。

**需要权限：**

API 9：ohos.permission.LOCATION 和 ohos.permission.APPROXIMATELY_LOCATION

API 10起：无

**系统能力：** SystemCapability.Communication.WiFi.P2P

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 固定填"p2pDeviceChange"字符串。 |
  | callback | Callback&lt;[WifiP2pDevice](#wifip2pdevice9)&gt; | 否 | 状态改变回调函数。如果callback不填，将取消注册该事件关联的所有回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

**示例：**
```ts
  import wifiManager from '@ohos.wifiManager';
  
  let recvP2pDeviceChangeFunc = (result:wifiManager.WifiP2pDevice) => {
      console.info("Receive p2p device change event: " + result);
  }
  
  // Register event
  wifiManager.on("p2pDeviceChange", recvP2pDeviceChangeFunc);
  
  // Unregister event
  wifiManager.off("p2pDeviceChange", recvP2pDeviceChangeFunc);
```

## wifiManager.on('p2pPeerDeviceChange')<sup>9+</sup>

on(type: "p2pPeerDeviceChange", callback: Callback&lt;WifiP2pDevice[]&gt;): void

注册P2P对端设备状态改变事件。

**需要权限：**

API 9：ohos.permission.GET_WIFI_INFO、ohos.permission.LOCATION 和 ohos.permission.APPROXIMATELY_LOCATION

API 10起：ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 固定填"p2pPeerDeviceChange"字符串。 |
| callback | Callback&lt;[WifiP2pDevice[]](#wifip2pdevice9)&gt; | 是 | 状态改变回调函数。如果应用申请了ohos.permission.GET_WIFI_PEERS_MAC权限，则返回结果中的deviceAddress为真实设备地址，否则为随机设备地址。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.off('p2pPeerDeviceChange')<sup>9+</sup>

off(type: "p2pPeerDeviceChange", callback?: Callback&lt;WifiP2pDevice[]&gt;): void

取消注册P2P对端设备状态改变事件。

**需要权限：**

API 9：ohos.permission.LOCATION 和 ohos.permission.APPROXIMATELY_LOCATION

API 10起：无

**系统能力：** SystemCapability.Communication.WiFi.P2P

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 固定填"p2pPeerDeviceChange"字符串。 |
| callback | Callback&lt;[WifiP2pDevice[]](#wifip2pdevice9)&gt; | 否 | 状态改变回调函数。如果callback不填，将取消注册该事件关联的所有回调函数。如果应用申请了ohos.permission.GET_WIFI_PEERS_MAC权限，则返回结果中的deviceAddress为真实设备地址，否则为随机设备地址。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

**示例：**
```ts
  import wifiManager from '@ohos.wifiManager';
  
  let recvP2pPeerDeviceChangeFunc = (result:wifiManager.WifiP2pDevice[]) => {
      console.info("Receive p2p peer device change event: " + result);
  }
  
  // Register event
  wifiManager.on("p2pPeerDeviceChange", recvP2pPeerDeviceChangeFunc);
  
  // Unregister event
  wifiManager.off("p2pPeerDeviceChange", recvP2pPeerDeviceChangeFunc);
```

## wifiManager.on('p2pPersistentGroupChange')<sup>9+</sup>

on(type: "p2pPersistentGroupChange", callback: Callback&lt;void&gt;): void

注册P2P永久组状态改变事件。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 固定填"p2pPersistentGroupChange"字符串。 |
  | callback | Callback&lt;void&gt; | 是 | 状态改变回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.off('p2pPersistentGroupChange')<sup>9+</sup>

off(type: "p2pPersistentGroupChange", callback?: Callback&lt;void&gt;): void

取消注册P2P永久组状态改变事件。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 固定填"p2pPersistentGroupChange"字符串。 |
| callback | Callback&lt;void&gt; | 否 | 状态改变回调函数。如果callback不填，将取消注册该事件关联的所有回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

**示例：**
```ts
  import wifiManager from '@ohos.wifiManager';
  
  let recvP2pPersistentGroupChangeFunc = (result:void) => {
      console.info("Receive p2p persistent group change event: " + result);
  }
  
  // Register event
  wifiManager.on("p2pPersistentGroupChange", recvP2pPersistentGroupChangeFunc);
  
  // Unregister event
  wifiManager.off("p2pPersistentGroupChange", recvP2pPersistentGroupChangeFunc);
```

## wifiManager.on('p2pDiscoveryChange')<sup>9+</sup>

on(type: "p2pDiscoveryChange", callback: Callback&lt;number&gt;): void

注册发现设备状态改变事件。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 固定填"p2pDiscoveryChange"字符串。 |
  | callback | Callback&lt;number&gt; | 是 | 状态改变回调函数。 |

**发现设备状态改变事件的枚举：**

| **枚举值** | **说明** |
| -------- | -------- |
| 0 | 初始状态。 |
| 1 | 发现成功。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.off('p2pDiscoveryChange')<sup>9+</sup>

off(type: "p2pDiscoveryChange", callback?: Callback&lt;number&gt;): void

取消注册发现设备状态改变事件。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**参数：**

  | **参数名** | **类型** | **必填** | **说明** |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 固定填"p2pDiscoveryChange"字符串。 |
  | callback | Callback&lt;number&gt; | 否 | 状态改变回调函数。如果callback不填，将取消注册该事件关联的所有回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[WIFI错误码](../errorcodes/errorcode-wifi.md)。

| **错误码ID** | **错误信息** |
  | -------- | -------- |
| 2801000  | Operation failed.|

**示例：**
```ts
  import wifiManager from '@ohos.wifiManager';
  
  let recvP2pDiscoveryChangeFunc = (result:number) => {
      console.info("Receive p2p discovery change event: " + result);
  }
  
  // Register event
  wifiManager.on("p2pDiscoveryChange", recvP2pDiscoveryChangeFunc);
  
  // Unregister event
  wifiManager.off("p2pDiscoveryChange", recvP2pDiscoveryChangeFunc);
```
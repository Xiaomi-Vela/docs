# wifi��ϵͳChangeLog

## cl.wifiManager.1 �ӿ�Ȩ�ޱ�����޸�Ϊ�ļ��ڶ�Ӧ�Ľӿ�Ȩ�ޱ����

1- �漰�ӿ�

| �ӿ����� |���ǰȨ�� |�����Ȩ�� |
|----|--------|--------|
|**function** getCandidateConfigs(): Array<WifiDeviceConfig>; | 1.��Ҫλ��Ȩ�� |1.ȡ��λ��Ȩ�� |
|**function** getDeviceConfigs(): Array<WifiDeviceConfig>;| 1.��Ҫλ��Ȩ�� | 1.ȡ��λ��Ȩ�� |
|**function** getStations(): Array<StationInfo>;| 1.��Ҫλ��Ȩ�� 2.��������MAC | 1.ȡ��λ��Ȩ��;2.�������MAC(GET_PEER_MACȨ�޷�����ʵMAC) |
| **function** getCurrentP2pGroup(): Promise<WifiP2pGroupInfo>;| 1.��Ҫλ��Ȩ�� | 1.ȡ��λ��Ȩ�� |
| **function** getCurrentP2pGroup(callback: AsyncCallback<WifiP2pGroupInfo>): **void**; | 1.��Ҫλ��Ȩ��| 1.ȡ��λ��Ȩ�� |
| **function** getP2pPeerDevices(): Promise<WifiP2pDevice[]>;| 1.��Ҫλ��Ȩ�� 2.��������MAC | 1.ȡ��λ��Ȩ��;2.�������MAC(GET_PEER_MACȨ�޷�����ʵMAC) |
| **function** getP2pPeerDevices(callback: AsyncCallback<WifiP2pDevice[]>): **void**;| 1.��Ҫλ��Ȩ�� | 1.ȡ��λ��Ȩ��;2.�������MAC(GET_PEER_MACȨ�޷�����ʵMAC) |
| **function** p2pConnect(config: WifiP2PConfig): **void**; | 1.��Ҫλ��Ȩ��| 1.ȡ��λ��Ȩ�� |
| **function** startDiscoverDevices(): **void**; | 1.��Ҫλ��Ȩ��| 1.ȡ��λ��Ȩ�� |
| **function** getP2pGroups(): Promise<Array<WifiP2pGroupInfo>>;| 1.��Ҫλ��Ȩ�� | 1.ȡ��λ��Ȩ�� |
| **function** getP2pGroups(callback: AsyncCallback<Array<WifiP2pGroupInfo>>): **void**; | 1.��Ҫλ��Ȩ��| 1.ȡ��λ��Ȩ�� |
| **function** on(**type**: "p2pDeviceChange", callback: Callback<WifiP2pDevice>): **void**;| 1.��Ҫλ��Ȩ�� 2.��������MAC | 1.ȡ��λ��Ȩ��;2.�������MAC(GET_PEER_MACȨ�޷�����ʵMAC) |
| **function** off(**type**: "p2pDeviceChange", callback?: Callback<WifiP2pDevice>): **void**; | 1.��Ҫλ��Ȩ�� 2.��������MAC| 1.ȡ��λ��Ȩ��;2.�������MAC(GET_PEER_MACȨ�޷�����ʵMAC) |
| **function** on(**type**: "p2pPeerDeviceChange", callback: Callback<WifiP2pDevice[]>): **void**; | 1.��Ҫλ��Ȩ�� 2.��������MAC | 1.ȡ��λ��Ȩ��;2.�������MAC(GET_PEER_MACȨ�޷�����ʵMAC) |
| **function** off(**type**: "p2pPeerDeviceChange", callback?: Callback<WifiP2pDevice[]>): **void**;| 1.��Ҫλ��Ȩ�� 2.��������MAC| 1.ȡ��λ��Ȩ��;2.�������MAC(GET_PEER_MACȨ�޷�����ʵMAC) |

**���Ӱ��**<br>
ʹ��֮ǰ�ѷ�����API 9��beta�汾��ʹ�õ��������ӿڵģ���Ҫ��Ϊʹ�ñ�����Ȩ�ޡ�

**�ؼ��Ľӿ�/������**<br>
��

**����ָ��**<br>
Ȩ����������


## cl.wifiManager.2 �޸Ľӿ�**function** scan(): **void** Ϊ **function** startScan(): **void**;

**���Ӱ��**<br>
ʹ��֮ǰ�ѷ�����API 9��beta�汾��ʹ�õ���������scan����Ҫ��Ϊʹ��startScan�ӿڡ�

**�ؼ��Ľӿ�/������**<br>
��

**����ָ��**<br>
��scan��Ҫ��Ϊʹ��startScan�ӿڡ�


## cl.wifiManager.3 �޸Ľӿ�getScanResults(): Promise<Array<WifiScanInfo>> Ϊ **function** getScanInfoList(): Array<WifiScanInfo>;
	
**���Ӱ��**<br>
ʹ��֮ǰ�ѷ�����API 9��beta�汾��ʹ�õ���������getScanResults����Ҫ��Ϊʹ��getScanInfoList�ӿڡ�

**�ؼ��Ľӿ�/������**<br>
��

**����ָ��**<br>
��getScanResults��Ҫ��Ϊʹ��getScanInfoList�ӿڡ�


## cl.wifiManager.4 �޸Ľӿ�function** getScanResults(callback: AsyncCallback<Array<WifiScanInfo>>): **void**; Ϊ **function** getScanInfoList(): Array<WifiScanInfo>;
	
**���Ӱ��**<br>
ʹ��֮ǰ�ѷ�����API 9��beta�汾��ʹ�õ���������getScanResults����Ҫ��Ϊʹ��getScanInfoList�ӿڡ�

**�ؼ��Ľӿ�/������**<br>
��

**����ָ��**<br>
��getScanResults��Ҫ��Ϊʹ��getScanInfoList�ӿڡ�


## cl.wifiManager.5 �޸Ľӿ�**function** getScanResultsSync(): Array<WifiScanInfo>; Ϊ **function** getScanInfoList(): Array<WifiScanInfo>;

**���Ӱ��**<br>
ʹ��֮ǰ�ѷ�����API 9��beta�汾��ʹ�õ���������getScanResultsSync����Ҫ��Ϊʹ��getScanInfoList�ӿڡ�

**�ؼ��Ľӿ�/������**<br>
��

**����ָ��**<br>
��getScanResultsSync��Ҫ��Ϊʹ��getScanInfoList�ӿڡ�


## cl.wifiManager.6 �����ӿ�����

| �ӿ����� | �ӿ����� |
|------|---------|
| **function** setScanAlwaysAllowed(isScanAlwaysAllowed: boolean): **void**; | ���ú�̨ɨ�迪��     |
| **function** getScanAlwaysAllowed(): boolean;                | ��ȡ��̨ɨ�迪��     |
| **function** getIpv6Info(): Ipv6Info;                        | ��ȡipv6��ַ��Ϣ     |
| **function** isBandTypeSupported(bandType: WifiBandType): boolean; | �ж��Ƿ�֧��BandType |
| **function** get5GChannelList(): Array<**number**>;          | ��ȡ5G�ŵ��б�       |
| **function** getDisconnectedReason(): DisconnectedReason;    | ��ȡ����Ͽ�ԭ��     |

**���Ӱ��**<br>
ʹ��֮ǰ�ѷ�����API ��Ӱ�졣

**�ؼ��Ľӿ�/������**<br>
��

**����ָ��**<br>
��������
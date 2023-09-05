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


## cl.wifiManager.2 ɨ��wifi�����Ľӿڷ���������
  
��Ϊ�Ż�ɨ��ӿ�scan(),getScanResults(),getScanResultsSync(),��ԭ�ӿڷ���,�Ƽ�ʹ���µĽӿڽ���Ӧ�ÿ���.

**���Ӱ��**<br>
���½ӿڴ�API 10��ʼ������������Ӱ���ѿ���Ӧ�õļ����ԣ��������Ϊʹ���µ�����ӿڡ�

**�ؼ��Ľӿ�/������**<br>
|�����ӿ� |��Ӧ�����ӿ� |����˵��|
| ------------- |-------------------------------------------------------- |-----------------------|
| **function** scan(): **void**; |**function** startScan(): **void**;| ʹ��startScan�ӿ�����ɨ�� |
| **function** getScanResults(): Promise<Array<WifiScanInfo>>;|**function** getScanInfoList(): Array<WifiScanInfo>;| ʹ��getScanInfoList��ȡɨ���б� |
| **function** getScanResults(callback: AsyncCallback<Array<WifiScanInfo>>): **void**;|**function** getScanInfoList(): Array<WifiScanInfo>; | ʹ��getScanInfoList��ȡɨ���б� |
| **function** getScanResultsSync(): Array<WifiScanInfo>; |**function** getScanInfoList(): Array<WifiScanInfo>; | ʹ��getScanInfoList��ȡɨ���б� |


**����ָ��**<br>
Ӧ����ʹ�÷����ӿڵģ���������API 10�Ժ��޸�Ϊ��Ӧ�������ӿڡ�








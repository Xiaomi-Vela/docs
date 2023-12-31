# @ohos.application.missionManager (missionManager)

missionManager模块提供系统任务管理能力，包括对系统任务执行锁定、解锁、清理、切换到前台等操作。

> **说明：**
> 
> 本模块首批接口从API version 8开始支持，从API version 9废弃，替换模块为[@ohos.app.ability.missionManager](js-apis-app-ability-missionManager.md)。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import missionManager from '@ohos.application.missionManager';
```

## 权限列表

ohos.permission.MANAGE_MISSIONS

## missionManager.registerMissionListener

registerMissionListener(listener: MissionListener): number

注册系统任务状态监听器。

**需要权限**：ohos.permission.MANAGE_MISSIONS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Mission

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | listener | [MissionListener](js-apis-inner-application-missionListener.md) | 是 | 系统任务监听器。 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | number | 监听器的index值，由系统创建，在注册系统任务状态监听器时分配，和监听器一一对应&nbsp;。 |

**示例：**

```ts
import missionManager from '@ohos.application.missionManager';

console.log('registerMissionListener');
let listenerid = missionManager.registerMissionListener({
  onMissionCreated: (mission) => {console.log('--------onMissionCreated-------');},
  onMissionDestroyed: (mission) => {console.log('--------onMissionDestroyed-------');},
  onMissionSnapshotChanged: (mission) => {console.log('--------onMissionSnapshotChanged-------');},
  onMissionMovedToFront: (mission) => {console.log('--------onMissionMovedToFront-------');},
  onMissionIconUpdated: (mission, icon) => {console.log('--------onMissionIconUpdated-------');},
  onMissionClosed: (mission) => {console.log('--------onMissionClosed-------');},
  onMissionLabelUpdated: (mission) => {console.log('--------onMissionLabelUpdated-------');}
});
```


## missionManager.unregisterMissionListener

unregisterMissionListener(listenerId: number, callback: AsyncCallback&lt;void&gt;): void

解注册任务状态监听器。

**需要权限**：ohos.permission.MANAGE_MISSIONS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Mission

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | listenerId | number | 是 | 系统任务状态监听器的index值，和监听器一一对应，由registerMissionListener方法返回。 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 执行结果回调函数。 |

**示例：**

```ts
  import missionManager from '@ohos.application.missionManager';

  console.log('registerMissionListener');
  let listenerid = missionManager.registerMissionListener({
    onMissionCreated: (mission) => {console.log('--------onMissionCreated-------');},
    onMissionDestroyed: (mission) => {console.log('--------onMissionDestroyed-------');},
    onMissionSnapshotChanged: (mission) => {console.log('--------onMissionSnapshotChanged-------');},
    onMissionMovedToFront: (mission) => {console.log('--------onMissionMovedToFront-------');},
    onMissionIconUpdated: (mission, icon) => {console.log('--------onMissionIconUpdated-------');},
    onMissionClosed: (mission) => {console.log('--------onMissionClosed-------');},
    onMissionLabelUpdated: (mission) => {console.log('--------onMissionLabelUpdated-------');}
  });

  missionManager.unregisterMissionListener(listenerid, (error) => {
      console.error('unregisterMissionListener fail, error: ${error}');
  });
```


## missionManager.unregisterMissionListener

unregisterMissionListener(listenerId: number): Promise&lt;void&gt;

反注册任务状态监听器，以promise方式返回执行结果。

**需要权限**：ohos.permission.MANAGE_MISSIONS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Mission

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | listenerId | number | 是 | 系统任务状态监听器的index值，和监听器一一对应，由registerMissionListener方法返回。 |

**返回值：**

  | 类型 | 说明 | 
  | -------- | -------- |
  | Promise&lt;void&gt; | promise方式返回执行结果。 | 

**示例：**

```ts
  import missionManager from '@ohos.application.missionManager';
  import { BusinessError } from '@ohos.base';

  console.log('registerMissionListener');
  let listenerid = missionManager.registerMissionListener({
    onMissionCreated: (mission) => {console.log('--------onMissionCreated-------');},
    onMissionDestroyed: (mission) => {console.log('--------onMissionDestroyed-------');},
    onMissionSnapshotChanged: (mission) => {console.log('--------onMissionSnapshotChanged-------');},
    onMissionMovedToFront: (mission) => {console.log('--------onMissionMovedToFront-------');},
    onMissionIconUpdated: (mission, icon) => {console.log('--------onMissionIconUpdated-------');},
    onMissionClosed: (mission) => {console.log('--------onMissionClosed-------');},
    onMissionLabelUpdated: (mission) => {console.log('--------onMissionLabelUpdated-------');}
  });

  missionManager.unregisterMissionListener(listenerid).catch((error: BusinessError) => {
      console.error('unregisterMissionListener fail, error: ${error}');
  });
```


## missionManager.getMissionInfo

getMissionInfo(deviceId: string, missionId: number, callback: AsyncCallback&lt;MissionInfo&gt;): void

获取单个任务信息，以异步回调的方式返回任务信息。

**需要权限**：ohos.permission.MANAGE_MISSIONS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Mission

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | deviceId | string | 是 | 设备ID，本机默认为空字符串。 |
  | missionId | number | 是 | 任务ID。 |
  | callback | AsyncCallback&lt;[MissionInfo](js-apis-inner-application-missionInfo.md)&gt; | 是 | 执行结果回调函数，返回任务信息。 |

**示例：**

  ```ts
  import missionManager from '@ohos.application.missionManager';
  import { BusinessError } from '@ohos.base';

  let allMissions=missionManager.getMissionInfos('',10).catch((err: BusinessError) => {
    console.log('${err}');});
  missionManager.getMissionInfo('', allMissions[0].missionId, (error, mission) => {
    if (error.code) {
      console.error('getMissionInfo failed, error.code: ${error.code}, error.message: ${error.message}');
      return;
    }

    console.log('mission.missionId = ${mission.missionId}');
    console.log('mission.runningState = ${mission.runningState}');
    console.log('mission.lockedState = ${mission.lockedState}');
    console.log('mission.timestamp = ${mission.timestamp}');
    console.log('mission.label = ${mission.label}');
    console.log('mission.iconPath = ${mission.iconPath}');
  });
  ```


## missionManager.getMissionInfo

getMissionInfo(deviceId: string, missionId: number): Promise&lt;MissionInfo&gt;

获取单个任务信息，以promise方式返回任务信息。

**需要权限**：ohos.permission.MANAGE_MISSIONS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Mission

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | deviceId | string | 是 | 设备ID，本机默认为空字符串。 |
  | missionId | number | 是 | 任务ID。 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;[MissionInfo](js-apis-inner-application-missionInfo.md)&gt; | 任务信息。 |

**示例：**

  ```ts
  import missionManager from '@ohos.application.missionManager';
  import { BusinessError } from '@ohos.base';

  let mission = missionManager.getMissionInfo('', 10).catch((error: BusinessError) => {
      console.error('getMissionInfo fail, error: ${error}');
  });
  ```


## missionManager.getMissionInfos

getMissionInfos(deviceId: string, numMax: number, callback: AsyncCallback&lt;Array&lt;MissionInfo&gt;&gt;): void

获取所有任务信息，以回调函数的方式返回任务信息数组。

**需要权限**：ohos.permission.MANAGE_MISSIONS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Mission

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | deviceId | string | 是 | 设备ID，本机默认为空字符串。 |
  | numMax | number | 是 | 任务信息数量上限。 |
  | callback | AsyncCallback&lt;Array&lt;[MissionInfo](js-apis-inner-application-missionInfo.md)&gt;&gt; | 是 | 执行结果回调函数，返回任务信息数组。 |

**示例：**

  ```ts
  import missionManager from '@ohos.application.missionManager';

  missionManager.getMissionInfos('', 10, (error, missions) => {
      if (error.code) {
          console.error(`getMissionInfos failed, error.code: ${error.code}, error.message: ${error.message}`);
          return;
      }
      console.log(`size = ${missions.length}`);
      console.log(`missions = ${JSON.stringify(missions)}`);
  });
  ```


## missionManager.getMissionInfos

getMissionInfos(deviceId: string, numMax: number): Promise&lt;Array&lt;MissionInfo&gt;&gt;

获取所有任务信息，以promise的方式返回任务信息数组。

**需要权限**：ohos.permission.MANAGE_MISSIONS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Mission

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | deviceId | string | 是 | 设备ID，本机默认为空字符串。 |
  | numMax | number | 是 | 任务信息数量上限。 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;Array&lt;[MissionInfo](js-apis-inner-application-missionInfo.md)&gt;&gt; | 任务信息数组。 |

**示例：**

  ```ts
  import missionManager from '@ohos.application.missionManager';
  import { BusinessError } from '@ohos.base';

  let allMissions = missionManager.getMissionInfos('', 10).catch((error: BusinessError) => {
      console.error('getMissionInfos fail, error: ${error}');
  });
  ```


## missionManager.getMissionSnapShot

getMissionSnapShot(deviceId: string, missionId: number, callback: AsyncCallback&lt;MissionSnapshot&gt;): void

获取任务快照，以回调函数的方式返回快照内容。

**需要权限**：ohos.permission.MANAGE_MISSIONS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Mission

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | deviceId | string | 是 | 设备ID，本机默认为空字符串。 |
  | missionId | number | 是 | 任务ID。 |
  | callback | AsyncCallback&lt;[MissionSnapshot](js-apis-inner-application-missionSnapshot.md)&gt; | 是 | 执行结果回调函数，返回任务快照信息。 |

**示例：**

  ```ts
  import missionManager from '@ohos.application.missionManager';

  missionManager.getMissionInfos('', 10, (error, missions) => {
    if (error.code) {
        console.error(`getMissionInfos failed, error.code: ${error.code}, error.message: ${error.message}`);
        return;
    }
    console.log(`size = ${missions.length}`);
    console.log(`missions = ${JSON.stringify(missions)}`);
    let id = missions[0].missionId;

    missionManager.getMissionSnapShot('', id, (error, snapshot) => {
      if (error.code) {
          console.error(`getMissionSnapShot failed, error.code: ${error.code}, error.message: ${error.message}`);
          return;
      }
      console.log(`bundleName = ${snapshot.ability.bundleName}`);
    });
  });
  ```


## missionManager.getMissionSnapShot

getMissionSnapShot(deviceId: string, missionId: number): Promise&lt;MissionSnapshot&gt;

获取任务快照，以promise的方式返回快照内容。

**需要权限**：ohos.permission.MANAGE_MISSIONS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Mission

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | deviceId | string | 是 | 设备ID，本机默认为空字符串。 |
  | missionId | number | 是 | 任务ID。 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;[MissionSnapshot](js-apis-inner-application-missionSnapshot.md)&gt; | 任务快照信息。 |

**示例：**

  ```ts
  import missionManager from '@ohos.application.missionManager';
  import { BusinessError } from '@ohos.base';

  let id: number = -1;
  missionManager.getMissionInfos('',10).then((res) => {
    let allMissions = res;
    console.log(`size = ${allMissions.length}`);
    console.log(`missions = ${JSON.stringify(allMissions)}`);
    id = allMissions[0].missionId;
  }).catch((error: BusinessError) => {
    console.error(`getMissionInfos fail, error: ${error}`);
  });

  let snapshot = missionManager.getMissionSnapShot('', id).catch((error: BusinessError) => {
    console.error(`getMissionSnapShot fail, error: ${error}`);
  });
  ```

## missionManager.lockMission

lockMission(missionId: number, callback: AsyncCallback&lt;void&gt;): void

锁定指定任务id的任务，以回调函数的方式返回。

**需要权限**：ohos.permission.MANAGE_MISSIONS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Mission

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | missionId | number | 是 | 任务ID。 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 执行结果回调函数。 |

**示例：**

  ```ts
  import missionManager from '@ohos.application.missionManager';

  missionManager.getMissionInfos('', 10, (error, missions) => {
    if (error.code) {
        console.error(`getMissionInfos failed, error.code: ${error.code}, error.message: ${error.message}`);
        return;
    }
    console.log(`size = ${missions.length}`);
    console.log(`missions = ${JSON.stringify(missions)}`);
    let id = missions[0].missionId;

    missionManager.lockMission(id).then(() => {
  	  console.log('lockMission is called ');
    });
  });
  ```


## missionManager.lockMission

lockMission(missionId: number): Promise&lt;void&gt;

锁定指定任务id的任务，以promise方式返回。

**需要权限**：ohos.permission.MANAGE_MISSIONS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Mission

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | missionId | number | 是 | 任务ID。 |

**返回值：**

  | 类型 | 说明 | 
  | -------- | -------- |
  | Promise&lt;void&gt; | promise方式返回执行结果。 | 

**示例：**

  ```ts
  import missionManager from '@ohos.application.missionManager';
  import { BusinessError } from '@ohos.base';

  let id: number = -1;
  missionManager.getMissionInfos('',10).then((res) => {
    let allMissions = res;
    console.log(`size = ${allMissions.length}`);
    console.log(`missions = ${JSON.stringify(allMissions)}`);
    id = allMissions[0].missionId;
  }).catch((error: BusinessError) => {
      console.error(`getMissionInfos fail, error: ${error}`);
  });

  missionManager.lockMission(id).catch((error: BusinessError) => {
      console.error(`lockMission fail, error: ${error}`);
  });
  ```


## missionManager.unlockMission

unlockMission(missionId: number, callback: AsyncCallback&lt;void&gt;): void

解锁指定任务id的任务，以回调函数的方式返回。

**需要权限**：ohos.permission.MANAGE_MISSIONS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Mission

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| missionId | number | 是 | 任务ID。 |
| callback | AsyncCallback&lt;void&gt; | 是 | 执行结果回调函数。 |

**示例：**

  ```ts
  import missionManager from '@ohos.application.missionManager';

  missionManager.getMissionInfos('', 10, (error, missions) => {
    if (error.code) {
        console.error(`getMissionInfos failed, error.code: ${error.code}, error.message: ${error.message}`);
        return;
    }
    console.log(`size = ${missions.length}`);
    console.log(`missions = ${JSON.stringify(missions)}`);
    let id = missions[0].missionId;

    missionManager.unlockMission(id).then(() => {
  	  console.log('unlockMission is called ');
    });
  });
  ```


## missionManager.unlockMission

unlockMission(missionId: number): Promise&lt;void&gt;

解锁指定任务id的任务，以promise的方式返回。

**需要权限**：ohos.permission.MANAGE_MISSIONS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Mission

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | missionId | number | 是 | 任务ID。 |

**返回值：**

  | 类型 | 说明 | 
  | -------- | -------- |
  | Promise&lt;void&gt; | promise方式返回执行结果。 | 

**示例：**

  ```ts
  import missionManager from '@ohos.application.missionManager';
  import { BusinessError } from '@ohos.base';

  let id: number = -1;
  missionManager.getMissionInfos('',10).then((res) => {
    let allMissions = res;
    console.log(`size = ${allMissions.length}`);
    console.log(`missions = ${JSON.stringify(allMissions)}`);
    id = allMissions[0].missionId;
  }).catch((error: BusinessError) => {
      console.error(`getMissionInfos fail, error: ${error}`);
  });

  missionManager.lockMission(id).catch((error: BusinessError) => {
      console.error(`lockMission fail, error: ${error}`);
  });
  missionManager.unlockMission(id).catch((error: BusinessError) => {
      console.error(`unlockMission fail, error: ${error}`);
  });
  ```


## missionManager.clearMission

clearMission(missionId: number, callback: AsyncCallback&lt;void&gt;): void

清理指定任务id的任务，无论该任务是否被锁定，以回调函数的方式返回。

**需要权限**：ohos.permission.MANAGE_MISSIONS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Mission

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | missionId | number | 是 | 任务ID。 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 执行结果回调函数。 |

**示例：**

  ```ts
  import missionManager from '@ohos.application.missionManager';

  missionManager.getMissionInfos('', 10, (error, missions) => {
    if (error.code) {
        console.error(`getMissionInfos failed, error.code: ${error.code}, error.message: ${error.message}`);
        return;
    }
    console.log(`size = ${missions.length}`);
    console.log(`missions = ${JSON.stringify(missions)}`);
    let id = missions[0].missionId;

    missionManager.clearMission(id).then(() => {
  	  console.log('clearMission is called ');
    });
  });
  ```


## missionManager.clearMission

clearMission(missionId: number): Promise&lt;void&gt;

清理指定任务id的任务，无论该任务是否被锁定，以promise的方式返回。

**需要权限**：ohos.permission.MANAGE_MISSIONS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Mission

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | missionId | number | 是 | 任务ID。 |

**返回值：**

  | 类型 | 说明 | 
  | -------- | -------- |
  | Promise&lt;void&gt; | promise方式返回执行结果。 | 

**示例：**

  ```ts
  import missionManager from '@ohos.application.missionManager';
  import { BusinessError } from '@ohos.base';

  let id: number = -1;
  missionManager.getMissionInfos('',10).then((res) => {
    let allMissions = res;
    console.log(`size = ${allMissions.length}`);
    console.log(`missions = ${JSON.stringify(allMissions)}`);
    id = allMissions[0].missionId;
  }).catch((error: BusinessError) => {
      console.error(`getMissionInfos fail, error: ${error}`);
  });

  missionManager.clearMission(id).catch((error: BusinessError) => {
    console.error(`clearMission fail, error: ${error}`);
  });
  ```


## missionManager.clearAllMissions

clearAllMissions(callback: AsyncCallback&lt;void&gt;): void

清理所有未锁定的任务，以回调函数的方式返回。

**需要权限**：ohos.permission.MANAGE_MISSIONS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Mission

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;void&gt; | 是 | 执行结果回调函数。 |

**示例：**

  ```ts
  import missionManager from '@ohos.application.missionManager'

  missionManager.clearAllMissions().then(() => {
    console.log('clearAllMissions is called ');
  });
  ```


## missionManager.clearAllMissions

clearAllMissions(): Promise&lt;void&gt;

清理所有未锁定的任务，以promise的方式返回。

**需要权限**：ohos.permission.MANAGE_MISSIONS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Mission

**系统API**: 此接口为系统接口，三方应用不支持调用。

**返回值：**

  | 类型 | 说明 | 
  | -------- | -------- |
  | Promise&lt;void&gt; | promise方式返回执行结果。 | 

**示例：**

  ```ts
  import missionManager from '@ohos.application.missionManager';
  import { BusinessError } from '@ohos.base';

  missionManager.clearAllMissions().catch((error: BusinessError) => {
      console.error('clearAllMissions fail, error: ${error}');
  });
  ```


## missionManager.moveMissionToFront

moveMissionToFront(missionId: number, callback: AsyncCallback&lt;void&gt;): void

把指定任务id的任务切到前台，以回调函数的方式返回。

**需要权限**：ohos.permission.MANAGE_MISSIONS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Mission

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | missionId | number | 是 | 任务ID。 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 执行结果回调函数。 |

**示例：**

  ```ts
  import missionManager from '@ohos.application.missionManager';

  missionManager.getMissionInfos('', 10, (error, missions) => {
    if (error.code) {
        console.error(`getMissionInfos failed, error.code: ${error.code}, error.message: ${error.message}`);
        return;
    }
    console.log(`size = ${missions.length}`);
    console.log(`missions = ${JSON.stringify(missions)}`);
    let id = missions[0].missionId;

    missionManager.moveMissionToFront(id).then(() => {
  	  console.log('moveMissionToFront is called ');
    });
  });
  ```


## missionManager.moveMissionToFront

moveMissionToFront(missionId: number, options: StartOptions, callback: AsyncCallback&lt;void&gt;): void

把指定任务id的任务切到前台，同时指定任务切换到前台时的启动参数，例如窗口模式、设备ID等，以回调函数的方式返回。

**需要权限**：ohos.permission.MANAGE_MISSIONS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Mission

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | missionId | number | 是 | 任务ID。 |
  | options | [StartOptions](js-apis-app-ability-startOptions.md) | 是 | 启动参数选项，用于指定任务切到前台时的窗口模式，设备ID等。 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 执行结果回调函数。 |

**示例：**

  ```ts
  import missionManager from '@ohos.application.missionManager';

  missionManager.getMissionInfos('', 10, (error, missions) => {
    if (error.code) {
        console.error(`getMissionInfos failed, error.code: ${error.code}, error.message: ${error.message}`);
        return;
    }
    console.log(`size = ${missions.length}`);
    console.log(`missions = ${JSON.stringify(missions)}`);
    let id = missions[0].missionId;

    missionManager.moveMissionToFront(id,{windowMode : 101}).then(() => {
  	  console.log('moveMissionToFront is called ');
    });
  });
  ```


## missionManager.moveMissionToFront

moveMissionToFront(missionId: number, options?: StartOptions): Promise&lt;void&gt;

把指定任务id的任务切到前台，同时指定任务切换到前台时的启动参数，例如窗口模式、设备ID等，以promise的方式返回。

**需要权限**：ohos.permission.MANAGE_MISSIONS

**系统能力**：SystemCapability.Ability.AbilityRuntime.Mission

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | missionId | number | 是 | 任务ID。 |
  | options | [StartOptions](js-apis-app-ability-startOptions.md) | 否 | 启动参数选项，用于指定任务切到前台时的窗口模式，设备ID等。 |

**返回值：**

  | 类型 | 说明 | 
  | -------- | -------- |
  | Promise&lt;void&gt; | promise方式返回执行结果。 | 

**示例：**

  ```ts
  import missionManager from '@ohos.application.missionManager';
  import { BusinessError } from '@ohos.base';

  let id: number = -1;
  missionManager.getMissionInfos('',10).then((res) => {
    let allMissions = res;
    console.log(`size = ${allMissions.length}`);
    console.log(`missions = ${JSON.stringify(allMissions)}`);
    id = allMissions[0].missionId;
  }).catch((error: BusinessError) => {
      console.error(`getMissionInfos fail, error: ${error}`);
  });

  missionManager.moveMissionToFront(id).catch((error: BusinessError) => {
    console.error(`moveMissionToFront fail, error: ${error}`);
  });
  ```
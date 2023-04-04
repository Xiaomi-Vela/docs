# 数据共享开发指导
DataShare即数据共享模块，提供了向其他应用共享以及管理其数据的方法。目前仅支持同个设备上应用之间的数据共享。

## 接口说明

**表1** 数据提供方API说明

|接口名|描述|
|:------|:------|
|onCreate?(want: Want, callback: AsyncCallback&lt;void&gt;): void|DataShareExtensionAbility生命周期回调，在数据提供方应用创建时回调，执行初始化业务逻辑操作，如创建数据库。|
|insert?(uri: string, valueBucket: ValuesBucket, callback: AsyncCallback&lt;number&gt;): void|业务函数，在访问方向数据库中插入数据时回调。|
|update?(uri: string, predicates: DataSharePredicates, valueBucket: ValuesBucket, callback: AsyncCallback&lt;number&gt;): void|业务函数，在访问方更新数据时回调。|
|query?(uri: string, predicates: DataSharePredicates, columns: Array&lt;string&gt;, callback: AsyncCallback&lt;Object&gt;): void|业务函数，在访问方查询数据时回调。|
|delete?(uri: string, predicates: DataSharePredicates, callback: AsyncCallback&lt;number&gt;): void|业务函数，在访问方删除数据时回调。|

完整的数据提供方接口请见[DataShareExtensionAbility](../reference/apis/js-apis-application-dataShareExtensionAbility.md)。

**表2** 数据访问方API说明

| 接口名                                                       | 描述                               |
| :----------------------------------------------------------- | :--------------------------------- |
| createDataShareHelper(context: Context, uri: string, callback: AsyncCallback&lt;DataShareHelper&gt;): void | 创建DataShare工具类。              |
| insert(uri: string, value: ValuesBucket, callback: AsyncCallback&lt;number&gt;): void | 将单条数据记录插入数据库。         |
| update(uri: string, predicates: DataSharePredicates, value: ValuesBucket, callback: AsyncCallback&lt;number&gt;): void | 更新数据库中的数据记录。           |
| query(uri: string, predicates: DataSharePredicates, columns: Array&lt;string&gt;, callback: AsyncCallback&lt;DataShareResultSet&gt;): void | 查询数据库中的数据。               |
| delete(uri: string, predicates: DataSharePredicates, callback: AsyncCallback&lt;number&gt;): void | 从数据库中删除一条或多条数据记录。 |

完整的数据访问方接口请见[DataShareHelper](../reference/apis/js-apis-data-dataShare.md)。

## 开发场景

数据共享可分为数据的提供方和访问方两部分。

- 提供方可以选择性实现数据的增、删、改、查，以及文件打开等功能，并对外共享这些数据。
- 访问方利用工具类，便可以访问提供方提供的这些数据。

以下是数据提供方和数据访问方应用的各自开发示例。

### 数据提供方应用的开发（仅限系统应用）

[DataShareExtensionAbility](../reference/apis/js-apis-application-dataShareExtensionAbility.md)提供以下API，根据需要重写对应回调方法。

- **onCreate**

  DataShare客户端连接DataShareExtensionAbility服务端时，服务端回调此接口，执行初始化业务逻辑操作。该方法可以选择性重写。

- **insert**

  业务函数，客户端请求插入数据时回调此接口，服务端需要在此回调中实现插入数据功能，该方法可以选择性重写。

- **update**

  业务函数，客户端请求更新数据时回调此接口，服务端需要在此回调中实现更新数据功能，该方法可以选择性重写。

- **delete**

  业务函数，客户端请求删除数据时回调此接口，服务端需要在此回调中实现删除数据功能，该方法可以选择性重写。

- **query**

  业务函数，客户端请求查询数据时回调此接口，服务端需要在此回调中实现查询数据功能，该方法可以选择性重写。

- **batchInsert**

  业务函数，客户端请求批量插入数据时回调此接口，服务端需要在此回调中实现批量插入数据数据功能，该方法可以选择性重写。

- **normalizeUri**

  业务函数，客户端给定的URI转换为服务端使用的URI时回调此接口，该方法可以选择性重写。

- **denormalizeUri**

  业务函数，服务端使用的URI转换为客户端传入的初始URI时服务端回调此接口，该方法可以选择性重写。

开发者在实现一个数据共享服务时，需要在DevEco Studio工程中手动新建一个DataShareExtensionAbility，具体步骤如下。

1. 在工程Module对应的ets目录下，右键选择“New &gt; Directory”，新建一个目录并命名为DataShareAbility。

2. 在DataShareAbility目录，右键选择“New &gt; TypeScript File”，新建一个TypeScript文件并命名为DataShareAbility.ts。

3. 在DataShareAbility.ts文件中，增加导入DataShareExtensionAbility的依赖包，开发者可根据应用需求选择性重写其业务实现。例如数据提供方只提供插入、删除和查询服务，则可只重写这些接口。


4. 导入基础依赖包。

   ```ts
   import Extension from '@ohos.application.DataShareExtensionAbility';
   import rdb from '@ohos.data.relationalStore';
   import fileIo from '@ohos.fileio';
   import dataSharePredicates from '@ohos.data.dataSharePredicates';
   ```

5. 数据提供方（也称服务端）继承于DataShareExtensionAbility，开发者可根据应用需求选择性重写其业务实现。例如数据提供方只提供查询服务，则可只重写查询接口。

6. 数据提供方的业务实现由开发者自定义。例如可以通过数据库、读写文件或访问网络等各方式实现数据提供方的数据存储。

   ```ts
   const DB_NAME = "DB00.db";
   const TBL_NAME = "TBL00";
   const DDL_TBL_CREATE = "CREATE TABLE IF NOT EXISTS "
   + TBL_NAME
   + " (id INTEGER PRIMARY KEY AUTOINCREMENT, name TEXT, age INTEGER, isStudent BOOLEAN, Binary BINARY)";

   let rdbStore;
   let result;

   export default class DataShareExtAbility extends Extension {
       private rdbStore_;

   	// 重写onCreate接口
       onCreate(want, callback) {
           result = this.context.cacheDir + '/datashare.txt';
           // 业务实现使用RDB
            rdb.getRdbStore(this.context, {
                name: DB_NAME,
                securityLevel: rdb.SecurityLevel.S1
            }, function (err, data) {
                rdbStore = data;
                rdbStore.executeSql(DDL_TBL_CREATE, [], function (err) {
                    console.log('DataShareExtAbility onCreate, executeSql done err:' + JSON.stringify(err));
               });
               if (callback) {
                    callback();
               }
           });
       }

   	// 重写query接口
       query(uri, predicates, columns, callback) {
           if (predicates == null || predicates == undefined) {
               console.info('invalid predicates');
           }
           try {
               rdbStore.query(TBL_NAME, predicates, columns, function (err, resultSet) {
                   if (resultSet != undefined) {
                       console.info('resultSet.rowCount: ' + resultSet.rowCount);
                   }
                   if (callback != undefined) {
                       callback(err, resultSet);
                   }
               });
           } catch (err) {
               console.error('error' + err);
           }
       }
       // 可根据应用需求，选择性重写各个接口
       // ...
   };
   ```

7. 在module.json5中定义DataShareExtensionAbility。

   | Json重要字段 | 备注说明                                                     | 必填 |
   | ------------ | ------------------------------------------------------------ | --- |
   | "name"       | Ability名称，对应Ability派生的ExtensionAbility类名。         | 是 |
   | "type"       | Ability类型，DataShare对应的Ability类型为”dataShare“，表示基于datashare模板开发的。 | 是 |
   | "uri"        | 通信使用的URI，是客户端链接服务端的唯一标识。                | 是 |
   | "visible"    | 对其他应用是否可见，设置为true时，才能与其他应用进行通信传输数据。 | 是 |
   | "metadata"   | 增加静默访问所需的额外配置项，包含name和resource字段。<br /> name类型固定为"ohos.extension.dataShare"，是配置的唯一标识。 <br /> resource类型固定为"$profile:data_share_config"，表示配置文件的名称为data_share_config.json. | 若Ability启动模式为"singleton"，则metadata必填，Ability启动模式可见[abilities对象的内部结构-launchType](../quick-start/module-structure.md#abilities对象的内部结构)；其他情况下选填。 |

   **module.json5配置样例**

   ```json
   "extensionAbilities": [
     {
       "srcEntrance": "./ets/DataShareExtAbility/DataShareExtAbility.ts",
       "name": "DataShareExtAbility",
       "icon": "$media:icon",
       "description": "$string:description_datashareextability",
       "type": "dataShare",
       "uri": "datashare://com.samples.datasharetest.DataShare",
       "visible": true,
       "metadata": [{"name": "ohos.extension.dataShare", "resource": "$profile:data_share_config"}]
     }
   ]
   ```

   **data_share_config.json说明**

   | 字段 | 备注说明                                                     | 必填 |
   | ------------ | ------------------------------------------------------------ | --- |
   | "tableConfig"       | 配置标签。 | 是 |
   | "uri"               | 指定配置生效的范围，uri支持以下三种格式，优先级为**表配置>库配置>\***，如果同时配置，高优先级会覆盖低优先级 。<br /> 1. "*" : 所有的数据库和表。<br /> 2. "datashare:///{bundleName}/{moduleName}/{storeName}" : 指定数据库。<br /> 3. "datashare:///{bundleName}/{moduleName}/{storeName}/{tableName}" : 指定表。 | 是 |
   | "crossUserMode"     | 标识数据是否为多用户共享，配置为1则多用户数据共享，配置为2则多用户数据隔离。                | 若Ability启动模式为"singleton"，则metadata必填，Ability启动模式可见[abilities对象的内部结构-launchType](../quick-start/module-structure.md#abilities对象的内部结构)；其他情况下不填。 |
   | "writePermission"   | 静默访问需要的写权限。 | 否 |
   | "readPermission"    | 静默访问需要的读权限。 | 否 |

   **data_share_config.json配置样例**

   ```json
   "tableConfig": [
    {
      "uri": "*",
      "writePermission": "ohos.permission.xxx"
    },
    {
      "uri": "datashare:///com.acts.datasharetest/entry/DB00",
      "crossUserMode": 1,
      "writePermission": "ohos.permission.xxx",
      "readPermission": "ohos.permission.xxx"
    },
    {
      "uri": "datashare:///com.acts.datasharetest/entry/DB00/TBL00",
      "crossUserMode": 2
    }
   ]
   ```

### 数据访问方应用的开发

1. 导入基础依赖包。

   ```ts
   import UIAbility from '@ohos.app.ability.UIAbility';
   import dataShare from '@ohos.data.dataShare';
   import dataSharePredicates from '@ohos.data.dataSharePredicates';
   ```

2. 定义与数据提供方通信的URI字符串。

   ```ts
   // 作为参数传递的URI，与module.json5中定义的URI的区别是多了一个"/"，是因为作为参数传递的URI中，在第二个与第三个"/"中间，存在一个DeviceID的参数
   let dseUri = ('datashare:///com.samples.datasharetest.DataShare');
   ```

3. 创建工具接口类对象。

   ```ts
   let dsHelper;
   let abilityContext;

   export default class EntryAbility extends UIAbility {
   	onWindowStageCreate(windowStage) {
   		abilityContext = this.context;
   		dataShare.createDataShareHelper(abilityContext, dseUri, (err, data)=>{
   			dsHelper = data;
   		});
   	}
   }
   ```

4. 获取到接口类对象后，便可利用其提供的接口访问提供方提供的服务，如进行数据的增删改查等。

   ```ts
   // 构建一条数据
   let valuesBucket = { "name": "ZhangSan", "age": 21, "isStudent": false, "Binary": new Uint8Array([1, 2, 3]) };
   let updateBucket = { "name": "LiSi", "age": 18, "isStudent": true, "Binary": new Uint8Array([1, 2, 3]) };
   let predicates = new dataSharePredicates.DataSharePredicates();
   let valArray = ['*'];
   // 插入一条数据
   dsHelper.insert(dseUri, valuesBucket, (err, data) => {
     console.log('dsHelper insert result: ' + data);
   });
   // 更新数据
   dsHelper.update(dseUri, predicates, updateBucket, (err, data) => {
     console.log('dsHelper update result: ' + data);
   });
   // 查询数据
   dsHelper.query(dseUri, predicates, valArray, (err, data) => {
     console.log('dsHelper query result: ' + data);
   });
   // 删除指定的数据
   dsHelper.delete(dseUri, predicates, (err, data) => {
     console.log('dsHelper delete result: ' + data);
   });
   ```
## 限制

为了降低DataShareExtensionAbility能力被三方应用滥用的风险，在DataShareExtensionAbility中限制以下接口的调用
- ./application/UIAbilityContext
- @ohos.ability.featureAbility.d.ts
- @ohos.ability.particleAbility.d.ts
- @ohos.account.osAccount.d.ts
- @ohos.backgroundTaskManager.d.ts
- @ohos.bluetooth.d.ts
- @ohos.bluetoothManager.d.ts
- @ohos.connectedTag.d.ts
- @ohos.continuation.continuationManage.d.ts
- @ohos.mutilmedia.audio.d.ts
- @ohos.multimedia.carema.d.ts
- @ohos.nfc.cardEmulation.d.ts
- @ohos.nfc.controller.d.ts
- @ohos.nfc.tag.d.ts
- @ohos.request.d.ts
- @ohos.resourceschedule.backgroundTaskManager.d.ts
- @ohos.telephony.call.d.ts
- @ohos.telephony.data.d.ts
- @ohos.telephony.observer.d.ts
- @ohos.telephony.radio.d.ts
- @ohos.telephony.sim.d.ts
- @ohos.telephony.sms.d.ts
- @ohos.vibrator.d.ts
- @ohos.wallpaper.d.ts
- @ohos.wifi.d.ts
- @ohos.wifiext.d.ts
- @ohos.wifiManager.d.ts
- @ohos.wifiManagerExt.d.ts
- @ohos.window.d.ts

## 相关示例

针对DataShareExtensionAbility开发，有以下相关示例可供参考：

[DataShareExtensionAbility：跨应用数据共享（ArkTS）（API9）（Full SDK）](https://gitee.com/openharmony/applications_app_samples/tree/master/data/CrossAppDataShare)

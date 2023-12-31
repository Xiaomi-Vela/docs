 # @ohos.data.distributedKVStore (分布式键值数据库)

分布式键值数据库为应用程序提供不同设备间数据库的分布式协同能力。通过调用分布式键值数据库各个接口，应用程序可将数据保存到分布式键值数据库中，并可对分布式键值数据库中的数据进行增加、删除、修改、查询、同步等操作。

该模块提供以下分布式键值数据库相关的常用功能：

- [KVManager](#kvmanager)：分布式键值数据库管理实例，用于获取数据库的相关信息。
- [KVStoreResultSet](#kvstoreresultset)：提供获取数据库结果集的相关方法，包括查询和移动数据读取位置等。
- [Query](#query)：使用谓词表示数据库查询，提供创建Query实例、查询数据库中的数据和添加谓词的方法。
- [SingleKVStore](#singlekvstore)：单版本分布式键值数据库，不对数据所属设备进行区分，提供查询数据和同步数据的方法。
- [DeviceKVStore](#devicekvstore)：设备协同数据库，继承自[SingleKVStore](#singlekvstore)，以设备维度对数据进行区分，提供查询数据和同步数据的方法。

> **说明：** 
>
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import distributedKVStore from '@ohos.data.distributedKVStore';
```

## KVManagerConfig

提供KVManager实例的配置信息，包括调用方的包名和应用的上下文。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

| 名称     | 类型              | 必填 | 说明                                                         |
| ---------- | --------------------- | ---- | ------------------------------------------------------------ |
| context    | Context               | 是   |应用的上下文。 <br>FA模型的应用Context定义见[Context](js-apis-inner-app-context.md)。<br>Stage模型的应用Context定义见[Context](js-apis-inner-application-uiAbilityContext.md)。<br>从API version 10开始，context的参数类型为[BaseContext](js-apis-inner-application-baseContext.md)。 |
| bundleName | string                | 是   | 调用方的包名。                                               |

## Constants

分布式键值数据库常量。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

| 名称                  | 值      | 说明                                    |
| --------------------- | ------- | --------------------------------------- |
| MAX_KEY_LENGTH        | 1024    | 数据库中Key允许的最大长度，单位字节。   |
| MAX_VALUE_LENGTH      | 4194303 | 数据库中Value允许的最大长度，单位字节。 |
| MAX_KEY_LENGTH_DEVICE | 896     | 设备协同数据库中key允许的最大长度，单位字节。 |
| MAX_STORE_ID_LENGTH   | 128     | 数据库标识符允许的最大长度，单位字节。  |
| MAX_QUERY_LENGTH      | 512000  | 最大查询长度，单位字节。                |
| MAX_BATCH_SIZE        | 128     | 最大批处理操作数量。                    |

## ValueType

数据类型枚举。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

| 名称       | 说明                   |
| ---------- | ---------------------- |
| STRING     | 表示值类型为字符串。   |
| INTEGER    | 表示值类型为整数。     |
| FLOAT      | 表示值类型为浮点数。   |
| BYTE_ARRAY | 表示值类型为字节数组。 |
| BOOLEAN    | 表示值类型为布尔值。   |
| DOUBLE     | 表示值类型为双浮点数。 |

## Value

存储在数据库中的值对象。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

| 名称  | 类型   |必填  | 说明                    |
| ----- | -------   |-----|------------------------ |
| type | [ValueType](#valuetype) | 是|值类型。   |
| value | Uint8Array \| string \| number \| boolean| 是|值。   |

## Entry

存储在数据库中的键值对。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

| 名称  | 类型        | 必填 | 说明     |
| ----- | --------------- | ---- | -------- |
| key   | string          | 是   | 键值。   |
| value | [Value](#value) | 是   | 值对象。 |

## ChangeNotification

数据变更时通知的对象，包括数据插入的数据、更新的数据、删除的数据和设备ID。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

| 名称          | 类型          | 必填       | 说明                     |
| ------------- | ----------------- | ---- | ------------------------ |
| insertEntries | [Entry](#entry)[] | 是   | 数据添加记录。           |
| updateEntries | [Entry](#entry)[] | 是   | 数据更新记录。           |
| deleteEntries | [Entry](#entry)[] | 是    | 数据删除记录。           |
| deviceId      | string            | 是    | 设备ID，此处为设备UUID。 |

## SyncMode

同步模式枚举。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

| 名称      | 说明                                                 |
| --------- | ---------------------------------------------------- |
| PULL_ONLY | 表示只能从远端拉取数据到本端。                       |
| PUSH_ONLY | 表示只能从本端推送数据到远端。                       |
| PUSH_PULL | 表示从本端推送数据到远端，然后从远端拉取数据到本端。 |

## SubscribeType

订阅类型枚举。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

| 名称                  | 说明                         |
| --------------------- | ---------------------------- |
| SUBSCRIBE_TYPE_LOCAL  | 表示订阅本地数据变更。       |
| SUBSCRIBE_TYPE_REMOTE | 表示订阅远端数据变更。       |
| SUBSCRIBE_TYPE_ALL    | 表示订阅远端和本地数据变更。 |

## KVStoreType

分布式键值数据库类型枚举。

| 名称                 | 说明                                                         |
| -------------------- | ------------------------------------------------------------ |
| DEVICE_COLLABORATION | 表示多设备协同数据库。<br> **数据库特点：** 数据以设备的维度管理，不存在冲突；支持按照设备的维度查询数据。<br>**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore |
| SINGLE_VERSION       | 表示单版本数据库。<br> **数据库特点：** 数据不分设备，设备之间修改相同的key会覆盖。 <br>**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core |

## SecurityLevel

数据库的安全级别枚举。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

| 名称        | 说明                                                         |
| -------:   | ------------------------------------------------------------ |
| S1         | 表示数据库的安全级别为低级别，数据的泄露、篡改、破坏、销毁可能会给个人或组织导致有限的不利影响。<br>例如，性别、国籍，用户申请记录等。 |
| S2         | 表示数据库的安全级别为中级别，数据的泄露、篡改、破坏、销毁可能会给个人或组织导致严重的不利影响。<br>例如，个人详细通信地址，姓名昵称等。 |
| S3         | 表示数据库的安全级别为高级别，数据的泄露、篡改、破坏、销毁可能会给个人或组织导致严峻的不利影响。<br>例如，个人实时精确定位信息、运动轨迹等。 |
| S4         | 表示数据库的安全级别为关键级别，业界法律法规中定义的特殊数据类型，涉及个人的最私密领域的信息或者一旦泄露、篡改、破坏、销毁可能会给个人或组织造成重大的不利影响数据。<br>例如，政治观点、宗教、和哲学信仰、工会成员资格、基因数据、生物信息、健康和性生活状况、性取向等或设备认证鉴权、个人的信用卡等财务信息。 |

## Options

用于提供创建数据库的配置信息。

| 名称          | 类型                        | 必填 | 说明                                                         |
| --------------- | -------------- | ---- | -------------------------|
| createIfMissing | boolean                         | 否  | 当数据库文件不存在时是否创建数据库，默认为true，即创建。<br>**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core |
| encrypt         | boolean                         | 否   | 设置数据库文件是否加密，默认为false，即不加密。<br>**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core |
| backup          | boolean                         | 否   | 设置数据库文件是否备份，默认为true，即备份。 <br>**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core |
| autoSync        | boolean                         | 否   | 设置数据库文件是否自动同步。默认为false，即手动同步。<br>**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core<br>**需要权限**： ohos.permission.DISTRIBUTED_DATASYNC |
| kvStoreType     | [KVStoreType](#kvstoretype)     | 否   | 设置要创建的数据库类型，默认为DEVICE_COLLABORATION，即多设备协同数据库。<br>**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core |
| securityLevel   | [SecurityLevel](#securitylevel) | 是   | 设置数据库安全级别。<br>**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core |
| schema          | [Schema](#schema)               | 否   | 设置定义存储在数据库中的值，默认为undefined，即不使用Schema。<br>**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore |

## Schema

表示数据库模式，可以在创建或打开数据库时创建Schema对象并将它们放入[Options](#options)中。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

| 名称    | 类型                    | 可读 | 可写 | 说明                       |
| ------- | ----------------------- | ---- | ---- | -------------------------- |
| root    | [FieldNode](#fieldnode) | 是   | 是   | 表示json根对象。           |
| indexes | Array\<string>          | 是   | 是   | 表示json类型的字符串数组。 |
| mode    | number                  | 是   | 是   | 表示Schema的模式。         |
| skip    | number                  | 是   | 是   | Schema的跳跃大小。         |

### constructor

constructor()

用于创建Schema实例的构造函数。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

## FieldNode

表示 Schema 实例的节点，提供定义存储在数据库中的值的方法。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

| 名称     | 类型    | 可读 | 可写 | 说明                           |
| -------- | ------- | ---- | ---- | ------------------------------ |
| nullable | boolean | 是   | 是   | 表示数据库字段是否可以为空。   |
| default  | string  | 是   | 是   | 表示Fieldnode的默认值。        |
| type     | number  | 是   | 是   | 表示指定节点对应数据类型的值。 |

### constructor

constructor(name: string)

用于创建带有string字段FieldNode实例的构造函数。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**参数：**

| 参数名 | 类型 | 必填 | 说明            |
| ------ | -------- | ---- | --------------- |
| name   | string   | 是   | FieldNode的值。 |

### appendChild

appendChild(child: FieldNode): boolean

在当前 FieldNode 中添加一个子节点。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**参数：**

| 参数名 | 类型                | 必填 | 说明             |
| ------ | ----------------------- | ---- | ---------------- |
| child  | [FieldNode](#fieldnode) | 是   | 要附加的域节点。 |

**返回值：**

| 类型    | 说明                                                         |
| ------- | ------------------------------------------------------------ |
| boolean | 返回true表示子节点成功添加到FieldNode；返回false则表示操作失败。 |

**示例：**

```ts

try {
  let node: distributedKVStore.FieldNode | null = new distributedKVStore.FieldNode("root");
  let child1: distributedKVStore.FieldNode | null = new distributedKVStore.FieldNode("child1");
  let child2: distributedKVStore.FieldNode | null = new distributedKVStore.FieldNode("child2");
  let child3: distributedKVStore.FieldNode | null = new distributedKVStore.FieldNode("child3");
  node.appendChild(child1);
  node.appendChild(child2);
  node.appendChild(child3);
  console.info("appendNode " + JSON.stringify(node));
  child1 = null;
  child2 = null;
  child3 = null;
  node = null;
} catch (e) {
  console.error("AppendChild " + e);
}
```

## distributedKVStore.createKVManager

createKVManager(config: KVManagerConfig): KVManager

创建一个KVManager对象实例，用于管理数据库对象。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型                      | 必填 | 说明                                                      |
| ------ | ----------------------------- | ---- | --------------------------------------------------------- |
| config | [KVManagerConfig](#kvmanagerconfig) | 是   | 提供KVManager实例的配置信息，包括调用方的包名和用户信息。 |

**返回值：**

| 类型                                   | 说明                                       |
| -------------------------------------- | ------------------------------------------ |
| [KVManager](#kvmanager) | 返回创建的KVManager对象实例。 |

**示例：**

Stage模型下的示例：

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import { BusinessError } from '@ohos.base';

let kvManager: distributedKVStore.KVManager;

export default class EntryAbility extends UIAbility {
  onCreate() {
    console.info("MyAbilityStage onCreate")
    let context = this.context
    const kvManagerConfig: distributedKVStore.KVManagerConfig = {
      context: context,
      bundleName: 'com.example.datamanagertest',
    }
    try {
      kvManager = distributedKVStore.createKVManager(kvManagerConfig);
      console.info("Succeeded in creating KVManager");
    } catch (e) {
      let error = e as BusinessError;
      console.error(`Failed to create KVManager.code is ${error.code},message is ${error.message}`);
    }
  }
}
```

FA模型下的示例：

```ts
import featureAbility from '@ohos.ability.featureAbility';
import { BusinessError } from '@ohos.base';

let kvManager: distributedKVStore.KVManager;
let context = featureAbility.getContext()
const kvManagerConfig: distributedKVStore.KVManagerConfig = {
  context: context,
  bundleName: 'com.example.datamanagertest',
}
try {
  kvManager = distributedKVStore.createKVManager(kvManagerConfig);
  console.info("Succeeded in creating KVManager");
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to create KVManager.code is ${error.code},message is ${error.message}`);
}
```

## KVManager

分布式键值数据库管理实例，用于获取分布式键值数据库的相关信息。在调用KVManager的方法前，需要先通过[createKVManager](#distributedkvstorecreatekvmanager)构建一个KVManager实例。

### getKVStore

getKVStore&lt;T&gt;(storeId: string, options: Options, callback: AsyncCallback&lt;T&gt;): void

通过指定Options和storeId，创建并获取分布式键值数据库，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型               | 必填 | 说明                                                         |
| -------- | ---------------------- | ---- | ------------------------------------------------------------ |
| storeId  | string                 | 是   | 数据库唯一标识符，长度不大于[MAX_STORE_ID_LENGTH](#constants)。 |
| options  | [Options](#options)    | 是   | 创建分布式键值实例的配置信息。                               |
| callback | AsyncCallback&lt;T&gt; | 是   | 回调函数。返回创建的分布式键值数据库实例（根据kvStoreType的不同，可以创建SingleKVStore实例和DeviceKVStore实例）。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                                |
| ------------ | ------------------------------------------- |
| 15100002     | Open existed database with changed options. |
| 15100003     | Database corrupted.                         |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let kvStore: distributedKVStore.SingleKVStore | null;
try {
  const options: distributedKVStore.Options = {
    createIfMissing: true,
    encrypt: false,
    backup: false,
    autoSync: true,
    kvStoreType: distributedKVStore.KVStoreType.SINGLE_VERSION,
    securityLevel: distributedKVStore.SecurityLevel.S2,
  };
  kvManager.getKVStore('storeId', options, (err, store: distributedKVStore.SingleKVStore) => {
    if (err) {
      console.error(`Failed to get KVStore.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info("Succeeded in getting KVStore");
    kvStore = store;
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### getKVStore

getKVStore&lt;T&gt;(storeId: string, options: Options): Promise&lt;T&gt;

通过指定Options和storeId，创建并获取分布式键值数据库，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名  | 类型            | 必填 | 说明                                                         |
| ------- | ------------------- | ---- | ------------------------------------------------------------ |
| storeId | string              | 是   | 数据库唯一标识符，长度不大于[MAX_STORE_ID_LENGTH](#constants)。 |
| options | [Options](#options) | 是   | 创建分布式键值实例的配置信息。                               |

**返回值：**

| 类型             | 说明                                                         |
| ---------------- | ------------------------------------------------------------ |
| Promise&lt;T&gt; | Promise对象。返回创建的分布式键值数据库实例（根据kvStoreType的不同，可以创建SingleKVStore实例和DeviceKVStore实例。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                                |
| ------------ | ------------------------------------------- |
| 15100002     | Open existed database with changed options. |
| 15100003     | Database corrupted.                         |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let kvStore: distributedKVStore.SingleKVStore | null;
try {
  const options: distributedKVStore.Options = {
    createIfMissing: true,
    encrypt: false,
    backup: false,
    autoSync: true,
    kvStoreType: distributedKVStore.KVStoreType.SINGLE_VERSION,
    securityLevel: distributedKVStore.SecurityLevel.S2,
  };
  kvManager.getKVStore<distributedKVStore.SingleKVStore>('storeId', options).then((store: distributedKVStore.SingleKVStore) => {
    console.info("Succeeded in getting KVStore");
    kvStore = store;
  }).catch((err: BusinessError) => {
    console.error(`Failed to get KVStore.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### closeKVStore

closeKVStore(appId: string, storeId: string, callback: AsyncCallback&lt;void&gt;): void

通过storeId的值关闭指定的分布式键值数据库，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                  | 必填 | 说明                                                         |
| -------- | ------------------------- | ---- | ------------------------------------------------------------ |
| appId    | string                    | 是   | 所调用数据库方的包名。                                       |
| storeId  | string                    | 是   | 要关闭的数据库唯一标识符，长度不大于[MAX_STORE_ID_LENGTH](#constants)。 |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。                                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let kvStore: distributedKVStore.SingleKVStore | null;
const options: distributedKVStore.Options = {
  createIfMissing: true,
  encrypt: false,
  backup: false,
  autoSync: true,
  kvStoreType: distributedKVStore.KVStoreType.SINGLE_VERSION,
  schema: undefined,
  securityLevel: distributedKVStore.SecurityLevel.S2,
}
try {
  kvManager.getKVStore('storeId', options, async (err, store: distributedKVStore.SingleKVStore | null) => {
    if (err != undefined) {
      console.error(`Failed to get KVStore.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in getting KVStore');
    kvStore = store;
    kvStore = null;
    store = null;
    kvManager.closeKVStore('appId', 'storeId', (err)=> {
      if (err != undefined) {
        console.error(`Failed to close KVStore.code is ${err.code},message is ${err.message}`);
        return;
      }
      console.info('Succeeded in closing KVStore');
    });
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### closeKVStore

closeKVStore(appId: string, storeId: string): Promise&lt;void&gt;

通过storeId的值关闭指定的分布式键值数据库，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名  | 类型 | 必填 | 说明                                                         |
| ------- | -------- | ---- | ------------------------------------------------------------ |
| appId   | string   | 是   | 所调用数据库方的包名。                                       |
| storeId | string   | 是   | 要关闭的数据库唯一标识符，长度不大于[MAX_STORE_ID_LENGTH](#constants)。 |

**返回值：**

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let kvStore: distributedKVStore.SingleKVStore | null;

const options: distributedKVStore.Options = {
  createIfMissing: true,
  encrypt: false,
  backup: false,
  autoSync: true,
  kvStoreType: distributedKVStore.KVStoreType.SINGLE_VERSION,
  schema: undefined,
  securityLevel: distributedKVStore.SecurityLevel.S2,
}
try {
  kvManager.getKVStore<distributedKVStore.SingleKVStore>('storeId', options).then(async (store: distributedKVStore.SingleKVStore | null) => {
    console.info('Succeeded in getting KVStore');
    kvStore = store;
    kvStore = null;
    store = null;
    kvManager.closeKVStore('appId', 'storeId').then(() => {
      console.info('Succeeded in closing KVStore');
    }).catch((err: BusinessError) => {
      console.error(`Failed to close KVStore.code is ${err.code},message is ${err.message}`);
    });
  }).catch((err: BusinessError) => {
    console.error(`Failed to get KVStore.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to close KVStore.code is ${error.code},message is ${error.message}`);
}
```

### deleteKVStore

deleteKVStore(appId: string, storeId: string, callback: AsyncCallback&lt;void&gt;): void

通过storeId的值删除指定的分布式键值数据库，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                  | 必填 | 说明                                                         |
| -------- | ------------------------- | ---- | ------------------------------------------------------------ |
| appId    | string                    | 是   | 所调用数据库方的包名。                                       |
| storeId  | string                    | 是   | 要删除的数据库唯一标识符，长度不大于[MAX_STORE_ID_LENGTH](#constants)。 |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。                                                   |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息** |
| ------------ | ------------ |
| 15100004     | Not found.   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let kvStore: distributedKVStore.SingleKVStore | null;

const options: distributedKVStore.Options = {
  createIfMissing: true,
  encrypt: false,
  backup: false,
  autoSync: true,
  kvStoreType: distributedKVStore.KVStoreType.SINGLE_VERSION,
  schema: undefined,
  securityLevel: distributedKVStore.SecurityLevel.S2,
}
try {
  kvManager.getKVStore('store', options, async (err, store: distributedKVStore.SingleKVStore | null) => {
    if (err != undefined) {
      console.error(`Failed to get KVStore.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in getting KVStore');
    kvStore = store;
    kvStore = null;
    store = null;
    kvManager.deleteKVStore('appId', 'storeId', (err) => {
      if (err != undefined) {
        console.error(`Failed to delete KVStore.code is ${err.code},message is ${err.message}`);
        return;
      }
      console.info(`Succeeded in deleting KVStore`);
    });
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to delete KVStore.code is ${error.code},message is ${error.message}`);
}
```

### deleteKVStore

deleteKVStore(appId: string, storeId: string): Promise&lt;void&gt;

通过storeId的值删除指定的分布式键值数据库，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名  | 类型 | 必填 | 说明                                                         |
| ------- | -------- | ---- | ------------------------------------------------------------ |
| appId   | string   | 是   | 所调用数据库方的包名。                                       |
| storeId | string   | 是   | 要删除的数据库唯一标识符，长度不大于[MAX_STORE_ID_LENGTH](#constants)。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息** |
| ------------ | ------------ |
| 15100004     | Not found.   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let kvStore: distributedKVStore.SingleKVStore | null;

const options: distributedKVStore.Options = {
  createIfMissing: true,
  encrypt: false,
  backup: false,
  autoSync: true,
  kvStoreType: distributedKVStore.KVStoreType.SINGLE_VERSION,
  schema: undefined,
  securityLevel: distributedKVStore.SecurityLevel.S2,
}
try {
  kvManager.getKVStore<distributedKVStore.SingleKVStore>('storeId', options).then(async (store: distributedKVStore.SingleKVStore | null) => {
    console.info('Succeeded in getting KVStore');
    kvStore = store;
    kvStore = null;
    store = null;
    kvManager.deleteKVStore('appId', 'storeId').then(() => {
      console.info('Succeeded in deleting KVStore');
    }).catch((err: BusinessError) => {
      console.error(`Failed to delete KVStore.code is ${err.code},message is ${err.message}`);
    });
  }).catch((err: BusinessError) => {
    console.error(`Failed to get KVStore.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to delete KVStore.code is ${error.code},message is ${error.message}`);
}
```

### getAllKVStoreId

getAllKVStoreId(appId: string, callback: AsyncCallback&lt;string[]&gt;): void

获取所有通过[getKVStore](#getkvstore)方法创建的且没有调用[deleteKVStore](#deletekvstore)方法删除的分布式键值数据库的storeId，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明                                                |
| -------- | ----------------------------- | ---- | --------------------------------------------------- |
| appId    | string                        | 是   | 所调用数据库方的包名。                              |
| callback | AsyncCallback&lt;string[]&gt; | 是   | 回调函数。返回所有创建的分布式键值数据库的storeId。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  kvManager.getAllKVStoreId('appId', (err, data) => {
    if (err != undefined) {
      console.error(`Failed to get AllKVStoreId.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in getting AllKVStoreId');
    console.info(`GetAllKVStoreId size = ${data.length}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to get AllKVStoreId.code is ${error.code},message is ${error.message}`);
}
```

### getAllKVStoreId

getAllKVStoreId(appId: string): Promise&lt;string[]&gt;

获取所有通过[getKVStore](#getkvstore)方法创建的且没有调用[deleteKVStore](#deletekvstore)方法删除的分布式键值数据库的storeId，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明                   |
| ------ | -------- | ---- | ---------------------- |
| appId  | string   | 是   | 所调用数据库方的包名。 |

**返回值：**

| 类型                    | 说明                                                   |
| ----------------------- | ------------------------------------------------------ |
| Promise&lt;string[]&gt; | Promise对象。返回所有创建的分布式键值数据库的storeId。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  console.info('GetAllKVStoreId');
  kvManager.getAllKVStoreId('appId').then((data: string[]) => {
    console.info('Succeeded in getting AllKVStoreId');
    console.info(`GetAllKVStoreId size = ${data.length}`);
  }).catch((err: BusinessError) => {
    console.error(`Failed to get AllKVStoreId.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to get AllKVStoreId.code is ${error.code},message is ${error.message}`);
}
```

### on('distributedDataServiceDie')

on(event: 'distributedDataServiceDie', deathCallback: Callback&lt;void&gt;): void

订阅服务状态变更通知。如果服务终止，需要重新注册数据变更通知和同步完成事件回调通知，并且同步操作会返回失败。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**参数：**

| 参数名        | 类型             | 必填 | 说明                                                         |
| ------------- | -------------------- | ---- | ------------------------------------------------------------ |
| event         | string               | 是   | 订阅的事件名，固定为'distributedDataServiceDie'，即服务状态变更事件。 |
| deathCallback | Callback&lt;void&gt; | 是   | 回调函数。                                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  console.info('KVManagerOn');
  const deathCallback = () => {
    console.info('death callback call');
  }
  kvManager.on('distributedDataServiceDie', deathCallback);
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### off('distributedDataServiceDie')

off(event: 'distributedDataServiceDie', deathCallback?: Callback&lt;void&gt;): void

取消订阅服务状态变更通知。参数中的deathCallback必须是已经订阅过的deathCallback，否则会取消订阅失败。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**参数：**

| 参数名        | 类型             | 必填 | 说明                                                         |
| ------------- | -------------------- | ---- | ------------------------------------------------------------ |
| event         | string               | 是   | 取消订阅的事件名，固定为'distributedDataServiceDie'，即服务状态变更事件。 |
| deathCallback | Callback&lt;void&gt; | 否   | 回调函数。如果该参数不填，那么会将之前订阅过的所有的deathCallback取消订阅。                                          |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  console.info('KVManagerOff');
  const deathCallback = () => {
    console.info('death callback call');
  }
  kvManager.off('distributedDataServiceDie', deathCallback);
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

## KVStoreResultSet

提供获取数据库结果集的相关方法，包括查询和移动数据读取位置等。同时允许打开的结果集的最大数量为8个。

在调用KVStoreResultSet的方法前，需要先通过[getKVStore](#getkvstore)构建一个SingleKVStore或者DeviceKVStore实例。

### getCount

getCount(): number

获取结果集中的总行数。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**返回值：**

| 类型   | 说明               |
| ------ | ------------------ |
| number | 返回数据的总行数。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let count: number;
  kvStore.getResultSet('batch_test_string_key').then((result) => {
    console.info('getResultSet succeed.');
    resultSet = result;
    count = resultSet.getCount();
    console.info("getCount succeed:" + count);
  }).catch((err: BusinessError) => {
    console.error('getResultSet failed: ' + err);
  });
} catch (e) {
  console.error("getCount failed: " + e);
}
```

### getPosition

getPosition(): number

获取结果集中当前的读取位置。读取位置会因[moveToFirst](#movetofirst)、[moveToLast](#movetolast)等操作而发生变化。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**返回值：**

| 类型   | 说明               |
| ------ | ------------------ |
| number | 返回当前读取位置。取值范围>= -1，值为 -1 时表示还未开始读取，值为 0 时表示第一行。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let position: number;
  kvStore.getResultSet('batch_test_string_key').then((result) => {
    console.info('getResultSet succeeded.');
    resultSet = result;
    position = resultSet.getPosition();
    console.info("getPosition succeed:" + position);
  }).catch((err: BusinessError) => {
    console.error('getResultSet failed: ' + err);
  });
} catch (e) {
  console.error("getPosition failed: " + e);
}
```

### moveToFirst

moveToFirst(): boolean

将读取位置移动到第一行。如果结果集为空，则返回false。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**返回值：**

| 类型    | 说明                                            |
| ------- | ----------------------------------------------- |
| boolean | 返回true表示操作成功；返回false则表示操作失败。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let moved: boolean;
  kvStore.getResultSet('batch_test_string_key').then((result) => {
    console.info('getResultSet succeed.');
    resultSet = result;
    moved = resultSet.moveToFirst();
    console.info("moveToFirst succeed: " + moved);
  }).catch((err: BusinessError) => {
    console.error('getResultSet failed: ' + err);
  });
} catch (e) {
  console.error("moveToFirst failed " + e);
}
```

### moveToLast

moveToLast(): boolean

将读取位置移动到最后一行。如果结果集为空，则返回false。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**返回值：**

| 类型    | 说明                                            |
| ------- | ----------------------------------------------- |
| boolean | 返回true表示操作成功；返回false则表示操作失败。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let moved: boolean;
  kvStore.getResultSet('batch_test_string_key').then((result) => {
    console.info('getResultSet succeed.');
    resultSet = result;
    moved = resultSet.moveToLast();
    console.info("moveToLast succeed:" + moved);
  }).catch((err: BusinessError) => {
    console.error('getResultSet failed: ' + err);
  });
} catch (e) {
  console.error("moveToLast failed: " + e);
}
```

### moveToNext

moveToNext(): boolean

将读取位置移动到下一行。如果结果集为空，则返回false。适用于全量获取数据库结果集的场景。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**返回值：**

| 类型    | 说明                                            |
| ------- | ----------------------------------------------- |
| boolean | 返回true表示操作成功；返回false则表示操作失败。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let moved: boolean;
  kvStore.getResultSet('batch_test_string_key').then((result) => {
    console.info('getResultSet succeed.');
    resultSet = result;
    do {
      moved = resultSet.moveToNext();
      console.info("moveToNext succeed: " + moved);
    } while (moved)
  }).catch((err: BusinessError) => {
    console.error('getResultSet failed: ' + err);
  });
} catch (e) {
  console.error("moveToNext failed: " + e);
}
```

### moveToPrevious

moveToPrevious(): boolean

将读取位置移动到上一行。如果结果集为空，则返回false。适用于全量获取数据库结果集的场景。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**返回值：**

| 类型    | 说明                                            |
| ------- | ----------------------------------------------- |
| boolean | 返回true表示操作成功；返回false则表示操作失败。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let moved: boolean;
  kvStore.getResultSet('batch_test_string_key').then((result) => {
    console.info('getResultSet succeed.');
    resultSet = result;
    moved = resultSet.moveToLast();
    moved = resultSet.moveToPrevious();
    console.info("moveToPrevious succeed:" + moved);
  }).catch((err: BusinessError) => {
    console.error('getResultSet failed: ' + err);
  });
} catch (e) {
  console.error("moveToPrevious failed: " + e);
}
```

### move

move(offset: number): boolean

将读取位置移动到当前位置的相对偏移量。即当前游标位置向下偏移 offset 行。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明                                                         |
| ------ | -------- | ---- | ------------------------------------------------------------ |
| offset | number   | 是   | 表示与当前位置的相对偏移量，负偏移表示向后移动，正偏移表示向前移动。 |

**返回值：**

| 类型    | 说明                                            |
| ------- | ----------------------------------------------- |
| boolean | 返回true表示操作成功；返回false则表示操作失败。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let moved: boolean;
  kvStore.getResultSet('batch_test_string_key').then((result) => {
    console.info('Succeeded in getting resultSet');
    resultSet = result;
    moved = resultSet.move(2); //若当前位置为0，将读取位置从绝对位置为0的位置移动2行，即移动到绝对位置为2，行数为3的位置
    console.info(`Succeeded in moving.moved = ${moved}`);
  }).catch((err: BusinessError) => {
    console.error(`Failed to get resultSet.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to move.code is ${error.code},message is ${error.message}`);
}
```

### moveToPosition

moveToPosition(position: number): boolean

将读取位置从 0 移动到绝对位置。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型 | 必填 | 说明           |
| -------- | -------- | ---- | -------------- |
| position | number   | 是   | 表示绝对位置。 |

**返回值：**

| 类型    | 说明                                            |
| ------- | ----------------------------------------------- |
| boolean | 返回true表示操作成功；返回false则表示操作失败。 |

**示例**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let moved: boolean;
  kvStore.getResultSet('batch_test_string_key').then((result) => {
    console.info('Succeeded in getting resultSet');
    resultSet = result;
    moved = resultSet.moveToPosition(1);
    console.info(`Succeeded in moving to position.moved=${moved}`);
  }).catch((err: BusinessError) => {
    console.error(`Failed to get resultSet.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to move to position.code is ${error.code},message is ${error.message}`);
}
```

### isFirst

isFirst(): boolean

检查读取位置是否为第一行。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**返回值：**

| 类型    | 说明                                                         |
| ------- | ------------------------------------------------------------ |
| boolean | 返回true表示读取位置为第一行；返回false表示读取位置不是第一行。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let isfirst: boolean;
  kvStore.getResultSet('batch_test_string_key').then((result) => {
    console.info('getResultSet succeed.');
    resultSet = result;
    isfirst = resultSet.isFirst();
    console.info("Check isFirst succeed:" + isfirst);
  }).catch((err: BusinessError) => {
    console.error('getResultSet failed: ' + err);
  });
} catch (e) {
  console.error("Check isFirst failed: " + e);
}
```

### isLast

isLast(): boolean

检查读取位置是否为最后一行。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**返回值：**

| 类型    | 说明                                                         |
| ------- | ------------------------------------------------------------ |
| boolean | 返回true表示读取位置为最后一行；返回false表示读取位置不是最后一行。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let islast: boolean;
  kvStore.getResultSet('batch_test_string_key').then((result) => {
    console.info('getResultSet succeed.');
    resultSet = result;
    islast = resultSet.isLast();
    console.info("Check isLast succeed: " + islast);
  }).catch((err: BusinessError) => {
    console.error('getResultSet failed: ' + err);
  });
} catch (e) {
  console.error("Check isLast failed: " + e);
}
```

### isBeforeFirst

isBeforeFirst(): boolean

检查读取位置是否在第一行之前。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**返回值：**

| 类型    | 说明                                                         |
| ------- | ------------------------------------------------------------ |
| boolean | 返回true表示读取位置在第一行之前；返回false表示读取位置不在第一行之前。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  kvStore.getResultSet('batch_test_string_key').then((result) => {
    console.info('getResultSet succeed.');
    resultSet = result;
    let isbeforefirst = resultSet.isBeforeFirst();
    console.info("Check isBeforeFirst succeed: " + isbeforefirst);
  }).catch((err: BusinessError) => {
    console.error('getResultSet failed: ' + err);
  });
} catch (e) {
  console.error("Check isBeforeFirst failed: " + e);
}
```

### isAfterLast

isAfterLast(): boolean

检查读取位置是否在最后一行之后。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**返回值：**

| 类型    | 说明                                                         |
| ------- | ------------------------------------------------------------ |
| boolean | 返回true表示读取位置在最后一行之后；返回false表示读取位置不在最后一行之后。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  kvStore.getResultSet('batch_test_string_key').then((result) => {
    console.info('getResultSet succeed.');
    resultSet = result;
    let isafterlast = resultSet.isAfterLast();
    console.info("Check isAfterLast succeed:" + isafterlast);
  }).catch((err: BusinessError) => {
    console.error('getResultSet failed: ' + err);
  });
} catch (e) {
  console.error("Check isAfterLast failed: " + e);
}
```

### getEntry

getEntry(): Entry

从当前位置获取对应的键值对。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**返回值：**

| 类型            | 说明         |
| --------------- | ------------ |
| [Entry](#entry) | 返回键值对。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  kvStore.getResultSet('batch_test_string_key').then((result) => {
    console.info('getResultSet succeed.');
    resultSet = result;
    let entry = resultSet.getEntry();
    console.info("getEntry succeed:" + JSON.stringify(entry));
  }).catch((err: BusinessError) => {
    console.error('getResultSet failed: ' + err);
  });
} catch (e) {
  console.error("getEntry failed: " + e);
}
```

## Query

使用谓词表示数据库查询，提供创建Query实例、查询数据库中的数据和添加谓词的方法。一个Query对象中谓词数量上限为256个。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

### constructor

constructor()

用于创建Schema实例的构造函数。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

### reset

reset(): Query

重置Query对象。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**返回值：**

| 类型           | 说明                  |
| -------------- | --------------------- |
| [Query](#query) | 返回重置的Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let query: distributedKVStore.Query | null = new distributedKVStore.Query();
  query.equalTo("key", "value");
  console.info("query is " + query.getSqlLike());
  query.reset();
  console.info("query is " + query.getSqlLike());
  query = null;
} catch (e) {
  console.error("simply calls should be ok :" + e);
}
```

### equalTo

equalTo(field: string, value: number|string|boolean): Query

构造一个Query对象来查询具有指定字段的条目，其值等于指定的值。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名  | 类型 | 必填  | 说明                    |
| -----  | ------  | ----  | ----------------------- |
| fieId  | string  | 是    |表示指定字段，不能包含' ^ '。  |
| value  | number\|string\|boolean  | 是    | 表示指定的值。|

**返回值：**

| 类型           | 说明            |
| -------------- | --------------- |
| [Query](#query) | 返回Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let query: distributedKVStore.Query | null = new distributedKVStore.Query();
  query.equalTo("field", "value");
  console.info(`query is ${query.getSqlLike()}`);
  query = null;
} catch (e) {
  let error = e as BusinessError;
  console.error(`duplicated calls should be ok.code is ${error.code},message is ${error.message}`);
}
```

### notEqualTo

notEqualTo(field: string, value: number|string|boolean): Query

构造一个Query对象以查询具有指定字段且值不等于指定值的条目。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名  | 类型 | 必填  | 说明                    |
| -----  | ------  | ----  | ----------------------- |
| fieId  | string  | 是    |表示指定字段，不能包含' ^ '。  |
| value  | number\|string\|boolean  | 是    | 表示指定的值。|

**返回值：**

| 类型           | 说明            |
| -------------- | --------------- |
| [Query](#query) | 返回Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let query: distributedKVStore.Query | null = new distributedKVStore.Query();
  query.notEqualTo("field", "value");
  console.info(`query is ${query.getSqlLike()}`);
  query = null;
} catch (e) {
  let error = e as BusinessError;
  console.error(`duplicated calls should be ok.code is ${error.code},message is ${error.message}`);
}
```

### greaterThan

greaterThan(field: string, value: number|string|boolean): Query

构造一个Query对象以查询具有大于指定值的指定字段的条目。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**
| 参数名  | 类型 | 必填  | 说明                    |
| -----  | ------  | ----  | ----------------------- |
| fieId  | string  | 是    |表示指定字段，不能包含' ^ '。  |
| value  | number\|string\|boolean  | 是    | 表示指定的值。|

**返回值：**

| 类型           | 说明            |
| -------------- | --------------- |
| [Query](#query) | 返回Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
    let query: distributedKVStore.Query | null = new distributedKVStore.Query();
    query.greaterThan("field", "value");
    console.info(`query is ${query.getSqlLike()}`);
    query = null;
} catch (e) {
    let error = e as BusinessError;
    console.error(`duplicated calls should be ok.code is ${error.code},message is ${error.message}`);
}
```

### lessThan

lessThan(field: string, value: number|string): Query

构造一个Query对象以查询具有小于指定值的指定字段的条目。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**


| 参数名  | 类型 | 必填  | 说明                    |
| -----  | ------  | ----  | ----------------------- |
| fieId  | string  | 是    |表示指定字段，不能包含' ^ '。  |
| value  | number\|string  | 是    | 表示指定的值。|

**返回值：**

| 类型           | 说明            |
| -------------- | --------------- |
| [Query](#query) | 返回Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
    let query: distributedKVStore.Query | null = new distributedKVStore.Query();
    query.lessThan("field", "value");
    console.info(`query is ${query.getSqlLike()}`);
    query = null;
} catch (e) {
    let error = e as BusinessError;
    console.error(`duplicated calls should be ok.code is ${error.code},message is ${error.message}`);
}
```

### greaterThanOrEqualTo

greaterThanOrEqualTo(field: string, value: number|string): Query

构造一个Query对象以查询具有指定字段且值大于或等于指定值的条目。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**


| 参数名  | 类型 | 必填  | 说明                    |
| -----  | ------  | ----  | ----------------------- |
| fieId  | string  | 是    |表示指定字段，不能包含' ^ '。  |
| value  | number\|string  | 是    | 表示指定的值。|

**返回值：**

| 类型           | 说明            |
| -------------- | --------------- |
| [Query](#query) | 返回Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
    let query: distributedKVStore.Query | null = new distributedKVStore.Query();
    query.greaterThanOrEqualTo("field", "value");
    console.info(`query is ${query.getSqlLike()}`);
    query = null;
} catch (e) {
    let error = e as BusinessError;
    console.error(`duplicated calls should be ok.code is ${error.code},message is ${error.message}`);
}
```

### lessThanOrEqualTo

lessThanOrEqualTo(field: string, value: number|string): Query

构造一个Query对象以查询具有指定字段且值小于或等于指定值的条目。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**


| 参数名  | 类型 | 必填  | 说明                    |
| -----  | ------  | ----  | ----------------------- |
| fieId  | string  | 是    |表示指定字段，不能包含' ^ '。  |
| value  | number\|string  | 是    | 表示指定的值。|

**返回值：**

| 类型           | 说明            |
| -------------- | --------------- |
| [Query](#query) | 返回Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
    let query: distributedKVStore.Query | null = new distributedKVStore.Query();
    query.lessThanOrEqualTo("field", "value");
    console.info(`query is ${query.getSqlLike()}`);
    query = null;
} catch (e) {
    let error = e as BusinessError;
    console.error(`duplicated calls should be ok.code is ${error.code},message is ${error.message}`);
}
```

### isNull

isNull(field: string): Query

构造一个Query对象以查询具有值为null的指定字段的条目。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明                          |
| ------ | -------- | ---- | ----------------------------- |
| fieId  | string   | 是   | 表示指定字段，不能包含' ^ '。 |

**返回值：**

| 类型           | 说明            |
| -------------- | --------------- |
| [Query](#query) | 返回Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
    let query: distributedKVStore.Query | null = new distributedKVStore.Query();
    query.isNull("field");
    console.info(`query is ${query.getSqlLike()}`);
    query = null;
} catch (e) {
    let error = e as BusinessError;
    console.error(`duplicated calls should be ok.code is ${error.code},message is ${error.message}`);
}
```

### inNumber

inNumber(field: string, valueList: number[]): Query

构造一个Query对象以查询具有指定字段的条目，其值在指定的值列表中。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名    | 类型 | 必填 | 说明                          |
| --------- | -------- | ---- | ----------------------------- |
| fieId     | string   | 是   | 表示指定字段，不能包含' ^ '。 |
| valueList | number[] | 是   | 表示指定的值列表。            |

**返回值：**

| 类型           | 说明            |
| -------------- | --------------- |
| [Query](#query) | 返回Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
    let query: distributedKVStore.Query | null = new distributedKVStore.Query();
    query.inNumber("field", [0, 1]);
    console.info(`query is ${query.getSqlLike()}`);
    query = null;
} catch (e) {
    let error = e as BusinessError;
    console.error(`duplicated calls should be ok.code is ${error.code},message is ${error.message}`);
}
```

### inString

inString(field: string, valueList: string[]): Query

构造一个Query对象以查询具有指定字段的条目，其值在指定的字符串值列表中。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名    | 类型 | 必填 | 说明                          |
| --------- | -------- | ---- | ----------------------------- |
| fieId     | string   | 是   | 表示指定字段，不能包含' ^ '。 |
| valueList | string[] | 是   | 表示指定的字符串值列表。      |

**返回值：**

| 类型           | 说明            |
| -------------- | --------------- |
| [Query](#query) | 返回Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
    let query: distributedKVStore.Query | null = new distributedKVStore.Query();
    query.inString("field", ['test1', 'test2']);
    console.info(`query is ${query.getSqlLike()}`);
    query = null;
} catch (e) {
    let error = e as BusinessError;
    console.error(`duplicated calls should be ok.code is ${error.code},message is ${error.message}`);
}
```

### notInNumber

notInNumber(field: string, valueList: number[]): Query

构造一个Query对象以查询具有指定字段的条目，该字段的值不在指定的值列表中。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名    | 类型 | 必填 | 说明                          |
| --------- | -------- | ---- | ----------------------------- |
| fieId     | string   | 是   | 表示指定字段，不能包含' ^ '。 |
| valueList | number[] | 是   | 表示指定的值列表。            |

**返回值：**

| 类型           | 说明            |
| -------------- | --------------- |
| [Query](#query) | 返回Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
    let query: distributedKVStore.Query | null = new distributedKVStore.Query();
    query.notInNumber("field", [0, 1]);
    console.info(`query is ${query.getSqlLike()}`);
    query = null;
} catch (e) {
    let error = e as BusinessError;
    console.error(`duplicated calls should be ok.code is ${error.code},message is ${error.message}`);
}
```

### notInString

notInString(field: string, valueList: string[]): Query

构造一个Query对象以查询具有指定字段且值不在指定字符串值列表中的条目。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名    | 类型 | 必填 | 说明                          |
| --------- | -------- | ---- | ----------------------------- |
| fieId     | string   | 是   | 表示指定字段，不能包含' ^ '。 |
| valueList | string[] | 是   | 表示指定的字符串值列表。      |

**返回值：**

| 类型           | 说明            |
| -------------- | --------------- |
| [Query](#query) | 返回Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
    let query: distributedKVStore.Query | null = new distributedKVStore.Query();
    query.notInString("field", ['test1', 'test2']);
    console.info(`query is ${query.getSqlLike()}`);
    query = null;
} catch (e) {
    let error = e as BusinessError;
    console.error(`duplicated calls should be ok.code is ${error.code},message is ${error.message}`);
}
```

### like

like(field: string, value: string): Query

构造一个Query对象以查询具有与指定字符串值相似的指定字段的条目。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明                          |
| ------ | -------- | ---- | ----------------------------- |
| fieId  | string   | 是   | 表示指定字段，不能包含' ^ '。 |
| value  | string   | 是   | 表示指定的字符串值。          |

**返回值：**

| 类型           | 说明            |
| -------------- | --------------- |
| [Query](#query) | 返回Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
    let query: distributedKVStore.Query | null = new distributedKVStore.Query();
    query.like("field", "value");
    console.info(`query is ${query.getSqlLike()}`);
    query = null;
} catch (e) {
    let error = e as BusinessError;
    console.error(`duplicated calls should be ok.code is ${error.code},message is ${error.message}`);
}
```

### unlike

unlike(field: string, value: string): Query

构造一个Query对象以查询具有与指定字符串值不相似的指定字段的条目。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明                          |
| ------ | -------- | ---- | ----------------------------- |
| fieId  | string   | 是   | 表示指定字段，不能包含' ^ '。 |
| value  | string   | 是   | 表示指定的字符串值。          |

**返回值：**

| 类型           | 说明            |
| -------------- | --------------- |
| [Query](#query) | 返回Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
    let query: distributedKVStore.Query | null = new distributedKVStore.Query();
    query.unlike("field", "value");
    console.info(`query is ${query.getSqlLike()}`);
    query = null;
} catch (e) {
    let error = e as BusinessError;
    console.error(`duplicated calls should be ok.code is ${error.code},message is ${error.message}`);
}
```

### and

and(): Query

构造一个带有与条件的查询对象。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**返回值：**

| 类型           | 说明           |
| -------------- | -------------- |
| [Query](#query) | 返回查询对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
    let query: distributedKVStore.Query | null = new distributedKVStore.Query();
    query.notEqualTo("field", "value1");
    query.and();
    query.notEqualTo("field", "value2");
    console.info("query is " + query.getSqlLike());
    query = null;
} catch (e) {
    console.error("duplicated calls should be ok :" + e);
}
```

### or

or(): Query

构造一个带有或条件的Query对象。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**返回值：**

| 类型           | 说明           |
| -------------- | -------------- |
| [Query](#query) | 返回查询对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
    let query: distributedKVStore.Query | null = new distributedKVStore.Query();
    query.notEqualTo("field", "value1");
    query.or();
    query.notEqualTo("field", "value2");
    console.info("query is " + query.getSqlLike());
    query = null;
} catch (e) {
    console.error("duplicated calls should be ok :" + e);
}
```

### orderByAsc

orderByAsc(field: string): Query

构造一个Query对象，将查询结果按升序排序。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明                          |
| ------ | -------- | ---- | ----------------------------- |
| fieId  | string   | 是   | 表示指定字段，不能包含' ^ '。 |

**返回值：**

| 类型           | 说明            |
| -------------- | --------------- |
| [Query](#query) | 返回Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
    let query: distributedKVStore.Query | null = new distributedKVStore.Query();
    query.notEqualTo("field", "value");
    query.orderByAsc("field");
    console.info(`query is ${query.getSqlLike()}`);
    query = null;
} catch (e) {
    let error = e as BusinessError;
    console.error(`duplicated calls should be ok.code is ${error.code},message is ${error.message}`);
}
```

### orderByDesc

orderByDesc(field: string): Query

构造一个Query对象，将查询结果按降序排序。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明                          |
| ------ | -------- | ---- | ----------------------------- |
| fieId  | string   | 是   | 表示指定字段，不能包含' ^ '。 |

**返回值：**

| 类型           | 说明            |
| -------------- | --------------- |
| [Query](#query) | 返回Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
    let query: distributedKVStore.Query | null = new distributedKVStore.Query();
    query.notEqualTo("field", "value");
    query.orderByDesc("field");
    console.info(`query is ${query.getSqlLike()}`);
    query = null;
} catch (e) {
    let error = e as BusinessError;
    console.error(`duplicated calls should be ok.code is ${error.code},message is ${error.message}`);
}
```

### limit

limit(total: number, offset: number): Query

构造一个Query对象来指定结果的数量和开始位置。该接口必须要在Query对象查询和升降序等操作之后调用，调用limit接口后，不可再对Query对象进行查询和升降序等操作。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明               |
| ------ | -------- | ---- | ------------------ |
| total  | number   | 是   | 表示指定的结果数。 |
| offset | number   | 是   | 表示起始位置。     |

**返回值：**

| 类型           | 说明            |
| -------------- | --------------- |
| [Query](#query) | 返回Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let total = 10;
let offset = 1;
try {
  let query: distributedKVStore.Query | null = new distributedKVStore.Query();
  query.notEqualTo("field", "value");
  query.limit(total, offset);
  console.info(`query is ${query.getSqlLike()}`);
  query = null;
} catch (e) {
  let error = e as BusinessError;
  console.error(`duplicated calls should be ok.code is ${error.code},message is ${error.message}`);
}
```

### isNotNull

isNotNull(field: string): Query

构造一个Query对象以查询具有值不为null的指定字段的条目。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明                          |
| ------ | -------- | ---- | ----------------------------- |
| fieId  | string   | 是   | 表示指定字段，不能包含' ^ '。 |

**返回值：**

| 类型           | 说明            |
| -------------- | --------------- |
| [Query](#query) | 返回Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let query: distributedKVStore.Query | null = new distributedKVStore.Query();
  query.isNotNull("field");
  console.info(`query is ${query.getSqlLike()}`);
  query = null;
} catch (e) {
  let error = e as BusinessError;
  console.error(`duplicated calls should be ok.code is ${error.code},message is ${error.message}`);
}
```

### beginGroup

beginGroup(): Query

创建一个带有左括号的查询条件组。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**返回值：**

| 类型           | 说明            |
| -------------- | --------------- |
| [Query](#query) | 返回Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
    let query: distributedKVStore.Query | null = new distributedKVStore.Query();
    query.beginGroup();
    query.isNotNull("field");
    query.endGroup();
    console.info("query is " + query.getSqlLike());
    query = null;
} catch (e) {
    console.error("duplicated calls should be ok :" + e);
}
```

### endGroup

endGroup(): Query

创建一个带有右括号的查询条件组。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**返回值：**

| 类型           | 说明            |
| -------------- | --------------- |
| [Query](#query) | 返回Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
    let query: distributedKVStore.Query | null = new distributedKVStore.Query();
    query.beginGroup();
    query.isNotNull("field");
    query.endGroup();
    console.info("query is " + query.getSqlLike());
    query = null;
} catch (e) {
    console.error("duplicated calls should be ok :" + e);
}
```

### prefixKey

prefixKey(prefix: string): Query

创建具有指定键前缀的查询条件。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明               |
| ------ | -------- | ---- | ------------------ |
| prefix | string   | 是   | 表示指定的键前缀。 |

**返回值：**

| 类型           | 说明            |
| -------------- | --------------- |
| [Query](#query) | 返回Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
    let query: distributedKVStore.Query | null = new distributedKVStore.Query();
    query.prefixKey("$.name");
    query.prefixKey("0");
    console.info(`query is ${query.getSqlLike()}`);
    query = null;
} catch (e) {
    let error = e as BusinessError;
    console.error(`duplicated calls should be ok.code is ${error.code},message is ${error.message}`);
}
```

### setSuggestIndex

setSuggestIndex(index: string): Query

设置一个指定的索引，将优先用于查询。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明               |
| ------ | -------- | ---- | ------------------ |
| index  | string   | 是   | 指示要设置的索引。 |

**返回值：**

| 类型           | 说明            |
| -------------- | --------------- |
| [Query](#query) | 返回Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
    let query: distributedKVStore.Query | null = new distributedKVStore.Query();
    query.setSuggestIndex("$.name");
    query.setSuggestIndex("0");
    console.info(`query is ${query.getSqlLike()}`);
    query = null;
} catch (e) {
    let error = e as BusinessError;
    console.error(`duplicated calls should be ok.code is ${error.code},message is ${error.message}`);
}
```

### deviceId

deviceId(deviceId:string):Query

添加设备ID作为key的前缀。
> **说明：** 
>
> 其中deviceId通过调用[deviceManager.getAvailableDeviceListSync](js-apis-distributedDeviceManager.md#getavailabledevicelistsync)方法得到。
> deviceId具体获取方式请参考[sync接口示例](#sync)

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型 | 必填 | 说明               |
| -------- | -------- | ---- | ------------------ |
| deviceId | string   | 是   | 指示查询的设备ID。 |

**返回值：**

| 类型           | 说明            |
| -------------- | --------------- |
| [Query](#query) | 返回Query对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
    let query: distributedKVStore.Query | null = new distributedKVStore.Query();
    query.deviceId("deviceId");
    console.info(`query is ${query.getSqlLike()}`);
} catch (e) {
    let error = e as BusinessError;
    console.error(`duplicated calls should be ok.code is ${error.code},message is ${error.message}`);
}
```

### getSqlLike

getSqlLike():string

获取Query对象的查询语句。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**返回值：**

| 类型   | 说明                                 |
| ------ | ------------------------------------ |
| string | 返回一个字段列中包含对应子串的结果。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
    let query: distributedKVStore.Query | null = new distributedKVStore.Query();
    let sql1 = query.getSqlLike();
    console.info(`GetSqlLike sql= ${sql1}`);
} catch (e) {
    console.error("duplicated calls should be ok : " + e);
}
```

## SingleKVStore

SingleKVStore数据库实例，提供增加数据、删除数据和订阅数据变更、订阅数据同步完成的方法。

在调用SingleKVStore的方法前，需要先通过[getKVStore](#getkvstore)构建一个SingleKVStore实例。

### put

put(key: string, value: Uint8Array | string | number | boolean, callback: AsyncCallback&lt;void&gt;): void

添加指定类型键值对到数据库，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名  | 类型 | 必填  | 说明                    |
| -----  | ------  | ----  | ----------------------- |
| key    | string  | 是    |要添加数据的key，不能为空且长度不大于[MAX_KEY_LENGTH](#constants)。   |
| value  | Uint8Array \| string \| number \| boolean | 是    |要添加数据的value，支持Uint8Array、number 、 string 、boolean，Uint8Array、string 的长度不大于[MAX_VALUE_LENGTH](#constants)。   |
| callback | AsyncCallback&lt;void&gt; | 是    |回调函数。   |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                             |
| ------------ | ---------------------------------------- |
| 15100003     | Database corrupted.                      |
| 15100005     | Database or result set already closed.   |

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

const KEY_TEST_STRING_ELEMENT = 'key_test_string';
const VALUE_TEST_STRING_ELEMENT = 'value-test-string';
try {
  kvStore.put(KEY_TEST_STRING_ELEMENT, VALUE_TEST_STRING_ELEMENT, (err) => {
    if (err != undefined) {
      console.error(`Failed to put.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info("Succeeded in putting");
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### put

put(key: string, value: Uint8Array | string | number | boolean): Promise&lt;void&gt;

添加指定类型键值对到数据库，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名  | 类型 | 必填  | 说明                    |
| -----  | ------  | ----  | ----------------------- |
| key    | string  | 是    |要添加数据的key，不能为空且长度不大于[MAX_KEY_LENGTH](#constants)。   |
| value  | Uint8Array \| string \| number \| boolean | 是    |要添加数据的value，支持Uint8Array、number 、 string 、boolean，Uint8Array、string 的长度不大于[MAX_VALUE_LENGTH](#constants)。   |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                             |
| ------------ | ---------------------------------------- |
| 15100003     | Database corrupted.                      |
| 15100005     | Database or result set already closed.   |

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

const KEY_TEST_STRING_ELEMENT = 'key_test_string';
const VALUE_TEST_STRING_ELEMENT = 'value-test-string';
try {
  kvStore.put(KEY_TEST_STRING_ELEMENT, VALUE_TEST_STRING_ELEMENT).then(() => {
    console.info(`Succeeded in putting data`);
  }).catch((err: BusinessError) => {
    console.error(`Failed to put.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### putBatch

putBatch(entries: Entry[], callback: AsyncCallback&lt;void&gt;): void

批量插入键值对到SingleKVStore数据库中，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                 | 必填 | 说明                     |
| -------- | ------------------------ | ---- | ------------------------ |
| entries  | [Entry](#entry)[]        | 是   | 表示要批量插入的键值对。一个entries对象中允许的最大条目个数为128个。 |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。               |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                             |
| ------------ | ---------------------------------------- |
| 15100003     | Database corrupted.                      |
| 15100005     | Database or result set already closed.   |

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  console.info(`entries: ${entries}`);
  kvStore.putBatch(entries, async (err) => {
    if (err != undefined) {
      console.error(`Failed to put Batch.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in putting Batch');
    if (kvStore != null) {
      kvStore.getEntries('batch_test_string_key', (err, entries) => {
        if (err != undefined) {
          console.error(`Failed to get Entries.code is ${err.code},message is ${err.message}`);
        }
        console.info('Succeeded in getting Entries');
        console.info(`entries.length: ${entries.length}`);
        console.info(`entries[0]: ${entries[0]}`);
      });
    } else {
      console.error('KvStore is null'); //后续示例代码与此处保持一致
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message} `);
}
```

### putBatch

putBatch(entries: Entry[]): Promise&lt;void&gt;

批量插入键值对到SingleKVStore数据库中，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名  | 类型          | 必填 | 说明                     |
| ------- | ----------------- | ---- | ------------------------ |
| entries | [Entry](#entry)[] | 是   | 表示要批量插入的键值对。一个entries对象中允许的最大条目个数为128个。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                             |
| ------------ | ---------------------------------------- |
| 15100003     | Database corrupted.                      |
| 15100005     | Database or result set already closed.   |

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  console.info(`entries: ${entries}`);
  kvStore.putBatch(entries).then(async () => {
    console.info('Succeeded in putting Batch');
    if (kvStore != null) {
      kvStore.getEntries('batch_test_string_key').then((entries) => {
        console.info('Succeeded in getting Entries');
        console.info(`PutBatch ${entries}`);
      }).catch((err: BusinessError) => {
        console.error(`Failed to get Entries.code is ${err.code},message is ${err.message}`);
      });
    }
  }).catch((err: BusinessError) => {
    console.error(`Failed to put Batch.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message} `);
}
```

### putBatch


putBatch(value: Array&lt;ValuesBucket&gt;, callback: AsyncCallback&lt;void&gt;): void

将值写入SingleKVStore数据库，使用callback异步回调。

**模型约束：** 此接口仅可在Stage模型下使用

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                                                     | 必填 | 说明               |
| -------- | ------------------------------------------------------------ | ---- | ------------------ |
| value    | Array&lt;[ValuesBucket](js-apis-data-valuesBucket.md#valuesbucket)&gt; | 是   | 表示要插入的数据。 |
| callback | AsyncCallback&lt;void&gt;                                     | 是   | 回调函数。         |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                             |
| ------------ | ---------------------------------------- |
| 15100003     | Database corrupted.                      |
| 15100005     | Database or result set already closed.   |

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let v8Arr: distributedKVStore.Entry[] = [];
  let arr = new Uint8Array([4, 5, 6, 7]);
  let vb1: distributedKVStore.Entry = { key: "name_1", value: 32 }
  let vb2: distributedKVStore.Entry = { key: "name_2", value: arr };
  let vb3: distributedKVStore.Entry = { key: "name_3", value: "lisi" };

  v8Arr.push(vb1);
  v8Arr.push(vb2);
  v8Arr.push(vb3);
  kvStore.putBatch(v8Arr, async (err) => {
    if (err != undefined) {
      console.error(`Failed to put batch.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in putting batch');
  })
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to put batch.code is ${error.code},message is ${error.message}`);
}
```

### putBatch

putBatch(value: Array&lt;ValuesBucket&gt;): Promise&lt;void&gt;

将valuesbucket类型的值写入SingleKVStore数据库，使用Promise异步回调。

**模型约束：** 此接口仅可在Stage模型下使用

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型                                                     | 必填 | 说明               |
| ------ | ------------------------------------------------------------ | ---- | ------------------ |
| value  | Array&lt;[ValuesBucket](js-apis-data-valuesBucket.md#valuesbucket)&gt; | 是   | 表示要插入的数据。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 五返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                             |
| ------------ | ---------------------------------------- |
| 15100003     | Database corrupted.                      |
| 15100005     | Database or result set already closed.   |

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let v8Arr: distributedKVStore.Entry[] = [];
  let arr = new Uint8Array([4, 5, 6, 7]);
  let vb1: distributedKVStore.Entry = { key: "name_1", value: 32 }
  let vb2: distributedKVStore.Entry = { key: "name_2", value: arr };
  let vb3: distributedKVStore.Entry = { key: "name_3", value: "lisi" };

  v8Arr.push(vb1);
  v8Arr.push(vb2);
  v8Arr.push(vb3);
  kvStore.putBatch(v8Arr).then(async () => {
    console.info(`Succeeded in putting patch`);
  }).catch((err: BusinessError) => {
    console.error(`putBatch fail.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`putBatch fail.code is ${error.code},message is ${error.message}`);
}
```

### delete

delete(key: string, callback: AsyncCallback&lt;void&gt;): void

从数据库中删除指定键值的数据，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                  | 必填 | 说明                                                         |
| -------- | ------------------------- | ---- | ------------------------------------------------------------ |
| key      | string                    | 是   | 要删除数据的key，不能为空且长度不大于[MAX_KEY_LENGTH](#constants)。 |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。                                                   |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100005    | Database or result set already closed. |

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

const KEY_TEST_STRING_ELEMENT = 'key_test_string';
const VALUE_TEST_STRING_ELEMENT = 'value-test-string';
try {
  kvStore.put(KEY_TEST_STRING_ELEMENT, VALUE_TEST_STRING_ELEMENT, (err) => {
    if (err != undefined) {
      console.error(`Failed to put.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in putting');
    if (kvStore != null) {
      kvStore.delete(KEY_TEST_STRING_ELEMENT, (err) => {
        if (err != undefined) {
          console.error(`Failed to delete.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in deleting');
      });
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### delete

delete(key: string): Promise&lt;void&gt;

从数据库中删除指定键值的数据，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明                                                         |
| ------ | -------- | ---- | ------------------------------------------------------------ |
| key    | string   | 是   | 要删除数据的key，不能为空且长度不大于[MAX_KEY_LENGTH](#constants)。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                             |
| ------------ | ---------------------------------------- |
| 15100003     | Database corrupted.                      |
| 15100005     | Database or result set already closed.   |

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

const KEY_TEST_STRING_ELEMENT = 'key_test_string';
const VALUE_TEST_STRING_ELEMENT = 'value-test-string';
try {
  kvStore.put(KEY_TEST_STRING_ELEMENT, VALUE_TEST_STRING_ELEMENT).then(() => {
    console.info(`Succeeded in putting data`);
    if (kvStore != null) {
      kvStore.delete(KEY_TEST_STRING_ELEMENT).then(() => {
        console.info('Succeeded in deleting');
      }).catch((err: BusinessError) => {
        console.error(`Failed to delete.code is ${err.code},message is ${err.message}`);
      });
    }
  }).catch((err: BusinessError) => {
    console.error(`Failed to put.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### delete

delete(predicates: dataSharePredicates.DataSharePredicates, callback: AsyncCallback&lt;void&gt;)

从数据库中删除符合predicates条件的键值对，使用callback异步回调。

**模型约束：** 此接口仅可在Stage模型下使用

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.DistributedDataManager.DataShare.Provider

**参数：**

| 参数名     | 类型                                                     | 必填 | 说明                                            |
| ---------- | ------------------------------------------------------------ | ---- | ----------------------------------------------- |
| predicates | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md#datasharepredicates) | 是   | 指示筛选条件，当此参数为null时，应定义处理逻辑。 |
| callback   | AsyncCallback&lt;void&gt;                                    | 是   | 回调函数。                                      |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100005    | Database or result set already closed. |

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

try {
  let predicates = new dataSharePredicates.DataSharePredicates();
  let arr = ["name"];
  predicates.inKeys(arr);
  kvStore.put("name", "bob", (err) => {
    if (err != undefined) {
      console.error(`Failed to put.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info("Succeeded in putting");
    if (kvStore != null) {
      kvStore.delete(predicates, (err) => {
        if (err == undefined) {
          console.info('Succeeded in deleting');
        } else {
          console.error(`Failed to delete.code is ${err.code},message is ${err.message}`);
        }
      });
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### delete

delete(predicates: dataSharePredicates.DataSharePredicates): Promise&lt;void&gt;

从数据库中删除符合predicates条件的键值对，使用Promise异步回调。

**模型约束：** 此接口仅可在Stage模型下使用

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.DistributedDataManager.DataShare.Provider

**参数：**

| 参数名     | 类型                                                     | 必填 | 说明                                            |
| ---------- | ------------------------------------------------------------ | ---- | ----------------------------------------------- |
| predicates | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md#datasharepredicates) | 是   | 指示筛选条件,当此参数为null时，应定义处理逻辑。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                             |
| ------------ | ---------------------------------------- |
| 15100003     | Database corrupted.                      |
| 15100005     | Database or result set already closed.   |

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

try {
  let predicates = new dataSharePredicates.DataSharePredicates();
  let arr = ["name"];
  predicates.inKeys(arr);
  kvStore.put("name", "bob").then(() => {
    console.info(`Succeeded in putting data`);
    if (kvStore != null) {
      kvStore.delete(predicates).then(() => {
        console.info('Succeeded in deleting');
      }).catch((err: BusinessError) => {
        console.error(`Failed to delete.code is ${err.code},message is ${err.message}`);
      });
    }
  }).catch((err: BusinessError) => {
    console.error(`Failed to put.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### deleteBatch

deleteBatch(keys: string[], callback: AsyncCallback&lt;void&gt;): void

批量删除SingleKVStore数据库中的键值对，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                  | 必填 | 说明                     |
| -------- | ------------------------- | ---- | ------------------------ |
| keys     | string[]                  | 是   | 表示要批量删除的键值对。 |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。               |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                             |
| ------------ | ---------------------------------------- |
| 15100003     | Database corrupted.                      |
| 15100005     | Database or result set already closed.   |

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let entries: distributedKVStore.Entry[] = [];
  let keys: string[] = [];
  for (let i = 0; i < 5; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
    keys.push(key + i);
  }
  console.info(`entries: ${entries}`);
  kvStore.putBatch(entries, async (err) => {
    if (err != undefined) {
      console.error(`Failed to put Batch.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in putting Batch');
    if (kvStore != null) {
      kvStore.deleteBatch(keys, async (err) => {
        if (err != undefined) {
          console.error(`Failed to delete Batch.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in deleting Batch');
      });
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### deleteBatch

deleteBatch(keys: string[]): Promise&lt;void&gt;

批量删除SingleKVStore数据库中的键值对，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明                     |
| ------ | -------- | ---- | ------------------------ |
| keys   | string[] | 是   | 表示要批量删除的键值对。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                             |
| ------------ | ---------------------------------------- |
| 15100003     | Database corrupted.                      |
| 15100005     | Database or result set already closed.   |

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let entries: distributedKVStore.Entry[] = [];
  let keys: string[] = [];
  for (let i = 0; i < 5; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
    keys.push(key + i);
  }
  console.info(`entries: ${entries}`);
  kvStore.putBatch(entries).then(async () => {
    console.info('Succeeded in putting Batch');
    if (kvStore != null) {
      kvStore.deleteBatch(keys).then(() => {
        console.info('Succeeded in deleting Batch');
      }).catch((err: BusinessError) => {
        console.error(`Failed to delete Batch.code is ${err.code},message is ${err.message}`);
      });
    }
  }).catch((err: BusinessError) => {
    console.error(`Failed to put Batch.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### removeDeviceData

removeDeviceData(deviceId: string, callback: AsyncCallback&lt;void&gt;): void

删除指定设备的数据，使用callback异步回调。
> **说明：** 
>
> 其中deviceId通过调用[deviceManager.getAvailableDeviceListSync](js-apis-distributedDeviceManager.md#getavailabledevicelistsync)方法得到。
> deviceId具体获取方式请参考[sync接口示例](#sync)

**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**参数：**

| 参数名   | 类型                  | 必填 | 说明                   |
| -------- | ------------------------- | ---- | ---------------------- |
| deviceId | string                    | 是   | 表示要删除设备的名称。 |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。             |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

const KEY_TEST_STRING_ELEMENT = 'key_test_string_2';
const VALUE_TEST_STRING_ELEMENT = 'value-string-002';
try {
  kvStore.put(KEY_TEST_STRING_ELEMENT, VALUE_TEST_STRING_ELEMENT, async (err) => {
    console.info('Succeeded in putting data');
    const deviceid = 'no_exist_device_id';
    if (kvStore != null) {
      kvStore.removeDeviceData(deviceid, async (err) => {
        if (err == undefined) {
          console.info('succeeded in removing device data');
        } else {
          console.error(`Failed to remove device data.code is ${err.code},message is ${err.message} `);
          if (kvStore != null) {
            kvStore.get(KEY_TEST_STRING_ELEMENT, async (err, data) => {
              console.info('Succeeded in getting data');
            });
          }
        }
      });
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`)
}
```

### removeDeviceData

removeDeviceData(deviceId: string): Promise&lt;void&gt;

删除指定设备的数据，使用Promise异步回调。
> **说明：** 
>
> 其中deviceId通过调用[deviceManager.getAvailableDeviceListSync](js-apis-distributedDeviceManager.md#getavailabledevicelistsync)方法得到。
> deviceId具体获取方式请参考[sync接口示例](#sync)

**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**参数：**

| 参数名   | 类型 | 必填 | 说明                   |
| -------- | -------- | ---- | ---------------------- |
| deviceId | string   | 是   | 表示要删除设备的名称。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

const KEY_TEST_STRING_ELEMENT = 'key_test_string_2';
const VALUE_TEST_STRING_ELEMENT = 'value-string-001';
try {
  kvStore.put(KEY_TEST_STRING_ELEMENT, VALUE_TEST_STRING_ELEMENT).then(() => {
    console.info('Succeeded in putting data');
  }).catch((err: BusinessError) => {
    console.error(`Failed to put data.code is ${err.code},message is ${err.message} `);
  });
  const deviceid = 'no_exist_device_id';
  kvStore.removeDeviceData(deviceid).then(() => {
    console.info('succeeded in removing device data');
  }).catch((err: BusinessError) => {
    console.error(`Failed to remove device data.code is ${err.code},message is ${err.message} `);
  });
  kvStore.get(KEY_TEST_STRING_ELEMENT).then((data) => {
    console.info('Succeeded in getting data');
  }).catch((err: BusinessError) => {
    console.error(`Failed to get data.code is ${err.code},message is ${err.message} `);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`)
}
```

### get

get(key: string, callback: AsyncCallback&lt;boolean | string | number | Uint8Array&gt;): void

获取指定键的值，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名  | 类型 | 必填  | 说明                    |
| -----  | ------  | ----  | ----------------------- |
| key    |string   | 是    |要查询数据的key，不能为空且长度不大于[MAX_KEY_LENGTH](#constants)。  |
| callback  |AsyncCallback&lt;boolean \| string \| number \| Uint8Array&gt; | 是    |回调函数。返回获取查询的值。  |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100004     | Not found.                             |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';


const KEY_TEST_STRING_ELEMENT = 'key_test_string';
const VALUE_TEST_STRING_ELEMENT = 'value-test-string';
try {
  kvStore.put(KEY_TEST_STRING_ELEMENT, VALUE_TEST_STRING_ELEMENT, (err) => {
    if (err != undefined) {
      console.error(`Failed to put.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info("Succeeded in putting");
    if (kvStore != null) {
      kvStore.get(KEY_TEST_STRING_ELEMENT, (err, data) => {
        if (err != undefined) {
          console.error(`Failed to get.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info(`Succeeded in getting data.data=${data}`);
      });
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to get.code is ${error.code},message is ${error.message}`);
}
```

### get

get(key: string): Promise&lt;boolean | string | number | Uint8Array&gt;

获取指定键的值，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明                                                         |
| ------ | -------- | ---- | ------------------------------------------------------------ |
| key    | string   | 是   | 要查询数据的key，不能为空且长度不大于[MAX_KEY_LENGTH](#constants)。 |

**返回值：**

| 类型    | 说明       |
| ------  | -------   |
|Promise&lt;Uint8Array \| string \| boolean \| number&gt; |Promise对象。返回获取查询的值。|

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100004     | Not found.                             |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';


const KEY_TEST_STRING_ELEMENT = 'key_test_string';
const VALUE_TEST_STRING_ELEMENT = 'value-test-string';
try {
  kvStore.put(KEY_TEST_STRING_ELEMENT, VALUE_TEST_STRING_ELEMENT).then(() => {
    console.info(`Succeeded in putting data`);
    if (kvStore != null) {
      kvStore.get(KEY_TEST_STRING_ELEMENT).then((data) => {
        console.info(`Succeeded in getting data.data=${data}`);
      }).catch((err: BusinessError) => {
        console.error(`Failed to get.code is ${err.code},message is ${err.message}`);
      });
    }
  }).catch((err: BusinessError) => {
    console.error(`Failed to put.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to get.code is ${error.code},message is ${error.message}`);
}
```

### getEntries

getEntries(keyPrefix: string, callback: AsyncCallback&lt;Entry[]&gt;): void

获取匹配指定键前缀的所有键值对，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名    | 类型                               | 必填 | 说明                                     |
| --------- | -------------------------------------- | ---- | ---------------------------------------- |
| keyPrefix | string                                 | 是   | 表示要匹配的键前缀。                     |
| callback  | AsyncCallback&lt;[Entry](#entry)[]&gt; | 是   | 回调函数。返回匹配指定前缀的键值对列表。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  console.info(`entries: ${entries}`);
  kvStore.putBatch(entries, async (err) => {
    if (err != undefined) {
      console.error(`Failed to put Batch.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in putting Batch');
    if (kvStore != null) {
      kvStore.getEntries('batch_test_string_key', (err, entries) => {
        if (err != undefined) {
          console.error(`Failed to get Entries.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in getting Entries');
        console.info(`entries.length: ${entries.length}`);
        console.info(`entries[0]: ${entries[0]}`);
      });
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message} `);
}
```

### getEntries

getEntries(keyPrefix: string): Promise&lt;Entry[]&gt;

获取匹配指定键前缀的所有键值对，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名    | 类型 | 必填 | 说明                 |
| --------- | -------- | ---- | -------------------- |
| keyPrefix | string   | 是   | 表示要匹配的键前缀。 |

**返回值：**

| 类型                             | 说明                                        |
| -------------------------------- | ------------------------------------------- |
| Promise&lt;[Entry](#entry)[]&gt; | Promise对象。返回匹配指定前缀的键值对列表。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';


try {
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  console.info(`entries: ${entries}`);
  kvStore.putBatch(entries).then(async () => {
    console.info('Succeeded in putting Batch');
    if (kvStore != null) {
      kvStore.getEntries('batch_test_string_key').then((entries) => {
        console.info('Succeeded in getting Entries');
        console.info(`PutBatch ${entries}`);
      }).catch((err: BusinessError) => {
        console.error(`Failed to get Entries.code is ${err.code},message is ${err.message}`);
      });
    }
  }).catch((err: BusinessError) => {
    console.error(`Failed to put Batch.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message} `);
}
```

### getEntries

getEntries(query: Query, callback: AsyncCallback&lt;Entry[]&gt;): void

获取与指定Query对象匹配的键值对列表，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                               | 必填 | 说明                                            |
| -------- | -------------------------------------- | ---- | ----------------------------------------------- |
| query    | [Query](#query)                         | 是   | 表示要匹配的键前缀。                            |
| callback | AsyncCallback&lt;[Entry](#entry)[]&gt; | 是   | 回调函数。返回与指定Query对象匹配的键值对列表。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let arr = new Uint8Array([21, 31]);
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_bool_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.BYTE_ARRAY,
        value: arr
      }
    }
    entries.push(entry);
  }
  console.info(`entries: {entries}`);
  kvStore.putBatch(entries, async (err) => {
    console.info('Succeeded in putting Batch');
    const query = new distributedKVStore.Query();
    query.prefixKey("batch_test");
    if (kvStore != null) {
      kvStore.getEntries(query, (err, entries) => {
        if (err != undefined) {
          console.error(`Failed to get Entries.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in getting Entries');
        console.info(`entries.length: ${entries.length}`);
        console.info(`entries[0]: ${entries[0]}`);
      });
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to get Entries.code is ${error.code},message is ${error.message}`);
}
```

### getEntries

getEntries(query: Query): Promise&lt;Entry[]&gt;

获取与指定Query对象匹配的键值对列表，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型       | 必填 | 说明           |
| ------ | -------------- | ---- | -------------- |
| query  | [Query](#query) | 是   | 表示查询对象。 |

**返回值：**

| 类型                             | 说明                                               |
| -------------------------------- | -------------------------------------------------- |
| Promise&lt;[Entry](#entry)[]&gt; | Promise对象。返回与指定Query对象匹配的键值对列表。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let arr = new Uint8Array([21, 31]);
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_bool_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.BYTE_ARRAY,
        value: arr
      }
    }
    entries.push(entry);
  }
  console.info(`entries: {entries}`);
  kvStore.putBatch(entries).then(async () => {
    console.info('Succeeded in putting Batch');
    const query = new distributedKVStore.Query();
    query.prefixKey("batch_test");
    if (kvStore != null) {
      kvStore.getEntries(query).then((entries) => {
        console.info('Succeeded in getting Entries');
      }).catch((err: BusinessError) => {
        console.error(`Failed to get Entries.code is ${err.code},message is ${err.message}`);
      });
    }
  }).catch((err: BusinessError) => {
    console.error(`Failed to get Entries.code is ${err.code},message is ${err.message}`)
  });
  console.info('Succeeded in getting Entries');
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to get Entries.code is ${error.code},message is ${error.message}`);
}
```

### getResultSet

getResultSet(keyPrefix: string, callback: AsyncCallback&lt;KVStoreResultSet&gt;): void

从SingleKVStore数据库中获取具有指定前缀的结果集，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名    | 类型                                                   | 必填 | 说明                                 |
| --------- | ---------------------------------------------------------- | ---- | ------------------------------------ |
| keyPrefix | string                                                     | 是   | 表示要匹配的键前缀。                 |
| callback  | AsyncCallback&lt;[KVStoreResultSet](#kvstoreresultset)&gt; | 是   | 回调函数。返回具有指定前缀的结果集。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100001     | Over max  limits.                      |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |


**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  kvStore.putBatch(entries, async (err) => {
    if (err != undefined) {
      console.error(`Failed to put batch.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in putting batch');
    if (kvStore != null) {
      kvStore.getResultSet('batch_test_string_key', async (err, result) => {
        if (err != undefined) {
          console.error(`Failed to get resultset.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in getting result set');
        resultSet = result;
        if (kvStore != null) {
          kvStore.closeResultSet(resultSet, (err) => {
            if (err != undefined) {
              console.error(`Failed to close resultset.code is ${err.code},message is ${err.message}`);
              return;
            }
            console.info('Succeeded in closing result set');
          });
        }
      });
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### getResultSet

getResultSet(keyPrefix: string): Promise&lt;KVStoreResultSet&gt;

从SingleKVStore数据库中获取具有指定前缀的结果集，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名    | 类型 | 必填 | 说明                 |
| --------- | -------- | ---- | -------------------- |
| keyPrefix | string   | 是   | 表示要匹配的键前缀。 |

**返回值：**

| 类型                                                 | 说明                                    |
| ---------------------------------------------------- | --------------------------------------- |
| Promise&lt;[KVStoreResultSet](#kvstoreresultset)&gt; | Promise对象。返回具有指定前缀的结果集。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100001     | Over max  limits.                      |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  kvStore.putBatch(entries).then(async () => {
    console.info('Succeeded in putting batch');
  }).catch((err: BusinessError) => {
    console.error(`Failed to put batch.code is ${err.code},message is ${err.message}`);
  });
  kvStore.getResultSet('batch_test_string_key').then((result) => {
    console.info('Succeeded in getting result set');
    resultSet = result;
    if (kvStore != null) {
      kvStore.closeResultSet(resultSet).then(() => {
        console.info('Succeeded in closing result set');
      }).catch((err: BusinessError) => {
        console.error(`Failed to close resultset.code is ${err.code},message is ${err.message}`);
      });
    }
  }).catch((err: BusinessError) => {
    console.error(`Failed to get resultset.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.code}`);
}
```

### getResultSet

getResultSet(query: Query, callback: AsyncCallback&lt;KVStoreResultSet&gt;): void

获取与指定Query对象匹配的KVStoreResultSet对象，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                                                   | 必填 | 说明                                                      |
| -------- | ---------------------------------------------------------- | ---- | --------------------------------------------------------- |
| query    | Query                                                      | 是   | 表示查询对象。                                            |
| callback | AsyncCallback&lt;[KVStoreResultSet](#kvstoreresultset)&gt; | 是   | 回调函数，获取与指定Query对象匹配的KVStoreResultSet对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100001     | Over max  limits.                      |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  kvStore.putBatch(entries, async (err) => {
    if (err != undefined) {
      console.error(`Failed to put batch.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in putting batch');
    const query = new distributedKVStore.Query();
    query.prefixKey("batch_test");
    if (kvStore != null) {
      kvStore.getResultSet(query, async (err, result) => {
        if (err != undefined) {
          console.error(`Failed to get resultset.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in getting result set');
      });
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### getResultSet

getResultSet(query: Query): Promise&lt;KVStoreResultSet&gt;

获取与指定Query对象匹配的KVStoreResultSet对象，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型       | 必填 | 说明           |
| ------ | -------------- | ---- | -------------- |
| query  | [Query](#query) | 是   | 表示查询对象。 |

**返回值：**

| 类型                                                 | 说明                                                         |
| ---------------------------------------------------- | ------------------------------------------------------------ |
| Promise&lt;[KVStoreResultSet](#kvstoreresultset)&gt; | Promise对象。获取与指定Query对象匹配的KVStoreResultSet对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100001     | Over max  limits.                      |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  kvStore.putBatch(entries).then(async () => {
    console.info('Succeeded in putting batch');
  }).catch((err: BusinessError) => {
    console.error(`Failed to put batch.code is ${err.code},message is ${err.message}`);
  });
  const query = new distributedKVStore.Query();
  query.prefixKey("batch_test");
  kvStore.getResultSet(query).then((result) => {
    console.info('Succeeded in getting result set');
    resultSet = result;
  }).catch((err: BusinessError) => {
    console.error(`Failed to get resultset.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.code}`);
}
```

### getResultSet

getResultSet(predicates: dataSharePredicates.DataSharePredicates, callback: AsyncCallback&lt;KVStoreResultSet&gt;): void

获取与指定Predicate对象匹配的KVStoreResultSet对象，使用callback异步回调。

**模型约束：** 此接口仅可在Stage模型下使用

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.DistributedDataManager.DataShare.Provider

**参数：**

| 参数名     | 类型                                                     | 必填 | 说明                                                         |
| ---------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| predicates | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md#datasharepredicates) | 是   | 指示筛选条件,当此参数为null时，应定义处理逻辑。              |
| callback   | AsyncCallback&lt;[KVStoreResultSet](#kvstoreresultset)&gt;   | 是   | 回调函数，获取与指定Predicates对象匹配的KVStoreResultSet对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100001     | Over max  limits.                      |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let predicates = new dataSharePredicates.DataSharePredicates();
  predicates.prefixKey("batch_test_string_key");
  kvStore.getResultSet(predicates, async (err, result) => {
    if (err != undefined) {
      console.error(`Failed to get resultset.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in getting result set');
    resultSet = result;
    if (kvStore != null) {
      kvStore.closeResultSet(resultSet, (err) => {
        if (err != undefined) {
          console.error(`Failed to close resultset.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in closing result set');
      });
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.code}`);
}
```

### getResultSet

getResultSet(predicates: dataSharePredicates.DataSharePredicates): Promise&lt;KVStoreResultSet&gt;

获取与指定Predicate对象匹配的KVStoreResultSet对象，使用Promise异步回调。

**模型约束：** 此接口仅可在Stage模型下使用

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.DistributedDataManager.DataShare.Provider

**参数：**

| 参数名     | 类型                                                     | 必填 | 说明                                            |
| ---------- | ------------------------------------------------------------ | ---- | ----------------------------------------------- |
| predicates | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md#datasharepredicates) | 是   | 指示筛选条件,当此参数为null时，应定义处理逻辑。 |

**返回值：**

| 类型                                                 | 说明                      |
| ---------------------------------------------------- | ------------------------- |
| Promise&lt;[KVStoreResultSet](#kvstoreresultset)&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100001     | Over max  limits.                      |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let predicates = new dataSharePredicates.DataSharePredicates();
  predicates.prefixKey("batch_test_string_key");
  kvStore.getResultSet(predicates).then((result) => {
    console.info('Succeeded in getting result set');
    resultSet = result;
    if (kvStore != null) {
      kvStore.closeResultSet(resultSet).then(() => {
        console.info('Succeeded in closing result set');
      }).catch((err: BusinessError) => {
        console.error(`Failed to close resultset.code is ${err.code},message is ${err.message}`);
      });
    }
  }).catch((err: BusinessError) => {
    console.error(`Failed to get resultset.code is ${err.code},message is ${err.message}`);
  });

} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.code}`);
}
```

### closeResultSet

closeResultSet(resultSet: KVStoreResultSet, callback: AsyncCallback&lt;void&gt;): void

关闭由[SingleKvStore.getResultSet](#getresultset-1)返回的KVStoreResultSet对象，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名    | 类型                              | 必填 | 说明                               |
| --------- | ------------------------------------- | ---- | ---------------------------------- |
| resultSet | [KVStoreResultSet](#kvstoreresultset) | 是   | 表示要关闭的KVStoreResultSet对象。 |
| callback  | AsyncCallback&lt;void&gt;             | 是   | 回调函数。                         |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let resultSet: distributedKVStore.KVStoreResultSet;
try {
  kvStore.getResultSet('batch_test_string_key', async (err, result) => {
    if (err != undefined) {
      console.error(`Failed to get resultset.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in getting result set');
    resultSet = result;
    if (kvStore != null) {
      kvStore.closeResultSet(resultSet, (err) => {
        if (err != undefined) {
          console.error(`Failed to close resultset.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in closing result set');
      })
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.code}`);
}

```

### closeResultSet

closeResultSet(resultSet: KVStoreResultSet): Promise&lt;void&gt;

关闭由[SingleKvStore.getResultSet](#getresultset-1)返回的KVStoreResultSet对象，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名    | 类型                              | 必填 | 说明                               |
| --------- | ------------------------------------- | ---- | ---------------------------------- |
| resultSet | [KVStoreResultSet](#kvstoreresultset) | 是   | 表示要关闭的KVStoreResultSet对象。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let resultSet: distributedKVStore.KVStoreResultSet;
try {
  kvStore.getResultSet('batch_test_string_key').then((result) => {
    console.info('Succeeded in getting result set');
    resultSet = result;
    if (kvStore != null) {
      kvStore.closeResultSet(resultSet).then(() => {
        console.info('Succeeded in closing result set');
      }).catch((err: BusinessError) => {
        console.error(`Failed to close resultset.code is ${err.code},message is ${err.message}`);
      });
    }
  }).catch((err: BusinessError) => {
    console.error(`Failed to get resultset.code is ${err.code},message is ${err.message}`);
  });

} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.code}`);
}
```

### getResultSize

getResultSize(query: Query, callback: AsyncCallback&lt;number&gt;): void

获取与指定Query对象匹配的结果数，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                    | 必填 | 说明                                        |
| -------- | --------------------------- | ---- | ------------------------------------------- |
| query    | [Query](#query)              | 是   | 表示查询对象。                              |
| callback | AsyncCallback&lt;number&gt; | 是   | 回调函数。返回与指定Query对象匹配的结果数。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  kvStore.putBatch(entries, async (err) => {
    console.info('Succeeded in putting batch');
    const query = new distributedKVStore.Query();
    query.prefixKey("batch_test");
    if (kvStore != null) {
      kvStore.getResultSize(query, async (err, resultSize) => {
        if (err != undefined) {
          console.error(`Failed to get result size.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in getting result set size');
      });
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.code}`);
}
```

### getResultSize

getResultSize(query: Query): Promise&lt;number&gt;

获取与指定Query对象匹配的结果数，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型       | 必填 | 说明           |
| ------ | -------------- | ---- | -------------- |
| query  | [Query](#query) | 是   | 表示查询对象。 |

**返回值：**

| 类型                  | 说明                                            |
| --------------------- | ----------------------------------------------- |
| Promise&lt;number&gt; | Promise对象。获取与指定QuerV9对象匹配的结果数。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  kvStore.putBatch(entries).then(async () => {
    console.info('Succeeded in putting batch');
  }).catch((err: BusinessError) => {
    console.error(`Failed to put batch.code is ${err.code},message is ${err.message}`);
  });
  const query = new distributedKVStore.Query();
  query.prefixKey("batch_test");
  kvStore.getResultSize(query).then((resultSize) => {
    console.info('Succeeded in getting result set size');
  }).catch((err: BusinessError) => {
    console.error(`Failed to get result size.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.code}`);
}
```

### backup

backup(file:string, callback: AsyncCallback&lt;void&gt;):void

以指定名称备份数据库，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                  | 必填 | 说明                                                         |
| -------- | ------------------------- | ---- | ------------------------------------------------------------ |
| file     | string                    | 是   | 备份数据库的指定名称，不能为空且长度不大于[MAX_KEY_LENGTH](#constants)。 |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。当以指定名称备份数据库成功，err为undefined，否则为错误对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let file = "BK001";
try {
  kvStore.backup(file, (err) => {
    if (err) {
      console.error(`Failed to backup.code is ${err.code},message is ${err.message} `);
    } else {
      console.info(`Succeeded in backupping data`);
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### backup

backup(file:string): Promise&lt;void&gt;

以指定名称备份数据库，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明                                                         |
| ------ | -------- | ---- | ------------------------------------------------------------ |
| file   | string   | 是   | 备份数据库的指定名称，不能为空且长度不大于[MAX_KEY_LENGTH](#constants)。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let file = "BK001";
try {
  kvStore.backup(file).then(() => {
    console.info(`Succeeded in backupping data`);
  }).catch((err: BusinessError) => {
    console.error(`Failed to backup.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### restore

restore(file:string, callback: AsyncCallback&lt;void&gt;):void

从指定的数据库文件恢复数据库，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                  | 必填 | 说明                                                         |
| -------- | ------------------------- | ---- | ------------------------------------------------------------ |
| file     | string                    | 是   | 指定的数据库文件名称，不能为空且长度不大于[MAX_KEY_LENGTH](#constants)。 |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。当从指定的数据库文件恢复数据库成功，err为undefined，否则为错误对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let file = "BK001";
try {
  kvStore.restore(file, (err) => {
    if (err) {
      console.error(`Failed to restore.code is ${err.code},message is ${err.message}`);
    } else {
      console.info(`Succeeded in restoring data`);
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### restore

restore(file:string): Promise&lt;void&gt;

从指定的数据库文件恢复数据库，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明                                                         |
| ------ | -------- | ---- | ------------------------------------------------------------ |
| file   | string   | 是   | 指定的数据库文件名称，不能为空且长度不大于[MAX_KEY_LENGTH](#constants)。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let file = "BK001";
try {
  kvStore.restore(file).then(() => {
    console.info(`Succeeded in restoring data`);
  }).catch((err: BusinessError) => {
    console.error(`Failed to restore.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### deleteBackup

deleteBackup(files:Array&lt;string&gt;, callback: AsyncCallback&lt;Array&lt;[string, number]&gt;&gt;):void

根据指定名称删除备份文件，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                                           | 必填 | 说明                                                         |
| -------- | -------------------------------------------------- | ---- | ------------------------------------------------------------ |
| files    | Array&lt;string&gt;                                | 是   | 删除备份文件所指定的名称，不能为空且长度不大于[MAX_KEY_LENGTH](#constants)。 |
| callback | AsyncCallback&lt;Array&lt;[string, number]&gt;&gt; | 是   | 回调函数，返回删除备份的文件名及其处理结果。                 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let files = ["BK001", "BK002"];
try {
  kvStore.deleteBackup(files, (err, data) => {
    if (err) {
      console.error(`Failed to delete Backup.code is ${err.code},message is ${err.message}`);
    } else {
      console.info(`Succeed in deleting Backup.data=${data}`);
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### deleteBackup

deleteBackup(files:Array&lt;string&gt;): Promise&lt;Array&lt;[string, number]&gt;&gt;

根据指定名称删除备份文件，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型            | 必填 | 说明                                                         |
| ------ | ------------------- | ---- | ------------------------------------------------------------ |
| files  | Array&lt;string&gt; | 是   | 删除备份文件所指定的名称，不能为空且长度不大于[MAX_KEY_LENGTH](#constants)。 |

**返回值：**

| 类型                                         | 说明                                            |
| -------------------------------------------- | ----------------------------------------------- |
| Promise&lt;Array&lt;[string, number]&gt;&gt; | Promise对象，返回删除备份的文件名及其处理结果。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let files = ["BK001", "BK002"];
try {
  kvStore.deleteBackup(files).then((data) => {
    console.info(`Succeed in deleting Backup.data=${data}`);
  }).catch((err: BusinessError) => {
    console.error(`Failed to delete Backup.code is ${err.code},message is ${err.message}`);
  })
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### startTransaction

startTransaction(callback: AsyncCallback&lt;void&gt;): void

启动SingleKVStore数据库中的事务，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                  | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                             |
| ------------ | ---------------------------------------- |
| 15100005     | Database or result set already closed.   |

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function putBatchString(len: number, prefix: string) {
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < len; i++) {
    let entry: distributedKVStore.Entry = {
      key: prefix + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  return entries;
} //自定义函数，放置在作用域最外侧，防止语法检查报错

try {
  let count = 0;
  kvStore.on('dataChange', 0, (data) => {
    console.info(`startTransaction 0 ${data}`);
    count++;
  });
  kvStore.startTransaction(async (err) => {
    if (err != undefined) {
      console.error(`Failed to start Transaction.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in starting Transaction');
    let entries = putBatchString(10, 'batch_test_string_key');
    console.info(`entries: ${entries}`);
    if (kvStore != null) {
      kvStore.putBatch(entries, async (err) => {
        if (err != undefined) {
          console.error(`Failed to put batch.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in putting Batch');
      });
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to start Transaction.code is ${error.code},message is ${error.message}`);
}
```

### startTransaction

startTransaction(): Promise&lt;void&gt;

启动SingleKVStore数据库中的事务，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                             |
| ------------ | ---------------------------------------- |
| 15100005     | Database or result set already closed.   |

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let count = 0;
  kvStore.on('dataChange', distributedKVStore.SubscribeType.SUBSCRIBE_TYPE_ALL, (data) => {
    console.info(`startTransaction 0 ${data}`);
    count++;
  });
  kvStore.startTransaction().then(async () => {
    console.info('Succeeded in starting Transaction');
  }).catch((err: BusinessError) => {
    console.error(`Failed to start Transaction.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to start Transaction.code is ${error.code},message is ${error.message}`);
}
```

### commit

commit(callback: AsyncCallback&lt;void&gt;): void

提交SingleKVStore数据库中的事务，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                  | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  kvStore.commit((err) => {
    if (err == undefined) {
      console.info('Succeeded in committing');
    } else {
      console.error(`Failed to commit.code is ${err.code},message is ${err.message}`);
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### commit

commit(): Promise&lt;void&gt;

提交SingleKVStore数据库中的事务，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  kvStore.commit().then(async () => {
    console.info('Succeeded in committing');
  }).catch((err: BusinessError) => {
    console.error(`Failed to commit.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### rollback

rollback(callback: AsyncCallback&lt;void&gt;): void

在SingleKVStore数据库中回滚事务，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                  | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  kvStore.rollback((err) => {
    if (err == undefined) {
      console.info('Succeeded in rolling back');
    } else {
      console.error(`Failed to rollback.code is ${err.code},message is ${err.message}`);
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### rollback

rollback(): Promise&lt;void&gt;

在SingleKVStore数据库中回滚事务，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  kvStore.rollback().then(async () => {
    console.info('Succeeded in rolling back');
  }).catch((err: BusinessError) => {
    console.error(`Failed to rollback.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### enableSync

enableSync(enabled: boolean, callback: AsyncCallback&lt;void&gt;): void

设定是否开启同步，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                  | 必填 | 说明                                                      |
| -------- | ------------------------- | ---- | --------------------------------------------------------- |
| enabled  | boolean                   | 是   | 设定是否开启同步，true表示开启同步，false表示不启用同步。 |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。                                                |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  kvStore.enableSync(true, (err) => {
    if (err == undefined) {
      console.info('Succeeded in enabling sync');
    } else {
      console.error(`Failed to enable sync.code is ${err.code},message is ${err.message}`);
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### enableSync

enableSync(enabled: boolean): Promise&lt;void&gt;

设定是否开启同步，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名  | 类型 | 必填 | 说明                                                      |
| ------- | -------- | ---- | --------------------------------------------------------- |
| enabled | boolean  | 是   | 设定是否开启同步，true表示开启同步，false表示不启用同步。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  kvStore.enableSync(true).then(() => {
    console.info('Succeeded in enabling sync');
  }).catch((err: BusinessError) => {
    console.error(`Failed to enable sync.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### setSyncRange

setSyncRange(localLabels: string[], remoteSupportLabels: string[], callback: AsyncCallback&lt;void&gt;): void

设置同步范围标签，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名              | 类型                  | 必填 | 说明                             |
| ------------------- | ------------------------- | ---- | -------------------------------- |
| localLabels         | string[]                  | 是   | 表示本地设备的同步标签。         |
| remoteSupportLabels | string[]                  | 是   | 表示要同步数据的设备的同步标签。 |
| callback            | AsyncCallback&lt;void&gt; | 是   | 回调函数。                       |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  const localLabels = ['A', 'B'];
  const remoteSupportLabels = ['C', 'D'];
  kvStore.setSyncRange(localLabels, remoteSupportLabels, (err) => {
    if (err != undefined) {
      console.error(`Failed to set syncRange.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in setting syncRange');
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### setSyncRange

setSyncRange(localLabels: string[], remoteSupportLabels: string[]): Promise&lt;void&gt;

设置同步范围标签，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名              | 类型 | 必填 | 说明                             |
| ------------------- | -------- | ---- | -------------------------------- |
| localLabels         | string[] | 是   | 表示本地设备的同步标签。         |
| remoteSupportLabels | string[] | 是   | 表示要同步数据的设备的同步标签。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  const localLabels = ['A', 'B'];
  const remoteSupportLabels = ['C', 'D'];
  kvStore.setSyncRange(localLabels, remoteSupportLabels).then(() => {
    console.info('Succeeded in setting syncRange');
  }).catch((err: BusinessError) => {
    console.error(`Failed to set syncRange.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### setSyncParam

setSyncParam(defaultAllowedDelayMs: number, callback: AsyncCallback&lt;void&gt;): void

设置数据库同步允许的默认延迟，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名                | 类型                  | 必填 | 说明                                         |
| --------------------- | ------------------------- | ---- | -------------------------------------------- |
| defaultAllowedDelayMs | number                    | 是   | 表示数据库同步允许的默认延迟，以毫秒为单位。 |
| callback              | AsyncCallback&lt;void&gt; | 是   | 回调函数。                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  const defaultAllowedDelayMs = 500;
  kvStore.setSyncParam(defaultAllowedDelayMs, (err) => {
    if (err != undefined) {
      console.error(`Failed to set syncParam.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in setting syncParam');
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### setSyncParam

setSyncParam(defaultAllowedDelayMs: number): Promise&lt;void&gt;

设置数据库同步允许的默认延迟，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名                | 类型 | 必填 | 说明                                         |
| --------------------- | -------- | ---- | -------------------------------------------- |
| defaultAllowedDelayMs | number   | 是   | 表示数据库同步允许的默认延迟，以毫秒为单位。 |

**返回值：**

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  const defaultAllowedDelayMs = 500;
  kvStore.setSyncParam(defaultAllowedDelayMs).then(() => {
    console.info('Succeeded in setting syncParam');
  }).catch((err: BusinessError) => {
    console.error(`Failed to set syncParam.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### sync

sync(deviceIds: string[], mode: SyncMode, delayMs?: number): void

在手动同步方式下，触发数据库同步。关于键值型数据库的同步方式说明，请见[键值型数据库跨设备数据同步](../../database/data-sync-of-kv-store.md)。
> **说明：** 
>
> 其中deviceIds为[DeviceBasicInfo](js-apis-distributedDeviceManager.md#devicebasicinfo)中的networkId, 通过调用[deviceManager.getAvailableDeviceListSync](js-apis-distributedDeviceManager.md#getavailabledevicelistsync)方法得到。

**需要权限**： ohos.permission.DISTRIBUTED_DATASYNC。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名    | 类型              | 必填 | 说明                                           |
| --------- | --------------------- | ---- | ---------------------------------------------- |
| deviceIds | string[]              | 是   | 同一组网环境下，需要同步的设备的networkId列表。 |
| mode      | [SyncMode](#syncmode) | 是   | 同步模式。                                     |
| delayMs   | number                | 否   | 可选参数，允许延时时间，单位：ms（毫秒），默认为0。     |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**        |
| ------------ | ------------------- |
| 15100003     | Database corrupted. |
| 15100004     | Not found.          |

**示例：**

```ts
import deviceManager from '@ohos.distributedDeviceManager';
import UIAbility from '@ohos.app.ability.UIAbility';
import { BusinessError } from '@ohos.base';

let devManager: deviceManager.DeviceManager;
const KEY_TEST_SYNC_ELEMENT = 'key_test_sync';
const VALUE_TEST_SYNC_ELEMENT = 'value-string-001';
// create deviceManager
export default class EntryAbility extends UIAbility {
  onCreate() {
    let context = this.context;
    try {
      devManager = deviceManager.createDeviceManager(context.applicationInfo.name);
      let deviceIds: string[] = [];
      if (devManager != null) {
        let devices = devManager.getAvailableDeviceListSync();
        for (let i = 0; i < devices.length; i++) {
          deviceIds[i] = devices[i].networkId as string;
        }
      }
      try {
        if (kvStore != null) {
          kvStore.on('syncComplete', (data) => {
            console.info('Sync dataChange');
          });
          if (kvStore != null) {
            kvStore.put(KEY_TEST_SYNC_ELEMENT + 'testSync101', VALUE_TEST_SYNC_ELEMENT, (err) => {
              if (err != undefined) {
                console.error(`Failed to sync.code is ${err.code},message is ${err.message}`);
                return;
              }
              console.info('Succeeded in putting data');
              const mode = distributedKVStore.SyncMode.PULL_ONLY;
              if (kvStore != null) {
                kvStore.sync(deviceIds, mode, 1000);
              }
            });
          }
        }
      } catch (e) {
        let error = e as BusinessError;
        console.error(`Failed to sync.code is ${error.code},message is ${error.message}`);
      }

    } catch (err) {
      let error = err as BusinessError;
      console.error("createDeviceManager errCode:" + error.code + ",errMessage:" + error.message);
    }
  }
}
```

### sync

sync(deviceIds: string[], query: Query, mode: SyncMode, delayMs?: number): void

在手动同步方式下，触发数据库同步，此方法为同步方法。关于键值型数据库的同步方式说明，请见[键值型数据库跨设备数据同步](../../database/data-sync-of-kv-store.md)。
> **说明：** 
>
> 其中deviceIds为[DeviceBasicInfo](js-apis-distributedDeviceManager.md#devicebasicinfo)中的networkId, 通过调用[deviceManager.getAvailableDeviceListSync](js-apis-distributedDeviceManager.md#getavailabledevicelistsync)方法得到。

**需要权限**： ohos.permission.DISTRIBUTED_DATASYNC。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名    | 类型              | 必填 | 说明                                           |
| --------- | --------------------- | ---- | ---------------------------------------------- |
| deviceIds | string[]              | 是   | 同一组网环境下，需要同步的设备的networkId列表。 |
| mode      | [SyncMode](#syncmode) | 是   | 同步模式。                                     |
| query     | [Query](#query)        | 是   | 表示数据库的查询谓词条件                       |
| delayMs   | number                | 否   | 可选参数，允许延时时间，单位：ms（毫秒），默认为0。     |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**        |
| ------------ | ------------------- |
| 15100003     | Database corrupted. |
| 15100004     | Not found.          |

**示例：**

```ts
import deviceManager from '@ohos.distributedDeviceManager';
import UIAbility from '@ohos.app.ability.UIAbility';
import { BusinessError } from '@ohos.base';

let devManager: deviceManager.DeviceManager;
const KEY_TEST_SYNC_ELEMENT = 'key_test_sync';
const VALUE_TEST_SYNC_ELEMENT = 'value-string-001';
// create deviceManager
export default class EntryAbility extends UIAbility {
  onCreate() {
    let context = this.context;
    try {
      let devManager = deviceManager.createDeviceManager(context.applicationInfo.name);
      let deviceIds: string[] = [];
      if (devManager != null) {
        let devices = devManager.getAvailableDeviceListSync();
        for (let i = 0; i < devices.length; i++) {
          deviceIds[i] = devices[i].networkId as string;
        }
      }
      try {
        if (kvStore != null) {
          kvStore.on('syncComplete', (data) => {
            console.info('Sync dataChange');
          });
          if (kvStore != null) {
            kvStore.put(KEY_TEST_SYNC_ELEMENT + 'testSync101', VALUE_TEST_SYNC_ELEMENT, (err) => {
              if (err != undefined) {
                console.error(`Failed to sync.code is ${err.code},message is ${err.message}`);
                return;
              }
              console.info('Succeeded in putting data');
              const mode = distributedKVStore.SyncMode.PULL_ONLY;
              const query = new distributedKVStore.Query();
              query.prefixKey("batch_test");
              query.deviceId(devManager.getLocalDeviceNetworkId());
              if (kvStore != null) {
                kvStore.sync(deviceIds, query, mode, 1000);
              }
            });
          }
        }
      } catch (e) {
        let error = e as BusinessError;
        console.error(`Failed to sync.code is ${error.code},message is ${error.message}`);
      }

    } catch (err) {
      let error = err as BusinessError;
      console.error("createDeviceManager errCode:" + error.code + ",errMessage:" + error.message);
    }
  }
}
```

### on('dataChange')

on(event: 'dataChange', type: SubscribeType, listener: Callback&lt;ChangeNotification&gt;): void

订阅指定类型的数据变更通知。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                                                  | 必填 | 说明                                                 |
| -------- | --------------------------------------------------------- | ---- | ---------------------------------------------------- |
| event    | string                                                    | 是   | 订阅的事件名，固定为'dataChange'，表示数据变更事件。 |
| type     | [SubscribeType](#subscribetype)                           | 是   | 表示订阅的类型。                                     |
| listener | Callback&lt;[ChangeNotification](#changenotification)&gt; | 是   | 回调函数。                                           |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100001     | Over max  limits.                      |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  kvStore.on('dataChange', distributedKVStore.SubscribeType.SUBSCRIBE_TYPE_LOCAL, (data) => {
    console.info(`dataChange callback call data: ${data}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### on('syncComplete')

on(event: 'syncComplete', syncCallback: Callback&lt;Array&lt;[string, number]&gt;&gt;): void

订阅同步完成事件回调通知。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名       | 类型                                      | 必填 | 说明                                                   |
| ------------ | --------------------------------------------- | ---- | ------------------------------------------------------ |
| event        | string                                        | 是   | 订阅的事件名，固定为'syncComplete'，表示同步完成事件。 |
| syncCallback | Callback&lt;Array&lt;[string, number]&gt;&gt; | 是   | 回调函数。用于向调用方发送同步结果的回调。             |

**示例：**

```ts
import { BusinessError } from '@ohos.base';


const KEY_TEST_FLOAT_ELEMENT = 'key_test_float';
const VALUE_TEST_FLOAT_ELEMENT = 321.12;
try {
  kvStore.on('syncComplete', (data) => {
    console.info(`syncComplete ${data}`);
  });
  kvStore.put(KEY_TEST_FLOAT_ELEMENT, VALUE_TEST_FLOAT_ELEMENT).then(() => {
    console.info('succeeded in putting');
  }).catch((err: BusinessError) => {
    console.error(`Failed to put.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to subscribe syncComplete.code is ${error.code},message is ${error.message}`);
}
```

### off('dataChange')

off(event:'dataChange', listener?: Callback&lt;ChangeNotification&gt;): void

取消订阅数据变更通知。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                                                  | 必填 | 说明                                                     |
| -------- | --------------------------------------------------------- | ---- | -------------------------------------------------------- |
| event    | string                                                    | 是   | 取消订阅的事件名，固定为'dataChange'，表示数据变更事件。 |
| listener | Callback&lt;[ChangeNotification](#changenotification)&gt; | 否   | 取消订阅的函数。如不设置callback，则取消所有已订阅的函数。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

class KvstoreModel {
  call(data: distributedKVStore.ChangeNotification) {
    console.info(`dataChange : ${data}`);
  }

  subscribeDataChange() {
    try {
      if (kvStore != null) {
        kvStore.on('dataChange', distributedKVStore.SubscribeType.SUBSCRIBE_TYPE_REMOTE, this.call);
      }
    } catch (err) {
      let error = err as BusinessError;
      console.error(`Failed to subscribeDataChange.code is ${error.code},message is ${error.message}`);
    }
  }

  unsubscribeDataChange() {
    try {
      if (kvStore != null) {
        kvStore.off('dataChange', this.call);
      }
    } catch (err) {
      let error = err as BusinessError;
      console.error(`Failed to unsubscribeDataChange.code is ${error.code},message is ${error.message}`);
    }
  }
}
```

### off('syncComplete')

off(event: 'syncComplete', syncCallback?: Callback&lt;Array&lt;[string, number]&gt;&gt;): void

取消订阅同步完成事件回调通知。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名       | 类型                                      | 必填 | 说明                                                       |
| ------------ | --------------------------------------------- | ---- | ---------------------------------------------------------- |
| event        | string                                        | 是   | 取消订阅的事件名，固定为'syncComplete'，表示同步完成事件。 |
| syncCallback | Callback&lt;Array&lt;[string, number]&gt;&gt; | 否   | 取消订阅的函数。如不设置callback，则取消所有已订阅的函数。  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

class KvstoreModel {
  call(data: [string, number][]) {
    console.info(`syncComplete : ${data}`);
  }

  subscribeDataChange() {
    try {
      if (kvStore != null) {
        kvStore.on('syncComplete', this.call);
      }
    } catch (err) {
      let error = err as BusinessError;
      console.error(`Failed to subscribeDataChange.code is ${error.code},message is ${error.message}`);
    }
  }

  unsubscribeDataChange() {
    try {
      if (kvStore != null) {
        kvStore.off('syncComplete', this.call);
      }
    } catch (err) {
      let error = err as BusinessError;
      console.error(`Failed to unsubscribeDataChange.code is ${error.code},message is ${error.message}`);
    }
  } 
}
```

### getSecurityLevel

getSecurityLevel(callback: AsyncCallback&lt;SecurityLevel&gt;): void

获取数据库的安全级别，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                                             | 必填 | 说明                             |
| -------- | ---------------------------------------------------- | ---- | -------------------------------- |
| callback | AsyncCallback&lt;[SecurityLevel](#securitylevel)&gt; | 是   | 回调函数。返回数据库的安全级别。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  kvStore.getSecurityLevel((err, data) => {
    if (err != undefined) {
      console.error(`Failed to get SecurityLevel.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in getting securityLevel');
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### getSecurityLevel

getSecurityLevel(): Promise&lt;SecurityLevel&gt;

获取数据库的安全级别，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**返回值：**

| 类型                                           | 说明                                |
| ---------------------------------------------- | ----------------------------------- |
| Promise&lt;[SecurityLevel](#securitylevel)&gt; | Promise对象。返回数据库的安全级别。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  kvStore.getSecurityLevel().then((data) => {
    console.info('Succeeded in getting securityLevel');
  }).catch((err: BusinessError) => {
    console.error(`Failed to get SecurityLevel.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

## DeviceKVStore

设备协同数据库，继承自SingleKVStore，提供查询数据和同步数据的方法。

设备协同数据库，以设备维度对数据进行区分，每台设备仅能写入和修改本设备的数据，其它设备的数据对其是只读的，无法修改其它设备的数据。

比如，可以使用设备协同数据库实现设备间的图片分享，可以查看其他设备的图片，但无法修改和删除其他设备的图片。

在调用DeviceKVStore的方法前，需要先通过[getKVStore](#getkvstore)构建一个DeviceKVStore实例。

### get

get(key: string, callback: AsyncCallback&lt;boolean | string | number | Uint8Array&gt;): void

获取本设备指定键的值，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| key      | string                                                       | 是   | 要查询数据的key，不能为空且长度不大于[MAX_KEY_LENGTH](#constants)。 |
| callback | AsyncCallback&lt;boolean \| string \| number \| Uint8Array&gt; | 是   | 回调函数。返回获取查询的值。                                 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100004     | Not found.                             |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

const KEY_TEST_STRING_ELEMENT = 'key_test_string';
const VALUE_TEST_STRING_ELEMENT = 'value-test-string';
try {
  kvStore.put(KEY_TEST_STRING_ELEMENT, VALUE_TEST_STRING_ELEMENT, (err) => {
    if (err != undefined) {
      console.error(`Failed to put.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info("Succeeded in putting");
    if (kvStore != null) {
      kvStore.get(KEY_TEST_STRING_ELEMENT, (err, data) => {
        if (err != undefined) {
          console.error(`Failed to get.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info(`Succeeded in getting data.data=${data}`);
      });
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to get.code is ${error.code},message is ${error.message}`);
}
```

### get

get(key: string): Promise&lt;boolean | string | number | Uint8Array&gt;

获取本设备指定键的值，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| key    | string | 是   | 要查询数据的key，不能为空且长度不大于[MAX_KEY_LENGTH](#constants)。 |

**返回值：**

| 类型                                                     | 说明                            |
| -------------------------------------------------------- | ------------------------------- |
| Promise&lt;Uint8Array \| string \| boolean \| number&gt; | Promise对象。返回获取查询的值。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100004     | Not found.                             |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

const KEY_TEST_STRING_ELEMENT = 'key_test_string';
const VALUE_TEST_STRING_ELEMENT = 'value-test-string';
try {
  kvStore.put(KEY_TEST_STRING_ELEMENT, VALUE_TEST_STRING_ELEMENT).then(() => {
    console.info(`Succeeded in putting data`);
    if (kvStore != null) {
      kvStore.get(KEY_TEST_STRING_ELEMENT).then((data) => {
        console.info(`Succeeded in getting data.data=${data}`);
      }).catch((err: BusinessError) => {
        console.error(`Failed to get.code is ${err.code},message is ${err.message}`);
      });
    }
  }).catch((err: BusinessError) => {
    console.error(`Failed to put.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to get.code is ${error.code},message is ${error.message}`);
}
```

### get

get(deviceId: string, key: string, callback: AsyncCallback&lt;boolean | string | number | Uint8Array&gt;): void

获取与指定设备ID和key匹配的string值，使用callback异步回调。
> **说明：** 
>
> 其中deviceId通过调用[deviceManager.getAvailableDeviceListSync](js-apis-distributedDeviceManager.md#getavailabledevicelistsync)方法得到。
> deviceId具体获取方式请参考[sync接口示例](#sync)。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**参数：**

| 参数名  | 类型 | 必填  | 说明                    |
| -----  | ------   | ----  | ----------------------- |
| deviceId  |string  | 是    |标识要查询其数据的设备。    |
| key       |string  | 是    |表示要查询key值的键。    |
| callback  |AsyncCallback&lt;boolean\|string\|number\|Uint8Array&gt;  | 是    |回调函数，返回匹配给定条件的字符串值。    |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100004     | Not found.                             |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

const KEY_TEST_STRING_ELEMENT = 'key_test_string_2';
const VALUE_TEST_STRING_ELEMENT = 'value-string-002';
try {
  kvStore.put(KEY_TEST_STRING_ELEMENT, VALUE_TEST_STRING_ELEMENT, async (err) => {
    if (err != undefined) {
      console.error(`Failed to put.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in putting');
    if (kvStore != null) {
      kvStore.get('localDeviceId', KEY_TEST_STRING_ELEMENT, (err, data) => {
        if (err != undefined) {
          console.error(`Failed to get.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in getting');
      });
    }
  })
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to get.code is ${error.code},message is ${error.message}`);
}
```

### get

get(deviceId: string, key: string): Promise&lt;boolean | string | number | Uint8Array&gt;

获取与指定设备ID和key匹配的string值，使用Promise异步回调。
> **说明：** 
>
> 其中deviceId通过调用[deviceManager.getAvailableDeviceListSync](js-apis-distributedDeviceManager.md#getavailabledevicelistsync)方法得到。
> deviceId具体获取方式请参考[sync接口示例](#sync)。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**参数：**

| 参数名   | 类型 | 必填 | 说明                     |
| -------- | -------- | ---- | ------------------------ |
| deviceId | string   | 是   | 标识要查询其数据的设备。 |
| key      | string   | 是   | 表示要查询key值的键。    |

**返回值：**

| 类型    | 说明       |
| ------  | -------   |
|Promise&lt;boolean\|string\|number\|Uint8Array&gt; |Promise对象。返回匹配给定条件的字符串值。|

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100004     | Not found.                             |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

const KEY_TEST_STRING_ELEMENT = 'key_test_string_2';
const VALUE_TEST_STRING_ELEMENT = 'value-string-002';
try {
  kvStore.put(KEY_TEST_STRING_ELEMENT, VALUE_TEST_STRING_ELEMENT).then(async () => {
    console.info('Succeeded in putting');
    if (kvStore != null) {
      kvStore.get('localDeviceId', KEY_TEST_STRING_ELEMENT).then((data) => {
        console.info('Succeeded in getting');
      }).catch((err: BusinessError) => {
        console.error(`Failed to get.code is ${err.code},message is ${err.message}`);
      });
    }
  }).catch((error: BusinessError) => {
    console.error(`Failed to put.code is ${error.code},message is ${error.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to get.code is ${error.code},message is ${error.message}`);
}
```

### getEntries

getEntries(keyPrefix: string, callback: AsyncCallback&lt;Entry[]&gt;): void

获取匹配本设备指定键前缀的所有键值对，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名    | 类型                                   | 必填 | 说明                                     |
| --------- | -------------------------------------- | ---- | ---------------------------------------- |
| keyPrefix | string                                 | 是   | 表示要匹配的键前缀。                     |
| callback  | AsyncCallback&lt;[Entry](#entry)[]&gt; | 是   | 回调函数。返回匹配指定前缀的键值对列表。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  console.info(`entries: ${entries}`);
  kvStore.putBatch(entries, async (err) => {
    if (err != undefined) {
      console.error(`Failed to put Batch.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in putting Batch');
    if (kvStore != null) {
      kvStore.getEntries('batch_test_string_key', (err, entries) => {
        if (err != undefined) {
          console.error(`Failed to get Entries.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in getting Entries');
        console.info(`entries.length: ${entries.length}`);
        console.info(`entries[0]: ${entries[0]}`);
      });
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message} `);
}
```

### getEntries

getEntries(keyPrefix: string): Promise&lt;Entry[]&gt;

获取匹配本设备指定键前缀的所有键值对，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名    | 类型   | 必填 | 说明                 |
| --------- | ------ | ---- | -------------------- |
| keyPrefix | string | 是   | 表示要匹配的键前缀。 |

**返回值：**

| 类型                             | 说明                                        |
| -------------------------------- | ------------------------------------------- |
| Promise&lt;[Entry](#entry)[]&gt; | Promise对象。返回匹配指定前缀的键值对列表。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  console.info(`entries: ${entries}`);
  kvStore.putBatch(entries).then(async () => {
    console.info('Succeeded in putting Batch');
    if (kvStore != null) {
      kvStore.getEntries('batch_test_string_key').then((entries) => {
        console.info('Succeeded in getting Entries');
        console.info(`PutBatch ${entries}`);
      }).catch((err: BusinessError) => {
        console.error(`Failed to get Entries.code is ${err.code},message is ${err.message}`);
      });
    }
  }).catch((err: BusinessError) => {
    console.error(`Failed to put Batch.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message} `);
}
```

### getEntries

getEntries(deviceId: string, keyPrefix: string, callback: AsyncCallback&lt;Entry[]&gt;): void

获取与指定设备ID和key前缀匹配的所有键值对，使用callback异步回调。
> **说明：** 
>
> 其中deviceId通过调用[deviceManager.getAvailableDeviceListSync](js-apis-distributedDeviceManager.md#getavailabledevicelistsync)方法得到。
> deviceId具体获取方式请参考[sync接口示例](#sync)。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**参数：**

| 参数名    | 类型                               | 必填 | 说明                                           |
| --------- | -------------------------------------- | ---- | ---------------------------------------------- |
| deviceId  | string                                 | 是   | 标识要查询其数据的设备。                       |
| keyPrefix | string                                 | 是   | 表示要匹配的键前缀。                           |
| callback  | AsyncCallback&lt;[Entry](#entry)[]&gt; | 是   | 回调函数，返回满足给定条件的所有键值对的列表。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  console.info(`entries : ${entries}`);
  kvStore.putBatch(entries, async (err) => {
    if (err != undefined) {
      console.error(`Failed to put batch.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in putting batch');
    if (kvStore != null) {
      kvStore.getEntries('localDeviceId', 'batch_test_string_key', (err, entries) => {
        if (err != undefined) {
          console.error(`Failed to get entries.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in getting entries');
        console.info(`entries.length: ${entries.length}`);
        console.info(`entries[0]: ${entries[0]}`);
      });
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to put batch.code is ${error.code},message is ${error.message}`);
}
```

### getEntries

getEntries(deviceId: string, keyPrefix: string): Promise&lt;Entry[]&gt;

获取与指定设备ID和key前缀匹配的所有键值对，使用Promise异步回调。
> **说明：** 
>
> 其中deviceId通过调用[deviceManager.getAvailableDeviceListSync](js-apis-distributedDeviceManager.md#getavailabledevicelistsync)方法得到。
> deviceId具体获取方式请参考[sync接口示例](#sync)。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**参数：**

| 参数名    | 类型 | 必填 | 说明                     |
| --------- | -------- | ---- | ------------------------ |
| deviceId  | string   | 是   | 标识要查询其数据的设备。 |
| keyPrefix | string   | 是   | 表示要匹配的键前缀。     |

**返回值：**

| 类型                             | 说明                                              |
| -------------------------------- | ------------------------------------------------- |
| Promise&lt;[Entry](#entry)[]&gt; | Promise对象。返回匹配给定条件的所有键值对的列表。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  console.info(`entries: ${entries}`);
  kvStore.putBatch(entries).then(async () => {
    console.info('Succeeded in putting batch');
    if (kvStore != null) {
      kvStore.getEntries('localDeviceId', 'batch_test_string_key').then((entries) => {
        console.info('Succeeded in getting entries');
        console.info(`entries.length: ${entries.length}`);
        console.info(`entries[0]: ${entries[0]}`);
        console.info(`entries[0].value: ${entries[0].value}`);
        console.info(`entries[0].value.value: ${entries[0].value.value}`);
      }).catch((err: BusinessError) => {
        console.error(`Failed to get entries.code is ${err.code},message is ${err.message}`);
      });
    }
  }).catch((err: BusinessError) => {
    console.error(`Failed to put batch.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to put batch.code is ${error.code},message is ${error.message}`);
}
```

### getEntries

getEntries(query: Query, callback: AsyncCallback&lt;Entry[]&gt;): void

获取本设备与指定Query对象匹配的键值对列表，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                                   | 必填 | 说明                                                  |
| -------- | -------------------------------------- | ---- | ----------------------------------------------------- |
| query    | [Query](#query)                         | 是   | 表示要匹配的键前缀。                                  |
| callback | AsyncCallback&lt;[Entry](#entry)[]&gt; | 是   | 回调函数。返回本设备与指定Query对象匹配的键值对列表。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let arr = new Uint8Array([21, 31]);
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_bool_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.BYTE_ARRAY,
        value: arr
      }
    }
    entries.push(entry);
  }
  console.info(`entries: {entries}`);
  kvStore.putBatch(entries, async (err) => {
    console.info('Succeeded in putting Batch');
    const query = new distributedKVStore.Query();
    query.prefixKey("batch_test");
    if (kvStore != null) {
      kvStore.getEntries(query, (err, entries) => {
        if (err != undefined) {
          console.error(`Failed to get Entries.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in getting Entries');
        console.info(`entries.length: ${entries.length}`);
        console.info(`entries[0]: ${entries[0]}`);
      });
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to get Entries.code is ${error.code},message is ${error.message}`);
}
```

### getEntries

getEntries(query: Query): Promise&lt;Entry[]&gt;

获取本设备与指定Query对象匹配的键值对列表，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型           | 必填 | 说明           |
| ------ | -------------- | ---- | -------------- |
| query  | [Query](#query) | 是   | 表示查询对象。 |

**返回值：**

| 类型                             | 说明                                                     |
| -------------------------------- | -------------------------------------------------------- |
| Promise&lt;[Entry](#entry)[]&gt; | Promise对象。返回本设备与指定Query对象匹配的键值对列表。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let arr = new Uint8Array([21, 31]);
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_bool_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.BYTE_ARRAY,
        value: arr
      }
    }
    entries.push(entry);
  }
  console.info(`entries: {entries}`);
  kvStore.putBatch(entries).then(async () => {
    console.info('Succeeded in putting Batch');
    const query = new distributedKVStore.Query();
    query.prefixKey("batch_test");
    if (kvStore != null) {
      kvStore.getEntries(query).then((entries) => {
        console.info('Succeeded in getting Entries');
      }).catch((err: BusinessError) => {
        console.error(`Failed to get Entries.code is ${err.code},message is ${err.message}`);
      });
    }
  }).catch((err: BusinessError) => {
    console.error(`Failed to get Entries.code is ${err.code},message is ${err.message}`)
  });
  console.info('Succeeded in getting Entries');
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to get Entries.code is ${error.code},message is ${error.message}`);
}
```

### getEntries

getEntries(deviceId: string, query: Query, callback: AsyncCallback&lt;Entry[]&gt;): void

获取与指定设备ID和Query对象匹配的键值对列表，使用callback异步回调。
> **说明：** 
>
> 其中deviceId通过调用[deviceManager.getAvailableDeviceListSync](js-apis-distributedDeviceManager.md#getavailabledevicelistsync)方法得到。
> deviceId具体获取方式请参考[sync接口示例](#sync)。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**参数：**

| 参数名   | 类型                               | 必填 | 说明                                                    |
| -------- | -------------------------------------- | ---- | ------------------------------------------------------- |
| deviceId | string                                 | 是   | 键值对所属的设备ID。                                    |
| query    | [Query](#query)                         | 是   | 表示查询对象。                                          |
| callback | AsyncCallback&lt;[Entry](#entry)[]&gt; | 是   | 回调函数。返回与指定设备ID和Query对象匹配的键值对列表。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let arr = new Uint8Array([21, 31]);
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_bool_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.BYTE_ARRAY,
        value: arr
      }
    }
    entries.push(entry);
  }
  console.info(`entries: ${entries}`);
  kvStore.putBatch(entries, async (err) => {
    if (err != undefined) {
      console.error(`Failed to put batch.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in putting batch');
    let query = new distributedKVStore.Query();
    query.deviceId('localDeviceId');
    query.prefixKey("batch_test");
    if (kvStore != null) {
      kvStore.getEntries('localDeviceId', query, (err, entries) => {
        if (err != undefined) {
          console.error(`Failed to get entries.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in getting entries');
        console.info(`entries.length: ${entries.length}`);
        console.info(`entries[0]: ${entries[0]}`);
      })
    }
  });
  console.info('Succeeded in getting entries');
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to get entries.code is ${error.code},message is ${error.message}`);
}
```

### getEntries

getEntries(deviceId: string, query: Query): Promise&lt;Entry[]&gt;

获取与指定设备ID和Query对象匹配的键值对列表，使用Promise异步回调。
> **说明：** 
>
> 其中deviceId通过调用[deviceManager.getAvailableDeviceListSync](js-apis-distributedDeviceManager.md#getavailabledevicelistsync)方法得到。
> deviceId具体获取方式请参考[sync接口示例](#sync)。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**参数：**

| 参数名   | 类型       | 必填 | 说明                 |
| -------- | -------------- | ---- | -------------------- |
| deviceId | string         | 是   | 键值对所属的设备ID。 |
| query    | [Query](#query) | 是   | 表示查询对象。       |

**返回值：**

| 类型                             | 说明                                                       |
| -------------------------------- | ---------------------------------------------------------- |
| Promise&lt;[Entry](#entry)[]&gt; | Promise对象。返回与指定设备ID和Query对象匹配的键值对列表。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let arr = new Uint8Array([21, 31]);
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_bool_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.BYTE_ARRAY,
        value: arr
      }
    }
    entries.push(entry);
  }
  console.info(`entries: ${entries}`);
  kvStore.putBatch(entries).then(async () => {
    console.info('Succeeded in putting batch');
    let query = new distributedKVStore.Query();
    query.deviceId('localDeviceId');
    query.prefixKey("batch_test");
    if (kvStore != null) {
      kvStore.getEntries('localDeviceId', query).then((entries) => {
        console.info('Succeeded in getting entries');
      }).catch((err: BusinessError) => {
        console.error(`Failed to get entries.code is ${err.code},message is ${err.message}`);
      });
    }
  }).catch((err: BusinessError) => {
    console.error(`Failed to put batch.code is ${err.code},message is ${err.message}`);
  });
  console.info('Succeeded in getting entries');
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to get entries.code is ${error.code},message is ${error.message}`);
}
```

### getResultSet

getResultSet(keyPrefix: string, callback: AsyncCallback&lt;KVStoreResultSet&gt;): void

从DeviceKVStore数据库中获取本设备具有指定前缀的结果集，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名    | 类型                                                       | 必填 | 说明                                 |
| --------- | ---------------------------------------------------------- | ---- | ------------------------------------ |
| keyPrefix | string                                                     | 是   | 表示要匹配的键前缀。                 |
| callback  | AsyncCallback&lt;[KVStoreResultSet](#kvstoreresultset)&gt; | 是   | 回调函数。返回具有指定前缀的结果集。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100001     | Over max  limits.                      |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  kvStore.putBatch(entries, async (err) => {
    if (err != undefined) {
      console.error(`Failed to put batch.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in putting batch');
    if (kvStore != null) {
      kvStore.getResultSet('batch_test_string_key', async (err, result) => {
        if (err != undefined) {
          console.error(`Failed to get resultset.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in getting result set');
        resultSet = result;
        if (kvStore != null) {
          kvStore.closeResultSet(resultSet, (err) => {
            if (err != undefined) {
              console.error(`Failed to close resultset.code is ${err.code},message is ${err.message}`);
              return;
            }
            console.info('Succeeded in closing result set');
          })
        }
      });
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.message}`);
}
```

### getResultSet

getResultSet(keyPrefix: string): Promise&lt;KVStoreResultSet&gt;

从DeviceKVStore数据库中获取本设备具有指定前缀的结果集，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名    | 类型   | 必填 | 说明                 |
| --------- | ------ | ---- | -------------------- |
| keyPrefix | string | 是   | 表示要匹配的键前缀。 |

**返回值：**

| 类型                                                 | 说明                                    |
| ---------------------------------------------------- | --------------------------------------- |
| Promise&lt;[KVStoreResultSet](#kvstoreresultset)&gt; | Promise对象。返回具有指定前缀的结果集。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100001     | Over max  limits.                      |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  kvStore.putBatch(entries).then(async () => {
    console.info('Succeeded in putting batch');
  }).catch((err: BusinessError) => {
    console.error(`Failed to put batch.code is ${err.code},message is ${err.message}`);
  });
  kvStore.getResultSet('batch_test_string_key').then((result) => {
    console.info('Succeeded in getting result set');
    resultSet = result;
    if (kvStore != null) {
      kvStore.closeResultSet(resultSet).then(() => {
        console.info('Succeeded in closing result set');
      }).catch((err: BusinessError) => {
        console.error(`Failed to close resultset.code is ${err.code},message is ${err.message}`);
      });
    }
  }).catch((err: BusinessError) => {
    console.error(`Failed to get resultset.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.code}`);
}
```

### getResultSet

getResultSet(deviceId: string, keyPrefix: string, callback: AsyncCallback&lt;KVStoreResultSet&gt;): void

获取与指定设备ID和key前缀匹配的KVStoreResultSet对象，使用callback异步回调。
> **说明：** 
>
> 其中deviceId通过调用[deviceManager.getAvailableDeviceListSync](js-apis-distributedDeviceManager.md#getavailabledevicelistsync)方法得到。
> deviceId具体获取方式请参考[sync接口示例](#sync)。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**参数：**

| 参数名    | 类型                                                     | 必填 | 说明                                                         |
| --------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| deviceId  | string                                                       | 是   | 标识要查询其数据的设备。                                     |
| keyPrefix | string                                                       | 是   | 表示要匹配的键前缀。                                         |
| callback  | AsyncCallback&lt;[KVStoreResultSet](#kvstoreresultset)&gt; | 是   | 回调函数。返回与指定设备ID和key前缀匹配的KVStoreResultSet对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100001     | Over max  limits.                      |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  kvStore.getResultSet('localDeviceId', 'batch_test_string_key', async (err, result) => {
    if (err != undefined) {
      console.error(`Failed to get resultSet.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in getting resultSet');
    resultSet = result;
    if (kvStore != null) {
      kvStore.closeResultSet(resultSet, (err) => {
        if (err != undefined) {
          console.error(`Failed to close resultSet.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in closing resultSet');
      })
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to get resultSet.code is ${error.code},message is ${error.message}`);
}
```

### getResultSet

getResultSet(deviceId: string, keyPrefix: string): Promise&lt;KVStoreResultSet&gt;

获取与指定设备ID和key前缀匹配的KVStoreResultSet对象，使用Promise异步回调。
> **说明：** 
>
> 其中deviceId通过调用[deviceManager.getAvailableDeviceListSync](js-apis-distributedDeviceManager.md#getavailabledevicelistsync)方法得到。
> deviceId具体获取方式请参考[sync接口示例](#sync)。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**参数：**

| 参数名    | 类型 | 必填 | 说明                     |
| --------- | -------- | ---- | ------------------------ |
| deviceId  | string   | 是   | 标识要查询其数据的设备。 |
| keyPrefix | string   | 是   | 表示要匹配的键前缀。     |

**返回值：**

| 类型                                                   | 说明                                                         |
| ------------------------------------------------------ | ------------------------------------------------------------ |
| Promise&lt;[KVStoreResultSet](#kvstoreresultset)&gt; | Promise对象。返回与指定设备ID和key前缀匹配的KVStoreResultSet对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100001     | Over max  limits.                      |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  kvStore.getResultSet('localDeviceId', 'batch_test_string_key').then((result) => {
    console.info('Succeeded in getting resultSet');
    resultSet = result;
    if (kvStore != null) {
      kvStore.closeResultSet(resultSet).then(() => {
        console.info('Succeeded in closing resultSet');
      }).catch((err: BusinessError) => {
        console.error(`Failed to close resultSet.code is ${err.code},message is ${err.message}`);
      });
    }
  }).catch((err: BusinessError) => {
    console.error(`Failed to get resultSet.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to get resultSet.code is ${error.code},message is ${error.message}`);
}
```

### getResultSet

getResultSet(deviceId: string, query: Query, callback: AsyncCallback&lt;KVStoreResultSet&gt;): void

获取与指定设备ID和Query对象匹配的KVStoreResultSet对象，使用callback异步回调。
> **说明：** 
>
> 其中deviceId通过调用[deviceManager.getAvailableDeviceListSync](js-apis-distributedDeviceManager.md#getavailabledevicelistsync)方法得到。
> deviceId具体获取方式请参考[sync接口示例](#sync)。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**参数：**

| 参数名   | 类型                                                     | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| deviceId | string                                                       | 是   | KVStoreResultSet对象所属的设备ID。                           |
| query    | [Query](#query)                                               | 是   | 表示查询对象。                                               |
| callback | AsyncCallback&lt;[KVStoreResultSet](#kvstoreresultset)&gt; | 是   | 回调函数。返回与指定设备ID和Query对象匹配的KVStoreResultSet对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100001     | Over max  limits.                      |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  kvStore.putBatch(entries, async (err) => {
    if (err != undefined) {
      console.error(`Failed to put batch.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in putting batch');
    const query = new distributedKVStore.Query();
    query.prefixKey("batch_test");
    if (kvStore != null) {
      kvStore.getResultSet('localDeviceId', query, async (err, result) => {
        if (err != undefined) {
          console.error(`Failed to get resultSet.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in getting resultSet');
        resultSet = result;
        if (kvStore != null) {
          kvStore.closeResultSet(resultSet, (err) => {
            if (err != undefined) {
              console.error(`Failed to close resultSet.code is ${err.code},message is ${err.message}`);
              return;
            }
            console.info('Succeeded in closing resultSet');
          })
        }
      });
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to get resultSet.code is ${error.code},message is ${error.message}`);
}
```

### getResultSet

getResultSet(deviceId: string, query: Query): Promise&lt;KVStoreResultSet&gt;

获取与指定设备ID和Query对象匹配的KVStoreResultSet对象，使用Promise异步回调。
> **说明：** 
>
> 其中deviceId通过调用[deviceManager.getAvailableDeviceListSync](js-apis-distributedDeviceManager.md#getavailabledevicelistsync)方法得到。
> deviceId具体获取方式请参考[sync接口示例](#sync)。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**参数：**

| 参数名   | 类型       | 必填 | 说明                               |
| -------- | -------------- | ---- | ---------------------------------- |
| deviceId | string         | 是   | KVStoreResultSet对象所属的设备ID。 |
| query    | [Query](#query) | 是   | 表示查询对象。                     |

**返回值：**

| 类型                                                   | 说明                                                         |
| ------------------------------------------------------ | ------------------------------------------------------------ |
| Promise&lt;[KVStoreResultSet](#kvstoreresultset)&gt; | Promise对象。返回与指定设备ID和Query对象匹配的KVStoreResultSet对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100001     | Over max  limits.                      |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  kvStore.putBatch(entries).then(async () => {
    console.info('Succeeded in putting batch');
  }).catch((err: BusinessError) => {
    console.error(`Failed to put batch.code is ${err.code},message is ${err.message}`);
  });
  const query = new distributedKVStore.Query();
  query.prefixKey("batch_test");
  if (kvStore != null) {
    kvStore.getResultSet('localDeviceId', query).then((result) => {
      console.info('Succeeded in getting resultSet');
      resultSet = result;
      if (kvStore != null) {
        kvStore.closeResultSet(resultSet).then(() => {
          console.info('Succeeded in closing resultSet');
        }).catch((err: BusinessError) => {
          console.error(`Failed to close resultSet.code is ${err.code},message is ${err.message}`);
        });
      }
    }).catch((err: BusinessError) => {
      console.error(`Failed to get resultSet.code is ${err.code},message is ${err.message}`);
    });
  }
  query.deviceId('localDeviceId');
  console.info("GetResultSet " + query.getSqlLike());

} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to get resultSet.code is ${error.code},message is ${error.message}`);
}
```

### getResultSet

getResultSet(query: Query): Promise&lt;KVStoreResultSet&gt;

获取与本设备指定Query对象匹配的KVStoreResultSet对象，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型           | 必填 | 说明           |
| ------ | -------------- | ---- | -------------- |
| query  | [Query](#query) | 是   | 表示查询对象。 |

**返回值：**

| 类型                                                 | 说明                                                         |
| ---------------------------------------------------- | ------------------------------------------------------------ |
| Promise&lt;[KVStoreResultSet](#kvstoreresultset)&gt; | Promise对象。获取与本设备指定Query对象匹配的KVStoreResultSet对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100001     | Over max  limits.                      |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  kvStore.putBatch(entries).then(async () => {
    console.info('Succeeded in putting batch');
  }).catch((err: BusinessError) => {
    console.error(`Failed to put batch.code is ${err.code},message is ${err.message}`);
  });
  const query = new distributedKVStore.Query();
  query.prefixKey("batch_test");
  kvStore.getResultSet(query).then((result) => {
    console.info('Succeeded in getting result set');
    resultSet = result;
  }).catch((err: BusinessError) => {
    console.error(`Failed to get resultset.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.code}`);
}
```

### getResultSet

getResultSet(query: Query, callback:AsyncCallback&lt;KVStoreResultSet&gt;): void

获取与本设备指定Query对象匹配的KVStoreResultSet对象，使用callback异步回调。
> **说明：** 
>
> 其中deviceId通过调用[deviceManager.getAvailableDeviceListSync](js-apis-distributedDeviceManager.md#getavailabledevicelistsync)方法得到。
> deviceId具体获取方式请参考[sync接口示例](#sync)。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型           | 必填 | 说明                               |
| -------- | -------------- | ---- | ---------------------------------- |
| query    | [Query](#query) | 是   | 表示查询对象。                     |
| callback    | AsyncCallback&lt;[KVStoreResultSet](#kvstoreresultset)&gt; | 是   | 回调函数，获取与指定Predicates对象匹配的KVStoreResultSet对象。         |


**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100001     | Over max  limits.                      |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  kvStore.putBatch(entries, async (err) => {
    if (err != undefined) {
      console.error(`Failed to put batch.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in putting batch');
    const query = new distributedKVStore.Query();
    query.prefixKey("batch_test");
    if (kvStore != null) {
      kvStore.getResultSet(query, async (err, result) => {
        if (err != undefined) {
          console.error(`Failed to get resultSet.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in getting resultSet');
        resultSet = result;
        if (kvStore != null) {
          kvStore.closeResultSet(resultSet, (err) => {
            if (err != undefined) {
              console.error(`Failed to close resultSet.code is ${err.code},message is ${err.message}`);
              return;
            }
            console.info('Succeeded in closing resultSet');
          })
        }
      });
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to get resultSet.code is ${error.code},message is ${error.message}`);
}
```

### getResultSet

getResultSet(predicates: dataSharePredicates.DataSharePredicates, callback: AsyncCallback&lt;KVStoreResultSet&gt;): void

获取与本设备指定Predicate对象匹配的KVStoreResultSet对象，使用callback异步回调。

**模型约束：** 此接口仅可在Stage模型下使用

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.DistributedDataManager.DataShare.Provider

**参数：**

| 参数名     | 类型                                                         | 必填 | 说明                                                         |
| ---------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| predicates | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md#datasharepredicates) | 是   | 指示筛选条件,当此参数为null时，应定义处理逻辑。              |
| callback   | AsyncCallback&lt;[KVStoreResultSet](#kvstoreresultset)&gt;   | 是   | 回调函数，获取与指定Predicates对象匹配的KVStoreResultSet对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100001     | Over max  limits.                      |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let predicates = new dataSharePredicates.DataSharePredicates();
  predicates.prefixKey("batch_test_string_key");
  kvStore.getResultSet(predicates, async (err, result) => {
    if (err != undefined) {
      console.error(`Failed to get resultset.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in getting result set');
    resultSet = result;
    if (kvStore != null) {
      kvStore.closeResultSet(resultSet, (err) => {
        if (err != undefined) {
          console.error(`Failed to close resultset.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in closing result set');
      })
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.code}`);
}
```

### getResultSet

getResultSet(predicates: dataSharePredicates.DataSharePredicates): Promise&lt;KVStoreResultSet&gt;

获取与本设备指定Predicate对象匹配的KVStoreResultSet对象，使用Promise异步回调。

**模型约束：** 此接口仅可在Stage模型下使用

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.DistributedDataManager.DataShare.Provider

**参数：**

| 参数名     | 类型                                                         | 必填 | 说明                                            |
| ---------- | ------------------------------------------------------------ | ---- | ----------------------------------------------- |
| predicates | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md#datasharepredicates) | 是   | 指示筛选条件,当此参数为null时，应定义处理逻辑。 |

**返回值：**

| 类型                                                 | 说明                      |
| ---------------------------------------------------- | ------------------------- |
| Promise&lt;[KVStoreResultSet](#kvstoreresultset)&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100001     | Over max  limits.                      |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let predicates = new dataSharePredicates.DataSharePredicates();
  predicates.prefixKey("batch_test_string_key");
  kvStore.getResultSet(predicates).then((result) => {
    console.info('Succeeded in getting result set');
    resultSet = result;
    if (kvStore != null) {
      kvStore.closeResultSet(resultSet).then(() => {
        console.info('Succeeded in closing result set');
      }).catch((err: BusinessError) => {
        console.error(`Failed to close resultset.code is ${err.code},message is ${err.message}`);
      });
    }
  }).catch((err: BusinessError) => {
    console.error(`Failed to get resultset.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.code}`);
}
```

### getResultSet

getResultSet(deviceId: string, predicates: dataSharePredicates.DataSharePredicates, callback: AsyncCallback&lt;KVStoreResultSet&gt;): void

获取与指定Predicate对象匹配的KVStoreResultSet对象，使用callback异步回调。
> **说明：** 
>
> 其中deviceId通过调用[deviceManager.getAvailableDeviceListSync](js-apis-distributedDeviceManager.md#getavailabledevicelistsync)方法得到。
> deviceId具体获取方式请参考[sync接口示例](#sync)。

**模型约束：** 此接口仅可在Stage模型下使用

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.DistributedDataManager.DataShare.Provider

**参数：**

| 参数名     | 类型                                                     | 必填 | 说明                                                         |
| ---------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| deviceId  | string                                                       | 是   | 标识要查询其数据的设备。                                     |
| predicates | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md#datasharepredicates) | 是   | 指示筛选条件,当此参数为null时，应定义处理逻辑。              |
| callback   | AsyncCallback&lt;[KVStoreResultSet](#kvstoreresultset)&gt;   | 是   | 回调函数，获取与指定Predicates对象匹配的KVStoreResultSet对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100001     | Over max  limits.                      |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let predicates = new dataSharePredicates.DataSharePredicates();
  predicates.prefixKey("batch_test_string_key");
  kvStore.getResultSet('localDeviceId', predicates, async (err, result) => {
    if (err != undefined) {
      console.error(`Failed to get resultset.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in getting result set');
    resultSet = result;
    if (kvStore != null) {
      kvStore.closeResultSet(resultSet, (err) => {
        if (err != undefined) {
          console.error(`Failed to close resultset.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in closing result set');
      })
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.code}`);
}
```

### getResultSet

getResultSet(deviceId: string, predicates: dataSharePredicates.DataSharePredicates): Promise&lt;KVStoreResultSet&gt;

获取与指定Predicate对象匹配的KVStoreResultSet对象，使用Promise异步回调。
> **说明：** 
>
> 其中deviceId通过调用[deviceManager.getAvailableDeviceListSync](js-apis-distributedDeviceManager.md#getavailabledevicelistsync)方法得到。
> deviceId具体获取方式请参考[sync接口示例](#sync)。

**模型约束：** 此接口仅可在Stage模型下使用

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.DistributedDataManager.DataShare.Provider

**参数：**

| 参数名     | 类型                                                     | 必填 | 说明                                            |
| ---------- | ------------------------------------------------------------ | ---- | ----------------------------------------------- |
| deviceId  | string                                                       | 是   | 标识要查询其数据的设备。                                     |
| predicates | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md#datasharepredicates) | 是   | 指示筛选条件,当此参数为null时，应定义处理逻辑。 |

**返回值：**

| 类型                                                 | 说明                      |
| ---------------------------------------------------- | ------------------------- |
| Promise&lt;[KVStoreResultSet](#kvstoreresultset)&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100001     | Over max  limits.                      |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

try {
  let resultSet: distributedKVStore.KVStoreResultSet;
  let predicates = new dataSharePredicates.DataSharePredicates();
  predicates.prefixKey("batch_test_string_key");
  kvStore.getResultSet('localDeviceId', predicates).then((result) => {
    console.info('Succeeded in getting result set');
    resultSet = result;
    if (kvStore != null) {
      kvStore.closeResultSet(resultSet).then(() => {
        console.info('Succeeded in closing result set');
      }).catch((err: BusinessError) => {
        console.error(`Failed to close resultset.code is ${err.code},message is ${err.message}`);
      });
    }
  }).catch((err: BusinessError) => {
    console.error(`Failed to get resultset.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.code}`);
}
```

### getResultSize

getResultSize(query: Query, callback: AsyncCallback&lt;number&gt;): void

获取与本设备指定Query对象匹配的结果数，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名   | 类型                        | 必填 | 说明                                              |
| -------- | --------------------------- | ---- | ------------------------------------------------- |
| query    | [Query](#query)              | 是   | 表示查询对象。                                    |
| callback | AsyncCallback&lt;number&gt; | 是   | 回调函数。返回与本设备指定Query对象匹配的结果数。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  kvStore.putBatch(entries, async (err) => {
    console.info('Succeeded in putting batch');
    const query = new distributedKVStore.Query();
    query.prefixKey("batch_test");
    if (kvStore != null) {
      kvStore.getResultSize(query, async (err, resultSize) => {
        if (err != undefined) {
          console.error(`Failed to get result size.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in getting result set size');
      });
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.code}`);
}
```

### getResultSize

getResultSize(query: Query): Promise&lt;number&gt;

获取与本设备指定Query对象匹配的结果数，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.Core

**参数：**

| 参数名 | 类型           | 必填 | 说明           |
| ------ | -------------- | ---- | -------------- |
| query  | [Query](#query) | 是   | 表示查询对象。 |

**返回值：**

| 类型                  | 说明                                                 |
| --------------------- | ---------------------------------------------------- |
| Promise&lt;number&gt; | Promise对象。获取与本设备指定Query对象匹配的结果数。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  kvStore.putBatch(entries).then(async () => {
    console.info('Succeeded in putting batch');
  }).catch((err: BusinessError) => {
    console.error(`Failed to put batch.code is ${err.code},message is ${err.message}`);
  });
  const query = new distributedKVStore.Query();
  query.prefixKey("batch_test");
  kvStore.getResultSize(query).then((resultSize) => {
    console.info('Succeeded in getting result set size');
  }).catch((err: BusinessError) => {
    console.error(`Failed to get result size.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`An unexpected error occurred.code is ${error.code},message is ${error.code}`);
}
```

### getResultSize

getResultSize(deviceId: string, query: Query, callback: AsyncCallback&lt;number&gt;): void;

获取与指定设备ID和Query对象匹配的结果数，使用callback异步回调。
> **说明：** 
>
> 其中deviceId通过调用[deviceManager.getAvailableDeviceListSync](js-apis-distributedDeviceManager.md#getavailabledevicelistsync)方法得到。
> deviceId具体获取方式请参考[sync接口示例](#sync)。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**参数：**

| 参数名   | 类型                    | 必填 | 说明                                                |
| -------- | --------------------------- | ---- | --------------------------------------------------- |
| deviceId | string                      | 是   | KVStoreResultSet对象所属的设备ID。                  |
| query    | [Query](#query)              | 是   | 表示查询对象。                                      |
| callback | AsyncCallback&lt;number&gt; | 是   | 回调函数。返回与指定设备ID和Query对象匹配的结果数。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  kvStore.putBatch(entries, async (err) => {
    if (err != undefined) {
      console.error(`Failed to put batch.code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info('Succeeded in putting batch');
    const query = new distributedKVStore.Query();
    query.prefixKey("batch_test");
    if (kvStore != null) {
      kvStore.getResultSize('localDeviceId', query, async (err, resultSize) => {
        if (err != undefined) {
          console.error(`Failed to get resultSize.code is ${err.code},message is ${err.message}`);
          return;
        }
        console.info('Succeeded in getting resultSize');
      });
    }
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to get resultSize.code is ${error.code},message is ${error.message}`);
}
```

### getResultSize

getResultSize(deviceId: string, query: Query): Promise&lt;number&gt;

获取与指定设备ID和Query对象匹配的结果数，使用Promise异步回调。
> **说明：** 
>
> 其中deviceId通过调用[deviceManager.getAvailableDeviceListSync](js-apis-distributedDeviceManager.md#getavailabledevicelistsync)方法得到。
> deviceId具体获取方式请参考[sync接口示例](#sync)。

**系统能力：** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**参数：**

| 参数名   | 类型       | 必填 | 说明                               |
| -------- | -------------- | ---- | ---------------------------------- |
| deviceId | string         | 是   | KVStoreResultSet对象所属的设备ID。 |
| query    | [Query](#query) | 是   | 表示查询对象。                     |

**返回值：**

| 类型                  | 说明                                                   |
| --------------------- | ------------------------------------------------------ |
| Promise&lt;number&gt; | Promise对象。返回与指定设备ID和Query对象匹配的结果数。 |

**错误码：**

以下错误码的详细介绍请参见[分布式键值数据库错误码](../errorcodes/errorcode-distributedKVStore.md)。

| **错误码ID** | **错误信息**                           |
| ------------ | -------------------------------------- |
| 15100003     | Database corrupted.                    |
| 15100005     | Database or result set already closed. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let entries: distributedKVStore.Entry[] = [];
  for (let i = 0; i < 10; i++) {
    let key = 'batch_test_string_key';
    let entry: distributedKVStore.Entry = {
      key: key + i,
      value: {
        type: distributedKVStore.ValueType.STRING,
        value: 'batch_test_string_value'
      }
    }
    entries.push(entry);
  }
  kvStore.putBatch(entries).then(async () => {
    console.info('Succeeded in putting batch');
  }).catch((err: BusinessError) => {
    console.error(`Failed to put batch.code is ${err.code},message is ${err.message}`);
  });
  let query = new distributedKVStore.Query();
  query.prefixKey("batch_test");
  kvStore.getResultSize('localDeviceId', query).then((resultSize) => {
    console.info('Succeeded in getting resultSize');
  }).catch((err: BusinessError) => {
    console.error(`Failed to get resultSize.code is ${err.code},message is ${err.message}`);
  });
} catch (e) {
  let error = e as BusinessError;
  console.error(`Failed to get resultSize.code is ${error.code},message is ${error.message}`);
}
```

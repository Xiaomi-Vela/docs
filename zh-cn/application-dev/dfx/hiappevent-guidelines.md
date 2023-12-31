# 应用事件打点开发指导

## 简介

传统的日志系统里汇聚了整个设备上所有程序运行的过程流水日志，难以识别其中的关键信息。因此，应用开发者需要一种数据打点机制，用来评估如访问数、日活、用户操作习惯以及影响用户使用的关键因素等关键信息。

HiAppEvent是在系统层面为应用开发者提供的一种事件打点机制，用于帮助应用记录在运行过程中发生的故障信息、统计信息、安全信息、用户行为信息，以支撑开发者分析应用的运行情况。

## 基本概念

- **打点**

  记录由用户操作引起的变化，提供业务数据信息，以供开发、产品、运维分析。

## 事件设计规范

- 事件领域：用于标识事件的领域，建议设置为业务模块名称，以便于区分不同的业务模块。
- 事件名称：用于指定事件的名称，建议设置为具体的业务名称，以便于描述实际的业务意义。
- 事件类型：用于指定事件的类型，支持以下四种类型事件：
  - 行为事件：用于记录用户日常操作行为的事件，例如按钮点击、界面跳转等行为。
  - 故障事件：用于定位和分析应用故障的事件，例如界面卡顿、掉网掉话等异常。
  - 统计事件：用于统计和度量应用关键行为的事件，例如对使用时长、访问数等的统计。
  - 安全事件：用于记录涉及应用安全行为的事件，例如密码修改、用户授权等行为。
- 事件参数：用于指定事件的参数，每个事件可以包含一组参数，建议设置为事件属性或事件发生上下文信息，以便于描述事件的详细信息。

## 接口说明

应用事件打点接口由hiAppEvent模块提供，API接口的具体使用说明（参数使用限制、具体取值范围等）请参考[应用事件打点API文档](../reference/apis/js-apis-hiviewdfx-hiappevent.md)。

**打点接口功能介绍：**

| 接口名                                                       | 描述                                                 |
| ------------------------------------------------------------ | ---------------------------------------------------- |
| write(info: AppEventInfo, callback: AsyncCallback\<void>): void | 应用事件异步打点方法，使用callback方式作为异步回调。 |
| write(info: AppEventInfo): Promise\<void>                    | 应用事件异步打点方法，使用Promise方式作为异步回调。  |

**订阅接口功能介绍：**

| 接口名                                              | 描述                                         |
| --------------------------------------------------- | -------------------------------------------- |
| addWatcher(watcher: Watcher): AppEventPackageHolder | 添加应用事件观察者，以添加对应用事件的订阅。 |
| removeWatcher(watcher: Watcher): void               | 移除应用事件观察者，以移除对应用事件的订阅。 |

**数据处理者接口功能介绍：**

| 接口名                                    | 描述                                             |
| ----------------------------------------- | ------------------------------------------------ |
| addProcessor(processor: Processor): number | 添加数据处理者，以通过预置的处理者进行事件上报。 |
| removeProcessor(id: number): void          | 移除数据处理者，以移除预置的处理者。             |

**用户ID接口功能介绍：**

| 接口名                                     | 描述                                         |
| ------------------------------------------ | -------------------------------------------- |
| setUserId(name: string, value: string): void | 设置用户ID，数据处理者上报事件时可携带用户ID。 |
| getUserId(name: string): void               | 获取已设置的用户ID。                           |

**用户属性接口功能介绍：**

| 接口名                                           | 描述                                             |
| ------------------------------------------------ | ------------------------------------------------ |
| setUserProperty(name: string, value: string): void | 设置用户属性，数据处理者上报事件时可携带用户属性。 |
| getUserProperty(name: string): void               | 获取已设置的用户属性。                            |

## 事件订阅开发步骤

以实现对用户点击按钮行为的事件打点及订阅为例，说明开发步骤。

1. 新建一个ArkTS应用工程，编辑工程中的“entry > src > main > ets  > entryability > EntryAbility.ts” 文件，在onCreate函数中添加对用户点击按钮事件的订阅，完整示例代码如下：

   ```ts
   import AbilityConstant from '@ohos.app.ability.AbilityConstant';
   import hiAppEvent from '@ohos.hiviewdfx.hiAppEvent';
   import hilog from '@ohos.hilog';
   import UIAbility from '@ohos.app.ability.UIAbility';
   import Want from '@ohos.app.ability.Want';
   import window from '@ohos.window';
   
   export default class EntryAbility extends UIAbility {
     onCreate(want: Want, launchParam: AbilityConstant.LaunchParam) {
       hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onCreate');
   
       hiAppEvent.addWatcher({
         // 开发者可以自定义观察者名称，系统会使用名称来标识不同的观察者
         name: "watcher1",
         // 开发者可以订阅感兴趣的应用事件，此处是订阅了按钮事件
         appEventFilters: [{ domain: "button" }],
         // 开发者可以设置订阅回调触发的条件，此处是设置为事件打点数量满足1个
         triggerCondition: { row: 1 },
         // 开发者可以自行实现订阅回调函数，以便对订阅获取到的事件打点数据进行自定义处理
         onTrigger: (curRow: number, curSize: number, holder: hiAppEvent.AppEventPackageHolder) => {
           // 返回的holder对象为null，表示订阅过程发生异常，因此在记录错误日志后直接返回
           if (holder == null) {
             hilog.error(0x0000, 'testTag', "HiAppEvent holder is null");
             return;
           }
           hilog.info(0x0000, 'testTag', `HiAppEvent onTrigger: curRow=%{public}d, curSize=%{public}d`, curRow, curSize);
           let eventPkg: hiAppEvent.AppEventPackage | null = null;
           // 根据设置阈值大小（默认为512KB）去获取订阅事件包，直到将订阅数据全部取出
           // 返回的事件包对象为null，表示当前订阅数据已被全部取出，此次订阅回调触发结束
           while ((eventPkg = holder.takeNext()) != null) {
             // 开发者可以对事件包中的事件打点数据进行自定义处理，此处是将事件打点数据打印在日志中
             hilog.info(0x0000, 'testTag', `HiAppEvent eventPkg.packageId=%{public}d`, eventPkg.packageId);
             hilog.info(0x0000, 'testTag', `HiAppEvent eventPkg.row=%{public}d`, eventPkg.row);
             hilog.info(0x0000, 'testTag', `HiAppEvent eventPkg.size=%{public}d`, eventPkg.size);
             for (const eventInfo of eventPkg.data) {
               hilog.info(0x0000, 'testTag', `HiAppEvent eventPkg.info=%{public}s`, eventInfo);
             }
           }
         }
       });
     }
   }

2. 编辑工程中的“entry > src > main > ets  > pages > Index.ets” 文件，添加一个按钮并在其onClick函数中进行事件打点，以记录按钮点击事件，完整示例代码如下：

   ```ts
     Button("writeTest").onClick(()=>{
       // 在按钮点击函数中进行事件打点，以记录按钮点击事件
       let eventParams: Record<string, number> = { 'click_time': 100 };
       let eventInfo: hiAppEvent.AppEventInfo = {
         // 事件领域定义
         domain: "button",
         // 事件名称定义
         name: "click",
         // 事件类型定义
         eventType: hiAppEvent.EventType.BEHAVIOR,
         // 事件参数定义
         params: eventParams,
       };
       hiAppEvent.write(eventInfo).then(() => {
         hilog.info(0x0000, 'testTag', `HiAppEvent success to write event`)
       }).catch((err: BusinessError) => {
         hilog.error(0x0000, 'testTag', `HiAppEvent err.code: ${err.code}, err.message: ${err.message}`)
       });
     })
   ```

3. 点击IDE界面中的运行按钮，运行应用工程，然后在应用界面中点击按钮“writeTest”，触发一次按钮点击事件打点。

4. 最终，可以在Log窗口看到按钮点击事件打点成功的日志，以及触发订阅回调后对打点事件数据的处理日志：

```text
HiAppEvent success to write event
HiAppEvent eventPkg.packageId=0
HiAppEvent eventPkg.row=1
HiAppEvent eventPkg.size=124
HiAppEvent eventPkg.info={"domain\_":"button","name\_":"click","type\_":4,"time\_":1670268234523,"tz\_":"+0800","pid\_":3295,"tid\_":3309,"click_time":100}
```

## 事件上报开发步骤

以实现对用户点击按钮行为的事件打点并由处理者进行事件上报为例，说明开发步骤。

1. 编辑工程中的“entry > src > main > ets  > pages > Index.ets” 文件，添加一个按钮并在其onClick函数中添加数据处理者。analytics_demo为预置在设备里面的数据处理者lib库，具体实现可以参考[《HiAppEvent数据处理者lib库概述》](../../device-dev/subsystems/subsys-dfx-hiappevent-extend-so.md)。完整示例代码如下：

   ```ts
   import { BusinessError } from '@ohos.base'
   import hiAppEvent from '@ohos.hiviewdfx.hiAppEvent'
   import hilog from '@ohos.hilog'
   
   @Entry
   @Component
   struct Index {
     @State message: string = 'Hello World'

     processorId: number = -1
   
     build() {
       Row() {
         Column() {
           Text(this.message)
             .fontSize(50)
             .fontWeight(FontWeight.Bold)
   
           Button("addProcessorTest").onClick(()=>{
             // 在按钮点击函数中进行数据处理者添加
             let eventConfig: hiAppEvent.AppEventReportConfig = {
               domain: 'button',
               name: 'click',
               isRealTime: true
             };
             let processor: hiAppEvent.Processor = {
               name: 'analytics_demo',
               debugMode: true,
               routeInfo: 'CN',
               onStartReport: true,
               onBackgroundReport: true,
               periodReport: 10,
               batchReport: 5,
               userIds: ['testUserIdName'],
               userProperties: ['testUserPropertyName'],
               eventConfigs: [eventConfig]
             };
             this.processorId = hiAppEvent.addProcessor(processor);
           })
         }
         .width('100%')
       }
       .height('100%')
     }
   }
   ```

2. 编辑工程中的“entry > src > main > ets  > pages > Index.ets” 文件，添加一个按钮并在其onClick函数中添加并查看用户ID，完整示例代码如下：

   ```ts
     Button("userIdTest").onClick(()=>{
       // 在按钮点击函数中设置用户ID
       hiAppEvent.setUserId('testUserIdName', '123456');

       // 在按钮点击函数中获取刚设置的用户ID
       let userId = hiAppEvent.getUserId('testUserIdName');
       hilog.info(0x0000, 'testTag', `userId: ${userId}`)
     })
   ```

3. 编辑工程中的“entry > src > main > ets  > pages > Index.ets” 文件，添加一个按钮并在其onClick函数中添加并查看用户属性，完整示例代码如下：

   ```ts
     Button("userPropertyTest").onClick(()=>{
       // 在按钮点击函数中设置用户ID
       hiAppEvent.setUserProperty('testUserPropertyName', '123456');

       // 在按钮点击函数中获取刚设置的用户ID
       let userProperty = hiAppEvent.getUserProperty('testUserPropertyName');
       hilog.info(0x0000, 'testTag', `userProperty: ${userProperty}`)
     })
   ```

4. 编辑工程中的“entry > src > main > ets  > pages > Index.ets” 文件，添加一个按钮并在其onClick函数中进行事件打点，以记录按钮点击事件，完整示例代码如下：

   ```ts
     Button("writeTest").onClick(()=>{
       // 在按钮点击函数中进行事件打点，以记录按钮点击事件
       let eventParams: Record<string, number> = { 'click_time': 100 };
       let eventInfo: hiAppEvent.AppEventInfo = {
         // 事件领域定义
         domain: "button",
         // 事件名称定义
         name: "click",
         // 事件类型定义
         eventType: hiAppEvent.EventType.BEHAVIOR,
         // 事件参数定义
         params: eventParams,
       };
       hiAppEvent.write(eventInfo).then(() => {
         hilog.info(0x0000, 'testTag', `HiAppEvent success to write event`)
       }).catch((err: BusinessError) => {
         hilog.error(0x0000, 'testTag', `HiAppEvent err.code: ${err.code}, err.message: ${err.message}`)
       });
     })
   ```

5. 编辑工程中的“entry > src > main > ets  > pages > Index.ets” 文件，添加一个按钮并在其onClick函数中进行数据处理者移除(第二步已完成数据处理者添加)，完整示例代码如下：

   ```ts
     Button("removeProcessorTest").onClick(()=>{
       // 在按钮点击函数中进行数据处理者移除
       hiAppEvent.removeProcessor(this.processorId);
     })
   ```

6. 点击IDE界面中的运行按钮，运行应用工程，然后在应用界面中依次点击按钮“addProcessorTest”、“userIdTest”、“userPropertyTest”、“writeTest”、“removeProcessorTest”，则成功通过数据处理者进行一次事件上报。

   最终，事件处理者成功接收到事件数据，并在Log窗口看到按钮点击事件打点成功的日志：

   ```text
   HiAppEvent success to write event
   ```

## 相关实例

针对应用事件开发，有以下相关实例可供参考：

- [测试打点（ArkTS）（API9）](https://gitee.com/openharmony/applications_app_samples/tree/master/code/BasicFeature/DFX/DotTest)

- [日志打印（ArkTS）（API9）](https://gitee.com/openharmony/applications_app_samples/tree/master/code/BasicFeature/DFX/Logger)
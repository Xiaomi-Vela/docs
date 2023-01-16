# @ohos.commonEventManager (公共事件模块)

本模块提供了公共事件相关的能力，包括发布公共事件、订阅公共事件、以及退订公共事件。

> **说明：**
>
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import CommonEventManager from '@ohos.commonEventManager';
```

## Support

系统公共事件是指由系统服务或系统应用发布的事件，订阅这些系统公共事件需要特定的权限。发布或订阅这些事件需要使用如下链接中的枚举定义。

全部系统公共事件枚举定义请参见[系统公共事件定义](./commonEventManager-definitions.md)。

## CommonEventManager.publish

```ts
publish(event: string, callback: AsyncCallback<void>): void
```

发布公共事件，并在发布后执行相应的回调函数。

**系统能力：** `SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名     | 类型                 | 必填 | 说明                   |
| -------- | -------------------- | ---- | ---------------------- |
| event    | string               | 是   | 表示要发送的公共事件。 |
| callback | AsyncCallback\<void> | 是   | 表示事件发布后将要执行的回调函数。 |

**错误码：**

错误码介绍请参考[@ohos.commonEventManager(事件)](../errorcodes/errorcode-CommonEventService.md)

**示例：**

```ts
//发布公共事件回调
function publishCB(err) {
	if (err) {
        console.error("publish failed " + JSON.stringify(err));
    } else {
        console.info("publish");
    }
}

//发布公共事件
try {
    CommonEventManager.publish("event", publishCB);
} catch(err) {
    console.error('publish failed, catch error' + JSON.stringify(err));
}
```

## CommonEventManager.publish

```ts
publish(event: string, options: CommonEventPublishData, callback: AsyncCallback<void>): void
```

以回调的形式发布公共事件。

**系统能力：** `SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名     | 类型                   | 必填 | 说明                   |
| -------- | ---------------------- | ---- | ---------------------- |
| event    | string                 | 是   | 表示要发布的公共事件。  |
| options  | [CommonEventPublishData](#commoneventpublishdata) | 是   | 表示发布公共事件的属性。 |
| callback | syncCallback\<void>   | 是   | 表示被指定的回调方法。  |

**错误码：**

错误码介绍请参考[@ohos.commonEventManager(事件)](../errorcodes/errorcode-CommonEventService.md)

**示例：**

```ts
//公共事件相关信息
let options = {
	code: 0,			 //公共事件的初始代码
	data: "initial data",//公共事件的初始数据
	isOrdered: true	 //有序公共事件
}

//发布公共事件回调
function publishCB(err) {
	if (err) {
        console.error("publish failed " + JSON.stringify(err));
    } else {
        console.info("publish");
    }
}

//发布公共事件
try {
    CommonEventManager.publish("event", options, publishCB);
} catch (err) {
    console.error('publish failed, catch error' + JSON.stringify(err));
}
```

## CommonEventManager.publishAsUser<sup>

```ts
publishAsUser(event: string, userId: number, callback: AsyncCallback<void>): void
```

以回调的形式向指定用户发布公共事件。

**系统能力：** `SystemCapability.Notification.CommonEvent`

**系统API**：此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名     | 类型                 | 必填 | 说明                               |
| -------- | -------------------- | ---- | ---------------------------------- |
| event    | string               | 是   | 表示要发送的公共事件。             |
| userId   | number               | 是   | 表示指定向该用户ID发送此公共事件。 |
| callback | AsyncCallback\<void> | 是   | 表示被指定的回调方法。             |

**错误码：**

错误码介绍请参考[@ohos.commonEventManager(事件)](../errorcodes/errorcode-CommonEventService.md)

**示例：**

```ts
//发布公共事件回调
function publishCB(err) {
	if (err) {
        console.error("publishAsUser failed " + JSON.stringify(err));
    } else {
        console.info("publishAsUser");
    }
}

//指定发送的用户
let userId = 100;

//发布公共事件
try {
    CommonEventManager.publishAsUser("event", userId, publishCB);
} catch (err) {
    console.error('publishAsUser failed, catch error' + JSON.stringify(err));
}
```

## CommonEventManager.publishAsUser

```ts
publishAsUser(event: string, userId: number, options: CommonEventPublishData, callback: AsyncCallback<void>): void
```

以回调形式向指定用户发布公共事件并指定发布信息。

**系统能力：** `SystemCapability.Notification.CommonEvent`

**系统API**：此接口为系统接口，三方应用不支持调用。

**参数：**

| 参数名     | 类型                   | 必填 | 说明                   |
| -------- | ---------------------- | ---- | ---------------------- |
| event    | string                 | 是   | 表示要发布的公共事件。  |
| userId   | number | 是 | 表示指定向该用户ID发送此公共事件。 |
| options  | [CommonEventPublishData](#commoneventpublishdata) | 是   | 表示发布公共事件的属性。 |
| callback | AsyncCallback\<void>   | 是   | 表示被指定的回调方法。  |

**错误码：**

错误码介绍请参考[@ohos.commonEventManager(事件)](../errorcodes/errorcode-CommonEventService.md)

**示例：**


```ts
//公共事件相关信息
let options = {
	code: 0,			 //公共事件的初始代码
	data: "initial data",//公共事件的初始数据
}

//发布公共事件回调
function publishCB(err) {
	if (err) {
        console.error("publishAsUser failed " + JSON.stringify(err));
    } else {
        console.info("publishAsUser");
    }
}

//指定发送的用户
let userId = 100;

//发布公共事件
try {
    CommonEventManager.publishAsUser("event", userId, options, publishCB);
} catch (err) {
    console.error('publishAsUser failed, catch error' + JSON.stringify(err));
}
```

## CommonEventManager.createSubscriber

```ts
createSubscriber(subscribeInfo: CommonEventSubscribeInfo, callback: AsyncCallback<CommonEventSubscriber>): void
```

以回调形式创建订阅者。

**系统能力：** `SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名          | 类型                                                         | 必填 | 说明                       |
| ------------- | ------------------------------------------------------------ | ---- | -------------------------- |
| subscribeInfo | [CommonEventSubscribeInfo](#commoneventsubscribeinfo)        | 是   | 表示订阅信息。             |
| callback      | AsyncCallback\<[CommonEventSubscriber](#commoneventsubscriber)> | 是   | 表示创建订阅者的回调方法。 |

**示例：**


```ts
let subscriber; //用于保存创建成功的订阅者对象，后续使用其完成订阅及退订的动作

//订阅者信息
let subscribeInfo = {
    events: ["event"]
};

//创建订阅者回调
function createCB(err, commonEventSubscriber) {
    if(!err) {
        console.info("createSubscriber");
        subscriber = commonEventSubscriber;
    } else {
        console.error("createSubscriber failed " + JSON.stringify(err));
    }
}

//创建订阅者
try {
    CommonEventManager.createSubscriber(subscribeInfo, createCB);
} catch (err) {
    console.error('createSubscriber failed, catch error' + JSON.stringify(err));
}
```

## CommonEventManager.createSubscriber

```ts
createSubscriber(subscribeInfo: CommonEventSubscribeInfo): Promise<CommonEventSubscriber>
```

以Promise形式创建订阅者。

**系统能力：** `SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名          | 类型                                                  | 必填 | 说明           |
| ------------- | ----------------------------------------------------- | ---- | -------------- |
| subscribeInfo | [CommonEventSubscribeInfo](#commoneventsubscribeinfo) | 是   | 表示订阅信息。 |

**返回值：**
| 类型                                                      | 说明             |
| --------------------------------------------------------- | ---------------- |
| Promise\<[CommonEventSubscriber](#commoneventsubscriber)> | 返回订阅者对象。 |

**示例：**

```ts
let subscriber; //用于保存创建成功的订阅者对象，后续使用其完成订阅及退订的动作

//订阅者信息
let subscribeInfo = {
	events: ["event"]
};

//创建订阅者
CommonEventManager.createSubscriber(subscribeInfo).then((commonEventSubscriber) => {
    console.info("createSubscriber");
    subscriber = commonEventSubscriber;
}).catch((err) => {
    console.error("createSubscriber failed " + JSON.stringify(err));
});

```

## CommonEventManager.subscribe

```ts
subscribe(subscriber: CommonEventSubscriber, callback: AsyncCallback<CommonEventData>): void
```

以回调形式订阅公共事件。

**系统能力：** `SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名       | 类型                                                | 必填 | 说明                             |
| ---------- | ---------------------------------------------------- | ---- | -------------------------------- |
| subscriber | [CommonEventSubscriber](#commoneventsubscriber)     | 是   | 表示订阅者对象。                 |
| callback   | AsyncCallback\<[CommonEventData](#commoneventdata)> | 是   | 表示接收公共事件数据的回调函数。 |

**示例：**

```ts
//订阅者信息
let subscriber; //用于保存创建成功的订阅者对象，后续使用其完成订阅及退订的动作

//订阅者信息
let subscribeInfo = {
    events: ["event"]
};

//订阅公共事件回调
function SubscribeCB(err, data) {
    if (err.code) {
        console.error("subscribe failed " + JSON.stringify(err));
    } else {
        console.info("subscribe ");
    }
}

//创建订阅者回调
function createCB(err, subscriber) {
    if(!err) {
        console.info("createSubscriber");
        //订阅公共事件
        try {
            CommonEventManager.subscribe(subscriber, SubscribeCB);
        } catch (err) {
            console.error("createSubscriber failed " + JSON.stringify(err));
        }
    } else {
        console.error("createSubscriber failed " + JSON.stringify(err));
    }
}

//创建订阅者
try {
    CommonEventManager.createSubscriber(subscribeInfo, createCB);
} catch (err) {
    console.error('createSubscriber failed, catch error' + JSON.stringify(err));
}
```

## CommonEventManager.unsubscribe

```ts
unsubscribe(subscriber: CommonEventSubscriber, callback?: AsyncCallback<void>): void
```

以回调形式取消订阅公共事件。

**系统能力：** `SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名       | 类型                                             | 必填 | 说明                     |
| ---------- | ----------------------------------------------- | ---- | ------------------------ |
| subscriber | [CommonEventSubscriber](#commoneventsubscriber) | 是   | 表示订阅者对象。         |
| callback   | AsyncCallback\<void>                            | 否   | 表示取消订阅的回调方法。 |

**示例：**

```ts
let subscriber; //用于保存创建成功的订阅者对象，后续使用其完成订阅及退订的动作
//订阅者信息
let subscribeInfo = {
    events: ["event"]
};
//订阅公共事件回调
function subscribeCB(err, data) {
    if (err) {
        console.info("subscribe failed " + JSON.stringify(err));
    } else {
        console.info("subscribe");
    }
}
//创建订阅者回调
function createCB(err, subscriber) {
    if (err) {
        console.info("createSubscriber failed " + JSON.stringify(err));
    } else {
        console.info("createSubscriber");
        //订阅公共事件
        try {
            CommonEventManager.subscribe(subscriber, subscribeCB);
        } catch(err) {
            console.info("subscribe failed " + JSON.stringify(err));
        }
    }
}
//取消订阅公共事件回调
function unsubscribeCB(err) {
    if (err) {
        console.info("unsubscribe failed " + JSON.stringify(err));
    } else {
        console.info("unsubscribe");
    }
}
//创建订阅者
try {
    CommonEventManager.createSubscriber(subscribeInfo, createCB);
} catch (err) {
    console.info("createSubscriber failed " + JSON.stringify(err));
}

//取消订阅公共事件
try {
    CommonEventManager.unsubscribe(subscriber, unsubscribeCB);
} catch (err) {
    console.info("unsubscribe failed " + JSON.stringify(err));
}
```

## CommonEventSubscriber

### getCode

```ts
getCode(callback: AsyncCallback<number>): void
```

以回调形式获取公共事件代码。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                   | 必填 | 说明               |
| -------- | ---------------------- | ---- | ------------------ |
| callback | AsyncCallback\<number\> | 是   | 公共事件代码。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

//获取有序公共事件代码回调
function getCodeCB(err, code) {
    if (err.code) {
        console.error("getCode failed " + JSON.stringify(err));
    } else {
        console.info("getCode " + JSON.stringify(code));
    }
}
subscriber.getCode(getCodeCB);
```

### getCode

```ts
getCode(): Promise<number>
```

以Promise形式获取公共事件代码。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型             | 说明                 |
| ---------------- | -------------------- |
| Promise\<number> | 公共事件代码。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

subscriber.getCode().then((code) => {
    console.info("getCode " + JSON.stringify(code));
}).catch((err) => {
    console.error("getCode failed " + JSON.stringify(err));
});
```

### setCode

```ts
setCode(code: number, callback: AsyncCallback<void>): void
```

以回调形式设置公共事件的代码。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                 | 必填 | 说明                   |
| -------- | -------------------- | ---- | ---------------------- |
| code     | number               | 是   | 公共事件的代码。   |
| callback | AsyncCallback\<void> | 是   | 表示被指定的回调方法。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

//设置有序公共事件的代码回调
function setCodeCB(err) {
    if (err.code) {
        console.error("setCode failed " + JSON.stringify(err));
    } else {
        console.info("setCode");
    }
}
subscriber.setCode(1, setCodeCB);
```

### setCode

```ts
setCode(code: number): Promise<void>
```

以Promise形式设置公共事件的代码。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名 | 类型   | 必填 | 说明               |
| ------ | ------ | ---- | ------------------ |
| code   | number | 是   | 公共事件的代码。 |

**返回值：**

| 类型             | 说明                 |
| ---------------- | -------------------- |
| Promise\<void>   | 返回一个Promise的结果。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

subscriber.setCode(1).then(() => {
    console.info("setCode");
}).catch((err) => {
    console.error("setCode failed " + JSON.stringify(err));
});
```

### getData

```ts
getData(callback: AsyncCallback<string>): void
```

以回调形式获取公共事件的数据。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                   | 必填 | 说明                 |
| -------- | ---------------------- | ---- | -------------------- |
| callback | AsyncCallback\<string> | 是   | 公共事件的数据。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

//获取有序公共事件代码数据回调
function getDataCB(err, data) {
    if (err.code) {
        console.error("getData failed " + JSON.stringify(err));
    } else {
        console.info("getData " + JSON.stringify(data));
    }
}
subscriber.getData(getDataCB);
```

### getData

```ts
getData(): Promise<string>
```

以Promise形式获取公共事件的数据。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型             | 说明               |
| ---------------- | ------------------ |
| Promise\<string> | 公共事件的数据。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

subscriber.getData().then((data) => {
    console.info("getData " + JSON.stringify(data));
}).catch((err) => {
    console.error("getData failed " + JSON.stringify(err));
});
```

### setData

setData(data: string, callback: AsyncCallback\<void>): void

以回调形式设置公共事件的数据。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                 | 必填 | 说明                 |
| -------- | -------------------- | ---- | -------------------- |
| data     | string               | 是   | 公共事件的数据。   |
| callback | AsyncCallback\<void> | 是   | 表示被指定的回调方法。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

//设置有序公共事件的结果数据回调
function setDataCB(err) {
    if (err.code) {
        console.error("setData failed " + JSON.stringify(err));
    } else {
        console.info("setData");
    }
}
subscriber.setData("publish_data_changed", setDataCB);
```

### setData

```ts
setData(data: string): Promise<void>
```

以Promise形式设置公共事件的果数据。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名 | 类型   | 必填 | 说明                 |
| ------ | ------ | ---- | -------------------- |
| data   | string | 是   | 公共事件的数据。 |

**返回值：**

| 类型             | 说明                 |
| ---------------- | -------------------- |
| Promise\<void>   | 返回一个Promise的结果。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

subscriber.setData("publish_data_changed").then(() => {
    console.info("setData");
}).catch((err) => {
    console.error("setData failed " + JSON.stringify(err));
});
```

### setCodeAndData

```ts
setCodeAndData(code: number, data: string, callback:AsyncCallback<void>): void
```

以回调形式设置公共事件代码和数据。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                 | 必填 | 说明                   |
| -------- | -------------------- | ---- | ---------------------- |
| code     | number               | 是   | 公共事件的代码。   |
| data     | string               | 是   | 公共事件的数据。   |
| callback | AsyncCallback\<void> | 是   | 表示被指定的回调方法。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

//设置有序公共事件的代码和数据回调
function setCodeDataCB(err) {
    if (err.code) {
        console.error("setCodeAndData failed " + JSON.stringify(err));
    } else {
        console.info("setCodeDataCallback");
    }
}
subscriber.setCodeAndData(1, "publish_data_changed", setCodeDataCB);
```

### setCodeAndData

```ts
setCodeAndData(code: number, data: string): Promise<void>
```

以Promise形式设置公共事件的代码和数据。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名 | 类型   | 必填 | 说明                 |
| ------ | ------ | ---- | -------------------- |
| code   | number | 是   | 公共事件的代码。 |
| data   | string | 是   | 公共事件的数据。 |

**返回值：**

| 类型             | 说明                 |
| ---------------- | -------------------- |
| Promise\<void>   | 返回一个Promise。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

subscriber.setCodeAndData(1, "publish_data_changed").then(() => {
    console.info("setCodeAndData");
}).catch((err) => {
    console.info("setCodeAndData failed " + JSON.stringify(err));
});
```

### isOrderedCommonEvent

```ts
isOrderedCommonEvent(callback: AsyncCallback<boolean>): void
```

以回调形式查询当前公共事件的是否为有序公共事件。

返回true代表是有序公共事件，false代表不是有序公共事件。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                    | 必填 | 说明                               |
| -------- | ----------------------- | ---- | ---------------------------------- |
| callback | AsyncCallback\<boolean> | 是   | 当前公共事件的是否为有序公共事件。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

//获取当前公共事件是否为有序事件的回调
function isOrderedCB(err, isOrdered) {
    if (err.code) {
        console.error("isOrderedCommonEvent failed " + JSON.stringify(err));
    } else {
        console.info("isOrdered " + JSON.stringify(isOrdered));
    }
}
subscriber.isOrderedCommonEvent(isOrderedCB);
```

### isOrderedCommonEvent

```ts
isOrderedCommonEvent(): Promise<boolean>
```

以Promise形式查询当前公共事件的是否为有序公共事件。

返回true代表是有序公共事件，false代表不是有序公共事件。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型              | 说明                             |
| ----------------- | -------------------------------- |
| Promise\<boolean> | 当前公共事件的是否为有序公共事件。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

subscriber.isOrderedCommonEvent().then((isOrdered) => {
    console.info("isOrdered " + JSON.stringify(isOrdered));
}).catch((err) => {
    console.error("isOrdered failed " + JSON.stringify(err));
});
```

### isStickyCommonEvent

```ts
isStickyCommonEvent(callback: AsyncCallback<boolean>): void
```

以回调形式检查当前公共事件是否为一个粘性事件。

返回true代表是粘性公共事件，false代表不是粘性公共事件。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                    | 必填 | 说明                               |
| -------- | ----------------------- | ---- | ---------------------------------- |
| callback | AsyncCallback\<boolean> | 是   | 当前公共事件的是否为粘性公共事件。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

//获取当前公共事件是否为粘性事件的回调
function isStickyCB(err, isSticky) {
    if (err.code) {
        console.error("isStickyCommonEvent failed " + JSON.stringify(err));
    } else {
        console.info("isSticky " + JSON.stringify(isSticky));
    }
}
subscriber.isStickyCommonEvent(isStickyCB);
```

### isStickyCommonEvent

```ts
isStickyCommonEvent(): Promise<boolean>
```

以Promise形式检查当前公共事件是否为一个粘性事件。

返回true代表是粘性公共事件，false代表不是粘性公共事件。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型              | 说明                             |
| ----------------- | -------------------------------- |
| Promise\<boolean> | 当前公共事件的是否为粘性公共事件。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

subscriber.isStickyCommonEvent().then((isSticky) => {
    console.info("isSticky " + JSON.stringify(isSticky));
}).catch((err) => {
    console.error("isSticky failed " + JSON.stringify(err));
});
```

### abortCommonEvent

```ts
abortCommonEvent(callback: AsyncCallback<void>): void
```

以回调形式取消当前的有序公共事件，取消后，有序公共事件不再向下一个订阅者传递。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                 | 必填 | 说明                 |
| -------- | -------------------- | ---- | -------------------- |
| callback | AsyncCallback\<void> | 是   | 取消当前的有序公共事件。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

//取消当前有序公共事件的回调
function abortCB(err) {
    if (err.code) {
        console.error("abortCommonEvent failed " + JSON.stringify(err));
    } else {
        console.info("abortCommonEvent");
    }
}
subscriber.abortCommonEvent(abortCB);
```

### abortCommonEvent

```ts
abortCommonEvent(): Promise<void>
```

以Promise形式取消当前的有序公共事件，取消后，公共事件不再向下一个订阅者传递。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型             | 说明                 |
| ---------------- | -------------------- |
| Promise\<void>   | 返回一个Promise的结果。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

subscriber.abortCommonEvent().then(() => {
    console.info("abortCommonEvent");
}).catch((err) => {
    console.error("abortCommonEvent failed " + JSON.stringify(err));
});
```

### clearAbortCommonEvent

```ts
clearAbortCommonEvent(callback: AsyncCallback<void>): void
```

以回调形式清除当前有序公共事件。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                 | 必填 | 说明                 |
| -------- | -------------------- | ---- | -------------------- |
| callback | AsyncCallback\<void> | 是   | 表示被指定的回调方法。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

//清除当前公共事件取消状态的回调
function clearAbortCB(err) {
    if (err.code) {
        console.error("clearAbortCommonEvent failed " + JSON.stringify(err));
    } else {
        console.info("clearAbortCommonEvent");
    }
}
subscriber.clearAbortCommonEvent(clearAbortCB);
```

### clearAbortCommonEvent

```ts
clearAbortCommonEvent(): Promise<void>
```

以Promise形式清除当前有序公共事件。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型             | 说明                 |
| ---------------- | -------------------- |
| Promise\<void>   | 返回一个Promise的结果。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

subscriber.clearAbortCommonEvent().then(() => {
    console.info("clearAbortCommonEvent");
}).catch((err) => {
    console.error("clearAbortCommonEvent failed " + JSON.stringify(err));
});
```

### getAbortCommonEvent

```ts
getAbortCommonEvent(callback: AsyncCallback<boolean>): void
```

以回调形式获取当前有序公共事件是否取消的状态。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                    | 必填 | 说明                               |
| -------- | ----------------------- | ---- | ---------------------------------- |
| callback | AsyncCallback\<boolean> | 是   | 表示当前有序公共事件是否取消的状态。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

//获取当前有序公共事件是否取消的回调
function getAbortCB(err, abortEvent) {
    if (err.code) {
        console.error("getAbortCommonEvent failed " + JSON.stringify(err));
    } else {
        console.info("abortCommonEvent " + abortEvent)
    }
}
subscriber.getAbortCommonEvent(getAbortCB);
```

### getAbortCommonEvent

```ts
getAbortCommonEvent(): Promise<boolean>
```

以Promise形式获取当前有序公共事件是否取消的状态。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型              | 说明                               |
| ----------------- | ---------------------------------- |
| Promise\<boolean> | 表示当前有序公共事件是否取消的状态。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

subscriber.getAbortCommonEvent().then((abortEvent) => {
    console.info("abortCommonEvent " + JSON.stringify(abortEvent));
}).catch((err) => {
    console.error("getAbortCommonEvent failed " + JSON.stringify(err));
});
```

### getSubscribeInfo

```ts
getSubscribeInfo(callback: AsyncCallback<CommonEventSubscribeInfo>): void
```

以回调形式获取订阅者的订阅信息。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                   |
| -------- | ------------------------------------------------------------ | ---- | ---------------------- |
| callback | AsyncCallback\<[CommonEventSubscribeInfo](#commoneventsubscribeinfo)> | 是   | 表示订阅者的订阅信息。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

//获取订阅者信息回调
function getCB(err, subscribeInfo) {
    if (err.code) {
        console.error("getSubscribeInfo failed " + JSON.stringify(err));
    } else {
        console.info("subscribeInfo " + JSON.stringify(subscribeInfo));
    }
}
subscriber.getSubscribeInfo(getCB);
```

### getSubscribeInfo

```ts
getSubscribeInfo(): Promise<CommonEventSubscribeInfo>
```

以Promise形式获取订阅者的订阅信息。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型                                                         | 说明                   |
| ------------------------------------------------------------ | ---------------------- |
| Promise\<[CommonEventSubscribeInfo](#commoneventsubscribeinfo)> | 表示订阅者的订阅信息。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

subscriber.getSubscribeInfo().then((subscribeInfo) => {
    console.info("subscribeInfo " + JSON.stringify(subscribeInfo));
}).catch((err) => {
    console.error("getSubscribeInfo failed " + JSON.stringify(err));
});
```

### finishCommonEvent<sup>9+</sup>

```ts
finishCommonEvent(callback: AsyncCallback<void>): void
```

以回调形式结束当前有序公共事件。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                  | 必填 | 说明                              |
| -------- | -------------------- | ---- | -------------------------------- |
| callback | AsyncCallback\<void> | 是   | 表示有序公共事件结束后的回调函数。 |

**示例：**

```ts
let subscriber; //创建成功的订阅者对象

//结束当前有序公共事件的回调
function finishCB(err) {
  if (err.code) {
    console.error("finishCommonEvent failed " + JSON.stringify(err));
} else {
    console.info("FinishCommonEvent");
}
}
subscriber.finishCommonEvent(finishCB);
```

### finishCommonEvent<sup>9+</sup>

```ts
finishCommonEvent(): Promise<void\>
```

以Promise形式结束当前有序公共事件。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型             | 说明                 |
| ---------------- | -------------------- |
| Promise\<void>   | 返回一个Promise的结果。 |

**示例：**

```ts
let subscriber;	//创建成功的订阅者对象

subscriber.finishCommonEvent().then(() => {
    console.info("FinishCommonEvent");
}).catch((err) => {
    console.error("finishCommonEvent failed " + JSON.stringify(err));
});
```

## CommonEventData

**系统能力：** `SystemCapability.Notification.CommonEvent`

| 名称       | 类型                 | 可读 | 可写 | 说明                                                    |
| ---------- |-------------------- | ---- | ---- |  ------------------------------------------------------- |
| event      | string               | 是  | 否  | 表示当前接收的公共事件名称。                              |
| bundleName | string               | 是  | 否  | 表示包名称。                                              |
| code       | number               | 是  | 否  | 表示公共事件的结果代码，用于传递int类型的数据。           |
| data       | string               | 是  | 否  | 表示公共事件的自定义结果数据，用于传递string类型的数据。 |
| parameters | {[key: string]: any} | 是  | 否  | 表示公共事件的附加信息。                                  |


## CommonEventPublishData

**系统能力：** `SystemCapability.Notification.CommonEvent`

| 名称                  | 类型                 | 可读 | 可写 | 说明                         |
| --------------------- | -------------------- | ---- | ---- | ---------------------------- |
| bundleName            | string               | 是  | 否  | 表示包名称。                   |
| code                  | number               | 是  | 否  | 表示公共事件的结果代码。       |
| data                  | string               | 是  | 否  | 表示公共事件的自定义结果数据。 |
| subscriberPermissions | Array\<string>       | 是  | 否  | 表示订阅者的权限。             |
| isOrdered             | boolean              | 是  | 否  | 表示是否是有序事件。           |
| isSticky              | boolean              | 是  | 否  | 表示是否是粘性事件。仅系统应用或系统服务允许发送粘性事件。 |
| parameters            | {[key: string]: any} | 是  | 否  | 表示公共事件的附加信息。       |

## CommonEventSubscribeInfo

**系统能力：** `SystemCapability.Notification.CommonEvent`

| 名称                | 类型           | 可读 | 可写 | 说明                                                         |
| ------------------- | -------------- | ---- | ---- | ------------------------------------------------------------ |
| events              | Array\<string> | 是  | 否  | 表示要发送的公共事件。                                         |
| publisherPermission | string         | 是  | 否  | 表示发布者的权限。                                             |
| publisherDeviceId   | string         | 是  | 否  | 表示设备ID，该值必须是同一ohos网络上的现有设备ID。             |
| userId              | number         | 是  | 否  | 表示用户ID。此参数是可选的，默认值当前用户的ID。如果指定了此参数，则该值必须是系统中现有的用户ID。 |
| priority            | number         | 是  | 否  | 表示订阅者的优先级。值的范围是-100到1000。                     |
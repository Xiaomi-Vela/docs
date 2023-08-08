# @ohos.calendarManager (日程管理能力)

本模块提供日历与日程管理能力，包括日历和日程的创建、删除、修改、查询等。日历[Calendar](#calendar)主要包含帐户信息[CalendarAccount](#calendaraccount)和配置信息[CalendarConfig](#calendarconfig)。日历Calendar与日程Event属于一对多关系，一个Calendar可以有多个Event，一个Event只属于一个Calendar。

> **说明：**
>
> 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```js
import calendarManager from '@ohos.calendarManager';
```


## calendarManager.createCalendar

createCalendar(calendarAccount: CalendarAccount, callback: AsyncCallback\<Calendar>): void

根据日历帐户信息，创建一个Calendar对象，使用callback异步回调。

**需要权限**： ohos.permission.WRITE_CALENDAR or ohos.permission.WRITE_WHOLE_CALENDAR

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名          | 类型                                  | 必填 | 说明                               |
| --------------- | ------------------------------------- | ---- | ---------------------------------- |
| calendarAccount | [CalendarAccount](#calendaraccount)   | 是   | 日历帐户信息。                     |
| callback        | AsyncCallback\<[Calendar](#calendar)> | 是   | 回调函数，返回创建的Calendar对象。 |

**示例**：

```js
let calendar = null;
const calendarAccount: calendarManager.CalendarAccount = {
  name: 'MyCalendar',
  type: calendarManager.CalendarType.LOCAL
};
calendarManager.createCalendar(calendarAccount, (err, data) => {
  if (err) {
    console.error("Failed to create calendar");
  } else {
    console.info("Succeeded in creating calendar");
    calendar = data;  
  }
});
```

## calendarManager.createCalendar

createCalendar(calendarAccount: CalendarAccount): Promise\<Calendar>

根据日历帐户信息，创建一个Calendar对象，使用Promise异步回调。

**需要权限**： ohos.permission.WRITE_CALENDAR or ohos.permission.WRITE_WHOLE_CALENDAR

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名          | 类型                                | 必填 | 说明           |
| --------------- | ----------------------------------- | ---- | -------------- |
| calendarAccount | [CalendarAccount](#calendaraccount) | 是   | 日历帐户信息。 |

**返回值**：

| 类型                           | 说明                                  |
| ------------------------------ | ------------------------------------- |
| Promise<[Calendar](#calendar)> | Promise对象，返回创建的Calendar对象。 |

**示例**：

```js
let calendar = null;
const calendarAccount: calendarManager.CalendarAccount = {
  name: 'MyCalendar',
  type: calendarManager.CalendarType.LOCAL
};
calendarManager.createCalendar(calendarAccount).then((data) => {
  console.info("succeeded in creating calendar");
  calendar = data;
}).catch((err) => {
  console.error("Failed to create calendar");
});
```

## calendarManager.deleteCalendar

deleteCalendar(calendar: Calendar, callback: AsyncCallback\<void>): void

删除指定Calendar对象，使用callback异步回调。

**需要权限**： ohos.permission.WRITE_CALENDAR or ohos.permission.WRITE_WHOLE_CALENDAR

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名   | 类型                  | 必填 | 说明           |
| -------- | --------------------- | ---- | -------------- |
| calendar | [Calendar](#calendar) | 是   | Calendar对象。 |
| callback | AsyncCallback\<void>  | 是   | 回调函数。     |

**示例**：

```js
calendarManager.deleteCalendar(specificCalendar, (err) => {
  if (err) {
    console.error("Failed to delete calendar");
  } else {
    console.info("Succeeded in deleting calendar");
  }
});
```

## calendarManager.deleteCalendar

deleteCalendar(calendar: Calendar): Promise\<void>

删除指定Calendar对象，使用Promise异步回调。

**需要权限**： ohos.permission.WRITE_CALENDAR or ohos.permission.WRITE_WHOLE_CALENDAR

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名   | 类型                  | 必填 | 说明           |
| -------- | --------------------- | ---- | -------------- |
| calendar | [Calendar](#calendar) | 是   | Calendar对象。 |

**返回值**：

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | 无返回结果的Promise对象。 |

**示例**：

```js
calendarManager.deleteCalendar(specificCalendar).then(() => {
  console.error("Succeeded in deleting calendar");
}).catch((err) => {
  console.info("Failed to delete calendar");
});
```

## calendarManager.getCalendar

getCalendar(callback: AsyncCallback\<Calendar>): void

获取默认Calendar对象，默认Calendar是初始化数据库时创建的，若创建Event时不关注其Calendar归属，无须通过[createCalendar()](#calendarmanagercreatecalendar)创建Calendar，直接使用默认Calendar，使用callback异步回调。

**需要权限**：ohos.permission.READ_CALENDAR or ohos.permission.READ_WHOLE_CALENDAR

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名   | 类型                                 | 必填 | 说明                                 |
| -------- | ------------------------------------ | ---- | ------------------------------------ |
| callback | AsyncCallback<[Calendar](#calendar)> | 是   | 回调函数，返回查询到的Calendar对象。 |

**示例**：

```js
let calendar = null;
calendarManager.getCalendar((err, data) => {
  if (err) {
    console.error("Failed to get calendar");
  } else {
    console.info("Succeeded in getting calendar");
    calendar = data;  
  }
});
```

## calendarManager.getCalendar

getCalendar(calendarAccount: CalendarAccount, callback: AsyncCallback\<Calendar>): void

获取指定Calendar对象，使用callback异步回调。

**需要权限**： ohos.permission.READ_CALENDAR or ohos.permission.READ_WHOLE_CALENDAR

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名          | 类型                                 | 必填 | 说明                                 |
| --------------- | ------------------------------------ | ---- | ------------------------------------ |
| calendarAccount | [CalendarAccount](#calendaraccount)  | 是   | 日历帐户信息。                       |
| callback        | AsyncCallback<[Calendar](#calendar)> | 是   | 回调函数，返回查询到的Calendar对象。 |

**示例**：

```js
let calendar = null;
calendarManager.getCalendar(calendarAccount, (err, data) => {
  if (err) {
    console.error("Failed to get calendar");
  } else {
    console.info("Succeeded in getting calendar");
    calendar = data;
  }
});
```

## calendarManager.getCalendar

getCalendar(calendarAccount?: CalendarAccount): Promise\<Calendar>

获取默认Calendar对象或者指定Calendar对象，使用Promise异步回调。

**需要权限**： ohos.permission.READ_CALENDAR or ohos.permission.READ_WHOLE_CALENDAR

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名          | 类型                                | 必填 | 说明                                                         |
| --------------- | ----------------------------------- | ---- | ------------------------------------------------------------ |
| calendarAccount | [CalendarAccount](#calendaraccount) | 否   | 日历帐户信息，用来获取指定Calendar对象，不填时，表示获取默认Calendar对象。 |

**返回值**：

| 类型                           | 说明                                    |
| ------------------------------ | --------------------------------------- |
| Promise<[Calendar](#calendar)> | Promise对象，返回查询到的Calendar对象。 |

**示例**：

```js
let calendar = null;
calendarManager.getCalendar().then((data) => {
  console.info("Succeeded in getting calendar");
  calendar = data;
}).catch((err) => {
  console.error("Failed to get calendar");
});
```

## calendarManager.getAllCalendars

getAllCalendars(callback: AsyncCallback\<Calendar[]>): void

获取当前应用所有创建的Calendar对象以及默认Calendar对象，使用callback异步回调。

**需要权限**：ohos.permission.READ_CALENDAR or ohos.permission.READ_WHOLE_CALENDAR

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名   | 类型                                   | 必填 | 说明                                      |
| -------- | -------------------------------------- | ---- | ----------------------------------------- |
| callback | AsyncCallback<[Calendar](#calendar)[]> | 是   | 回调函数， 返回查询到的Calendar对象数组。 |

**示例**：

```js
calendarManager.getAllCalendars((err, data) => {
  if (err) {
    console.error("Failed to get all calendars");
  } else {
    console.info("Succeeded in getting all calendars");
  }
});
```

## calendarManager.getAllCalendars

getAllCalendars(): Promise\<Calendar[]>

获取当前应用所有创建的Calendar对象以及默认Calendar对象，使用Promise异步回调。

**需要权限**： ohos.permission.READ_CALENDAR or ohos.permission.WRITE_WHOLE_CALENDAR

**系统能力**： SystemCapability.Applications.CalendarData

**返回值**：

| 类型                             | 说明                                        |
| -------------------------------- | ------------------------------------------- |
| Promise<[Calendar](#calendar)[]> | Promise对象，返回查询到的Calendar对象数组。 |

**示例**：

```js
calendarManager.getAllCalendars().then((data) => {
  console.info("Succeeded in getting all calendars");
}).catch((err) => {
  console.error("Failed to get all calendars");
});
```

## Calendar

下列API示例中需先通过[createCalendar()](#calendarmanagercreatecalendar)、[getCalendar()](#calendarmanagergetcalendar)中任一方法获取Calendar对象，再通过此对象调用对应方法，对该Calendar下的日程进行创建、删除、修改、查询等操作。

### 属性

**系统能力**：SystemCapability.Applications.CalendarData

| 名称 | 类型   | 只读 | 必填 | 说明     |
| ---- | ------ | ---- | ---- | -------- |
| id   | number | 是   | 是   | 帐户id。 |

### addEvent

addEvent(event: Event, callback: AsyncCallback\<number>): void

创建日程，入参[Event](#event)不填日程id，使用callback异步回调。

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名   | 类型                   | 必填 | 说明                   |
| -------- | ---------------------- | ---- | ---------------------- |
| event    | [Event](#event)        | 是   | Event对象。            |
| callback | AsyncCallback\<number> | 是   | 回调函数，返回日程id。 |

**示例**：

```js
const date = new Date();
const event: calendarManager.Event = {
  type: calendarManager.EventType.NORMAL,
  startTime: date.getTime(),
  endTime: date.getTime() + 60 * 60 * 1000
};
calendar.addEvent(event, (err, data) => {
  if (err) {
    console.error("Failed to add event");
  } else {
    console.info("Succeeded in adding event");
  }
});
```

### addEvent

addEvent(event: Event): Promise\<number>

创建日程，入参[Event](#event)不填日程id，使用Promise异步回调。

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名 | 类型            | 必填 | 说明        |
| ------ | --------------- | ---- | ----------- |
| event  | [Event](#event) | 是   | Event对象。 |

**返回值**：

| 类型             | 说明                        |
| ---------------- | --------------------------- |
| Promise\<number> | Promise对象，返回日程的id。 |

**示例**：

```js
const date = new Date();
const event: calendarManager.Event = {
  type: calendarManager.EventType.NORMAL,
  startTime: date.getTime(),
  endTime: date.getTime() + 60 * 60 * 1000
};
calendar.addEvent(event).then((data) => {
  console.info("Succeeded in adding event");
}).catch((err) => {
  console.error("Failed to add event");
});
```

### addEvents

addEvents(events: Event[], callback: AsyncCallback\<void>): void

批量创建日程，入参[Event](#event)不填日程id，使用callback异步回调。

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名   | 类型                 | 必填 | 说明            |
| -------- | -------------------- | ---- | --------------- |
| events   | [Event](#event)[]    | 是   | Event对象数组。 |
| callback | AsyncCallback\<void> | 是   | 回调函数。      |

**示例**：

```js
const date = new Date();
const events: calendarManager.Event[] = [
  {
    type: calendarManager.EventType.NORMAL,
    startTime: date.getTime(),
    endTime: date.getTime() + 60 * 60 * 1000
  },
  {
    type: calendarManager.EventType.NORMAL,
    startTime: date.getTime(),
    endTime: date.getTime() + 60 * 60 * 1000
  }
];
calendar.addEvents(events, (err) => {
  if (err) {
    console.error("Failed to add events");
  } else {
    console.info("Succeeded in adding events");
  }
});
```

### addEvents

addEvents(events: Event[]): Promise\<void>

批量创建日程，入参[Event](#event)不填日程id，使用Promise异步回调。

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名 | 类型              | 必填 | 说明            |
| ------ | ----------------- | ---- | --------------- |
| events | [Event](#event)[] | 是   | Event对象数组。 |

**返回值**：

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | 无返回结果的Promise对象。 |

**示例**：

```js
const date = new Date();
const events: calendarManager.Event[] = [
  {
    type: calendarManager.EventType.NORMAL,
    startTime: date.getTime(),
    endTime: date.getTime() + 60 * 60 * 1000
  },
  {
    type: calendarManager.EventType.NORMAL,
    startTime: date.getTime(),
    endTime: date.getTime() + 60 * 60 * 1000
  }
];
calendar.addEvents(events).then(() => {
  console.info("Succeeded in adding events");
}).catch((err) => {
  console.error("Failed to add events");
});
```

### deleteEvent

deleteEvent(id: number, callback: AsyncCallback\<void>): void

删除指定id的日程，使用callback异步回调。

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名   | 类型                 | 必填 | 说明       |
| -------- | -------------------- | ---- | ---------- |
| id       | number               | 是   | 日程id。   |
| callback | AsyncCallback\<void> | 是   | 回调函数。 |

**示例**：

```js
calendar.deleteEvent(1, (err) => {
  if (err) {
    console.error("Failed to delete event");
  } else {
    console.info("Succeeded in deleting event");
  }
});
```

### deleteEvent

deleteEvent(id: number): Promise\<void>

删除指定id的日程，使用Promise异步回调。

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名 | 类型   | 必填 | 说明     |
| ------ | ------ | ---- | -------- |
| id     | number | 是   | 日程id。 |

**返回值**：

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | 无返回结果的Promise对象。 |

**示例**：

```js
calendar.deleteEvent(1).then(() => {
  console.info("Succeeded in deleting event");
}).catch((err) => {
  console.error("Failed to delete event");
});
```

### deleteEvents

deleteEvents(ids: number[], callback: AsyncCallback\<void>): void

根据日程id，批量删除日程，使用callback异步回调。

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名   | 类型                 | 必填 | 说明         |
| -------- | -------------------- | ---- | ------------ |
| ids      | number[]             | 是   | 日程id数组。 |
| callback | AsyncCallback\<void> | 是   | 回调函数。   |

**示例**：

```js
calendar.deleteEvents([1, 2], (err) => {
  if (err) {
    console.error("Failed to delete events");
  } else {
    console.info("Succeeded in deleting events");
  }
});
```

### deleteEvents

deleteEvents(ids: number[]): Promise\<void>

根据日程id，批量删除日程，使用Promise异步回调。

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名 | 类型     | 必填 | 说明         |
| ------ | -------- | ---- | ------------ |
| ids    | number[] | 是   | 日程id数组。 |

**返回值**：

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | 无返回结果的Promise对象。 |

**示例**：

```js
calendar.deleteEvents([1, 2]).then(() => {
  console.info("Succeeded in deleting events");
}).catch((err) => {
  console.error("Failed to delete events");
});
```

### updateEvent

updateEvent(event: Event, callback: AsyncCallback\<void>): void

更新日程，使用callback异步回调。

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名   | 类型                 | 必填 | 说明        |
| -------- | -------------------- | ---- | ----------- |
| event    | [Event](#event)      | 是   | Event对象。 |
| callback | AsyncCallback\<void> | 是   | 回调函数。  |

**示例**：

```js
const date = new Date();
const event: calendarManager.Event = {
  id: 1,
  title: 'update',
  type: calendarManager.EventType.NORMAL,
  startTime: date.getTime(),
  endTime: date.getTime() + 60 * 60 * 1000
};
calendar.updateEvent(event, (err) => {
  if (err) {
    console.error("Failed to update event");
  } else {
    console.info("Succeeded in updating event");
  }
});
```

### updateEvent

updateEvent(event: Event): Promise\<void>

更新日程，使用Promise异步回调。

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名 | 类型            | 必填 | 说明        |
| ------ | --------------- | ---- | ----------- |
| event  | [Event](#event) | 是   | Event对象。 |

**返回值**：

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | 无返回结果的Promise对象。 |

**示例**：

```js
const date = new Date();
const event: calendarManager.Event = {
  id: 1,
  title: 'update',
  type: calendarManager.EventType.NORMAL,
  startTime: date.getTime(),
  endTime: date.getTime() + 60 * 60 * 1000
};
calendar.updateEvent(event).then(() => {
  console.info("Succeeded in updating event");
}).catch((err) => {
  console.error("Failed to update event");
});
```

### getEvents

getEvents(callback: AsyncCallback\<Event[]>): void

查询Calendar下所有Event，使用callback异步回调。

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名   | 类型                             | 必填 | 说明                              |
| -------- | -------------------------------- | ---- | --------------------------------- |
| callback | AsyncCallback<[Event](#event)[]> | 是   | 回调函数，返回的是Event对象数组。 |

**示例**：

```js
calendar.getEvents((err, data) => {
  if (err) {
    console.error("Failed to get events");
  } else {
    console.info("Succeeded in getting events");
  }
});
```

### getEvents

getEvents(eventFilter: EventFilter, eventKey: (keyof Event)[], callback: AsyncCallback\<Event[]>):void

获取Calendar下符合查询条件的Event，使用callback异步回调。

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名      | 类型                             | 必填 | 说明                              |
| ----------- | -------------------------------- | ---- | --------------------------------- |
| eventFilter | [EventFilter](#eventfilter)      | 是   | 查询条件。                        |
| eventKey    | (keyof [Event](#event))[]        | 是   | 查询字段。                        |
| callback    | AsyncCallback<[Event](#event)[]> | 是   | 回调函数，返回的是Event对象数组。 |

**示例**：

```js
const filter = calendarManager.EventFilter.filterById([1, 2]);
const columns: (keyof calendarManager.Event)[] =  ['title', 'type', 'startTime', 'endTime'];
calendar.getEvents(filter, columns, (err, data) => {
  if (err) {
    console.error("Failed to get events");
  } else {
    console.info("Succeeded in getting events");
  }
});
```

### getEvents

getEvents(eventFilter?: EventFilter, eventKey?: (keyof Event)[]): Promise\<Event[]>

获取Calendar下符合查询条件的Event，使用Promise异步回调。

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名      | 类型                        | 必填 | 说明       |
| ----------- | --------------------------- | ---- | ---------- |
| eventFilter | [EventFilter](#eventfilter) | 否   | 查询条件。 |
| eventKey    | (keyof [Event](#event))[]   | 否   | 查询字段。 |

**返回值**：

| 类型                       | 说明                                |
| -------------------------- | ----------------------------------- |
| Promise<[Event](#event)[]> | Promise对象，返回日程配置信息数组。 |

**示例**：

```js
const filter = calendarManager.EventFilter.filterByTitle('MyEvent');
calendar.getEvents(filter).then((data) => {
  console.info("Succeeded in getting events");
}).catch((err) => {
  console.error("Failed to get events");
});
```

### getConfig

getConfig(): CalendarConfig

获取日历配置信息。

**系统能力**： SystemCapability.Applications.CalendarData

**返回值**：

| 类型                              | 说明           |
| --------------------------------- | -------------- |
| [CalendarConfig](#calendarconfig) | 日历配置信息。 |

**示例**：

```js
const config = calendar.getConfig();
console.info("get config success");
```

### setConfig

setConfig(config: CalendarConfig, callback: AsyncCallback\<void>): void

设置日历配置信息，使用callback异步回调。

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名   | 类型                              | 必填 | 说明           |
| -------- | --------------------------------- | ---- | -------------- |
| config   | [CalendarConfig](#calendarconfig) | 是   | 日历配置信息。 |
| callback | AsyncCallback\<void>              | 是   | 回调函数。     |

**示例**：

```js
const config: calendarManager.CalendarConfig = {
  enableReminder: true
};
calendar.setConfig(config, (err) => {
  if (err) {
    console.error("Failed to set config");
  } else {
    console.info("Succeeded in setting config");
  }
});
```

### setConfig

setConfig(config: CalendarConfig): Promise\<void>

设置日历配置信息，使用Promise异步回调。

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名 | 类型                              | 必填 | 说明           |
| ------ | --------------------------------- | ---- | -------------- |
| config | [CalendarConfig](#calendarconfig) | 是   | 日历配置信息。 |

**返回值**：

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | 无返回结果的Promise对象。 |

**示例**：

```js
const config: calendarManager.CalendarConfig = {
  enableReminder: true
};
calendar.setConfig(config).then(() => {
  console.info("Succeeded in setting config");
}).catch((err) => {
  console.error("Failed to set config");
});
```

### getAccount

getAccount(): CalendarAccount

获取日历账户信息。

**系统能力**： SystemCapability.Applications.CalendarData

**返回值**：

| 类型                                | 说明           |
| ----------------------------------- | -------------- |
| [CalendarAccount](#calendaraccount) | 日历帐户信息。 |

**示例**：

```js
const account = calendar.getAccount();
console.info("get account success");
```

## CalendarAccount

日历帐户信息。

**系统能力**：SystemCapability.Applications.CalendarData

| 名称        | 类型                          | 只读 | 必填 | 说明                                   |
| ----------- | ----------------------------- | ---- | ---- | -------------------------------------- |
| name        | string                        | 是   | 是   | 帐户名称。                             |
| type        | [CalendarType](#calendartype) | 否   | 是   | 帐户类型。                             |
| displayName | string                        | 否   | 否   | 帐户的显示名称。不填时，默认为空字符串 |

## CalendarConfig

日历配置信息。

**系统能力**：SystemCapability.Applications.CalendarData

| 名称           | 类型                                                | 只读 | 必填 | 说明                                                         |
| -------------- | --------------------------------------------------- | ---- | ---- | ------------------------------------------------------------ |
| enableReminder | boolean                                             | 否   | 否   | 是否打开Calendar下所有Event提醒能力。当取值为true时，该Calendar下所有Event具备提醒能力；当取值为false时，不具备提醒能力，默认具备提醒能力。 |
| color          | [ResourceColor](../arkui-ts/ts-types.md#resourcecolor) | 否   | 否   | 设置Calendar颜色。不填时，默认值为'#0A59F7'。                |

## Event

日程对象，包含日程标题、开始时间、结束时间等信息。

**系统能力**：SystemCapability.Applications.CalendarData

| 名称           | 类型                              | 只读 | 必填 | 说明                                                         |
| -------------- | --------------------------------- | ---- | ---- | ------------------------------------------------------------ |
| id             | number                            | 是   | 否   | 日程id。当调用[addEvent()](#addevent)、[addEvents()](#addevents)创建日程时，不填写此参数。 |
| type           | [EventType](#eventtype)           | 否   | 是   | 日程类型。                                                   |
| title          | string                            | 否   | 否   | 日程标题。不填时，默认为空字符串。                             |
| location       | [Location](#location)             | 否   | 否   | 日程地点。不填时，默认为null。                               |
| startTime      | number                            | 否   | 是   | 日程开始时间。                                               |
| endTime        | number                            | 否   | 是   | 日程结束时间。                                               |
| isAllDay       | boolean                           | 否   | 否   | 是否为全天日程。当取值为true时，说明为全天日程；当取值为false时，说明不是全天日程，默认为非全天日程。 |
| attendee       | [Attendee](#attendee)[]           | 否   | 否   | 日程参与者。不填时，默认为null。                             |
| timeZone       | string                            | 否   | 否   | 日程时区。不填时，默认为当前所在时区，当需要创建与当前不一样的时区时，可填入对应的时区。可通过[getTimeZone()](js-apis-system-date-time.md#systemdatetimegettimezone)获取当前系统时区。 |
| reminderTime   | number[]                          | 否   | 否   | 日程提醒时间。不填时，默认为不提醒。                           |
| recurrenceRule | [RecurrenceRule](#recurrencerule) | 否   | 否   | 日程重复规则。不填时，默认为不重复。                           |
| description    | string                            | 否   | 否   | 日程描述。不填时，默认为空字符串。                             |
| service        | [EventService](#eventservice)     | 否   | 否   | 日程服务。不填时，默认没有一键服务。                           |

## CalendarType

帐户类型枚举。

**系统能力**：SystemCapability.Applications.CalendarData

| 名称       | 值           | 说明                 |
| ---------- | ------------ | -------------------- |
| LOCAL      | 'local'      | 本地帐户。           |
| EMAIL      | 'email'      | 邮箱帐户。           |
| BIRTHDAY   | 'birthday'   | 生日帐户。           |
| CALDAV     | 'caldav'     | 支持CalDAV协议帐户。 |
| SUBSCRIBED | 'subscribed' | 订阅帐户。           |

## Location

日程地点。

**系统能力**：SystemCapability.Applications.CalendarData

| 名称      | 类型   | 只读 | 必填 | 说明                     |
| --------- | ------ | ---- | ---- | ------------------------ |
| location  | string | 否   | 否   | 地点位置。默认为空字符串 |
| longitude | number | 否   | 否   | 地点经度。默认为0。        |
| latitude  | number | 否   | 否   | 地点纬度。默认为0。        |

## EventFilter

日程过滤器，查询日程时进行筛选过滤，获取符合条件的日程。

通过[filterById()](#filterbyid)、[filterByTime()](#filterbytime)、[filterByTitle()](#filterbytitle)任一方法获取日程过滤器，传入[getEvents()](#getevents)过滤。

### filterById

static filterById(ids: number[]): EventFilter

根据日程id过滤日程。

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名 | 类型     | 必填 | 说明         |
| ------ | -------- | ---- | ------------ |
| ids    | number[] | 是   | 日程id数组。 |

**返回值**：

| 类型                        | 说明                 |
| --------------------------- | -------------------- |
| [EventFilter](#eventfilter) | 返回日程过滤器对象。 |

**示例**：

```js
const filter = calendarManager.EventFilter.filterById([1, 2]);
calendar.getEvents(filter).then((data) => {
  console.info("Succeeded in filtering by id");
}).catch((err) => {
  console.error("Failed to filter by id");
});
```

### filterByTime

static filterByTime(start: number, end: number): EventFilter

根据日程时间过滤日程。

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名 | 类型   | 必填 | 说明       |
| ------ | ------ | ---- | ---------- |
| start  | number | 是   | 开始时间。 |
| end    | number | 是   | 结束时间。 |

**返回值**：

| 类型                        | 说明                 |
| --------------------------- | -------------------- |
| [EventFilter](#eventfilter) | 返回日程过滤器对象。 |

**示例**：

```js
const filter = calendarManager.EventFilter.filterByTime(1686931200000, 1687017600000);
calendar.getEvents(filter).then((data) => {
  console.info("Succeeded in filtering by time");
}).catch((err) => {
  console.error("Failed to filter by time");
});
```

### filterByTitle

static filterByTitle(title: string): EventFilter

根据日程标题过滤日程。

**系统能力**： SystemCapability.Applications.CalendarData

**参数**：

| 参数名 | 类型   | 必填 | 说明       |
| ------ | ------ | ---- | ---------- |
| title  | string | 是   | 日程标题。 |

**返回值**：

| 类型                        | 说明                 |
| --------------------------- | -------------------- |
| [EventFilter](#eventfilter) | 返回日程过滤器对象。 |

**示例**：

```js
const filter = calendarManager.EventFilter.filterByTitle('MyEvent');
calendar.getEvents(filter).then((data) => {
  console.info("Succeeded in filtering by title");
}).catch((err) => {
  console.error("Failed to filter by title");
});
```

## EventType

日程类型枚举。

**系统能力**：SystemCapability.Applications.CalendarData

| 名称      | 值   | 说明                 |
| --------- | ---- | -------------------- |
| NORMAL    | 0    | 普通日程。           |
| IMPORTANT | 1    | 重要日程。支持倒计时。 |

## RecurrenceRule

日程重复规则。

**系统能力**：SystemCapability.Applications.CalendarData

| 名称                | 类型                                        | 只读 | 必填 | 说明                            |
| ------------------- | ------------------------------------------- | ---- | ---- | ------------------------------- |
| recurrenceFrequency | [RecurrenceFrequency](#recurrencefrequency) | 否   | 是   | 日程重复规则类型。              |
| expire              | number                                      | 否   | 否   | 重复周期截止日。不填时，默认为0。 |

## RecurrenceFrequency

日程重复规则类型枚举。

**系统能力**：SystemCapability.Applications.CalendarData

| 名称    | 值   | 说明       |
| ------- | ---- | ---------- |
| YEARLY  | 0    | 每年重复。 |
| MONTHLY | 1    | 每月重复。 |
| WEEKLY  | 2    | 每周重复。 |
| DAILY   | 3    | 每天重复。 |

## Attendee

日程参与者。

**系统能力**：SystemCapability.Applications.CalendarData

| 名称  | 类型   | 只读 | 必填 | 说明           |
| ----- | ------ | ---- | ---- | -------------- |
| name  | string | 否   | 是   | 参与者的姓名。 |
| email | string | 否   | 是   | 参与者的邮箱。 |

## EventService

日程服务。

**系统能力**：SystemCapability.Applications.CalendarData

| 名称        | 类型                        | 只读 | 必填 | 说明                                  |
| ----------- | --------------------------- | ---- | ---- | ------------------------------------- |
| type        | [ServiceType](#servicetype) | 否   | 是   | 服务类型。                            |
| uri         | string                      | 否   | 是   | 服务的uri。可以跳转到三方应用相应界面。 |
| description | string                      | 否   | 否   | 服务辅助描述。不填时，默认为空字符串。  |

## ServiceType

日程服务类型枚举。

**系统能力**：SystemCapability.Applications.CalendarData

| 名称            | 值               | 说明         |
| --------------- | ---------------- | ------------ |
| MEETING         | 'Meeting'        | 一键入会。   |
| WATCHING        | 'Watching'       | 一键追剧。   |
| REPAYMENT       | 'Repayment'      | 一键还款。   |
| LIVE            | 'Live'           | 一键直播。   |
| SHOPPING        | 'Shopping'       | 一键购物。   |
| TRIP            | 'Trip'           | 一键查看。   |
| CLASS           | 'Class'          | 一键上课。   |
| SPORTS_EVENTS   | 'SportsEvents'   | 一键看赛事。 |
| SPORTS_EXERCISE | 'SportsExercise' | 一键运动。   |
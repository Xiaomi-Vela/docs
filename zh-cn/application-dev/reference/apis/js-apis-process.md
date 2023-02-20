# 获取进程相关的信息

> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```
import process from '@ohos.process';
```


## 属性

**系统能力：** 以下各项对应的系统能力均为SystemCapability.Utils.Lang。

| 名称 | 类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| egid | number | 是 | 否 | 进程的有效组标识。该接口为系统接口，三方应用不支持调用。 |
| euid | number | 是 | 否 | 进程的有效用户身份。该接口为系统接口，三方应用不支持调用。 |
| gid | number | 是 | 否 | 进程的组标识。该接口为系统接口，三方应用不支持调用。 |
| uid | number | 是 | 否 | 进程的用户标识。 |
| groups | number[] | 是 | 否 | 带有补充组id的数组。该接口为系统接口，三方应用不支持调用。 |
| pid | number | 是 | 否 | 当前进程的pid。 |
| ppid | number | 是 | 否 | 当前进程的父进程的pid。该接口为系统接口，三方应用不支持调用。 |
| tid<sup>8+</sup> | number | 是 | 否 | 当前线程的tid。 |


## ChildProcess

主进程可以获取子进程的标准输入输出，以及发送信号和关闭子进程。


### 属性

**系统能力：** 以下各项对应的系统能力均为SystemCapability.Utils.Lang。

| 名称 | 类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| pid | number | 是 | 否 | 子进程的pid。该接口为系统接口，三方应用不支持调用。 |
| ppid | number | 是 | 否 | 子进程的父进程的pid。该接口为系统接口，三方应用不支持调用。 |
| exitCode | number | 是 | 否 | 子进程的退出码。该接口为系统接口，三方应用不支持调用。 |
| killed | boolean | 是 | 否 | 父进程给子进程发信号是否成功。该接口为系统接口，三方应用不支持调用。 |


### wait

wait(): Promise&lt;number&gt;

等待子进程运行结束，返回promise对象，其值为子进程的退出码。

该接口为系统接口，三方应用不支持调用。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;number&gt; | 异步返回子进程的退出码。 |

**示例：**

```js
var child = process.runCmd('ls');
var result = child.wait();
result.then(val=>{
    console.log("result = " + val);
})
```


### getOutput

getOutput(): Promise&lt;Uint8Array&gt;

获取子进程的标准输出。

该接口为系统接口，三方应用不支持调用。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;Uint8Array&gt; | 异步返回标准输出的字节流。 |

**示例：**

```js
var child = process.runCmd('ls');
var result = child.wait();
child.getOutput.then(val=>{
    console.log("child.getOutput = " + val);
})
```


### getErrorOutput

getErrorOutput(): Promise&lt;Uint8Array&gt;

获取子进程的标准错误输出。

该接口为系统接口，三方应用不支持调用。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;Uint8Array&gt; | 异步返回标准错误输出的字节流。 |

**示例：**

```js
var child = process.runCmd('madir test.text');
var result = child.wait();
child.getErrorOutput.then(val=>{
    console.log("child.getErrorOutput= " + val);
})
```


### close

close(): void

关闭正在运行的子进程。

该接口为系统接口，三方应用不支持调用。

**系统能力：** SystemCapability.Utils.Lang

**示例：**

```js
var child = process.runCmd('sleep 5; ls');
child.close();
```


### kill

kill(signal: number | string): void

用于发送信号给子进程，结束指定进程。

该接口为系统接口，三方应用不支持调用。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| signal | number&nbsp;\|&nbsp;string | 是 | 数字或字符串。 |

**示例：**

```js
var child = process.runCmd('sleep 5; ls');
child.kill(9);
```


## process.isIsolatedProcess<sup>8+</sup>

isIsolatedProcess(): boolean

判断进程是否被隔离。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 返回判断结果，如果返回true表示进程被隔离。 |

**示例：**

```js
var result = process.isIsolatedProcess();
```


## process.isAppUid<sup>8+</sup>

isAppUid(v: number): boolean

判断uid是否属于应用程序。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| v | number | 是 | 应用程序的uid。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 返回判断结果，如果返回true表示为应用程序的uid。|

**示例：**

```js
var result = process.isAppUid(688);
```


## process.is64Bit<sup>8+</sup>

is64Bit(): boolean

判断运行环境是否64位。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 返回判断结果，如果返回true表示为64位环境。 |

**示例：**

```js
var ressult = process.is64Bit();
```


## process.getUidForName<sup>8+</sup>

getUidForName(v: string): number

通过进程名获取进程uid。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| v | string | 是 | 进程名。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回进程uid。|

**示例：**

```js
var pres = process.getUidForName("tool")
```


## process.getThreadPriority<sup>8+</sup>

getThreadPriority(v: number): number

根据指定的tid获取线程优先级。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| v | number | 是 | 指定的线程tid。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回线程的优先级。 |

**示例：**

```js
var tid = process.getTid();
var pres = process.getThreadPriority(tid);
```


## process.getStartRealtime<sup>8+</sup>

getStartRealtime(): number

获取从系统启动到进程启动所经过的实时时间（以毫秒为单位）。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回经过的实时时间。|

**示例：**

```js
var realtime = process.getStartRealtime();
```

## process.getPastCpuTime<sup>8+</sup>

getPastCpuTime(): number

获取进程启动到当前时间的CPU时间（以毫秒为单位）。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回经过的CPU时间。 |

**示例：**

```js
var result = process.getPastCpuTime() ;
```


## process.getSystemConfig<sup>8+</sup>

getSystemConfig(name: number): number

获取系统配置信息。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| name | number | 是 | 指定系统配置参数名。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回系统配置信息。 |

**示例：**

```js
var _SC_ARG_MAX = 0
var pres = process.getSystemConfig(_SC_ARG_MAX)
```


## process.getEnvironmentVar<sup>8+</sup>

getEnvironmentVar(name: string): string

用该方法获取环境变量对应的值。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| name | string | 是 | 环境变量名。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| string | 返回环境变量名对应的value。 |

**示例：**

```js
var pres = process.getEnvironmentVar("PATH")
```


## process.runCmd

runCmd(command: string, options?: { timeout : number, killSignal : number | string, maxBuffer : number }): ChildProcess

通过runcmd可以fork一个新的进程来运行一段shell，并返回ChildProcess对象。

该接口为系统接口，三方应用不支持调用。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| command | string | 是 | shell命令。 |
| options | Object | 否 | 相关选项参数。 |

**表1** options

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| timeout | number | 否 | 子进程运行的ms数，当子进程运行时间超出此时间，则父进程发送killSignal信号给子进程。timeout默认为0。 |
| killSignal | number&nbsp;&nbsp;\|&nbsp;string | 否 | 子进程运行时间超出timeout时，父进程发送killSignal&nbsp;信号给子进程。killSignal&nbsp;默认为'SIGTERM'。 |
| maxBuffer | number | 否 | 子进程标准输入输出的最大缓冲区大小，当超出此大小时则终止子进程。maxBuffer默认1024\*1024。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [ChildProcess](#childprocess) | 子进程对象。 |

**示例：**

```js
var child = process.runCmd('ls', { maxBuffer : 2 });
var result = child.wait();
child.getOutput.then(val=>{
    console.log("child.getOutput = " + val);
})
```


## process.abort

abort(): void

该方法会导致进程立即退出并生成一个核心文件，谨慎使用。

**系统能力：** SystemCapability.Utils.Lang

**示例：**

```js
process.abort();
```


## process.on

on(type: string, listener: EventListener): void

存储用户所触发的事件。

该接口为系统接口，三方应用不支持调用。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 存储事件的type。 |
| listener | EventListener | 是 | 回调的事件。 |

**表2** EventListener

| 名称 | 说明 |
| -------- | -------- |
| EventListener&nbsp;=&nbsp;(evt: &nbsp;Object)&nbsp;=&gt;&nbsp;void | 用户存储的事件。 |

**示例：**

```js
process.on("data", (e)=>{
    console.log("data callback");
})
```


## process.off

off(type: string): boolean

删除用户存储的事件。

该接口为系统接口，三方应用不支持调用。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 删除事件的type。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 事件是否删除成功。 |

**示例：**

```js
process.on("data", (e)=>{
    console.log("data callback");
})
var result = process.off("data");
```


## process.exit

exit(code: number): void

终止程序。

请谨慎使用此接口。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| code | number | 是 | 进程的退出码。 |

**示例：**

```js
process.exit(0);
```


## process.cwd

cwd(): string

用该方法获取进程的工作目录。

该接口为系统接口，三方应用不支持调用。

**系统能力：** SystemCapability.Utils.Lang

**示例：**

```js
var path = process.cwd();
```


## process.chdir

chdir(dir: string): void

更改进程的当前工作目录。

该接口为系统接口，三方应用不支持调用。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| dir | string | 是 | 路径。 |

**示例：**

```js
process.chdir('/system');
```


## process.uptime

uptime(): number

获取当前系统已运行的秒数。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 当前系统已运行的秒数。 |

**示例：**

```js
var time = process.uptime();
```


## process.kill

kill(signal: number, pid: number): boolean

发送signal到指定的进程，结束指定进程。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| pid | number | 是 | 进程的id。 |
| signal | number | 是 | 发送的信号。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 信号是否发送成功。 |

**示例：**

```js
var pres = process.pid
var result = that.kill(28, pres)
```

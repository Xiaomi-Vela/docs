# TaskPool和Worker的对比


TaskPool（任务池）和Worker的作用是为应用程序提供一个多线程的运行环境，用于处理耗时的计算任务或其他密集型任务。可以有效地避免这些任务阻塞主线程，从而最大化系统的利用率，降低整体资源消耗，并提高系统的整体性能。


本文将从[实现特点](#实现特点对比)和[适用场景](#适用场景对比)两个方面来进行TaskPool与Worker的比较，同时提供了各自运作机制和注意事项的相关说明。


## 实现特点对比

**表1** TaskPool和Worker的实现特点对比

| 实现 | TaskPool | Worker |
| -------- | -------- | -------- |
| 内存模型 | 线程间隔离，内存不共享。 | 线程间隔离，内存不共享。 |
| 参数传递机制 | 采用标准的结构化克隆算法（Structured Clone）进行序列化、反序列化，完成参数传递。<br/>支持ArrayBuffer转移和SharedArrayBuffer共享。 | 采用标准的结构化克隆算法（Structured Clone）进行序列化、反序列化，完成参数传递。<br/>支持ArrayBuffer转移和SharedArrayBuffer共享。 |
| 参数传递 | 直接传递，无需封装，默认进行transfer。 | 消息对象唯一参数，需要自己封装。 |
| 方法调用 | 直接将方法传入调用。 | 在Worker线程中进行消息解析并调用对应方法。 |
| 返回值 | 异步调用后默认返回。 | 主动发送消息，需在onmessage解析赋值。 |
| 生命周期 | TaskPool自行管理生命周期，无需关心任务负载高低。 | 开发者自行管理Worker的数量及生命周期。 |
| 任务池个数上限 | 自动管理，无需配置。 | 最多开启8个Worker。 |
| 任务执行时长上限 | 3分钟（不包含Promise和async/await异步调用的耗时，例如网络下载、文件读写等I/O任务的耗时）。 | 无限制。 |
| 设置任务的优先级 | 支持配置任务优先级。 | 不支持。 |
| 执行任务的取消 | 支持取消已经发起的任务。 | 不支持。 |


## 适用场景对比

TaskPool和Worker均支持多线程并发能力。由于TaskPool的工作线程会绑定系统的调度优先级，并且支持负载均衡（自动扩缩容），而Worker需要开发者自行创建，存在创建耗时以及不支持设置调度优先级，故在性能方面使用TaskPool会优于Worker，因此大多数场景推荐使用TaskPool。

TaskPool偏向独立任务维度，该任务在线程中执行，无需关注线程的生命周期，超长任务（大于3分钟）会被系统自动回收；而Worker偏向线程的维度，支持长时间占据线程执行，需要主动管理线程生命周期。

常见的一些开发场景及适用具体说明如下：

- 运行时间超过3分钟（不包含Promise和async/await异步调用的耗时，例如网络下载、文件读写等I/O任务的耗时）的任务。例如后台进行1小时的预测算法训练等CPU密集型任务，需要使用Worker。

- 有关联的一系列同步任务。例如在一些需要创建、使用句柄的场景中，句柄创建每次都是不同的，该句柄需永久保存，保证使用该句柄进行操作，需要使用Worker。

- 需要设置优先级的任务。例如图库直方图绘制场景，后台计算的直方图数据会用于前台界面的显示，影响用户体验，需要高优先级处理，需要使用TaskPool。

- 需要频繁取消的任务。例如图库大图浏览场景，为提升体验，会同时缓存当前图片左右侧各2张图片，往一侧滑动跳到下一张图片时，要取消另一侧的一个缓存任务，需要使用TaskPool。

- 大量或者调度点较分散的任务。例如大型应用的多个模块包含多个耗时任务，不方便使用8个Worker去做负载管理，推荐采用TaskPool。


## TaskPool运作机制

**图1** TaskPool运作机制示意图

![taskpool](figures/taskpool.png)

TaskPool支持开发者在主线程封装任务抛给任务队列，系统选择合适的工作线程，进行任务的分发及执行，再将结果返回给主线程。接口直观易用，支持任务的执行、取消，以及指定优先级的能力，同时通过系统统一线程管理，结合动态调度及负载均衡算法，可以节约系统资源。系统默认会启动一个任务工作线程，当任务较多时会扩容，工作线程数量上限跟当前设备的物理核数相关，具体数量内部管理，保证最优的调度及执行效率，长时间没有任务分发时会缩容，减少工作线程数量。


## Worker运作机制

**图2** Worker运作机制示意图

![worker](figures/worker.png)

创建Worker的线程称为宿主线程（不一定是主线程，工作线程也支持创建Worker子线程），Worker自身的线程称为Worker子线程（或Actor线程、工作线程）。每个Worker子线程与宿主线程拥有独立的实例，包含基础设施、对象、代码段等。Worker子线程和宿主线程之间的通信是基于消息传递的，Worker通过序列化机制与宿主线程之间相互通信，完成命令及数据交互。


## TaskPool注意事项

- 实现任务的函数需要使用装饰器[\@Concurrent](arkts-concurrent.md)标注，且仅支持在.ets文件中使用。

- 任务函数在TaskPool工作线程的执行耗时不能超过3分钟（不包含Promise和async/await异步调用的耗时，例如网络下载、文件读写等I/O任务的耗时），否则会被强制退出。

- 实现任务的函数入参需满足序列化支持的类型，详情请参见[数据传输对象](multi-thread-concurrency-overview.md#数据传输对象)。

- ArrayBuffer参数在TaskPool中默认转移，需要设置转移列表的话可通过接口[setTransferList()](../reference/apis/js-apis-taskpool.md#settransferlist10)设置。

- 由于不同线程中上下文对象是不同的，因此TaskPool工作线程只能使用线程安全的库，例如UI相关的非线程安全库不能使用，具体请见[多线程安全注意事项](#多线程安全注意事项)。

- 序列化传输的数据量大小限制为16MB。


## Worker注意事项

- 创建Worker时，传入的Worker.ts路径在不同版本有不同的规则，详情请参见[文件路径注意事项](#文件路径注意事项)。

- Worker创建后需要手动管理生命周期，且最多同时运行的Worker子线程数量为8个，详情请参见[生命周期注意事项](#生命周期注意事项)。

- [Ability类型](../quick-start/application-package-structure-stage.md)的Module支持使用Worker，[Library类型](../quick-start/application-package-structure-stage.md)的Module不支持使用Worker。

- 创建Worker不支持使用其他Module的Worker.ts文件，即不支持跨模块调用Worker。

- 由于不同线程中上下文对象是不同的，因此Worker线程只能使用线程安全的库，例如UI相关的非线程安全库不能使用，具体请见[多线程安全注意事项](#多线程安全注意事项)。

- 序列化传输的数据量大小限制为16MB。

- 使用Worker模块时，需要在主线程中注册onerror接口，否则当worker线程出现异常时会发生jscrash问题。


### 文件路径注意事项

  当使用Worker模块具体功能时，均需先构造Worker实例对象，其构造函数与API版本相关。

```ts
// 导入模块
import worker form '@ohos.worker';

// API 9及之后版本使用：
const worker1: worker.ThreadWorker = new worker.ThreadWorker('entry/ets/workers/MyWorker.ts');
// API 8及之前版本使用：
const worker2: worker.Worker = new worker.Worker('entry/ets/workers/MyWorker.ts');
```

构造函数需要传入Worker的路径（scriptURL），Worker文件存放位置默认路径为Worker文件所在目录与pages目录属于同级。

**Stage模型**

构造函数中的scriptURL示例如下：


```ts
// 导入模块
import worker form '@ohos.worker';

// 写法一
// Stage模型-目录同级（entry模块下，workers目录与pages目录同级）
const worker1: worker.ThreadWorker = new worker.ThreadWorker('entry/ets/workers/MyWorker.ts', {name:"first worker in Stage model"});
// Stage模型-目录不同级（entry模块下，workers目录是pages目录的子目录）
const worker2: worker.ThreadWorker = new worker.ThreadWorker('entry/ets/pages/workers/MyWorker.ts');

// 写法二
// Stage模型-目录同级（entry模块下，workers目录与pages目录同级），假设bundlename是com.example.workerdemo
const worker3: worker.ThreadWorker = new worker.ThreadWorker('@bundle:com.example.workerdemo/entry/ets/workers/worker');
// Stage模型-目录不同级（entry模块下，workers目录是pages目录的子目录），假设bundlename是com.example.workerdemo
const worker4: worker.ThreadWorker = new worker.ThreadWorker('@bundle:com.example.workerdemo/entry/ets/pages/workers/worker');
```


- 基于Stage模型工程目录结构，写法一的路径含义：
  - entry：module.json5文件中module的name属性对应值。
  - ets：用于存放ets源码，固定目录。
  - workers/MyWorker.ts：worker源文件在ets目录下的路径。

- 基于Stage模型工程目录结构，写法二的路径含义：
  - \@bundle：固定标签。
  - bundlename：当前应用包名。
  - entryname：module.json5文件中module的name属性对应值。
  - ets：用于存放ets源码，固定目录。
  - workerdir/workerfile：worker源文件在ets目录下的路径，可不带文件后缀名。


**FA模型**


  构造函数中的scriptURL示例如下：

```ts
// 导入模块
import worker form '@ohos.worker';

// FA模型-目录同级（entry模块下，workers目录与pages目录同级）
const worker1: worker.ThreadWorker = new worker.ThreadWorker('workers/worker.js', {name:'first worker in FA model'});
// FA模型-目录不同级（entry模块下，workers目录与pages目录的父目录同级）
const worker2: worker.ThreadWorker = new worker.ThreadWorker('../workers/worker.js');
```


### 生命周期注意事项

- Worker的创建和销毁耗费性能，建议开发者合理管理已创建的Worker并重复使用。Worker空闲时也会一直运行，因此当不需要Worker时，可以调用[terminate()](../reference/apis/js-apis-worker.md#terminate9)接口或[parentPort.close()](../reference/apis/js-apis-worker.md#close9)方法主动销毁Worker。若Worker处于已销毁或正在销毁等非运行状态时，调用其功能接口，会抛出相应的错误。


- Worker存在数量限制，支持最多同时存在8个Worker。
  - 在API version 8及之前的版本，当Worker数量超出限制时，会抛出“Too many workers, the number of workers exceeds the maximum.”错误。
  - 从API version 9开始，当Worker数量超出限制时，会抛出“Worker initialization failure, the number of workers exceeds the maximum.”错误。

## 多线程安全注意事项
多线程安全是指多个线程同时访问或修改共享资源时，能够保证程序的正确性和可靠性。

开发者选择TaskPool或Worker进行多线程开发时，在TaskPool和Worker的工作线程中导入的API和模块需要支持多线程安全，否则可能会导致多线程数据竞争问题，造成应用程序异常或崩溃。

在TaskPool或Worker的工作线程中支持使用以下模块，其他模块在使用时需要验证是否满足线程安全。

 - console
 - setInterval
 - setTimeout
 - clearInterval
 - clearTimeout
 - @ohos.buffer
 - @ohos.convertxml
 - @ohos.file
   - @ohos.file.backup
   - @ohos.file.cloudSync
   - @ohos.file.cloudSyncManager
   - @ohos.file.environment
   - @ohos.file.fileAccess
   - @ohos.file.fileExtensionInfo
   - @ohos.file.fileuri
   - @ohos.file.fs
   - @ohos.file.hash
   - @ohos.file.photoAccessHelper
   - @ohos.file.picker
   - @ohos.file.securityLabel
   - @ohos.file.statvfs
   - @ohos.file.storageStatistics
   - @ohos.file.volumeManager
 - @ohos.fileio
 - @ohos.hilog
 - @ohos.multimedia
   - @ohos.multimedia.image
 - @ohos.net
   - @ohos.net.http
 - @ohos.pasteboard
 - @ohos.systemDateTime
 - @ohos.systemTimer
 - @ohos.taskpool
 - @ohos.uri
 - @ohos.url
 - @ohos.util
   - @ohos.util.ArrayList
   - @ohos.util.Deque
   - @ohos.util.HashMap
   - @ohos.util.HashSet
   - @ohos.util.LightWeightMap
   - @ohos.util.LightWeightSet
   - @ohos.util.LinkedList
   - @ohos.util.List
   - @ohos.util.PlainArray
   - @ohos.util.Queue
   - @ohos.util.Stack
   - @ohos.util.TreeMap
   - @ohos.util.TreeSet
   - @ohos.util
 - @ohos.worker
 - @ohos.xml

# 启动指定页面


当PageAbility的启动模式设置为单例时（具体设置方法和典型场景示例见[PageAbility的启动模式](pageability-launch-type.md)，缺省情况下是单实例模式），若PageAbility已被拉起，再次启动PageAbility会触发onNewWant回调（即非首次拉起）。应用开发者可以通过want传递启动参数，例如开发者希望指定页面启动PageAbility，可以通过want中的parameters参数传递pages信息，具体示例代码如下：


调用方PageAbility的app.ets中或者page中，使用startAbility再次拉起PageAbility，通过want中的uri参数传递页面信息：

```ts
import featureAbility from '@ohos.ability.featureAbility';
import Want from '@ohos.app.ability.Want';

async function restartAbility() {
    let wantInfo: Want = {
        bundleName: "com.sample.MyApplication",
        abilityName: "EntryAbility",
        parameters: {
            page: "pages/second"
        }
    };
    featureAbility.startAbility({
        want: wantInfo
    }).then((data) => {
        console.info('restartAbility success.');
    });
}
```


在目标端PageAbility的onNewWant回调中获取包含页面信息的want参数：

```ts
// GlobalContext.ts 构造单例对象
export class GlobalContext {
  private constructor() {}
  private static instance: GlobalContext;
  private _objects = new Map<string, Object>();

  public static getContext(): GlobalContext {
    if (!GlobalContext.instance) {
      GlobalContext.instance = new GlobalContext();
    }
    return GlobalContext.instance;
  }

  getObject(value: string): Object | undefined {
    return this._objects.get(value);
  }

  setObject(key: string, objectClass: Object): void {
    this._objects.set(key, objectClass);
  }
}
```

```ts
import Want from '@ohos.app.ability.Want';
import { GlobalContext } from './GlobalContext';

class EntryAbility {  
  onNewWant(want: Want) { 
    GlobalContext.getContext().setObject("newWant", want);  
  }
}

export default new EntryAbility()
```


在目标端页面的自定义组件中获取包含页面信息的want参数并根据uri做路由处理：

```ts
import Want from '@ohos.app.ability.Want';
import router from '@ohos.router';
import { GlobalContext } from '../GlobalContext';

@Entry
@Component
struct Index {
  @State message: string = 'Router Page'
  
  onPageShow() {
    console.info('Index onPageShow')
    let newWant = GlobalContext.getContext().getObject("newWant") as Want
    if (newWant.parameters) {
      if (newWant.parameters.page) {
        router.push({ url: newWant.parameters.page });
        GlobalContext.getContext().setObject("newWant", undefined)
      }
    }
  }

  build() {
    Row() {
      Column() {
        Text(this.message)
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
      }
      .width('100%')
    }
    .height('100%')
  }
}
```


当PageAbility的启动模式设置为多实例模式或为首次启动单例模式的PageAbility时（具体设置方法和典型场景示例见[PageAbility的启动模式](pageability-launch-type.md)），在调用方PageAbility中，通过want中的parameters参数传递要启动的指定页面的pages信息，调用startAbility()方法启动PageAbility。被调用方可以在onCreate中使用featureAbility的getWant方法获取want，再通过调用router.push实现启动指定页面。


调用方的页面中实现按钮点击触发startAbility方法启动目标端PageAbility，startAbility方法的入参want中携带指定页面信息，示例代码如下：

```ts
import featureAbility from '@ohos.ability.featureAbility';
import { BusinessError } from '@ohos.base';

@Entry
@Component
struct Index {
  @State message: string = 'Hello World'

  build() {
    Row() {
      Button("startAbility")
        .onClick(() => {
          featureAbility.startAbility({
            want: {
              bundleName: "com.exm.myapplication",
              abilityName: "com.exm.myapplication.EntryAbility",
              parameters: { page: "pages/page1" }
            }
          }).then((data) => {
            console.info("startAbility finish");
          }).catch((err: BusinessError) => {
            console.info("startAbility failed errcode:" + err.code)
          })
        })
      ...
      Button("page2")
        .onClick(() => {
          featureAbility.startAbility({
            want: {
              bundleName: "com.exm.myapplication",
              abilityName: "com.exm.myapplication.EntryAbility",
              parameters: { page: "pages/page2" }
            }
          }).then((data) => {
            console.info("startAbility finish");
          }).catch((err: BusinessError) => {
            console.info("startAbility failed errcode:" + err.code)
          })
        })
      ...
    }
    ...
  }
}
```


目标端PageAbility的onCreate生命周期回调中通过featureAbility的getWant方法获取want，并对参数进行解析，实现指定页面拉起：

```ts
import featureAbility from '@ohos.ability.featureAbility';
import router from '@ohos.router';
import { BusinessError } from '@ohos.base';

class EntryAbility {
  onCreate() {
    featureAbility.getWant().then((want) => {
      if (want.parameters) {
        if (want.parameters.page) {
          router.pushUrl({
            url: want.parameters.page as string
          }, (error: BusinessError)=>{
            console.error(`error: ${JSON.stringify(error)}`);
          })
        }
      }
    })
  }
  onDestroy() {
    // ...
  }
}

export default new EntryAbility()
```

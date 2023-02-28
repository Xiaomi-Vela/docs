# HAR共享包
## HAR共享包概述
HAR（OpenHarmony Archive）是OpenHarmony静态共享包，可以包含代码、C++库、资源和配置文件。通过HAR共享包，可以实现多个模块或多个工程共享OpenHarmony组件、资源等相关代码。HAR不同于HAP，不能独立安装运行在设备上，只能作为应用模块的依赖项被引用。

## 创建HAR模块
HAR包对应DevEco Studio工程中的“Library”类型的[Module](https://developer.harmonyos.com/cn/docs/documentation/doc-guides-V3/ohos-adding-deleting-module-0000001218760594-V3)，可以通过DevEco Studio创建一个HAR模块。HAR模块默认不开启混淆能力，开启混淆能力，需要把HAR模块的build-profile.json5文件中的artifactType字段设置为obfuscation，配置如下所示：

```json
// build-profile.json5
{
  "apiType": "stageMode",
  "buildOption": {
      "artifactType": "obfuscation"
  }
}
```
artifactType字段有以下两种取值，默认缺省为original。
- original：不混淆。
- obfuscation：混淆，目前仅支持uglify混淆。

注意：artifactType字段设置为obfuscation时，apiType字段必须设置为stageMode，因为Stage模型才支持混淆。

## 导出HAR共享包接口
index.ets文件是HAR共享包导出声明文件的入口，HAR共享包需要导出的接口，统一在index.ets文件中导出。在模块的package.json文件中的main字段配置如下所示：
```json
// package.json
{
  "main": "index.ets"
}
```
### 导出ArkUI组件
ArkUI组件的导出方式与ts的导出方式一致，通过export导出ArkUI组件，示例如下：
```js
// library/src/main/ets/components/MainPage/MainPage.ets
@Component
export struct MainPage {
  @State message: string = 'Hello World'
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
HAR对外暴露的接口，在index.ets导出文件中声明如下所示：
```js
// library/index.ets
export { MainPage } from './src/main/ets/components/MainPage/MainPage'
```
### 导出ts类和方法
通过export导出ts类和方法，支持导出多个ts类和方法，示例如下所示：
```js
// library/src/main/ts/test.ets
export class Log {
    static info(msg) {
        console.info(msg);
    }
}

export function func() {
  return "har func";
}

export function func2() {
  return "har func2";
}
```
HAR对外暴露的接口，在index.ets导出文件中声明如下所示：
```js
// library/index.ets
export { Log } from './src/main/ts/test'
export { func } from './src/main/ts/test'
export { func2 } from './src/main/ts/test'
```
### 资源
HAR模块编译打包时会把资源打包到HAR包中。在编译构建HAP时，DevEco Studio会从HAP模块及依赖的模块中收集资源文件，如果不同模块下的资源文件出现重名冲突时，DevEco Studio会按照以下优先级进行覆盖（优先级由高到低）：
- AppScope（仅API9的Stage模型支持）。
- HAP包自身模块。
- 依赖的HAR模块，如果依赖的多个HAR之间有资源冲突，会按照依赖顺序进行覆盖（依赖顺序在前的优先级较高）。

## 引用HAR共享包接口
### 引用HAR共享包的ArkUI组件

HAR共享包的依赖配置成功后，可以引用HAR共享包的ArkUI组件。ArkUI组件的导入方式与ts的导入方式一致，通过import引入HAR共享包导出的ArkUI组件，示例如下所示：
```js
// entry/src/main/ets/pages/index.ets
import { MainPage } from "@ohos/library"

@Entry
@Component
struct Index {
  @State message: string = 'Hello World'
  build() {
    Row() {
      // 引用HAR共享包的ArkUI组件
      MainPage()
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
### 引用HAR共享包的类和方法
通过import引用HAR共享包导出的ts类和方法，示例如下所示：
```js
// entry/src/main/ets/pages/index.ets
import { Log } from "@ohos/library"
import { func } from "@ohos/library"

@Entry
@Component
struct Index {
  build() {
    Row() {
      Column() {
        Button('Button')
          .onClick(()=>{
            // 引用HAR共享包的类和方法
            Log.info("har msg");
            func();
        })
      }
      .width('100%')
    }
    .height('100%')
  }
}
```
### 引用HAR共享包的资源
通过$r引用HAR共享包中的资源，例如在HAR模块的src/main/resources里添加字符串资源（在string.json中定义，name：hello_har）和图片资源（icon_har.png），然后在Entry模块中引用该字符串和图片资源的示例如下所示：
```js
// entry/src/main/ets/pages/index.ets
@Entry
@Component
struct Index {
  build() {
    Row() {
      Column() {
        // 引用HAR共享包的字符串资源
        Text($r("app.string.hello_har"))
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
        // 引用HAR共享包的图片资源
        Image($r("app.media.icon_npm"))
      }
      .width('100%')
    }
    .height('100%')
  }
}
```
## HAR共享包开发注意事项
- HAR不支持在配置文件中声明ability、extensionAbility组件。
- HAR不支持在配置文件中声明pages页面。
- HAR不支持在build-profile.json5文件的buildOption中配置worker。
- FA模型与Stage模型的HAR不支持相互引用。
- Stage模型的HAR，不能引用AppScope内的内容。在编译构建时不会将AppScope中的内容打包到HAR中，会导致资源引用失败。
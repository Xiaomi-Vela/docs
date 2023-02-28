# Web

Web是提供网页显示能力的组件，具体用法请参考 [Web API](../reference/arkui-ts/ts-basic-components-web.md)。

## 创建组件

在main/ets/MainAbility/pages目录下的ets文件中创建一个Web组件。在web组件中通过src指定引用的网页路径，controller为组件的控制器，通过controller绑定Web组件，用于调用Web组件的方法。

  ```ts
  // xxx.ets
  import web_webview from '@ohos.web.webview';

  @Entry
  @Component
  struct WebComponent {
    controller: web_webview.WebviewController = new web_webview.WebviewController();
    build() {
      Column() {
        Web({ src: 'https://www.example.com', controller: this.controller })
      }
    }
  }
  ```

## 设置样式和属性

Web组件的使用需要添加丰富的页面样式和功能属性。设置height、padding样式可为Web组件添加高和内边距，设置fileAccess属性可为Web组件添加文件访问权限，设置javaScriptAccess属性为true使Web组件具有执行JavaScript代码的能力。

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';

@Entry
@Component
struct WebComponent {
  fileAccess: boolean = true;
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  build() {
    Column() {
      Text('Hello world!')
        .fontSize(20)
      Web({ src: 'https://www.example.com', controller: this.controller })
        // 设置高和内边距
        .height(500)
        .padding(20)
        // 设置文件访问权限和脚本执行权限
        .fileAccess(this.fileAccess)
        .javaScriptAccess(true)
      Text('End')
        .fontSize(20)
    }
  }
}
```
## 添加事件和方法

为Web组件添加onProgressChange事件，该事件回调Web引擎加载页面的进度值。将该进度值赋值给Progress组件的value，控制Progress组件的状态。当进度为100%时隐藏Progress组件，Web页面加载完成。

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';

@Entry
@Component
struct WebComponent {
  @State progress: number = 0;
  @State hideProgress: boolean = true;
  fileAccess: boolean = true;
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  build() {
    Column() {
      Text('Hello world!')
        .fontSize(20)
      Progress({value: this.progress, total: 100})
        .color('#0000ff')
        .visibility(this.hideProgress ? Visibility.None : Visibility.Visible)
      Web({ src: 'https://www.example.com', controller: this.controller })
        .fileAccess(this.fileAccess)
        .javaScriptAccess(true)
        .height(500)
        .padding(20)
        // 添加onProgressChange事件
        .onProgressChange(e => {
          this.progress = e.newProgress;
          // 当进度100%时，进度条消失
          if (this.progress === 100) {
            this.hideProgress = true;
          } else {
            this.hideProgress = false;
          }
        })
      Text('End')
        .fontSize(20)
    }
  }
}
```
在onPageEnd事件中添加runJavaScript方法。onPageEnd事件是网页加载完成时的回调，runJavaScript方法可以执行HTML中的JavaScript脚本。当页面加载完成时，触发onPageEnd事件，调用HTML文件中的test方法，在控制台打印信息。

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';

@Entry
@Component
struct WebComponent {
  @State progress: number = 0;
  @State hideProgress: boolean = true;
  @State webResult: string = ''
  fileAccess: boolean = true;
  // 定义Web组件的控制器controller
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  build() {
    Column() {
      Text('Hello world!')
        .fontSize(20)
      Progress({value: this.progress, total: 100})
        .color('#0000ff')
        .visibility(this.hideProgress ? Visibility.None : Visibility.Visible)
      // 初始化Web组件，并绑定controller
      Web({ src: $rawfile('index.html'), controller: this.controller })
        .fileAccess(this.fileAccess)
        .javaScriptAccess(true)
        .height(500)
        .padding(20)
        .onProgressChange(e => {
          this.progress = e.newProgress;
          if (this.progress === 100) {
            this.hideProgress = true;
          } else {
            this.hideProgress = false;
          }
        })
        .onPageEnd(e => {
          // test()在index.html中定义
          try {
            this.controller.runJavaScript(
              'test()',
              (error, result) => {
                if (error) {
                  console.info(`run JavaScript error: ` + JSON.stringify(error))
                  return;
                }
                if (result) {
                  this.webResult = result
                  console.info(`The test() return value is: ${result}`)
                }
              });
            console.info('url: ', e.url);
          } catch (error) {
            console.error(`ErrorCode: ${error.code},  Message: ${error.message}`);
          }
        })
      Text('End')
        .fontSize(20)
    }
  }
}
```

在main/resources/rawfile目录下创建一个HTML文件。

```html
<!-- index.html -->
<!DOCTYPE html>
<html>
<meta charset="utf-8">
<body>
    Hello world!
</body>
<script type="text/javascript">
  function test() {
      console.info('Ark Web Component');
  }
</script>
</html>
```

## 开启网页调试
在PC上启用端口转发，以及设置Web组件属性webDebuggingAccess为true后，便可以在PC上调试通过USB连接的开发设备上的Web组件里的网页。

设置步骤如下：

1、首先设置Web组件属性webDebuggingAccess为true。
  ```ts
  // xxx.ets
  import web_webview from '@ohos.web.webview';

  @Entry
  @Component
  struct WebComponent {
    controller: web_webview.WebviewController = new web_webview.WebviewController();
    build() {
      Column() {
        Web({ src: 'www.example.com', controller: this.controller })
          .webDebuggingAccess(true) // true表示启用调试功能
      }
    }
  }
  ```

2、PC上启用端口转发功能，添加TCP端口9222映射。
  ```ts
  hdc fport tcp:9222 tcp:9222
  ```
  添加是否成功可以通过如下命令来查看已存在的映射关系表。
  ```ts
  hdc fport ls
  ```
如上设置完成后，首先打开应用Web组件、访问要调试的网页，然后在PC上使用chrome浏览器访问：http://localhost:9222, 就可以在PC上调试开发设备刚才访问的网页。

## 场景示例

该场景实现了Web组件中视频的动态播放。首先在HTML页面内嵌入视频资源，再使用Web组件的控制器调用onActive和onInactive方法激活和暂停页面渲染。点击onInactive按钮，Web页面停止渲染，视频暂停播放；点击onActive按钮，激活Web组件，视频继续播放。

  ```ts
  // xxx.ets
import web_webview from '@ohos.web.webview';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  build() {
    Column() {
      Row() {
        Button('onActive').onClick(() => {
          console.info("Web Component onActive");
          try {
            this.controller.onActive();
          } catch (error) {
            console.error(`Errorcode: ${error.code}, Message: ${error.message}`);
          }
        })
        Button('onInactive').onClick(() => {
          console.info("Web Component onInactive");
          try {
            this.controller.onInactive();
          } catch (error) {
            console.error(`Errorcode: ${error.code}, Message: ${error.message}`);
          }
        })
      }
      Web({ src: $rawfile('index.html'), controller: this.controller })
        .fileAccess(true)
    }
  }
}
  ```

  ```html
  <!-- index.html -->
  <!DOCTYPE html>
  <html>
  <meta charset="utf-8">
  <body>
      <video width="320" height="240" controls="controls" muted="muted" autoplay="autoplay">
          <!-- test.mp4视频文件放在main/resources/rawfile目录下 -->
          <source src="test.mp4" type="video/mp4">
      </video>
  </body>
  </html>
  ```

## 相关实例

针对Web开发，有以下相关实例可供参考：

- [`Web`：Web（ArkTS）（API8）](https://gitee.com/openharmony/applications_app_samples/tree/OpenHarmony-3.2-Beta5/ETSUI/Web)

- [Web组件的使用（ArkTS）（API9）](https://gitee.com/openharmony/codelabs/tree/master/ETSUI/WebCookie)

- [Web组件抽奖案例（ArkTS）（API9）](https://gitee.com/openharmony/codelabs/tree/master/ETSUI/WebComponent)
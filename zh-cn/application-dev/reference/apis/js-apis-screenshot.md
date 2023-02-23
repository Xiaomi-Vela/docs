# 屏幕截图
本模块提供屏幕截图的能力，截取屏幕时支持设置截取的区域、大小等图像信息。

>  **说明：**
>
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>
> 该模块接口为系统接口。

## 导入模块

```js
import screenshot from '@ohos.screenshot';
```

## ScreenshotOptions

设置截取图像的信息。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core


| 参数名                 | 类型          | 必填 | 说明                                                         |
| ---------------------- | ------------- | ---- | ------------------------------------------------------------ |
| screenRect             | [Rect](#rect) | 否   | 表示截取图像的区域，不传值默认为全屏。                       |
| imageSize              | [Size](#size) | 否   | 表示截取图像的大小，不传值默认为全屏。                       |
| rotation               | number        | 否   | 表示截取图像的旋转角度，当前仅支持输入值为0，默认值为0。     |
| displayId<sup>8+</sup> | number        | 否   | 表示截取图像的显示设备[Display](js-apis-display.md#display)的ID号。 |


## Rect

表示截取图像的区域。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| left   | number | 是   | 表示截取图像区域的左边界，单位为像素。|
| top    | number | 是   | 表示截取图像区域的上边界，单位为像素。|
| width  | number | 是   | 表示截取图像区域的宽度，单位为像素。|
| height | number | 是   | 表示截取图像区域的高度，单位为像素。|


## Size

表示截取图像的大小。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| width  | number | 是   | 表示截取图像的宽度，单位为像素。|
| height | number | 是   | 表示截取图像的高度，单位为像素。|

## screenshot.save

save(options?: ScreenshotOptions, callback: AsyncCallback&lt;image.PixelMap&gt;): void

获取屏幕截图。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**需要权限**：ohos.permission.CAPTURE_SCREEN，仅系统应用可用。

**参数：**

| 参数名   | 类型                                    | 必填 | 说明                                                         |
| -------- | --------------------------------------- | ---- | ------------------------------------------------------------ |
| options  | [ScreenshotOptions](#screenshotoptions) | 否   | 该类型的参数包含screenRect，imageSize，rotation， displayId四个参数，可以分别设置这四个参数。 |
| callback | AsyncCallback&lt;image.PixelMap&gt;     | 是   | 回调函数。返回一个PixelMap对象。                                   |

**示例：**

  ```js
  var ScreenshotOptions = {
  	"screenRect": {
  		"left": 200,
  		"top": 100,
  		"width": 200,
  		"height": 200},
  	"imageSize": {
  		"width": 300,
  		"height": 300},
  	"rotation": 0,
  	"displayId": 0
  };
  screenshot.save(ScreenshotOptions, (err, data) => {
  	if (err) {
  		console.error('Failed to save the screenshot. Error: ' + JSON.stringify(err));
  		return;
  	}
  	console.info('Screenshot saved. Data: ' + JSON.stringify(data));
  });
  ```

## screenshot.save

save(options?: ScreenshotOptions): Promise&lt;image.PixelMap&gt;

获取屏幕截图。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**需要权限**：ohos.permission.CAPTURE_SCREEN，仅系统应用可用。

**参数：**

| 参数名  | 类型                                    | 必填 | 说明                                                         |
| ------- | --------------------------------------- | ---- | ------------------------------------------------------------ |
| options | [ScreenshotOptions](#screenshotoptions) | 否   | 该类型的参数包含screenRect、imageSize、rotation、displayId四个参数，可以分别设置这四个参数。 |

**返回值：**

| 类型                          | 说明                                            |
| ----------------------------- | ----------------------------------------------- |
| Promise&lt;image.PixelMap&gt; | Promise对象。返回一个PixelMap对象。 |

**示例：**

  ```js
  var ScreenshotOptions = {
  	"screenRect": {
  		"left": 200,
  		"top": 100,
  		"width": 200,
  		"height": 200},
  	"imageSize": {
  		"width": 300,
  		"height": 300},
  	"rotation": 0,
  	"displayId": 0
  };
  let promise = screenshot.save(ScreenshotOptions);
  promise.then(() => {
      console.log('screenshot save success');
  }).catch((err) => {
      console.log('screenshot save fail: ' + JSON.stringify(err));
  });
  ```

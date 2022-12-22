# 壁纸

> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块


```
import wallpaper from '@ohos.wallpaper';
```


## WallpaperType

定义壁纸类型。

**系统能力**: 以下各项对应的系统能力均为SystemCapability.MiscServices.Wallpaper。

| 名称 | 说明 |
| -------- | -------- |
| WALLPAPER_LOCKSCREEN | 锁屏壁纸标识。 |
| WALLPAPER_SYSTEM | 主屏幕壁纸标识。 |


## wallpaper.getColors

getColors(wallpaperType: WallpaperType, callback: AsyncCallback&lt;Array&lt;RgbaColor&gt;&gt;): void

获取指定类型壁纸的主要颜色信息。

**系统能力**: SystemCapability.MiscServices.Wallpaper

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | wallpaperType | [WallpaperType](#wallpapertype) | 是 | 壁纸类型。 |
  | callback | AsyncCallback&lt;Array&lt;[RgbaColor](#rgbacolor)&gt;&gt; | 是 | 回调函数，返回壁纸的主要颜色信息。 |

**示例：**
  
  ```js
  wallpaper.getColors(wallpaper.WallpaperType.WALLPAPER_SYSTEM, (error, data) => {
      if (error) {
          console.error(`failed to getColors because: ` + JSON.stringify(error));
          return;
      }
      console.log(`success to getColors.`);
  });
  ```


## wallpaper.getColors

getColors(wallpaperType: WallpaperType): Promise&lt;Array&lt;RgbaColor&gt;&gt;

获取指定类型壁纸的主要颜色信息。

**系统能力**: SystemCapability.MiscServices.Wallpaper

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | wallpaperType | [WallpaperType](#wallpapertype) | 是 | 壁纸类型。 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;Array&lt;[RgbaColor](#rgbacolor)&gt;&gt; | 返回壁纸的主要颜色信息。 |

**示例：**
  
  ```js
  wallpaper.getColors(wallpaper.WallpaperType.WALLPAPER_SYSTEM).then((data) => {
      console.log(`success to getColors.`);
  }).catch((error) => {
      console.error(`failed to getColors because: ` + JSON.stringify(error));
  });
  ```


## wallpaper.getId

getId(wallpaperType: WallpaperType, callback: AsyncCallback&lt;number&gt;): void

获取指定类型壁纸的ID。

**系统能力**: SystemCapability.MiscServices.Wallpaper

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | wallpaperType | [WallpaperType](#wallpapertype) | 是 | 壁纸类型。 |
  | callback | AsyncCallback&lt;number&gt; | 是 | 回调函数，返回壁纸的ID。如果配置了指定类型的壁纸就返回一个大于等于0的数，否则返回-1。取值范围是-1到（2^31-1）。 |

**示例：**
  
  ```js
  wallpaper.getId(wallpaper.WallpaperType.WALLPAPER_SYSTEM, (error, data) => {
      if (error) {
          console.error(`failed to getId because: ` + JSON.stringify(error));
          return;
      }
      console.log(`success to getId: ` + JSON.stringify(data));
  });
  ```


## wallpaper.getId

getId(wallpaperType: WallpaperType): Promise&lt;number&gt;

获取指定类型壁纸的ID。

**系统能力**: SystemCapability.MiscServices.Wallpaper


**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | wallpaperType | [WallpaperType](#wallpapertype) | 是 | 壁纸类型。 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;number&gt; | 壁纸的ID。如果配置了这种壁纸类型的壁纸就返回一个大于等于0的数，否则返回-1。取值范围是-1到（2^31-1）。 |

**示例：**
  
  ```js
  wallpaper.getId(wallpaper.WallpaperType.WALLPAPER_SYSTEM).then((data) => {
      console.log(`success to getId: ` + JSON.stringify(data));
  }).catch((error) => {
      console.error(`failed to getId because: ` + JSON.stringify(error));
  });
  ```


## wallpaper.getMinHeight

getMinHeight(callback: AsyncCallback&lt;number&gt;): void

获取壁纸的最小高度值。

**系统能力**: SystemCapability.MiscServices.Wallpaper

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;number&gt; | 是 | 回调函数，返回壁纸的最小高度值，单位是像素。如果返回值等于0，说明没有设置壁纸，调用者应该使用默认显示的高度值代替。 |

**示例：**
  
  ```js
  wallpaper.getMinHeight((error, data) => {
      if (error) {
          console.error(`failed to getMinHeight because: ` + JSON.stringify(error));
          return;
      }
      console.log(`success to getMinHeight: ` + JSON.stringify(data));
  });
  ```


## wallpaper.getMinHeight

getMinHeight(): Promise&lt;number&gt;

获取壁纸的最小高度值。

**系统能力**: SystemCapability.MiscServices.Wallpaper


**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;number&gt; | 返回壁纸的最小高度值，单位是像素。如果返回值等于0，说明没有设置壁纸，调用者应该使用默认显示的高度值代替。 |

**示例：**
  
  ```js
  wallpaper.getMinHeight().then((data) => {
      console.log(`success to getMinHeight: ` + JSON.stringify(data));
  }).catch((error) => {
      console.error(`failed to getMinHeight because: ` + JSON.stringify(error));
  });
  ```


## wallpaper.getMinWidth

getMinWidth(callback: AsyncCallback&lt;number&gt;): void

获取壁纸的最小宽度值。

**系统能力**: SystemCapability.MiscServices.Wallpaper


**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;number&gt; | 是 | 回调函数，壁纸的最小宽度值，单位是像素。如果返回值等于0，说明没有设置壁纸，调用者应该使用默认显示的宽度值代替。 |

**示例：**
  
  ```js
  wallpaper.getMinWidth((error, data) => {
      if (error) {
          console.error(`failed to getMinWidth because: ` + JSON.stringify(error));
          return;
      }
      console.log(`success to getMinWidth: ` + JSON.stringify(data));
  });
  ```


## wallpaper.getMinWidth

getMinWidth(): Promise&lt;number&gt;

获取壁纸的最小宽度值。

**系统能力**: SystemCapability.MiscServices.Wallpaper

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;number&gt; | 壁纸的最小宽度值，单位是像素。如果返回值等于0，说明没有设置壁纸，调用者应该使用默认显示的宽度值代替。 |

**示例：**
  
  ```js
  wallpaper.getMinWidth().then((data) => {
      console.log(`success to getMinWidth: ` + JSON.stringify(data));
  }).catch((error) => {
      console.error(`failed to getMinWidth because: ` + JSON.stringify(error));
  });
  ```


## wallpaper.isChangePermitted

isChangePermitted(callback: AsyncCallback&lt;boolean&gt;): void

是否允许应用改变当前用户的壁纸。

**系统能力**: SystemCapability.MiscServices.Wallpaper

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 回调函数，返回是否允许应用改变当前用户的壁纸。如果允许返回true，否则返回false。 |

**示例：**
  
  ```js
  wallpaper.isChangePermitted((error, data) => {
      if (error) {
          console.error(`failed to isChangePermitted because: ` + JSON.stringify(error));
          return;
      }
      console.log(`success to isChangePermitted: ` + JSON.stringify(data));
  });
  ```


## wallpaper.isChangePermitted

isChangePermitted(): Promise&lt;boolean&gt;

是否允许应用改变当前用户的壁纸。

**系统能力**: SystemCapability.MiscServices.Wallpaper

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 返回是否允许应用改变当前用户的壁纸。如果允许返回true，否则返回false。 |

**示例：**
  
  ```js
  wallpaper.isChangePermitted().then((data) => {
      console.log(`success to isChangePermitted: ` + JSON.stringify(data));
  }).catch((error) => {
      console.error(`failed to isChangePermitted because: ` + JSON.stringify(error));
  });
  ```


## wallpaper.isOperationAllowed

isOperationAllowed(callback: AsyncCallback&lt;boolean&gt;): void

是否允许用户设置壁纸。

**系统能力**: SystemCapability.MiscServices.Wallpaper

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 回调函数，返回是否允许用户设置壁纸。如果允许返回true，否则返回false。 |

**示例：**
  
  ```js
  wallpaper.isOperationAllowed((error, data) => {
      if (error) {
          console.error(`failed to isOperationAllowed because: ` + JSON.stringify(error));
          return;
      }
      console.log(`success to isOperationAllowed: ` + JSON.stringify(data));
  });
  ```


## wallpaper.isOperationAllowed

isOperationAllowed(): Promise&lt;boolean&gt;

是否允许用户设置壁纸。

**系统能力**: SystemCapability.MiscServices.Wallpaper

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 异步回调函数，返回是否允许用户设置壁纸。如果允许返回true，否则返回false。 |

**示例：**
  
  ```js
  wallpaper.isOperationAllowed().then((data) => {
      console.log(`success to isOperationAllowed: ` + JSON.stringify(data));
  }).catch((error) => {
      console.error(`failed to isOperationAllowed because: ` + JSON.stringify(error));
  });
  ```


## wallpaper.reset

reset(wallpaperType: WallpaperType, callback: AsyncCallback&lt;void&gt;): void

移除指定类型的壁纸，恢复为默认显示的壁纸。

**需要权限**：ohos.permission.SET_WALLPAPER

**系统能力**: SystemCapability.MiscServices.Wallpaper

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | wallpaperType | [WallpaperType](#wallpapertype) | 是 | 壁纸类型。 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 回调函数，调用成功则返回是否移除成功的结果，调用失败则返回error信息。 |

**示例：**
  
  ```js
  wallpaper.reset(wallpaper.WallpaperType.WALLPAPER_SYSTEM, (error, data) => {
      if (error) {
          console.error(`failed to reset because: ` + JSON.stringify(error));
          return;
      }
      console.log(`success to reset.`);
  });
  ```


## wallpaper.reset

reset(wallpaperType: WallpaperType): Promise&lt;void&gt;

移除指定类型的壁纸，恢复为默认显示的壁纸。

**需要权限**：ohos.permission.SET_WALLPAPER

**系统能力**: SystemCapability.MiscServices.Wallpaper

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | wallpaperType | [WallpaperType](#wallpapertype) | 是 | 壁纸类型。 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 调用成功则返回是否移除成功的结果，调用失败则返回error信息。 |

**示例：**
  
  ```js
  wallpaper.reset(wallpaper.WallpaperType.WALLPAPER_SYSTEM).then((data) => {
      console.log(`success to reset.`);
  }).catch((error) => {
      console.error(`failed to reset because: ` + JSON.stringify(error));
  });
  ```


## wallpaper.setWallpaper

setWallpaper(source: string | image.PixelMap, wallpaperType: WallpaperType, callback: AsyncCallback&lt;void&gt;): void

将指定资源设置为指定类型的壁纸。

**需要权限**：ohos.permission.SET_WALLPAPER

**系统能力**: SystemCapability.MiscServices.Wallpaper

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | source | string&nbsp;\|[PixelMap](js-apis-image.md#pixelmap7) |  | JPEG或PNG文件的Uri路径，或者PNG格式文件的位图。 |
  | wallpaperType | [WallpaperType](#wallpapertype) | 是 | 壁纸类型。 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 回调函数，调用成功则返回是返回设置的结果，调用失败则返回error信息。 |

**示例：**
  
  ```js
  // source类型为string
  let wallpaperPath = "/data/data/ohos.acts.aafwk.plrdtest.form/files/Cup_ic.jpg";
  wallpaper.setWallpaper(wallpaperPath, wallpaper.WallpaperType.WALLPAPER_SYSTEM, (error, data) => {    
      if (error) {        
          console.error(`failed to setWallpaper because: ` + JSON.stringify(error));       
          return;   
      }    
      console.log(`success to setWallpaper.`);
  });
  
  // source类型为image.PixelMap
  import image from '@ohos.multimedia.image';
  let imageSource = image.createImageSource("file://" + wallpaperPath);
  let opts = {
      "desiredSize": {
          "height": 3648,
          "width": 2736
      }
  };
  imageSource.createPixelMap(opts).then((pixelMap) => {      
      wallpaper.setWallpaper(pixelMap, wallpaper.WallpaperType.WALLPAPER_SYSTEM, (error, data) => {    
          if (error) {       
              console.error(`failed to setWallpaper because: ` + JSON.stringify(error));
              return;
          }    
          console.log(`success to setWallpaper.`);
      });
  }).catch((error) => {       
      console.error(`failed to createPixelMap because: ` + JSON.stringify(error));
  });
  ```


## wallpaper.setWallpaper

setWallpaper(source: string | image.PixelMap, wallpaperType: WallpaperType): Promise&lt;void&gt;

将指定资源设置为指定类型的壁纸。

**需要权限**：ohos.permission.SET_WALLPAPER

**系统能力**: SystemCapability.MiscServices.Wallpaper

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | source | string&nbsp;\|[PixelMap](js-apis-image.md#pixelmap7) | 是 | JPEG或PNG文件的Uri路径，或者PNG格式文件的位图。 |
  | wallpaperType | [WallpaperType](#wallpapertype) | 是 | 壁纸类型。 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 调用成功则返回是返回设置的结果，调用失败则返回error信息。 |

**示例：**
  
  ```js
  // source类型为string
  let wallpaperPath = "/data/data/ohos.acts.aafwk.plrdtest.form/files/Cup_ic.jpg";
  wallpaper.setWallpaper(wallpaperPath, wallpaper.WallpaperType.WALLPAPER_SYSTEM).then((data) => {
      console.log(`success to setWallpaper.`);
  }).catch((error) => {
      console.error(`failed to setWallpaper because: ` + JSON.stringify(error));
  });
  
  // source类型为image.PixelMap
  import image from '@ohos.multimedia.image';
  let imageSource = image.createImageSource("file://" + wallpaperPath);
  let opts = {
      "desiredSize": {
          "height": 3648,
          "width": 2736
      }
  };
  imageSource.createPixelMap(opts).then((pixelMap) => {      
      wallpaper.setWallpaper(pixelMap, wallpaper.WallpaperType.WALLPAPER_SYSTEM).then((data) => {
          console.log(`success to setWallpaper.`);
      }).catch((error) => {
          console.error(`failed to setWallpaper because: ` + JSON.stringify(error));
      });
  }).catch((error) => {       
      console.error(`failed to createPixelMap because: ` + JSON.stringify(error));
  });
  ```

## wallpaper.getFile<sup>8+</sup>

getFile(wallpaperType: WallpaperType, callback: AsyncCallback&lt;number&gt;): void

获取指定类型的壁纸文件。

**需要权限**：ohos.permission.GET_WALLPAPER 和 ohos.permission.READ_USER_STORAGE

**系统能力**: SystemCapability.MiscServices.Wallpaper

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | wallpaperType | [WallpaperType](#wallpapertype) | 是 | 壁纸类型。 |
  | callback | AsyncCallback&lt;number&gt; | 是 | 回调函数，调用成功则返回壁纸文件描述符ID，调用失败则返回error信息。 |

**示例：**
  
  ```js
  wallpaper.getFile(wallpaper.WallpaperType.WALLPAPER_SYSTEM, (error, data) => {
      if (error) {
          console.error(`failed to getFile because: ` + JSON.stringify(error));
          return;
      }
      console.log(`success to getFile: ` + JSON.stringify(data));
  });
  ```

## wallpaper.getFile<sup>8+</sup>

getFile(wallpaperType: WallpaperType): Promise&lt;number&gt;

获取指定类型的壁纸文件。

**需要权限**：ohos.permission.GET_WALLPAPER 和 ohos.permission.READ_USER_STORAGE

**系统能力**: SystemCapability.MiscServices.Wallpaper

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | wallpaperType | [WallpaperType](#wallpapertype) | 是 | 壁纸类型。 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;number&gt; | 调用成功则返回壁纸文件描述符ID，调用失败则返回error信息。 |

**示例：**
  
  ```js
  wallpaper.getFile(wallpaper.WallpaperType.WALLPAPER_SYSTEM).then((data) => {
      console.log(`success to getFile: ` + JSON.stringify(data));
  }).catch((error) => {
      console.error(`failed to getFile because: ` + JSON.stringify(error));
  });
  ```


## wallpaper.getPixelMap

getPixelMap(wallpaperType: WallpaperType, callback: AsyncCallback&lt;image.PixelMap&gt;): void;

获取壁纸图片的像素图。

**需要权限**：ohos.permission.GET_WALLPAPER 和 ohos.permission.READ_USER_STORAGE

**系统能力**: SystemCapability.MiscServices.Wallpaper

**系统API**：此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | wallpaperType | [WallpaperType](#wallpapertype) | 是 | 壁纸类型。 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 回调函数，调用成功则返回壁纸图片的像素图对象，调用失败则返回error信息。 |

**示例：**
  
  ```js
  wallpaper.getPixelMap(wallpaper.WallpaperType.WALLPAPER_SYSTEM, function (err, data) {
      console.info('wallpaperXTS ===> testGetPixelMapCallbackSystem err : ' + JSON.stringify(err));
      console.info('wallpaperXTS ===> testGetPixelMapCallbackSystem data : ' + JSON.stringify(data));
  });
  ```


## wallpaper.getPixelMap

getPixelMap(wallpaperType: WallpaperType): Promise&lt;image.PixelMap&gt;

获取壁纸图片的像素图。

**需要权限**：ohos.permission.GET_WALLPAPER 和 ohos.permission.READ_USER_STORAGE

**系统能力**: SystemCapability.MiscServices.Wallpaper

**系统API**：此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | wallpaperType | [WallpaperType](#wallpapertype) | 是 | 壁纸类型。 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 调用成功则返回壁纸图片的像素图对象，调用失败则返回error信息。 |

**示例：**
  
  ```js
  wallpaper.getPixelMap(wallpaper.WallpaperType.WALLPAPER_SYSTEM).then((data) => {
      console.info('wallpaperXTS ===> testGetPixelMapPromiseSystem data : ' + data);
      console.info('wallpaperXTS ===> testGetPixelMapPromiseSystem data : ' + JSON.stringify(data));
  }).catch((err) => {
      console.info('wallpaperXTS ===> testGetPixelMapPromiseSystem err : ' + err);
      console.info('wallpaperXTS ===> testGetPixelMapPromiseSystem err : ' + JSON.stringify(err));
  });
  ```


## wallpaper.on('colorChange')

on(type: 'colorChange', callback: (colors: Array&lt;RgbaColor&gt;, wallpaperType: WallpaperType) =&gt; void): void

订阅壁纸颜色变化结果上报事件。

**系统能力**: SystemCapability.MiscServices.Wallpaper

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 取值为'colorChange'，表示壁纸颜色变化结果上报事件。 |
  | callback | function | 是 | 壁纸颜色变化触发该回调方法，返回壁纸类型和壁纸的主要颜色信息。<br/>-&nbsp;colors<br/>&nbsp;&nbsp;壁纸的主要颜色信息，其类型见[RgbaColor](#rgbacolor)。<br/>-&nbsp;wallpaperType<br/>&nbsp;&nbsp;壁纸类型。 |

**示例：**
  
  ```js
  let listener = (colors, wallpaperType) => {
      console.log(`wallpaper color changed.`);
  };
  wallpaper.on('colorChange', listener);
  ```


## wallpaper.off('colorChange')

off(type: 'colorChange', callback?: (colors: Array&lt;RgbaColor&gt;, wallpaperType: WallpaperType) =&gt; void): void

取消订阅壁纸颜色变化结果上报事件。

**系统能力**: SystemCapability.MiscServices.Wallpaper

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 取值为'colorChange'，表示取消订阅壁纸颜色变化结果上报事件。 |
  | callback | function | 否 | &nbsp;&nbsp;表示取消壁纸颜色变化结果上报，不填写该参数则取消订阅该type对应的所有回调。<br/>-&nbsp;colors<br/>&nbsp;&nbsp;壁纸的主要颜色信息，其类型见[RgbaColor](#rgbacolor)。<br/>-&nbsp;wallpaperType<br/>&nbsp;&nbsp;壁纸类型。 |

**示例：**
  
  ```js
  let listener = (colors, wallpaperType) => {
      console.log(`wallpaper color changed.`);
  };
  wallpaper.on('colorChange', listener);
  // 取消订阅listener
  wallpaper.off('colorChange', listener);
  // 取消所有'colorChange'类型的订阅
  wallpaper.off('colorChange');
  ```


## RgbaColor

**系统能力**: 以下各项对应的系统能力均为SystemCapability.MiscServices.Wallpaper。

| 名称 | 参数类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| red | number | 是 | 是 | 表示红色值，范围为&nbsp;0&nbsp;到&nbsp;255。 |
| green | number | 是 | 是 | 表示绿色值，范围为&nbsp;0&nbsp;到&nbsp;255。 |
| blue | number | 是 | 是 | 表示蓝色值，范围为&nbsp;0&nbsp;到&nbsp;255。 |
| alpha | number | 是 | 是 | 表示&nbsp;alpha&nbsp;值，范围为&nbsp;0&nbsp;到&nbsp;255。 |

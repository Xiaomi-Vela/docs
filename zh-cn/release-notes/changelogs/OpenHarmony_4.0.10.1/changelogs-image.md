# 图形子系统ChangeLog

# cl.image.1 @ohos.multimedia.image中getDelayTime更名为getDelayTimeList

**变更影响**

对于已发布的JS接口，可能影响应用的兼容性。

**适配指导**

针对已使用该接口开发的应用工程，需要对接口进行适配，将接口修改为getDelayTimeList。

**示例：**
```js
    import image from '@ohos.multimedia.image';

    let testJpg = new Uint8Array([255, 216, 255, 224, 0, 16, 74, 70, 73, 70, 0, 1, 1, 1, 0, 96, 0, 96, 0, 0, 255, 219, 0, 67, 0, 2, 1, 1, 2, 1, 1, 2,
      2, 2, 2, 2, 2, 2, 2, 3, 5, 3, 3, 3, 3, 3, 6, 4, 4, 3, 5, 7, 6, 7, 7, 7, 6, 7, 7, 8, 9, 11, 9, 8,
      8, 10, 8, 7, 7, 10, 13, 10, 10, 11, 12, 12, 12, 12, 7, 9, 14, 15, 13, 12, 14, 11, 12, 12, 12, 255, 219, 0, 67, 1, 2, 2,
      2, 3, 3, 3, 6, 3, 3, 6, 12, 8, 7, 8, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12,
      12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 255, 192,
      0, 17, 8, 0, 226, 1, 216, 3, 1, 34, 0, 2, 17, 1, 3, 17, 1, 255, 196, 0, 31, 0, 0, 1, 5, 1, 1, 1, 1, 1, 1, 0,
      0, 0, 0, 0, 0, 0, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 255, 196, 0, 181, 16, 0, 2, 1, 3, 3, 2, 4, 3, 5,
      5, 4, 4, 0, 0, 1, 125, 1, 2, 3, 0, 4, 17, 5, 18, 33, 49, 65, 6, 19, 81, 97, 7, 34, 113, 20, 50, 129, 145, 161, 8, 35,
      66, 177, 193, 21, 82, 209, 240, 36, 51, 98, 114, 130, 9, 10, 22, 23, 24, 25, 26, 37, 38, 39, 40, 41, 42, 52, 53, 54, 55, 56, 57, 58,
      67, 68, 69, 70, 71, 72, 73, 74, 83, 84, 85, 86, 87, 88, 89, 90, 99, 100, 101, 102, 103, 104, 105, 106, 115, 116, 117, 118, 119, 120, 121, 122,
      131, 132, 133, 134, 135, 136, 137, 138, 146, 147, 148, 149, 150, 151, 152, 153, 154, 162, 163, 164, 165, 166, 167, 168, 169, 170, 178, 179, 180, 181, 182, 183,
      184, 185, 186, 194, 195, 196, 197, 198, 199, 200, 201, 202, 210, 211, 212, 213, 214, 215, 216, 217, 218, 225, 226, 227, 228, 229, 230, 231, 232, 233, 234, 241,
      242, 243, 244, 245, 246, 247, 248, 249, 250, 255, 196, 0, 31, 1, 0, 3, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 1,
      2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 255, 196, 0, 181, 17, 0, 2, 1, 2, 4, 4, 3, 4, 7, 5, 4, 4, 0, 1, 2, 119, 0,
      1, 2, 3, 17, 4, 5, 33, 49, 6, 18, 65, 81, 7, 97, 113, 19, 34, 50, 129, 8, 20, 66, 145, 161, 177, 193, 9, 35, 51, 82, 240, 21,
      98, 114, 209, 10, 22, 36, 52, 225, 37, 241, 23, 24, 25, 26, 38, 39, 40, 41, 42, 53, 54, 55, 56, 57, 58, 67, 68, 69, 70, 71, 72, 73,
      74, 83, 84, 85, 86, 87, 88, 89, 90, 99, 100, 101, 102, 103, 104, 105, 106, 115, 116, 117, 118, 119, 120, 121, 122, 130, 131, 132, 133, 134, 135, 136,
      137, 138, 146, 147, 148, 149, 150, 151, 152, 153, 154, 162, 163, 164, 165, 166, 167, 168, 169, 170, 178, 179, 180, 181, 182, 183, 184, 185, 186, 194, 195, 196,
      197, 198, 199, 200, 201, 202, 210, 211, 212, 213, 214, 215, 216, 217, 218, 226, 227, 228, 229, 230, 231, 232, 233, 234, 242, 243, 244, 245, 246, 247, 248, 249,
      250, 255, 218, 0, 12, 3, 1, 0, 2, 17, 3, 17, 0, 63, 0, 253, 16, 162, 138, 43, 252, 99, 63, 170, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160,
      2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 2, 138, 40, 160, 15, 255, 217])

    const imageSourceApi = image.createImageSource(testJpg.buffer);
    if (imageSourceApi == undefined) {
      console.log('renhw   ==============  imageSourceApi == undefined');
    } else {
      imageSourceApi.getDelayTimeList((err, delayTimes) => {
        if (err != undefined) {
          console.info(`getDelayTimeCallBack getDelayTime failed err` + err);
        } else {
          console.info(`getDelayTimeCallBack getDelayTime success`);
        }
      });
    }
```

# cl.image.2 NDK接口变更
1. image_pixel_map_napi.h 废弃API8接口
2. image_pixel_map_napi.h 移动除API8以外的接口到image_pixel_map_mdk.h，并去除命名空间

**变更影响**

对于已发布的Ndk接口，可能影响应用的兼容性。
废弃接口替换方案如下：
OHOS::Media::OH_GetImageInfo 替换为 OH_PixelMap_GetImageInfo
OHOS::Media::OH_AccessPixels 替换为 OH_PixelMap_AccessPixels
OHOS::Media::OH_UnAccessPixels 替换为 OH_PixelMap_UnAccessPixels

涉及变更的接口范围如下：
OH_PixelMap_CreatePixelMap (napi_env env, OhosPixelMapCreateOps info, void *buf, size_t len, napi_value *res)
OH_PixelMap_CreateAlphaPixelMap (napi_env env, napi_value source, napi_value *alpha)
OH_PixelMap_InitNativePixelMap (napi_env env, napi_value source)
OH_PixelMap_GetBytesNumberPerRow (const NativePixelMap *native, int32_t *num)
OH_PixelMap_GetIsEditable (const NativePixelMap *native, int32_t *editable)
OH_PixelMap_IsSupportAlpha (const NativePixelMap *native, int32_t *alpha)
OH_PixelMap_SetAlphaAble (const NativePixelMap *native, int32_t alpha)
OH_PixelMap_GetDensity (const NativePixelMap *native, int32_t *density)
OH_PixelMap_SetDensity (const NativePixelMap *native, int32_t density)
OH_PixelMap_SetOpacity (const NativePixelMap *native, float opacity)
OH_PixelMap_Scale (const NativePixelMap *native, float x, float y)
OH_PixelMap_Translate (const NativePixelMap *native, float x, float y)
OH_PixelMap_Rotate (const NativePixelMap *native, float angle)
OH_PixelMap_Flip (const NativePixelMap *native, int32_t x, int32_t y)
OH_PixelMap_Crop (const NativePixelMap *native, int32_t x, int32_t y, int32_t width, int32_t height)
OH_PixelMap_GetImageInfo (const NativePixelMap *native, OhosPixelMapInfos *info)
OH_PixelMap_AccessPixels (const NativePixelMap *native, void **addr)
OH_PixelMap_UnAccessPixels (const NativePixelMap *native)

**适配指导**

1. 添加头文件image_pixel_map_mdk.h。
2. 去除image_pixel_map_mdk.h中接口调用中的命名空间。

**示例：**
```
#include "napi/native_api.h"
#include "image_pixel_map_mdk.h"
#include "image_pixel_map_napi.h"

...
static NativePixelMap* getNativePixelMap(napi_env env, napi_callback_info info)
{
    napi_value thisVar = nullptr;
    napi_value argValue[NUM_1] = {0};
    size_t argCount = NUM_1;

    if (napi_get_cb_info(env, info, &argCount, argValue, &thisVar, nullptr) != napi_ok ||
        argCount < NUM_1 || argValue[NUM_0] == nullptr) {
        return nullptr;
    }
    return OH_PixelMap_InitNativePixelMap(env, argValue[NUM_0]);
}
...
```
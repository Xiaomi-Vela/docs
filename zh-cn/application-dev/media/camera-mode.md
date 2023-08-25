# 人像模式拍照实现方案

## 开发流程

人像模式依赖于模式化管理器，在获取到模式化管理的能力后，开始创建拍照流

模式化管理是对于cameraManager功能的增强与扩充，主要用于一些高级功能的管理，开发流程如下

![portraitgraphing Development Process](figures/portrait-capture-development-process.png)

## 完整示例

```ts
import camera from '@ohos.multimedia.camera'
import image from '@ohos.multimedia.image'
import media from '@ohos.multimedia.media'


// 创建CameraManager对象
context: any = getContext(this)
let cameraManager = camera.getCameraManager(this.context)
if (!cameraManager) {
    console.error("camera.getCameraManager error")
    return;
} 
// 创建ModeManager对象
context: any = getContext(this)
let modeManager = camera.getModeManager(this.context)
if (!cameraManager) {
    console.error("camera.getModeManager error")
    return;
} 
// 监听相机状态变化
cameraManager.on('cameraStatus', (err, cameraStatusInfo) => {
    console.info(`camera : ${cameraStatusInfo.camera.cameraId}`);
    console.info(`status: ${cameraStatusInfo.status}`);
})
// 获取相机列表
let cameraArray = cameraManager.getSupportedCameras();
if (cameraArray.length <= 0) {
    console.error("cameraManager.getSupportedCameras error")
    return;
} 

for (let index = 0; index < cameraArray.length; index++) {
    console.info('cameraId : ' + cameraArray[index].cameraId);                          // 获取相机ID
    console.info('cameraPosition : ' + cameraArray[index].cameraPosition);              // 获取相机位置
    console.info('cameraType : ' + cameraArray[index].cameraType);                      // 获取相机类型
    console.info('connectionType : ' + cameraArray[index].connectionType);              // 获取相机连接类型
}

// 获取模式列表
let cameraModeArray = modeManager.getSupportedModes(cameraArray[0]);
if (cameraModeArray.length <= 0) {
    console.error("modeManager.getSupportedModes error")
    return;
} 
// 创建相机输入流
let cameraInput
try {
    cameraInput = cameraManager.createCameraInput(cameraArray[0]);
} catch (error) {
   console.error('Failed to createCameraInput errorCode = ' + error.code);
}
// 监听cameraInput错误信息
let cameraDevice = cameraArray[0];
cameraInput.on('error', cameraDevice, (error) => {
    console.info(`Camera input error code: ${error.code}`);
})

// 打开相机
await cameraInput.open();

// 获取当前模式相机设备支持的输出流能力
let cameraOutputCap = modeManager.getSupportedOutputCapability(cameraArray[0], cameraModeArray[0]);
if (!cameraOutputCap) {
    console.error("modeManager.getSupportedOutputCapability error")
    return;
}
console.info("outputCapability: " + JSON.stringify(cameraOutputCap));

let previewProfilesArray = cameraOutputCap.previewProfiles;
if (!previewProfilesArray) {
    console.error("createOutput previewProfilesArray == null || undefined")
} 

let photoProfilesArray = cameraOutputCap.photoProfiles;
if (!photoProfilesArray) {
    console.error("createOutput photoProfilesArray == null || undefined")
} 

// 创建预览输出流,其中参数 surfaceId 参考上文 XComponent 组件，预览流为XComponent组件提供的surface
let previewOutput
try {
    previewOutput = cameraManager.createPreviewOutput(previewProfilesArray[0], surfaceId)
} catch (error) {
    console.error("Failed to create the PreviewOutput instance.")
}
// 监听预览输出错误信息
previewOutput.on('error', (error) => {
    console.info(`Preview output error code: ${error.code}`);
})
// 创建ImageReceiver对象，并设置照片参数：分辨率大小是根据前面 photoProfilesArray 获取的当前设备所支持的拍照分辨率大小去设置
let imageReceiver = await image.createImageReceiver(1920, 1080, 4, 8)
// 获取照片显示SurfaceId
let photoSurfaceId = await imageReceiver.getReceivingSurfaceId()
// 创建拍照输出流
let photoOutput
try {
    photoOutput = cameraManager.createPhotoOutput(photoProfilesArray[0], photoSurfaceId)
} catch (error) {
   console.error('Failed to createPhotoOutput errorCode = ' + error.code);
}
//创建portrait会话
let portraitSession
try {
    portraitSession = modeManager.createCaptureSession(cameraModeArray[0])
} catch (error) {
    console.error('Failed to create the CaptureSession instance. errorCode = ' + error.code);
}

// 监听portraitSession错误信息
portraitSession.on('error', (error) => {
    console.info(`Capture session error code: ${error.code}`);
})

// 开始配置会话
try {
    portraitSession.beginConfig()
} catch (error) {
    console.error('Failed to beginConfig. errorCode = ' + error.code);
}

// 向会话中添加相机输入流
try {
    portraitSession.addInput(cameraInput)
} catch (error) {
    console.error('Failed to addInput. errorCode = ' + error.code);
}

// 向会话中添加预览输出流
try {
    portraitSession.addOutput(previewOutput)
} catch (error) {
    console.error('Failed to addOutput(previewOutput). errorCode = ' + error.code);
}

// 向会话中添加拍照输出流
try {
    portraitSession.addOutput(photoOutput)
} catch (error) {
    console.error('Failed to addOutput(photoOutput). errorCode = ' + error.code);
}

// 提交会话配置
await portraitSession.commitConfig()

// 启动会话
await portraitSession.start().then(() => {
    console.info('Promise returned to indicate the session start success.');
})

// 获取支持的美颜类型
let beautyTypes
try {
    beautyTypes = portraitSession.getSupportedBeautyTypes()
} catch (error) {
    console.error('Failed to get the beauty types. errorCode = ' + error.code);
}
// 获取支持的美颜类型对应的美颜强度范围
let beautyRanges
try {
    beautyRanges = portraitSession.getSupportedBeautyRanges(beautyTypes[0])
} catch (error) {
    console.error('Failed to get the beauty types ranges. errorCode = ' + error.code);
}
// 设置美颜类型及对应的美颜强度
try {
    portraitSession.setBeauty(beautyTypes[0], beautyRanges[0])
} catch (error) {
    console.error('Failed to set the beauty type value. errorCode = ' + error.code);
}
// 获取已经设置的美颜类型对应的美颜强度
let beautyLevel
try {
    beautyLevel = portraitSession.getBeauty(beautyTypes[0])
} catch (error) {
    console.error('Failed to get the beauty type value. errorCode = ' + error.code);
}

// 获取支持的滤镜类型
let filterTypes
try {
    filterTypes = portraitSession.getSupportedFilters()
} catch (error) {
    console.error('Failed to get the filter types. errorCode = ' + error.code);
}
// 设置滤镜类型
try {
    portraitSession.setFilter(filterTypes[0])
} catch (error) {
    console.error('Failed to set the filter type value. errorCode = ' + error.code);
}
// 获取已经设置的滤镜类型
let filter
try {
    filter = portraitSession.getFilter()
} catch (error) {
    console.error('Failed to get the filter type value. errorCode = ' + error.code);
}

// 获取支持的虚化类型
let portraitTypes
try {
    portraitTypes = portraitSession.getSupportedPortraitEffects()
} catch (error) {
    console.error('Failed to get the portrait effects types. errorCode = ' + error.code);
}
// 设置虚化类型
try {
    portraitSession.setPortraitEffect(portraitTypes[0])
} catch (error) {
    console.error('Failed to set the portrait effects value. errorCode = ' + error.code);
}
// 获取已经设置的虚化类型
let effect
try {
    effect = portraitSession.getPortraitEffect()
} catch (error) {
    console.error('Failed to get the portrait effects value. errorCode = ' + error.code);
}

// 使用当前拍照设置进行拍照
photoOutput.capture(settings, async (err) => {
    if (err) {
        console.error('Failed to capture the photo ${err.message}');
        return;
    }
    console.info('Callback invoked to indicate the photo capture request success.');
});
// 停止当前会话
portraitSession.stop()

// 释放相机输入流
cameraInput.close()

// 释放预览输出流
previewOutput.release()

// 释放拍照输出流
photoOutput.release()

// 释放会话
portraitSession.release()

// 会话置空
portraitSession = null
```
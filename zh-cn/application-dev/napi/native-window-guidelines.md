# NativeWindow开发指导

## 场景介绍

NativeWindow是`OpenHarmony`**本地平台化窗口**，表示图形队列的生产者端。接口能力包括从`Surface`构建`NativeWindow`的能力，从`SurfaceBuffer`构建出`NativeWindowBuffer`的能力，开发者可以通过`NativeWindow`接口进行申请和提交`Buffer`。
针对NativeWindow，常见的开发场景如下：

* 通过`NativeWindow`提供的`NAPI`接口申请图形`Buffer`，并将生产图形内容写入图形`Buffer`，最终提交`Buffer`到图形队列
* 在适配EGL层的`eglswapbuffer`接口时，进行申请和提交`Buffer`

## 接口说明

| 接口名 | 描述 | 
| -------- | -------- |
| OH_NativeWindow_CreateNativeWindowFromSurface (void \*pSurface) | 创建NativeWindow实例，每次调用都会产生一个新的NativeWindow实例。 | 
| OH_NativeWindow_DestroyNativeWindow (OHNativeWindow \*window) | 将NativeWindow对象的引用计数减1，当引用计数为0的时候，该NativeWindow对象会被析构掉。 | 
| OH_NativeWindow_CreateNativeWindowBufferFromSurfaceBuffer (void \*pSurfaceBuffer) | 创建NativeWindowBuffer实例，每次调用都会产生一个新的NativeWindowBuffer实例。 | 
| OH_NativeWindow_DestroyNativeWindowBuffer (OHNativeWindowBuffer \*buffer) | 将NativeWindowBuffer对象的引用计数减1，当引用计数为0的时候，该NativeWindowBuffer对象会被析构掉。 | 
| OH_NativeWindow_NativeWindowRequestBuffer (OHNativeWindow \*window, OHNativeWindowBuffer \*\*buffer, int \*fenceFd) | 通过NativeWindow对象申请一块NativeWindowBuffer，用以内容生产。 | 
| OH_NativeWindow_NativeWindowFlushBuffer (OHNativeWindow \*window, OHNativeWindowBuffer \*buffer, int fenceFd, Region region) | 通过NativeWindow将生产好内容的NativeWindowBuffer放回到Buffer队列中，用以内容消费。 | 
| OH_NativeWindow_NativeWindowAbortBuffer (OHNativeWindow \*window, OHNativeWindowBuffer \*buffer) | 通过NativeWindow将之前申请出来的NativeWindowBuffer返还到Buffer队列中，供下次再申请。 | 
| OH_NativeWindow_NativeWindowHandleOpt (OHNativeWindow \*window, int code,...) | 设置/获取NativeWindow的属性，包括设置/获取宽高、内容格式等。 | 
| OH_NativeWindow_GetBufferHandleFromNative (OHNativeWindowBuffer \*buffer) | 通过NativeWindowBuffer获取该buffer的BufferHandle指针。 | 
| OH_NativeWindow_NativeObjectReference (void \*obj) | 增加一个NativeObject的引用计数。 | 
| OH_NativeWindow_NativeObjectUnreference (void \*obj) | 减少一个NativeObject的引用计数，当引用计数减少为0时，该NativeObject将被析构掉。 | 
| OH_NativeWindow_GetNativeObjectMagic (void \*obj) | 获取NativeObject的MagicId。 | 
| OH_NativeWindow_NativeWindowSetScalingMode (OHNativeWindow \*window, uint32_t sequence, OHScalingMode scalingMode) | 设置NativeWindow的缩放模式。 | 
| OH_NativeWindow_NativeWindowSetMetaData(OHNativeWindow \*window, uint32_t sequence, int32_t size, const OHHDRMetaData \*metaData) | 设置NativeWindow的HDR静态元数据。 | 
| OH_NativeWindow_NativeWindowSetMetaDataSet(OHNativeWindow \*window, uint32_t sequence, OHHDRMetadataKey key, int32_t size, const uint8_t \*metaData) | 设置NativeWindow的HDR静态元数据集。 | 
| OH_NativeWindow_NativeWindowSetTunnelHandle(OHNativeWindow \*window, const OHExtDataHandle \*handle) | 设置NativeWindow的TunnelHandle。 | 

详细的接口说明请参考[native_window](../reference/native-apis/_native_window.md)。

## 开发步骤

以下步骤描述了在**OpenHarmony**中如何使用`NativeWindow`提供的`NAPI`接口，申请图形`Buffer`，并将生产图形内容写入图形`Buffer`后，最终提交`Buffer`到图形队列。

1. **获取NativeWindow实例**。可在[`OH_NativeXComponent_Callback`](../reference/native-apis/_o_h___native_x_component___callback.md)提供的接口中获取。
   1. 在xxx.ets 中定义 XComponent。
        ```ts
        XComponent({ id: 'xcomponentId', type: 'surface', libraryname: 'nativerender'})
            .onLoad((context) => {
                this.context = context;
            })
            .onDestroy(() => {
            })
        ```
   2. 在 native c++ 层获取 NativeXComponent。
       ```c++
       napi_value exportInstance = nullptr;
       napi_get_named_property(env, exports, OH_NATIVE_XCOMPONENT_OBJ, &exportInstance);

       OH_NativeXComponent *nativeXComponent = nullptr;
       napi_unwrap(env, exportInstance, reinterpret_cast<void**>(&nativeXComponent));

       char idStr[OH_XCOMPONENT_ID_LEN_MAX + 1] = { };
       uint64_t idSize = OH_XCOMPONENT_ID_LEN_MAX + 1;
       OH_NativeXComponent_GetXComponentId(nativeXComponent, idStr, &idSize);
        ```
   3. 定义 OH_NativeXComponent_Callback。
       ```c++
       // 定义回调函数
       void OnSurfaceCreatedCB(OH_NativeXComponent* component, void* window)
       {
           // 可获取 NativeWindow 实例
           OHNativeWindow* nativeWindow = window;
           // ...
       }
       void OnSurfaceChangedCB(OH_NativeXComponent* component, void* window)
       {
           // 可获取 NativeWindow 实例
           OHNativeWindow* nativeWindow = window;
           // ...
       }
       void OnSurfaceDestroyedCB(OH_NativeXComponent* component, void* window)
       {
           // 可获取 NativeWindow 实例
           OHNativeWindow* nativeWindow = window;
           // ...
       }
       void DispatchTouchEventCB(OH_NativeXComponent* component, void* window)
       {
           // 可获取 NativeWindow 实例
           OHNativeWindow* nativeWindow = window;
           // ...
       }
       ```
       ```c++
       // 初始化 OH_NativeXComponent_Callback
       OH_NativeXComponent_Callback callback_;
       callback_->OnSurfaceCreated = OnSurfaceCreatedCB;
       callback_->OnSurfaceChanged = OnSurfaceChangedCB;
       callback_->OnSurfaceDestroyed = OnSurfaceDestroyedCB;
       callback_->DispatchTouchEvent = DispatchTouchEventCB;
       ```
   4. 将 OH_NativeXComponent_Callback 注册给 NativeXComponent。
       ```c++
       OH_NativeXComponent_RegisterCallback(nativeXComponent, &callback_);
       ```

2. **设置NativeWindowBuffer的属性**。使用`OH_NativeWindow_NativeWindowHandleOpt`设置`NativeWindowBuffer`的属性。
    ```c++
    // 设置 NativeWindowBuffer 的读写场景
    int code = SET_USAGE;
    int32_t usage = BUFFER_USAGE_CPU_READ | BUFFER_USAGE_CPU_WRITE | BUFFER_USAGE_MEM_DMA;
    int32_t ret = OH_NativeWindow_NativeWindowHandleOpt(nativeWindow, code, usage);
    // 设置 NativeWindowBuffer 的宽高
    code = SET_BUFFER_GEOMETRY;
    int32_t width = 0x100;
    int32_t height = 0x100;
    ret = OH_NativeWindow_NativeWindowHandleOpt(nativeWindow, code, width, height);
    // 设置 NativeWindowBuffer 的步长
    code = SET_STRIDE;
    int32_t stride = 0x8;
    ret = OH_NativeWindow_NativeWindowHandleOpt(nativeWindow, code, stride);
    // 设置 NativeWindowBuffer 的格式
    code = SET_FORMAT;
    int32_t format = PIXEL_FMT_RGBA_8888;
    ret = OH_NativeWindow_NativeWindowHandleOpt(nativeWindow, code, format);
    ```

3. **从图形队列申请NativeWindowBuffer**。
    ```c++
    struct NativeWindowBuffer* buffer = nullptr;
    int fenceFd;
    // 通过 OH_NativeWindow_NativeWindowRequestBuffer 获取 NativeWindowBuffer 实例
    OH_NativeWindow_NativeWindowRequestBuffer(nativeWindow_, &buffer, &fenceFd);
    // 通过 OH_NativeWindow_GetNativeBufferHandleFromNative 获取 buffer 的 handle
    BufferHandle* bufferHandle = OH_NativeWindow_GetNativeBufferHandleFromNative(buffer);
    ```

4. **将生产的内容写入NativeWindowBuffer**。
    ```c++
    auto image = static_cast<uint8_t *>(buffer->sfbuffer->GetVirAddr());
    static uint32_t value = 0x00;
    value++;

    uint32_t *pixel = static_cast<uint32_t *>(image);
    for (uint32_t x = 0; x < width; x++) {
        for (uint32_t y = 0;  y < height; y++) {
            *pixel++ = value;
        }
    }
    ```

5. **提交NativeWindowBuffer到图形队列**。
    ```c++
    // 设置刷新区域，如果Region中的Rect为nullptr,或者rectNumber为0，则认为NativeWindowBuffer全部有内容更改。
    Region region{nullptr, 0};
    // 通过OH_NativeWindow_NativeWindowFlushBuffer 提交给消费者使用，例如：显示在屏幕上。
    OH_NativeWindow_NativeWindowFlushBuffer(nativeWindow_, buffer, fenceFd, region);
    ```

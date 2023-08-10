# image_mdk.h


## Overview

The **image_mdk.h** file declares the functions that access the image rectangle, size, format, and component data.

**Since**

10

**Related Modules**

[Image](image.md)


## Summary


### Structs

| Name| Description| 
| -------- | -------- |
| [OHOS::Media::OhosImageRect](_o_h_o_s_1_1_media_1_1_ohos_image_rect.md) | Defines the information about an image rectangle.| 
| [OHOS::Media::OhosImageComponent](_o_h_o_s_1_1_media_1_1_ohos_image_component.md) | Defines the information about an image component.| 


### Types

| Name| Description| 
| -------- | -------- |
| [OHOS::Media::ImageNative](image.md#imagenative) | Defines an image object at the native layer.| 


### Enums

| Name| Description| 
| -------- | -------- |
| { [OHOS::Media::OHOS_IMAGE_FORMAT_YCBCR_422_SP](image.md) = 1000,<br>[OHOS::Media::OHOS_IMAGE_FORMAT_JPEG](image.md) = 2000, } | Enumerates the image formats.| 
| { [OHOS::Media::OHOS_IMAGE_COMPONENT_FORMAT_YUV_Y](image.md) = 1,<br>[OHOS::Media::OHOS_IMAGE_COMPONENT_FORMAT_YUV_U](image.md) = 2,<br>[OHOS::Media::OHOS_IMAGE_COMPONENT_FORMAT_YUV_V](image.md) = 3,<br>[OHOS::Media::OHOS_IMAGE_COMPONENT_FORMAT_JPEG](image.md) = 4, } | Enumerates the image components.| 


### Functions

| Name| Description| 
| -------- | -------- |
| [OHOS::Media::OH_Image_InitImageNative](image.md#oh_image_initimagenative) (napi_env env, napi_value source) | Parses an **ImageNative** object from an **Image** object at the JavaScript native layer.| 
| [OHOS::Media::OH_Image_ClipRect](image.md#oh_image_cliprect) (const [ImageNative](image.md#imagenative) \*native, struct [OhosImageRect](_o_h_o_s_1_1_media_1_1_ohos_image_rect.md) \*rect) | Obtains [OhosImageRect](_o_h_o_s_1_1_media_1_1_ohos_image_rect.md) of an **ImageNative** object.| 
| [OHOS::Media::OH_Image_Size](image.md#oh_image_size) (const [ImageNative](image.md#imagenative) \*native, struct [OhosImageSize](_ohos_image_size.md) \*size) | Obtains [OhosImageSize](_ohos_image_size.md) of an **ImageNative** object.| 
| [OHOS::Media::OH_Image_Format](image.md#oh_image_format) (const [ImageNative](image.md#imagenative) \*native, int32_t \*format) | Obtains the image format of an **ImageNative** object.| 
| [OHOS::Media::OH_Image_GetComponent](image.md#oh_image_getcomponent) (const [ImageNative](image.md#imagenative) \*native, int32_t componentType, struct [OhosImageComponent](_o_h_o_s_1_1_media_1_1_ohos_image_component.md) \*componentNative) | Obtains [OhosImageComponent](_o_h_o_s_1_1_media_1_1_ohos_image_component.md) of an **ImageNative** object.| 
| [OHOS::Media::OH_Image_Release](image.md#oh_image_release) ([ImageNative](image.md#imagenative) \*native) | Releases an **ImageNative** object.| 

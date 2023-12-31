# AudioEncoder

## Overview

The **AudioEncoder** module provides the functions for audio encoding. This module may not be supported on some devices. You can call [CanIUse](../syscap.md) to check whether your device supports this module.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**Since**

9

## Summary

### Files

| Name                                                             | Description                                                                                                       |
| ----------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| [native_avcodec_audioencoder.h](native__avcodec__audioencoder_8h.md) | Declares the native APIs used for audio encoding.<br>**File to include**: <multimedia/player_framework/native_avcodec_audioencoder.h><br>**Library**: libnative_media_aenc.so|

### Functions

| Name                                                                                                                                         | Description                                                                            |
| --------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| \*[OH_AudioEncoder_CreateByMime](#oh_audioencoder_createbymime) (const char \*mime)                                                 | Creates an audio encoder instance based on a Multipurpose Internet Mail Extension (MIME) type. This function is recommended in most cases.                    |
| \*[OH_AudioEncoder_CreateByName](#oh_audioencoder_createbyname) (const char \*name)                                                 | Creates an audio encoder instance based on an encoder name. To use this function, you must know the exact name of the encoder.  |
| [OH_AudioEncoder_Destroy](#oh_audioencoder_destroy) (OH_AVCodec \*codec)                                                            | Clears the internal resources of an audio encoder and destroys the encoder instance.                                            |
| [OH_AudioEncoder_SetCallback](#oh_audioencoder_setcallback) (OH_AVCodec \*codec, OH_AVCodecAsyncCallback callback, void \*userData) | Sets an asynchronous callback so that your application can respond to events generated by an audio encoder.                  |
| [OH_AudioEncoder_Configure](#oh_audioencoder_configure) (OH_AVCodec \*codec, OH_AVFormat \*format)                                  | Configures an audio encoder. Typically, you need to configure the description information about the audio track to be encoded.                          |
| [OH_AudioEncoder_Prepare](#oh_audioencoder_prepare) (OH_AVCodec \*codec)                                                            | Prepares internal resources for an audio encoder. This function must be called after **Configure**.                   |
| [OH_AudioEncoder_Start](#oh_audioencoder_start) (OH_AVCodec \*codec)                                                                | Starts an audio encoder. This function can be called only after the encoder is prepared successfully.                                             |
| [OH_AudioEncoder_Stop](#oh_audioencoder_stop) (OH_AVCodec \*codec)                                                                  | Stops an audio encoder.                                                                    |
| [OH_AudioEncoder_Flush](#oh_audioencoder_flush) (OH_AVCodec \*codec)                                                                | Clears the input and output data in the internal buffer of an audio encoder.                                              |
| [OH_AudioEncoder_Reset](#oh_audioencoder_reset) (OH_AVCodec \*codec)                                                                | Resets an audio encoder.                                                                    |
| \*[OH_AudioEncoder_GetOutputDescription](#oh_audioencoder_getoutputdescription) (OH_AVCodec \*codec)                                | Obtains the description information about the output data of an audio encoder. For details, see [OH_AVFormat](native__avformat_8h.md).|
| [OH_AudioEncoder_SetParameter](#oh_audioencoder_setparameter) (OH_AVCodec \*codec, OH_AVFormat \*format)                            | Sets dynamic parameters for an audio encoder.                                                          |
| [OH_AudioEncoder_PushInputData](#oh_audioencoder_pushinputdata) (OH_AVCodec \*codec, uint32_t index, OH_AVCodecBufferAttr attr)     | Pushes the input buffer filled with data to an audio encoder.                                      |
| [OH_AudioEncoder_FreeOutputData](#oh_audioencoder_freeoutputdata) (OH_AVCodec \*codec, uint32_t index)                              | Frees an output buffer of an audio encoder.                                              |
| [OH_AudioEncoder_IsValid](#oh_audioencoder_isvalid) (OH_AVCodec \*codec, bool \*isValid)                                            | Checks whether an audio encoder instance is valid.                                                    |

## Function Description

### OH_AudioEncoder_Configure()

```
OH_AVErrCode OH_AudioEncoder_Configure (OH_AVCodec * codec, OH_AVFormat * format )
```

**Description**

Configures an audio encoder. Typically, you need to configure the description information about the audio track to be encoded.

This function must be called prior to **Prepare**.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**Parameters**

| Name  | Description                                               |
| ------ | --------------------------------------------------- |
| codec  | Pointer to an **OH_AVCodec** instance.                         |
| format | Pointer to an **OH_AVFormat** instance, which provides the description information about the audio track to be encoded.|

**Returns**

Returns **AV_ERR_OK** if the operation is successful; returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) otherwise.

**Since**

9

### OH_AudioEncoder_CreateByMime()

```
OH_AVCodec* OH_AudioEncoder_CreateByMime (const char * mime)
```

**Description**

Creates an audio encoder instance based on a MIME type. This function is recommended in most cases.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**Parameters**

| Name| Description                                                   |
| ---- | ------------------------------------------------------- |
| mime | Pointer to a string that describes the MIME type. For details, see [AVCODEC_MIMETYPE](_codec_base.md#variables).|

**Returns**

Returns the pointer to an **OH_AVCodec** instance.

**Since**

9

### OH_AudioEncoder_CreateByName()

```
OH_AVCodec* OH_AudioEncoder_CreateByName (const char * name)
```

**Description**

Creates an audio encoder instance based on an encoder name. To use this function, you must know the exact name of the encoder.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**Parameters**

| Name| Description            |
| ---- | ---------------- |
| name | Pointer to an audio encoder name.|

**Returns**

Returns the pointer to an **OH_AVCodec** instance.

**Since**

9

### OH_AudioEncoder_Destroy()

```
OH_AVErrCode OH_AudioEncoder_Destroy (OH_AVCodec * codec)
```

**Description**

Clears the internal resources of an audio encoder and destroys the encoder instance.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**Parameters**

| Name | Description                      |
| ----- | -------------------------- |
| codec | Pointer to an **OH_AVCodec** instance.|

**Returns**

Returns **AV_ERR_OK** if the operation is successful; returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) otherwise.

**Since**

9

### OH_AudioEncoder_Flush()

```
OH_AVErrCode OH_AudioEncoder_Flush (OH_AVCodec * codec)
```

**Description**

Clears the input and output data in the internal buffer of an audio encoder.

This function invalidates the indexes of all buffers previously reported through the asynchronous callback. Therefore, before calling this function, ensure that the buffers with the specified indexes are no longer required.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**Parameters**

| Name | Description                      |
| ----- | -------------------------- |
| codec | Pointer to an **OH_AVCodec** instance.|

**Returns**

Returns **AV_ERR_OK** if the operation is successful; returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) otherwise.

**Since**

9

### OH_AudioEncoder_FreeOutputData()

```
OH_AVErrCode OH_AudioEncoder_FreeOutputData (OH_AVCodec * codec, uint32_t index )
```

**Description**

Frees an output buffer of an audio encoder.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**Parameters**

| Name | Description                          |
| ----- | ------------------------------ |
| codec | Pointer to an **OH_AVCodec** instance.    |
| index | Index of the output buffer.|

**Returns**

Returns **AV_ERR_OK** if the operation is successful; returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) otherwise.

**Since**

9

### OH_AudioEncoder_GetOutputDescription()

```
OH_AVFormat* OH_AudioEncoder_GetOutputDescription (OH_AVCodec * codec)
```

**Description**

Obtains the description information about the output data of an audio encoder. For details, see [OH_AVFormat](native__avformat_8h.md).

The caller must manually release the **OH_AVFormat** instance in the return value.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**Parameters**

| Name | Description                      |
| ----- | -------------------------- |
| codec | Pointer to an **OH_AVCodec** instance.|

**Returns**

Returns the handle to an **OH_AVFormat** instance. The lifecycle of this instance is refreshed when **GetOutputDescription** is called again and destroyed when the **OH_AVCodec** instance is destroyed.

**Since**

9

### OH_AudioEncoder_IsValid()

```
OH_AVErrCode OH_AudioEncoder_IsValid (OH_AVCodec * codec, bool * isValid )
```

**Description**

Checks whether an audio encoder instance is valid.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**Parameters**

| Name   | Description                                                             |
| ------- | ----------------------------------------------------------------- |
| codec   | Pointer to an **OH_AVCodec** instance.                                       |
| isValid | Pointer to an instance of the Boolean type. The value **true** means that the encoder instance is valid and **false** means the opposite.|

**Returns**

Returns **AV_ERR_OK** if the operation is successful; returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) otherwise.

**Since**

10

### OH_AudioEncoder_Prepare()

```
OH_AVErrCode OH_AudioEncoder_Prepare (OH_AVCodec * codec)
```

**Description**

Prepares internal resources for an audio encoder. This function must be called after **Configure**.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**Parameters**

| Name | Description                      |
| ----- | -------------------------- |
| codec | Pointer to an **OH_AVCodec** instance.|

**Returns**

Returns **AV_ERR_OK** if the operation is successful; returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) otherwise.

**Since**

9

### OH_AudioEncoder_PushInputData()

```
OH_AVErrCode OH_AudioEncoder_PushInputData (OH_AVCodec * codec, uint32_t index, OH_AVCodecBufferAttr attr )
```

**Description**

Pushes the input buffer filled with data to an audio encoder.

The **OH_AVCodecOnNeedInputData** callback reports the available input buffer and the index. After being pushed to the encoder, a buffer is not accessible until the buffer with the same index is reported again through the **OH_AVCodecOnNeedInputData** callback. In addition, some encoders require the input of specific data to initialize the encoding process.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**Parameters**

| Name | Description                          |
| ----- | ------------------------------ |
| codec | Pointer to an **OH_AVCodec** instance.    |
| index | Index of the input buffer.|
| attr  | Description information about the data in the buffer.|

**Returns**

Returns **AV_ERR_OK** if the operation is successful; returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) otherwise.

**Since**

9

### OH_AudioEncoder_Reset()

```
OH_AVErrCode OH_AudioEncoder_Reset (OH_AVCodec * codec)
```

**Description**

Resets an audio encoder. To continue encoding, you must call **Configure** to configure the encoder again.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**Parameters**

| Name | Description                      |
| ----- | -------------------------- |
| codec | Pointer to an **OH_AVCodec** instance.|

**Returns**

Returns **AV_ERR_OK** if the operation is successful; returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) otherwise.

### OH_AudioEncoder_SetCallback()

```
OH_AVErrCode OH_AudioEncoder_SetCallback (OH_AVCodec * codec, OH_AVCodecAsyncCallback callback, void * userData )
```

**Description**

Sets an asynchronous callback so that your application can respond to events generated by an audio encoder.

This function must be called prior to **Prepare**.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**Parameters**

| Name    | Description                                                         |
| -------- | ------------------------------------------------------------- |
| codec    | Pointer to an **OH_AVCodec** instance.                                   |
| callback | Callback function to set. For details, see **OH_AVCodecAsyncCallback**.|
| userData | User-specific data.                                               |

**Returns**

Returns **AV_ERR_OK** if the operation is successful; returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) otherwise.

**Since**

9

### OH_AudioEncoder_SetParameter()

```
OH_AVErrCode OH_AudioEncoder_SetParameter (OH_AVCodec * codec, OH_AVFormat * format )
```

**Description**

Sets dynamic parameters for an audio encoder.

This function can be called only after the encoder is started. Incorrect parameter settings may cause encoding failure.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**Parameters**

| Name  | Description                      |
| ------ | -------------------------- |
| codec  | Pointer to an **OH_AVCodec** instance.|
| format | Handle to an **OH_AVFormat** instance.     |

**Returns**

Returns **AV_ERR_OK** if the operation is successful; returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) otherwise.

**Since**

9

### OH_AudioEncoder_Start()

```
OH_AVErrCode OH_AudioEncoder_Start (OH_AVCodec * codec)
```

**Description**

Starts an audio encoder. This function can be called only after the encoder is prepared successfully.

After being started, the encoder starts to report the **OH_AVCodecOnNeedInputData** event.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**Parameters**

| Name | Description                      |
| ----- | -------------------------- |
| codec | Pointer to an **OH_AVCodec** instance.|

**Returns**

Returns **AV_ERR_OK** if the operation is successful; returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) otherwise.

**Since**

9

### OH_AudioEncoder_Stop()

```
OH_AVErrCode OH_AudioEncoder_Stop (OH_AVCodec * codec)
```

**Description**

Stops an audio encoder. After the encoder is stopped, you can call **Start** to start it again.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**Parameters**

| Name | Description                      |
| ----- | -------------------------- |
| codec | Pointer to an **OH_AVCodec** instance.|

**Returns**

Returns **AV_ERR_OK** if the operation is successful; returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) otherwise.

**Since**

9

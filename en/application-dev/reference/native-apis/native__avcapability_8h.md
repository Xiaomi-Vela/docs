# native_avcapability.h


## Overview

The **native_avcapability.h** file declares the native APIs used to query the codec capability.

**Since**

10

**Related Modules**

[AVCapability](_a_v_capability.md)


## Summary


### Structs

| Name| Description| 
| -------- | -------- |
| [OH_AVRange](_o_h___a_v_range.md) | Defines the value range, which contains the minimum value and maximum value.| 


### Types

| Name| Description| 
| -------- | -------- |
| [OH_BitrateMode](_a_v_capability.md#oh_bitratemode) | Defines an enum that enumerates the bit rate modes of an encoder.| 
| [OH_AVRange](_a_v_capability.md#oh_avrange) | Defines a struct for the value range, which contains the minimum value and maximum value.| 
| [OH_AVCodecCategory](_a_v_capability.md#oh_avcodeccategory) | Defines an enum that enumerates the codec categories.| 


### Enums

| Name| Description| 
| -------- | -------- |
| [OH_BitrateMode](_a_v_capability.md#oh_bitratemode) {<br>&nbsp;&nbsp;&nbsp;&nbsp;**BITRATE_MODE_CBR** = 0,<br>&nbsp;&nbsp;&nbsp;&nbsp;**BITRATE_MODE_VBR** = 1,<br>&nbsp;&nbsp;&nbsp;&nbsp;**BITRATE_MODE_CQ** = 2<br>} | Enumerates the bit rate modes of an encoder.| 
| [OH_AVCodecCategory](_a_v_capability.md#oh_avcodeccategory) {<br>&nbsp;&nbsp;&nbsp;&nbsp;**HARDWARE** = 0,<br>&nbsp;&nbsp;&nbsp;&nbsp;**SOFTWARE**<br>} | Enumerates the codec categories.| 


### Functions

| Name| Description| 
| -------- | -------- |
| \*[OH_AVCodec_GetCapability](_a_v_capability.md#oh_avcodec_getcapability) (const char \*mime, bool isEncoder) | Obtains the codec capability recommended by the system.| 
| \*[OH_AVCodec_GetCapabilityByCategory](_a_v_capability.md#oh_avcodec_getcapabilitybycategory) (const char \*mime, bool isEncoder, [OH_AVCodecCategory](_a_v_capability.md#oh_avcodeccategory) category) | Obtains the codec capability by category, which can be a hardware codec or software codec.| 
| [OH_AVCapability_IsHardware](_a_v_capability.md#oh_avcapability_ishardware) (OH_AVCapability \*capability) | Checks whether a codec capability instance describes a hardware codec.| 
| \*[OH_AVCapability_GetName](_a_v_capability.md#oh_avcapability_getname) (OH_AVCapability \*capability) | Obtains the codec name.| 
| [OH_AVCapability_GetMaxSupportedInstances](_a_v_capability.md#oh_avcapability_getmaxsupportedinstances) (OH_AVCapability \*capability) | Obtains the maximum number of codec instances supported by a codec.| 
| [OH_AVCapability_GetEncoderBitrateRange](_a_v_capability.md#oh_avcapability_getencoderbitraterange) (OH_AVCapability \*capability, [OH_AVRange](_o_h___a_v_range.md) \*bitrateRange) | Obtains the bit rate range supported by an encoder.| 
| [OH_AVCapability_IsEncoderBitrateModeSupported](_a_v_capability.md#oh_avcapability_isencoderbitratemodesupported) (OH_AVCapability \*capability, [OH_BitrateMode](_a_v_capability.md#oh_bitratemode) bitrateMode) | Checks whether an encoder supports a specific bit rate mode.| 
| [OH_AVCapability_GetEncoderQualityRange](_a_v_capability.md#oh_avcapability_getencoderqualityrange) (OH_AVCapability \*capability, [OH_AVRange](_o_h___a_v_range.md) \*qualityRange) | Obtains the quality range supported by an encoder.| 
| [OH_AVCapability_GetEncoderComplexityRange](_a_v_capability.md#oh_avcapability_getencodercomplexityrange) (OH_AVCapability \*capability, [OH_AVRange](_o_h___a_v_range.md) \*complexityRange) | Obtains the complexity range supported by an encoder.| 
| [OH_AVCapability_GetAudioSupportedSampleRates](_a_v_capability.md#oh_avcapability_getaudiosupportedsamplerates) (OH_AVCapability \*capability, const int32_t \*\*sampleRates, uint32_t \*sampleRateNum) | Obtains the sampling rates supported by an audio codec.| 
| [OH_AVCapability_GetAudioChannelCountRange](_a_v_capability.md#oh_avcapability_getaudiochannelcountrange) (OH_AVCapability \*capability, [OH_AVRange](_o_h___a_v_range.md) \*channelCountRange) | Obtains the count range of audio channels supported by an audio codec.| 
| [OH_AVCapability_GetVideoWidthAlignment](_a_v_capability.md#oh_avcapability_getvideowidthalignment) (OH_AVCapability \*capability, int32_t \*widthAlignment) | Obtains the video width alignment supported by a video codec.| 
| [OH_AVCapability_GetVideoHeightAlignment](_a_v_capability.md#oh_avcapability_getvideoheightalignment) (OH_AVCapability \*capability, int32_t \*heightAlignment) | Obtains the video height alignment supported by a video codec.| 
| [OH_AVCapability_GetVideoWidthRangeForHeight](_a_v_capability.md#oh_avcapability_getvideowidthrangeforheight) (OH_AVCapability \*capability, int32_t height, [OH_AVRange](_o_h___a_v_range.md) \*widthRange) | Obtains the video width range supported by a video codec based on a given height.| 
| [OH_AVCapability_GetVideoHeightRangeForWidth](_a_v_capability.md#oh_avcapability_getvideoheightrangeforwidth) (OH_AVCapability \*capability, int32_t width, [OH_AVRange](_o_h___a_v_range.md) \*heightRange) | Obtains the video height range supported by a video codec based on a given width.| 
| [OH_AVCapability_GetVideoWidthRange](_a_v_capability.md#oh_avcapability_getvideowidthrange) (OH_AVCapability \*capability, [OH_AVRange](_o_h___a_v_range.md) \*widthRange) | Obtains the video width range supported by a video codec.| 
| [OH_AVCapability_GetVideoHeightRange](_a_v_capability.md#oh_avcapability_getvideoheightrange) (OH_AVCapability \*capability, [OH_AVRange](_o_h___a_v_range.md) \*heightRange) | Obtains the video height range supported by a video codec.| 
| [OH_AVCapability_IsVideoSizeSupported](_a_v_capability.md#oh_avcapability_isvideosizesupported) (OH_AVCapability \*capability, int32_t width, int32_t height) | Checks whether a video codec supports a specific video size.| 
| [OH_AVCapability_GetVideoFrameRateRange](_a_v_capability.md#oh_avcapability_getvideoframeraterange) (OH_AVCapability \*capability, [OH_AVRange](_o_h___a_v_range.md) \*frameRateRange) | Obtains the video frame rate range supported by a video codec.| 
| [OH_AVCapability_GetVideoFrameRateRangeForSize](_a_v_capability.md#oh_avcapability_getvideoframeraterangeforsize) (OH_AVCapability \*capability, int32_t width, int32_t height, [OH_AVRange](_o_h___a_v_range.md) \*frameRateRange) | Obtains the video frame rate range supported by a video codec based on a given video size.| 
| [OH_AVCapability_AreVideoSizeAndFrameRateSupported](_a_v_capability.md#oh_avcapability_arevideosizeandframeratesupported) (OH_AVCapability \*capability, int32_t width, int32_t height, int32_t frameRate) | Checks whether a video codec supports the combination of a video size and frame rate.| 
| [OH_AVCapability_GetVideoSupportedPixelFormats](_a_v_capability.md#oh_avcapability_getvideosupportedpixelformats) (OH_AVCapability \*capability, const int32_t \*\*pixelFormats, uint32_t \*pixelFormatNum) | Obtains the video pixel formats supported by a video codec.| 
| [OH_AVCapability_GetSupportedProfiles](_a_v_capability.md#oh_avcapability_getsupportedprofiles) (OH_AVCapability \*capability, const int32_t \*\*profiles, uint32_t \*profileNum) | Obtains the profiles supported by a codec.| 
| [OH_AVCapability_GetSupportedLevelsForProfile](_a_v_capability.md#oh_avcapability_getsupportedlevelsforprofile) (OH_AVCapability \*capability, int32_t profile, const int32_t \*\*levels, uint32_t \*levelNum) | Obtains the codec levels supported by a profile.| 
| [OH_AVCapability_AreProfileAndLevelSupported](_a_v_capability.md#oh_avcapability_areprofileandlevelsupported) (OH_AVCapability \*capability, int32_t profile, int32_t level) | Checks whether a codec supports the combination of a profile and level.| 

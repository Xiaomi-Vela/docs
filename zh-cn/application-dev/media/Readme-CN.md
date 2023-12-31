# 媒体

- [媒体应用开发概述](media-application-overview.md)
- 音视频
  - [音视频概述](av-overview.md)
  - [AVPlayer和AVRecorder](avplayer-avrecorder-overview.md)
  - 音频播放
    - [音频播放开发概述](audio-playback-overview.md)
    - [使用AVPlayer开发音频播放功能(ArkTS)](using-avplayer-for-playback.md)
    - [使用AVPlayer开发音频播放功能(C/C++)](using-ndk-avplayer-for-playerback.md)
    - [使用AudioRenderer开发音频播放功能(ArkTS)](using-audiorenderer-for-playback.md)
    - [使用OpenSL ES开发音频播放功能(C/C++)](using-opensl-es-for-playback.md)
    - [使用TonePlayer开发音频播放功能(仅对系统应用开放)(ArkTS)](using-toneplayer-for-playback.md)
    - [使用OHAudio开发音频播放功能(C/C++)](using-ohaudio-for-playback.md)
    - [使用SoundPool开发音频播放功能(ArkTS)](using-soundpool-for-playback.md)
    - [多音频播放的并发策略(ArkTS)](audio-playback-concurrency.md)
    - [播放音量管理(ArkTS)](volume-management.md)
    - [音效管理(ArkTS)](audio-effect-management.md)
    - [音频播放流管理(ArkTS)](audio-playback-stream-management.md)
    - [音频输出设备管理(ArkTS)](audio-output-device-management.md)
    - [分布式音频播放(仅对系统应用开放)(ArkTS)](distributed-audio-playback.md)
  - 音频录制
    - [音频录制开发概述](audio-recording-overview.md)
    - [使用AVRecorder开发音频录制功能(ArkTS)](using-avrecorder-for-recording.md)
    - [使用AudioCapturer开发音频录制功能(ArkTS)](using-audiocapturer-for-recording.md)
    - [使用OpenSL ES开发音频录制功能(C/C++)](using-opensl-es-for-recording.md)
    - [使用OHAudio开发音频录制功能(C/C++)](using-ohaudio-for-recording.md)
    - [管理麦克风(ArkTS)](mic-management.md)
    - [音频录制流管理(ArkTS)](audio-recording-stream-management.md)
    - [音频输入设备管理(ArkTS)](audio-input-device-management.md)
  - 音频通话
    - [音频通话开发概述](audio-call-overview.md)
    - [开发音频通话功能(ArkTS)](audio-call-development.md)
  - [视频播放(ArkTS)](video-playback.md)
  - [视频录制(ArkTS)](video-recording.md)
  - [屏幕录制(C/C++)](avscreen-capture.md)
  - [获取音视频元数据(ArkTS)](avmetadataextractor.md)
  - [获取视频缩略图(ArkTS)](avimagegenerator.md)
  - 音视频编解码
    - [获取支持的编解码能力(C/C++)](obtain-supported-codecs.md)
    - [音频编码(C/C++)](audio-encoding.md)
    - [音频解码(C/C++)](audio-decoding.md)
    - [视频编码(C/C++)](video-encoding.md)
    - [视频解码(C/C++)](video-decoding.md)
    - [音视频封装(C/C++)](audio-video-encapsulation.md)
    - [音视频解封装(C/C++)](audio-video-decapsulation.md)
- 媒体会话
  - [媒体会话概述](avsession-overview.md)
  - 本地媒体会话
    - [本地媒体会话概述](local-avsession-overview.md)
    - [媒体会话提供方(ArkTS)](using-avsession-developer.md)
    - [媒体会话控制方(ArkTS)](using-avsession-controller.md)
  - 分布式媒体会话
    - [分布式媒体会话概述](distributed-avsession-overview.md)
    - [使用分布式媒体会话(ArkTS)](using-distributed-avsession.md)
- 相机
  - [相机开发概述](camera-overview.md)
  - [开发准备](camera-preparation.md)
  - 相机开发指导(ArkTS)
    - [设备输入(ArkTS)](camera-device-input.md)
    - [会话管理(ArkTS)](camera-session-management.md)
    - [预览(ArkTS)](camera-preview.md)
    - [拍照(ArkTS)](camera-shooting.md)
    - [录像(ArkTS)](camera-recording.md)
    - [元数据(ArkTS)](camera-metadata.md)
  - 相机最佳实践(ArkTS)
    - [拍照实现方案(ArkTS)](camera-shooting-case.md)
    - [录像实现方案(ArkTS)](camera-recording-case.md)
    - [使用人像模式拍照(ArkTS)](camera-mode.md)
    - [双路预览(ArkTS)](camera-dual-channel-preview.md)
    - [性能提升方案(仅对系统应用开放)(ArkTS)](camera-performance-improvement.md)
  - 相机开发指导(C/C++)
    - [设备输入(C/C++)](native-camera-device-input.md)
    - [会话管理(C/C++)](native-camera-session-management.md)
    - [预览(C/C++)](native-camera-preview.md)
    - [预览流二次处理(C/C++)](native-camera-preview-imageReceiver.md)
    - [拍照(C/C++)](native-camera-shooting.md)
    - [录像(C/C++)](native-camera-recording.md)
    - [录像流二次处理(C/C++)](native-camera-recording-imageReceiver.md)
    - [元数据(C/C++)](native-camera-metadata.md)
  - 相机最佳实践(C/C++)
    - [拍照实现方案(C/C++)](native-camera-shooting-case.md)
    - [录像实现方案(C/C++)](native-camera-recording-case.md)
    - [录像流二次处理的实现方案(C/C++)](native-camera-recording-case-imageReceiver.md)
- 图片
  - [图片开发概述](image-overview.md)
  - [图片解码(ArkTS)](image-decoding.md)
  - 图片处理
    - [图像变换(ArkTS)](image-transformation.md)
    - [图像变换(C/C++)](image-transformation-native.md)
    - [PixelMap数据处理(C/C++)](image-pixelmap-operation-native.md)
    - [位图操作(ArkTS)](image-pixelmap-operation.md)
  - [图片编码(ArkTS)](image-encoding.md)
  - [图片编码(C/C++)](image-encoding-native.md)
  - [图片工具(ArkTS)](image-tool.md)

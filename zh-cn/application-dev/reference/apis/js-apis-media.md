# 媒体服务

> **说明：**
> 本模块首批接口从API version 6开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


媒体子系统为开发者提供一套简单且易于理解的接口，使得开发者能够方便接入系统并使用系统的媒体资源。

媒体子系统包含了音视频相关媒体业务，提供以下常用功能：

- 音频播放（[AudioPlayer](#audioplayer)）
- 视频播放（[VideoPlayer](#videoplayer8)）
- 音频录制（[AudioRecorder](#audiorecorder)）

后续将提供以下功能：DataSource音视频播放、音视频编解码、容器封装解封装、媒体能力查询等功能。

## 导入模块

```js
import media from '@ohos.multimedia.media';
```

##  media.createAudioPlayer

createAudioPlayer(): [AudioPlayer](#audioplayer)

同步方式创建音频播放实例。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**返回值：**

| 类型                        | 说明                                                         |
| --------------------------- | ------------------------------------------------------------ |
| [AudioPlayer](#audioplayer) | 返回AudioPlayer类实例，失败时返回null。可用于音频播放、暂停、停止等操作。 |

**示例：**

```js
let audioPlayer = media.createAudioPlayer();
```

## media.createVideoPlayer<sup>8+</sup>

createVideoPlayer(callback: AsyncCallback\<[VideoPlayer](#videoplayer8)>): void

异步方式创建视频播放实例，通过注册回调函数获取返回值。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型                                        | 必填 | 说明                           |
| -------- | ------------------------------------------- | ---- | ------------------------------ |
| callback | AsyncCallback<[VideoPlayer](#videoplayer8)> | 是   | 异步创建视频播放实例回调方法。 |

**示例：**

```js
let videoPlayer

media.createVideoPlayer((error, video) => {
   if (video != null) {
       videoPlayer = video;
       console.info('video createVideoPlayer success');
   } else {
       console.info(`video createVideoPlayer fail, error:${error.message}`);
   }
});
```

## media.createVideoPlayer<sup>8+</sup>

createVideoPlayer(): Promise<[VideoPlayer](#videoplayer8)>

异步方式创建视频播放实例，通过Promise获取返回值。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**返回值：**

| 类型                                  | 说明                                |
| ------------------------------------- | ----------------------------------- |
| Promise<[VideoPlayer](#videoplayer8)> | 异步创建视频播放实例Promise返回值。 |

**示例：**

```js
let videoPlayer

media.createVideoPlayer().then((video) => {
   if (video != null) {
       videoPlayer = video;
       console.info('video createVideoPlayer success');
   } else {
       console.info('video createVideoPlayer fail');
   }
}).catch((error) => {
   console.info(`video catchCallback, error:${error.message}`);
});
```

## media.createAudioRecorder

createAudioRecorder(): AudioRecorder

创建音频录制的实例来控制音频的录制。
一台设备只允许创建一个录制实例。

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

**返回值:**

| 类型                            | 说明                                      |
| ------------------------------- | ----------------------------------------- |
| [AudioRecorder](#audiorecorder) | 返回AudioRecorder类实例，失败时返回null。 |

**示例：**

```js
let audioRecorder = media.createAudioRecorder();
```




## MediaErrorCode<sup>8+</sup>

媒体服务错误类型枚举。

**系统能力：** 以下各项对应的系统能力均为 SystemCapability.Multimedia.Media.Core。

| 名称                       | 值   | 说明                                   |
| -------------------------- | ---- | -------------------------------------- |
| MSERR_OK                   | 0    | 表示操作成功。                         |
| MSERR_NO_MEMORY            | 1    | 表示申请内存失败，系统可能无可用内存。 |
| MSERR_OPERATION_NOT_PERMIT | 2    | 表示无权限执行此操作。                 |
| MSERR_INVALID_VAL          | 3    | 表示传入入参无效。                     |
| MSERR_IO                   | 4    | 表示发生IO错误。                       |
| MSERR_TIMEOUT              | 5    | 表示操作超时。                         |
| MSERR_UNKNOWN              | 6    | 表示未知错误。                         |
| MSERR_SERVICE_DIED         | 7    | 表示服务端失效。                       |
| MSERR_INVALID_STATE        | 8    | 表示在当前状态下，不允许执行此操作。   |
| MSERR_UNSUPPORTED          | 9    | 表示在当前版本下，不支持此操作。       |

## MediaType<sup>8+</sup>

媒体类型枚举。

**系统能力：** 以下各项对应的系统能力均为 SystemCapability.Multimedia.Media.Core。

| 名称           | 值   | 说明       |
| -------------- | ---- | ---------- |
| MEDIA_TYPE_AUD | 0    | 表示音频。 |
| MEDIA_TYPE_VID | 1    | 表示视频。 |

## CodecMimeType<sup>8+</sup>

Codec MIME类型枚举。

**系统能力：** 以下各项对应的系统能力均为 SystemCapability.Multimedia.Media.Core。

| 名称         | 值                    | 说明                     |
| ------------ | --------------------- | ------------------------ |
| VIDEO_H263   | 'video/h263'          | 表示视频/h263类型。      |
| VIDEO_AVC    | 'video/avc'           | 表示视频/avc类型。       |
| VIDEO_MPEG2  | 'video/mpeg2'         | 表示视频/mpeg2类型。     |
| VIDEO_MPEG4  | 'video/mp4v-es'       | 表示视频/mpeg4类型。     |
| VIDEO_VP8    | 'video/x-vnd.on2.vp8' | 表示视频/vp8类型。       |
| AUDIO_AAC    | "audio/mp4a-latm"     | 表示音频/mp4a-latm类型。 |
| AUDIO_VORBIS | 'audio/vorbis'        | 表示音频/vorbis类型。    |
| AUDIO_FLAC   | 'audio/flac'          | 表示音频/flac类型。      |

## MediaDescriptionKey<sup>8+</sup>

媒体信息描述枚举。

**系统能力：** 以下各项对应的系统能力均为 SystemCapability.Multimedia.Media.Core。

| 名称                     | 值              | 说明                                                         |
| ------------------------ | --------------- | ------------------------------------------------------------ |
| MD_KEY_TRACK_INDEX       | "track_index"   | 表示轨道序号，其对应键值类型为number。                       |
| MD_KEY_TRACK_TYPE        | "track_type"    | 表示轨道类型，其对应键值类型为number，参考[MediaType](#mediatype8)。 |
| MD_KEY_CODEC_MIME        | "codec_mime"    | 表示codec_mime类型，其对应键值类型为string。                 |
| MD_KEY_DURATION          | "duration"      | 表示媒体时长，其对应键值类型为number，单位为毫秒（ms）。     |
| MD_KEY_BITRATE           | "bitrate"       | 表示比特率，其对应键值类型为number，单位为比特率（bps）。    |
| MD_KEY_WIDTH             | "width"         | 表示视频宽度，其对应键值类型为number，单位为像素（px）。     |
| MD_KEY_HEIGHT            | "height"        | 表示视频高度，其对应键值类型为number，单位为像素（px）。     |
| MD_KEY_FRAME_RATE        | "frame_rate"    | 表示视频帧率，其对应键值类型为number，单位为100帧每秒（100fps）。 |
| MD_KEY_AUD_CHANNEL_COUNT | "channel_count" | 表示声道数，其对应键值类型为number。                         |
| MD_KEY_AUD_SAMPLE_RATE   | "sample_rate"   | 表示采样率，其对应键值类型为number，单位为赫兹（Hz）。       |

## BufferingInfoType<sup>8+</sup>

缓存事件类型枚举。

**系统能力：** 以下各项对应的系统能力均为 SystemCapability.Multimedia.Media.Core。

| 名称              | 值   | 说明                             |
| ----------------- | ---- | -------------------------------- |
| BUFFERING_START   | 1    | 表示开始缓存。                   |
| BUFFERING_END     | 2    | 表示结束缓存。                   |
| BUFFERING_PERCENT | 3    | 表示缓存百分比。                 |
| CACHED_DURATION   | 4    | 表示缓存时长，单位为毫秒（ms）。 |

## AudioPlayer

音频播放管理类，用于管理和播放音频媒体。在调用AudioPlayer的方法前，需要先通过[createAudioPlayer()](#mediacreateaudioplayer)构建一个[AudioPlayer](#audioplayer)实例。

音频播放demo可参考：[音频播放开发指导](../../media/audio-playback.md)

### 属性<a name=audioplayer_属性></a>

**系统能力：** 以下各项对应的系统能力均为 SystemCapability.Multimedia.Media.AudioPlayer。

| 名称        | 类型                      | 可读 | 可写 | 说明                                                         |
| ----------- | ------------------------- | ---- | ---- | ------------------------------------------------------------ |
| src         | string                    | 是   | 是   | 音频媒体URI，支持当前主流的视频格式(mp4、mpeg-ts、webm、mkv)。<br>**支持路径示例**：<br>1. fd类型播放：fd://xx<br>![](figures/zh-cn_image_url.png)<br>2. http网络播放: http://xx<br/>3. https网络播放: https://xx<br/>4. hls网络播放路径：http://xx或者https://xx<br/>**注意事项**：<br>使用媒体素材需要获取读权限，否则无法正常播放。|
| loop        | boolean                   | 是   | 是   | 音频循环播放属性，设置为'true'表示循环播放。                 |
| currentTime | number                    | 是   | 否   | 音频的当前播放位置。                                         |
| duration    | number                    | 是   | 否   | 音频时长。                                                   |
| state       | [AudioState](#audiostate) | 是   | 否   | 音频播放的状态。                                             |

### play<a name=audioplayer_play></a>

play(): void

开始播放音频资源，需在[dataLoad](#audioplayer_on)事件成功触发后，才能调用。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**示例：**

```js
audioPlayer.on('play', () => {    //设置'play'事件回调
    console.log('audio play success');
});
audioPlayer.play();
```

### pause<a name=audioplayer_pause></a>

pause(): void

暂停播放音频资源。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**示例：**

```js
audioPlayer.on('pause', () => {    //设置'pause'事件回调
    console.log('audio pause success');
});
audioPlayer.pause();
```

### stop<a name=audioplayer_stop></a>

stop(): void

停止播放音频资源。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**示例：**

```js
audioPlayer.on('stop', () => {    //设置'stop'事件回调
    console.log('audio stop success');
});
audioPlayer.stop();
```

### reset<sup>7+</sup><a name=audioplayer_reset></a>

reset(): void

切换播放音频资源。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**示例：**

```js
audioPlayer.on('reset', () => {    //设置'reset'事件回调
    console.log('audio reset success');
});
audioPlayer.reset();
```

### seek<a name=audioplayer_seek></a>

seek(timeMs: number): void

跳转到指定播放位置。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                 |
| ------ | ------ | ---- | ------------------------------------ |
| timeMs | number | 是   | 指定的跳转时间节点，单位毫秒（ms）。 |

**示例：**

```js
audioPlayer.on('timeUpdate', (seekDoneTime) => {    //设置'timeUpdate'事件回调
    if (seekDoneTime == null) {
        console.info('audio seek fail');
        return;
    }
    console.log('audio seek success. seekDoneTime: ' + seekDoneTime);
});
audioPlayer.seek(30000);    //seek到30000ms的位置
```

### setVolume<a name=audioplayer_setvolume></a>

setVolume(vol: number): void

设置音量。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| vol    | number | 是   | 指定的相对音量大小，取值范围为[0.00-1.00]，1表示最大音量，即100%。 |

**示例：**

```js
audioPlayer.on('volumeChange', () => {    //设置'volumeChange'事件回调
    console.log('audio volumeChange success');
});
audioPlayer.setVolume(1);    //设置音量到100%
```

### release<a name=audioplayer_release></a>

release(): void

释放音频资源。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**示例：**

```js
audioPlayer.release();
audioPlayer = undefined;
```

### getTrackDescription<sup>8+</sup><a name=audioplayer_gettrackdescription1></a>

getTrackDescription(callback: AsyncCallback<Array\<MediaDescription>>): void

通过回调方式获取音频轨道信息。需在[dataLoad](#audioplayer_on)事件成功触发后，才能调用。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                       |
| -------- | ------------------------------------------------------------ | ---- | -------------------------- |
| callback | AsyncCallback<Array<[MediaDescription](#mediadescription8)>> | 是   | 获取音频轨道信息回调方法。 |

**示例：**

```js
function printfDescription(obj) {
    for (let item in obj) {
        let property = obj[item];
        console.info('audio key is ' + item);
        console.info('audio value is ' + property);
    }
}

audioPlayer.getTrackDescription((error, arrlist) => {
    if (arrlist != null) {
        for (let i = 0; i < arrlist.length; i++) {
            printfDescription(arrlist[i]);
        }
    } else {
        console.log(`audio getTrackDescription fail, error:${error.message}`);
    }
});
```

### getTrackDescription<sup>8+</sup><a name=audioplayer_gettrackdescription2></a>

getTrackDescription(): Promise<Array\<MediaDescription>>

通过Promise方式获取音频轨道信息。需在[dataLoad](#audioplayer_on)事件成功触发后，才能调用

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**返回值：**

| 类型                                                   | 说明                            |
| ------------------------------------------------------ | ------------------------------- |
| Promise<Array<[MediaDescription](#mediadescription8)>> | 获取音频轨道信息Promise返回值。 |

**示例：**

```js
function printfDescription(obj) {
    for (let item in obj) {
        let property = obj[item];
        console.info('audio key is ' + item);
        console.info('audio value is ' + property);
    }
}

audioPlayer.getTrackDescription().then((arrlist) => {
    if (arrlist != null) {
        arrayDescription = arrlist;
    } else {
        console.log('audio getTrackDescription fail');
    }
}).catch((error) => {
   console.info(`audio catchCallback, error:${error.message}`);
});

for (let i = 0; i < arrayDescription.length; i++) {
    printfDescription(arrayDescription[i]);
}
```

### on('bufferingUpdate')<sup>8+</sup>

on(type: 'bufferingUpdate', callback: (infoType: [BufferingInfoType](#bufferinginfotype8), value: number) => void): void

开始订阅音频缓存更新事件。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   | 音频缓存事件回调类型，支持的事件：'bufferingUpdate'。        |
| callback | function | 是   | 音频缓存事件回调方法。<br>[BufferingInfoType](#bufferinginfotype8)为BUFFERING_PERCENT或CACHED_DURATION时，value值有效，否则固定为0。 |

**示例：**

```js
audioPlayer.on('bufferingUpdate', (infoType, value) => {
    console.log('audio bufferingInfo type: ' + infoType);
    console.log('audio bufferingInfo value: ' + value);
});
```

 ### on('play' | 'pause' | 'stop' | 'reset' | 'dataLoad' | 'finish' | 'volumeChange')<a name = audioplayer_on></a>

on(type: 'play' | 'pause' | 'stop' | 'reset' | 'dataLoad' | 'finish' | 'volumeChange', callback: () => void): void

开始订阅音频播放事件。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**参数：**

| 参数名   | 类型       | 必填 | 说明                                                         |
| -------- | ---------- | ---- | ------------------------------------------------------------ |
| type     | string     | 是   | 播放事件回调类型，支持的事件包括：'play' \| 'pause' \| 'stop' \| 'reset' \| 'dataLoad' \| 'finish' \| 'volumeChange'。<br>- 'play'：完成[play()](#audioplayer_play)调用，音频开始播放，触发该事件。<br>- 'pause'：完成[pause()](#audioplayer_pause)调用，音频暂停播放，触发该事件。<br>- 'stop'：完成[stop()](#audioplayer_stop)调用，音频停止播放，触发该事件。<br>- 'reset'：完成[reset()](#audioplayer_reset)调用，播放器重置，触发该事件。<br>- 'dataLoad'：完成音频数据加载后触发该事件，即src属性设置完成后触发该事件。<br>- 'finish'：完成音频播放后触发该事件。<br>- 'volumeChange'：完成[setVolume()](#audioplayer_setvolume)调用，播放音量改变后触发该事件。 |
| callback | () => void | 是   | 播放事件回调方法。                                           |

**示例：**

```js
let audioPlayer = media.createAudioPlayer();  //创建一个音频播放实例
audioPlayer.on('dataLoad', () => {            //设置'dataLoad'事件回调，src属性设置成功后，触发此回调
    console.info('audio set source success');
    audioPlayer.play();                       //开始播放，并触发'play'事件回调
});
audioPlayer.on('play', () => {                //设置'play'事件回调
    console.info('audio play success');
    audioPlayer.seek(30000);                  //调用seek方法，并触发'timeUpdate'事件回调
});
audioPlayer.on('pause', () => {               //设置'pause'事件回调
    console.info('audio pause success');
    audioPlayer.stop();                       //停止播放，并触发'stop'事件回调
});
audioPlayer.on('reset', () => {               //设置'reset'事件回调
    console.info('audio reset success');
    audioPlayer.release();                    //释放播放实例资源
    audioPlayer = undefined;
});
audioPlayer.on('timeUpdate', (seekDoneTime) => {  //设置'timeUpdate'事件回调
    if (seekDoneTime == null) {
        console.info('audio seek fail');
        return;
    }
    console.info('audio seek success, and seek time is ' + seekDoneTime);
    audioPlayer.setVolume(0.5);                //设置音量为50%，并触发'volumeChange'事件回调
});
audioPlayer.on('volumeChange', () => {         //设置'volumeChange'事件回调
    console.info('audio volumeChange success');
    audioPlayer.pause();                       //暂停播放，并触发'pause'事件回调
});
audioPlayer.on('finish', () => {               //设置'finish'事件回调
    console.info('audio play finish');
    audioPlayer.stop();                        //停止播放，并触发'stop'事件回调
});
audioPlayer.on('error', (error) => {           //设置'error'事件回调
    console.info(`audio error called, errName is ${error.name}`);
    console.info(`audio error called, errCode is ${error.code}`);
    console.info(`audio error called, errMessage is ${error.message}`);
});

// 用户选择音频设置fd(本地播放)
let fdPath = 'fd://'
// path路径的码流可通过"hdc file send D:\xxx\01.mp3 /data/accounts/account_0/appdata" 命令，将其推送到设备上
let path = '/data/accounts/account_0/appdata/ohos.xxx.xxx.xxx/01.mp3';
fileIO.open(path).then(fdNumber) => {
   fdPath = fdPath + '' + fdNumber;
   console.info('open fd success fd is' + fdPath);
}, (err) => {
   console.info('open fd failed err is' + err);
}).catch((err) => {
   console.info('open fd failed err is' + err);
});
audioPlayer.src = fdPath;  //设置src属性，并触发'dataLoad'事件回调
```

### on('timeUpdate')

on(type: 'timeUpdate', callback: Callback\<number>): void

开始订阅音频播放[seek()](#seek)时间更新事件。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**参数：**

| 参数名   | 类型              | 必填 | 说明                                                         |
| -------- | ----------------- | ---- | ------------------------------------------------------------ |
| type     | string            | 是   | 播放事件回调类型，支持的事件包括：'timeUpdate'。<br>- 'timeUpdate'：[seek()](#audioplayer_seek)调用完成，触发该事件。 |
| callback | Callback\<number> | 是   | 播放事件回调方法。回调方法入参为成功seek的时间。             |

**示例：**

```js
audioPlayer.on('timeUpdate', (seekDoneTime) => {    //设置'timeUpdate'事件回调
    if (seekDoneTime == null) {
        console.info('audio seek fail');
        return;
    }
    console.log('audio seek success. seekDoneTime: ' + seekDoneTime);
});
audioPlayer.seek(30000);    //seek到30000ms的位置
```

### on('error')

on(type: 'error', callback: ErrorCallback): void

开始订阅音频播放错误事件。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**参数：**

| 参数名   | 类型          | 必填 | 说明                                                         |
| -------- | ------------- | ---- | ------------------------------------------------------------ |
| type     | string        | 是   | 播放错误事件回调类型，支持的事件包括：'error'。<br>- 'error'：音频播放中发生错误，触发该事件。 |
| callback | ErrorCallback | 是   | 播放错误事件回调方法。                                       |

**示例：**

```js
audioPlayer.on('error', (error) => {      //设置'error'事件回调
    console.info(`audio error called, errName is ${error.name}`);      //打印错误类型名称
    console.info(`audio error called, errCode is ${error.code}`);      //打印错误码
    console.info(`audio error called, errMessage is ${error.message}`);//打印错误类型详细描述
});
audioPlayer.setVolume(3);  //设置volume为无效值，触发'error'事件
```

## AudioState

音频播放的状态机。可通过state属性获取当前状态。

**系统能力：** 以下各项对应的系统能力均为 SystemCapability.Multimedia.Media.AudioPlayer。

| 名称               | 类型   | 描述           |
| ------------------ | ------ | -------------- |
| idle               | string | 音频播放空闲。 |
| playing            | string | 音频正在播放。 |
| paused             | string | 音频暂停播放。 |
| stopped            | string | 音频播放停止。 |
| error<sup>8+</sup> | string | 错误状态。     |

## VideoPlayer<sup>8+</sup>

视频播放管理类，用于管理和播放视频媒体。在调用VideoPlayer的方法前，需要先通过[createVideoPlayer()](#mediacreatevideoplayer8)构建一个[VideoPlayer](#videoplayer8)实例。

视频播放demo可参考：[视频播放开发指导](../../media/video-playback.md)

### 属性<a name=videoplayer_属性></a>

**系统能力：** 以下各项对应的系统能力均为 SystemCapability.Multimedia.Media.VideoPlayer。

| 名称                     | 类型                               | 可读 | 可写 | 说明                                                         |
| ------------------------ | ---------------------------------- | ---- | ---- | ------------------------------------------------------------ |
| url<sup>8+</sup>         | string                             | 是   | 是   | 视频媒体URL，支持当前主流的视频格式(mp4、mpeg-ts、webm、mkv)。<br>**支持路径示例**：<br>1. fd类型播放：fd://xx<br>![](figures/zh-cn_image_url.png)<br>2. http网络播放: http://xx<br/>3. https网络播放: https://xx<br/>4. hls网络播放路径：http://xx或者https://xx<br/>**注意事项**：<br>使用媒体素材需要获取读权限，否则无法正常播放。 |
| loop<sup>8+</sup>        | boolean                            | 是   | 是   | 视频循环播放属性，设置为'true'表示循环播放。                 |
| currentTime<sup>8+</sup> | number                             | 是   | 否   | 视频的当前播放位置。                                         |
| duration<sup>8+</sup>    | number                             | 是   | 否   | 视频时长，返回-1表示直播模式。                               |
| state<sup>8+</sup>       | [VideoPlayState](#videoplaystate8) | 是   | 否   | 视频播放的状态。                                             |
| width<sup>8+</sup>       | number                             | 是   | 否   | 视频宽。                                                     |
| height<sup>8+</sup>      | number                             | 是   | 否   | 视频高。                                                     |

### setDisplaySurface<sup>8+</sup>

setDisplaySurface(surfaceId: string, callback: AsyncCallback\<void>): void

通过回调方式设置SurfaceId。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名    | 类型     | 必填 | 说明                      |
| --------- | -------- | ---- | ------------------------- |
| surfaceId | string   | 是   | SurfaceId                 |
| callback  | function | 是   | 设置SurfaceId的回调方法。 |

**示例：**

```js
videoPlayer.setDisplaySurface(surfaceId, (err) => {
    if (err == null) {
        console.info('setDisplaySurface success!');
    } else {
        console.info('setDisplaySurface fail!');
    }
});
```

### setDisplaySurface<sup>8+</sup>

setDisplaySurface(surfaceId: string): Promise\<void>

通过Promise方式设置SurfaceId。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名    | 类型   | 必填 | 说明      |
| --------- | ------ | ---- | --------- |
| surfaceId | string | 是   | SurfaceId |

**返回值：**

| 类型           | 说明                           |
| -------------- | ------------------------------ |
| Promise\<void> | 设置SurfaceId的Promise返回值。 |

**示例：**

```js
videoPlayer.setDisplaySurface(surfaceId).then(() => {
    console.info('setDisplaySurface success');
}).catch((error) => {
   console.info(`video catchCallback, error:${error.message}`);
});
```

### prepare<sup>8+</sup>

prepare(callback: AsyncCallback\<void>): void

通过回调方式准备播放视频。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                     |
| -------- | -------- | ---- | ------------------------ |
| callback | function | 是   | 准备播放视频的回调方法。 |

**示例：**

```js
videoPlayer.prepare((err) => {
    if (err == null) {
        console.info('prepare success!');
    } else {
        console.info('prepare fail!');
    }
});
```

### prepare<sup>8+</sup>

prepare(): Promise\<void>

通过Promise方式准备播放视频。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | 准备播放视频的Promise返回值。 |

**示例：**

```js
videoPlayer.prepare().then(() => {
    console.info('prepare success');
}).catch((error) => {
   console.info(`video catchCallback, error:${error.message}`);
});
```

### play<sup>8+</sup>

play(callback: AsyncCallback\<void>): void;

通过回调方式开始播放视频。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                     |
| -------- | -------- | ---- | ------------------------ |
| callback | function | 是   | 开始播放视频的回调方法。 |

**示例：**

```js
videoPlayer.play((err) => {
    if (err == null) {
        console.info('play success!');
    } else {
        console.info('play fail!');
    }
});
```

### play<sup>8+</sup>

play(): Promise\<void>;

通过Promise方式开始播放视频。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | 开始播放视频的Promise返回值。 |

**示例：**

```js
videoPlayer.play().then(() => {
    console.info('play success');
}).catch((error) => {
   console.info(`video catchCallback, error:${error.message}`);
});
```

### pause<sup>8+</sup>

pause(callback: AsyncCallback\<void>): void

通过回调方式暂停播放视频。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                     |
| -------- | -------- | ---- | ------------------------ |
| callback | function | 是   | 暂停播放视频的回调方法。 |

**示例：**

```js
videoPlayer.pause((err) => {
    if (err == null) {
        console.info('pause success!');
    } else {
        console.info('pause fail!');
    }
});
```

### pause<sup>8+</sup>

pause(): Promise\<void>

通过Promise方式暂停播放视频。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | 暂停播放视频的Promise返回值。 |

**示例：**

```js
videoPlayer.pause().then(() => {
    console.info('pause success');
}).catch((error) => {
   console.info(`video catchCallback, error:${error.message}`);
});
```

### stop<sup>8+</sup>

stop(callback: AsyncCallback\<void>): void

通过回调方式停止播放视频。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                     |
| -------- | -------- | ---- | ------------------------ |
| callback | function | 是   | 停止播放视频的回调方法。 |

**示例：**

```js
videoPlayer.stop((err) => {
    if (err == null) {
        console.info('stop success!');
    } else {
        console.info('stop fail!');
    }
});
```

### stop<sup>8+</sup>

stop(): Promise\<void>

通过Promise方式停止播放视频。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | 停止播放视频的Promise返回值。 |

**示例：**

```js
videoPlayer.stop().then(() => {
    console.info('stop success');
}).catch((error) => {
   console.info(`video catchCallback, error:${error.message}`);
});
```

### reset<sup>8+</sup>

reset(callback: AsyncCallback\<void>): void

通过回调方式切换播放视频。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                     |
| -------- | -------- | ---- | ------------------------ |
| callback | function | 是   | 切换播放视频的回调方法。 |

**示例：**

```js
videoPlayer.reset((err) => {
    if (err == null) {
        console.info('reset success!');
    } else {
        console.info('reset fail!');
    }
});
```

### reset<sup>8+</sup>

reset(): Promise\<void>

通过Promise方式切换播放视频。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | 切换播放视频的Promise返回值。 |

**示例：**

```js
videoPlayer.reset().then(() => {
    console.info('reset success');
}).catch((error) => {
   console.info(`video catchCallback, error:${error.message}`);
});
```

### seek<sup>8+</sup>

seek(timeMs: number, callback: AsyncCallback\<number>): void

通过回调方式跳转到指定播放位置，默认跳转到指定时间点的下一个关键帧。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                 |
| -------- | -------- | ---- | ------------------------------------ |
| timeMs   | number   | 是   | 指定的跳转时间节点，单位毫秒（ms）。 |
| callback | function | 是   | 跳转到指定播放位置的回调方法。       |

**示例：**

```js
videoPlayer.seek((seekTime, err) => {
    if (err == null) {
        console.info('seek success!');
    } else {
        console.info('seek fail!');
    }
});
```

### seek<sup>8+</sup>

seek(timeMs: number, mode:SeekMode, callback: AsyncCallback\<number>): void

通过回调方式跳转到指定播放位置。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型                   | 必填 | 说明                                 |
| -------- | ---------------------- | ---- | ------------------------------------ |
| timeMs   | number                 | 是   | 指定的跳转时间节点，单位毫秒（ms）。 |
| mode     | [SeekMode](#seekmode8) | 是   | 跳转模式。                           |
| callback | function               | 是   | 跳转到指定播放位置的回调方法。       |

**示例：**

```js
videoPlayer.seek((seekTime, seekMode, err) => {
    if (err == null) {
        console.info('seek success!');
    } else {
        console.info('seek fail!');
    }
});
```

### seek<sup>8+</sup>

seek(timeMs: number, mode?:SeekMode): Promise\<number>

通过Promise方式跳转到指定播放位置，如果没有设置mode则跳转到指定时间点的下一个关键帧。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名 | 类型                   | 必填 | 说明                                 |
| ------ | ---------------------- | ---- | ------------------------------------ |
| timeMs | number                 | 是   | 指定的跳转时间节点，单位毫秒（ms）。 |
| mode   | [SeekMode](#seekmode8) | 否   | 跳转模式。                           |

**返回值：**

| 类型           | 说明                                |
| -------------- | ----------------------------------- |
| Promise\<void> | 跳转到指定播放位置的Promise返回值。 |

**示例：**

```js
videoPlayer.seek(seekTime).then((seekDoneTime) => { // seekDoneTime表示seek完成后的时间点
    console.info('seek success');
}).catch((error) => {
   console.info(`video catchCallback, error:${error.message}`);
});

videoPlayer.seek(seekTime, seekMode).then((seekDoneTime) => {
    console.info('seek success');
}).catch((error) => {
   console.info(`video catchCallback, error:${error.message}`);
});
```

### setVolume<sup>8+</sup>

setVolume(vol: number, callback: AsyncCallback\<void>): void

通过回调方式设置音量。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| vol      | number   | 是   | 指定的相对音量大小，取值范围为[0.00-1.00]，1表示最大音量，即100%。 |
| callback | function | 是   | 设置音量的回调方法。                                         |

**示例：**

```js
videoPlayer.setVolume((vol, err) => {
    if (err == null) {
        console.info('setVolume success!');
    } else {
        console.info('setVolume fail!');
    }
});
```

### setVolume<sup>8+</sup>

setVolume(vol: number): Promise\<void>

通过Promise方式设置音量。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| vol    | number | 是   | 指定的相对音量大小，取值范围为[0.00-1.00]，1表示最大音量，即100%。 |

**返回值：**

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | 设置音量的Promise返回值。 |

**示例：**

```js
videoPlayer.setVolume(vol).then() => {
    console.info('setVolume success');
}).catch((error) => {
   console.info(`video catchCallback, error:${error.message}`);
});
```

### release<sup>8+</sup>

release(callback: AsyncCallback\<void>): void

通过回调方式释放视频资源。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                     |
| -------- | -------- | ---- | ------------------------ |
| callback | function | 是   | 释放视频资源的回调方法。 |

**示例：**

```js
videoPlayer.release((err) => {
    if (err == null) {
        console.info('release success!');
    } else {
        console.info('release fail!');
    }
});
```

### release<sup>8+</sup>

release(): Promise\<void>

通过Promise方式释放视频资源。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | 释放视频资源的Promise返回值。 |

**示例：**

```js
videoPlayer.release().then() => {
    console.info('release success');
}).catch((error) => {
   console.info(`video catchCallback, error:${error.message}`);
});
```

### getTrackDescription<sup>8+</sup>

getTrackDescription(callback: AsyncCallback<Array\<MediaDescription>>): void

通过回调方式获取视频轨道信息。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                       |
| -------- | ------------------------------------------------------------ | ---- | -------------------------- |
| callback | AsyncCallback<Array<[MediaDescription](#mediadescription8)>> | 是   | 获取视频轨道信息回调方法。 |

**示例：**

```js
function printfDescription(obj) {
    for (let item in obj) {
        let property = obj[item];
        console.info('video key is ' + item);
        console.info('video value is ' + property);
    }
}

videoPlayer.getTrackDescription((error, arrlist) => {
    if (arrlist != null) {
        for (let i = 0; i < arrlist.length; i++) {
            printfDescription(arrlist[i]);
        }
    } else {
        console.log(`video getTrackDescription fail, error:${error.message}`);
    }
});
```

### getTrackDescription<sup>8+</sup>

getTrackDescription(): Promise<Array\<MediaDescription>>

通过Promise方式获取视频轨道信息。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**返回值：**

| 类型                                                   | 说明                            |
| ------------------------------------------------------ | ------------------------------- |
| Promise<Array<[MediaDescription](#mediadescription8)>> | 获取视频轨道信息Promise返回值。 |

**示例：**

```js
function printfDescription(obj) {
    for (let item in obj) {
        let property = obj[item];
        console.info('video key is ' + item);
        console.info('video value is ' + property);
    }
}

let arrayDescription;
videoPlayer.getTrackDescription().then((arrlist) => {
    if (arrlist != null) {
        arrayDescription = arrlist;
    } else {
        console.log('video getTrackDescription fail');
    }
}).catch((error) => {
   console.info(`video catchCallback, error:${error.message}`);
});
for (let i = 0; i < arrayDescription.length; i++) {
    printfDescription(arrayDescription[i]);
}
```

### setSpeed<sup>8+</sup>

setSpeed(speed:number, callback: AsyncCallback\<number>): void

通过回调方式设置播放速度。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                       |
| -------- | -------- | ---- | ---------------------------------------------------------- |
| speed    | number   | 是   | 指定播放视频速度，具体见[PlaybackSpeed](#playbackspeed8)。 |
| callback | function | 是   | 设置播放速度的回调方法。                                   |

**示例：**

```js
videoPlayer.setSpeed((speed:number, err) => {
    if (err == null) {
        console.info('setSpeed success!');
    } else {
        console.info('setSpeed fail!');
    }
});
```

### setSpeed<sup>8+</sup>

setSpeed(speed:number): Promise\<number>

通过Promise方式设置播放速度。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                       |
| ------ | ------ | ---- | ---------------------------------------------------------- |
| speed  | number | 是   | 指定播放视频速度，具体见[PlaybackSpeed](#playbackspeed8)。 |

**返回值：**

| 类型             | 说明                      |
| ---------------- | ------------------------- |
| Promise\<number> | 通过Promise获取设置结果。 |

**示例：**

```js
videoPlayer.setSpeed(speed).then() => {
    console.info('setSpeed success');
}).catch((error) => {
   console.info(`video catchCallback, error:${error.message}`);
});
```

### on('playbackCompleted')<sup>8+</sup>

on(type: 'playbackCompleted', callback: Callback\<void>): void

开始监听视频播放完成事件。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                        |
| -------- | -------- | ---- | ----------------------------------------------------------- |
| type     | string   | 是   | 视频播放完成事件回调类型，支持的事件：'playbackCompleted'。 |
| callback | function | 是   | 视频播放完成事件回调方法。                                  |

**示例：**

```js
videoPlayer.on('playbackCompleted', () => {
    console.info('playbackCompleted success!');
});
```

### on('bufferingUpdate')<sup>8+</sup>

on(type: 'bufferingUpdate', callback: (infoType: BufferingInfoType, value: number) => void): void

开始监听视频缓存更新事件。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   | 视频缓存事件回调类型，支持的事件：'bufferingUpdate'。        |
| callback | function | 是   | 视频缓存事件回调方法。<br>[BufferingInfoType](#bufferinginfotype8)为BUFFERING_PERCENT或CACHED_DURATION时，value值有效，否则固定为0。 |

**示例：**

```js
videoPlayer.on('bufferingUpdate', (infoType, value) => {
    console.log('video bufferingInfo type: ' + infoType);
    console.log('video bufferingInfo value: ' + value);
});
```

### on('startRenderFrame')<sup>8+</sup>

on(type: 'startRenderFrame', callback: Callback\<void>): void

开始监听视频播放首帧送显上报事件。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型            | 必填 | 说明                                                         |
| -------- | --------------- | ---- | ------------------------------------------------------------ |
| type     | string          | 是   | 视频播放首帧送显上报事件回调类型，支持的事件：'startRenderFrame'。 |
| callback | Callback\<void> | 是   | 视频播放首帧送显上报事件回调方法。                           |

**示例：**

```js
videoPlayer.on('startRenderFrame', () => {
    console.info('startRenderFrame success!');
});
```

### on('videoSizeChanged')<sup>8+</sup>

on(type: 'videoSizeChanged', callback: (width: number, height: number) => void): void

开始监听视频播放宽高变化事件。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   | 视频播放宽高变化事件回调类型，支持的事件：'videoSizeChanged'。 |
| callback | function | 是   | 视频播放宽高变化事件回调方法，width表示宽，height表示高。    |

**示例：**

```js
videoPlayer.on('videoSizeChanged', (width, height) => {
    console.log('video width is: ' + width);
    console.log('video height is: ' + height);
});
```

### on('error')<sup>8+</sup>

on(type: 'error', callback: ErrorCallback): void

开始监听视频播放错误事件。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型          | 必填 | 说明                                                         |
| -------- | ------------- | ---- | ------------------------------------------------------------ |
| type     | string        | 是   | 播放错误事件回调类型，支持的事件包括：'error'。<br>- 'error'：视频播放中发生错误，触发该事件。 |
| callback | ErrorCallback | 是   | 播放错误事件回调方法。                                       |

**示例：**

```js
videoPlayer.on('error', (error) => {      // 设置'error'事件回调
    console.info(`video error called, errName is ${error.name}`);      // 打印错误类型名称
    console.info(`video error called, errCode is ${error.code}`);      // 打印错误码
    console.info(`video error called, errMessage is ${error.message}`);// 打印错误类型详细描述
});
videoPlayer.setVolume(3);  //设置volume为无效值，触发'error'事件
```

## VideoPlayState<sup>8+</sup>

视频播放的状态机，可通过state属性获取当前状态。

**系统能力：** 以下各项对应的系统能力均为 SystemCapability.Multimedia.Media.VideoPlayer。

| 名称     | 类型   | 描述           |
| -------- | ------ | -------------- |
| idle     | string | 视频播放空闲。 |
| prepared | string | 视频播放准备。 |
| playing  | string | 视频正在播放。 |
| paused   | string | 视频暂停播放。 |
| stopped  | string | 视频播放停止。 |
| error    | string | 错误状态。     |

## SeekMode<sup>8+</sup>

视频播放的Seek模式枚举，可通过seek方法作为参数传递下去。

**系统能力：** 以下各项对应的系统能力均为 SystemCapability.Multimedia.Media.Core。

| 名称           | 值   | 描述                                                         |
| -------------- | ---- | ------------------------------------------------------------ |
| SEEK_NEXT_SYNC | 0    | 表示跳转到指定时间点的下一个关键帧，建议向后快进的时候用这个枚举值。 |
| SEEK_PREV_SYNC | 1    | 表示跳转到指定时间点的上一个关键帧，建议向前快进的时候用这个枚举值。 |

## PlaybackSpeed<sup>8+</sup>

视频播放的倍速枚举，可通过setSpeed方法作为参数传递下去。

**系统能力：** 以下各项对应的系统能力均为 SystemCapability.Multimedia.Media.VideoPlayer。

| 名称                 | 值   | 描述                           |
| -------------------- | ---- | ------------------------------ |
| SPEED_FORWARD_0_75_X | 0    | 表示视频播放正常播速的0.75倍。 |
| SPEED_FORWARD_1_00_X | 1    | 表示视频播放正常播速。         |
| SPEED_FORWARD_1_25_X | 2    | 表示视频播放正常播速的1.25倍。 |
| SPEED_FORWARD_1_75_X | 3    | 表示视频播放正常播速的1.75倍。 |
| SPEED_FORWARD_2_00_X | 4    | 表示视频播放正常播速的2.00倍。 |

## MediaDescription<sup>8+</sup>

### [key : string] : Object

通过key-value方式获取媒体信息。

**系统能力：** 以下各项对应的系统能力均为 SystemCapability.Multimedia.Media.Core。

| 名称  | 类型   | 说明                                                         |
| ----- | ------ | ------------------------------------------------------------ |
| key   | string | 通过key值获取对应的value。key值具体可见[MediaDescriptionKey](#mediadescriptionkey8)。 |
| value | any    | 对应key值得value。其类型可为任意类型，具体key对应value的类型可参考[MediaDescriptionKey](#mediadescriptionkey8)的描述信息。 |

**示例：**

```js
function printfItemDescription(obj, key) {
    let property = obj[key];
    console.info('audio key is ' + key);
    console.info('audio value is ' + property);
}

audioPlayer.getTrackDescription((error, arrlist) => {
    if (arrlist != null) {
        for (let i = 0; i < arrlist.length; i++) {
            printfItemDescription(arrlist[i], MD_KEY_TRACK_TYPE);  //打印出每条轨道MD_KEY_TRACK_TYPE的值
        }
    } else {
        console.log(`audio getTrackDescription fail, error:${error.message}`);
    }
});
```

## AudioRecorder

音频录制管理类，用于录制音频媒体。在调用AudioRecorder的方法前，需要先通过[createAudioRecorder()](#mediacreateaudiorecorder) 构建一个[AudioRecorder](#audiorecorder)实例。

音频录制demo可参考：[音频录制开发指导](../../media/audio-recorder.md)

### prepare<a name=audiorecorder_prepare></a>

prepare(config: AudioRecorderConfig): void

录音准备。

**需要权限：** ohos.permission.MICROPHONE

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

**参数：**

| 参数名 | 类型                                        | 必填 | 说明                                                         |
| ------ | ------------------------------------------- | ---- | ------------------------------------------------------------ |
| config | [AudioRecorderConfig](#audiorecorderconfig) | 是   | 配置录音的相关参数，包括音频输出URI、编码格式、采样率、声道数、输出格式等。 |

**示例：**

```js
let audioRecorderConfig = {
    audioEncoder : media.AudioEncoder.AAC_LC,
    audioEncodeBitRate : 22050,
    audioSampleRate : 22050,
    numberOfChannels : 2,
    format : media.AudioOutputFormat.AAC_ADTS,
    uri : 'fd://1',       // 文件需先由调用者创建，并给予适当的权限
    location : { latitude : 30, longitude : 130},
}
audioRecorder.on('prepare', () => {    //设置'prepare'事件回调
    console.log('prepare success');
});
audioRecorder.prepare(audioRecorderConfig);
```


### start<a name=audiorecorder_start></a>

start(): void

开始录制，需在[prepare](#audiorecorder_on)事件成功触发后，才能调用start方法。

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

**示例：**

```js
audioRecorder.on('start', () => {    //设置'start'事件回调
    console.log('audio recorder start success');
});
audioRecorder.start();
```

### pause<a name=audiorecorder_pause></a>

pause():void

暂停录制，需要在[start](#audiorecorder_on)事件成功触发后，才能调用pause方法。

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

**示例：**

```js
audioRecorder.on('pause', () => {    //设置'pause'事件回调
    console.log('audio recorder pause success');
});
audioRecorder.pause();
```

### resume<a name=audiorecorder_resume></a>

resume():void

恢复录制，需要在[pause](#audiorecorder_on)事件成功触发后，才能调用resume方法。

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

**示例：**

```js
audioRecorder.on('resume', () => {    //设置'resume'事件回调
    console.log('audio recorder resume success');
});
audioRecorder.resume();
```

### stop<a name=audiorecorder_stop></a>

stop(): void

停止录音。

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

**示例：**

```js
audioRecorder.on('stop', () => {    //设置'stop'事件回调
    console.log('audio recorder stop success');
});
audioRecorder.stop();
```

### release<a name=audiorecorder_release></a>

release(): void

释放录音资源。

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

**示例：**

```js
audioRecorder.on('release', () => {    //设置'release'事件回调
    console.log('audio recorder release success');
});
audioRecorder.release();
audioRecorder = undefined;
```

### reset<a name=audiorecorder_reset></a>

reset(): void

重置录音。

进行重置录音之前，需要先调用[stop()](#audiorecorder_stop)停止录音。重置录音之后，需要调用[prepare()](#audiorecorder_prepare)设置录音参数项，才能再次进行录音。

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

**示例：**

```js
audioRecorder.on('reset', () => {    //设置'reset'事件回调
    console.log('audio recorder reset success');
});
audioRecorder.reset();
```

### on('prepare' | 'start' | 'pause' | 'resume' | 'stop' | 'release' | 'reset')<a name=audiorecorder_on></a>

on(type: 'prepare' | 'start' | 'pause' | 'resume' | 'stop' | 'release' | 'reset', callback: () => void): void

开始订阅音频录制事件。

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   | 录制事件回调类型，支持的事件包括：'prepare'&nbsp;\|&nbsp;'start'&nbsp;\|  'pause' \| ’resume‘ \|&nbsp;'stop'&nbsp;\|&nbsp;'release'&nbsp;\|&nbsp;'reset'。<br/>-&nbsp;'prepare'&nbsp;：完成[prepare](#audiorecorder_prepare)调用，音频录制参数设置完成，触发该事件。<br/>-&nbsp;'start'&nbsp;：完成[start](#audiorecorder_start)调用，音频录制开始，触发该事件。<br/>-&nbsp;'pause': 完成[pause](#audiorecorder_pause)调用，音频暂停录制，触发该事件。<br/>-&nbsp;'resume': 完成[resume](#audiorecorder_resume)调用，音频恢复录制，触发该事件。<br/>-&nbsp;'stop'&nbsp;：完成[stop](#audiorecorder_stop)调用，音频停止录制，触发该事件。<br/>-&nbsp;'release'&nbsp;：完成[release](#audiorecorder_release)调用，音频释放录制资源，触发该事件。<br/>-&nbsp;'reset'：完成[reset](#audiorecorder_reset)调用，音频重置为初始状态，触发该事件。 |
| callback | ()=>void | 是   | 录制事件回调方法。                                           |

**示例：**

```js
let audiorecorder = media.createAudioRecorder();                                  // 创建一个音频录制实例
let audioRecorderConfig = {
    audioEncoder : media.AudioEncoder.AAC_LC, ,
    audioEncodeBitRate : 22050,
    audioSampleRate : 22050,
    numberOfChannels : 2,
    format : media.AudioOutputFormat.AAC_ADTS,
    uri : 'fd://xx',                                                            // 文件需先由调用者创建，并给予适当的权限
    location : { latitude : 30, longitude : 130},
}
audioRecorder.on('error', (error) => {                                             // 设置'error'事件回调
    console.info(`audio error called, errName is ${error.name}`);
    console.info(`audio error called, errCode is ${error.code}`);
    console.info(`audio error called, errMessage is ${error.message}`);
});
audioRecorder.on('prepare', () => {                                              // 设置'prepare'事件回调
    console.log('prepare success');
    audioRecorder.start();                                                       // 开始录制，并触发'start'事件回调
});
audioRecorder.on('start', () => {                                                 // 设置'start'事件回调
    console.log('audio recorder start success');
});
audioRecorder.on('pause', () => {                                                 // 设置'pause'事件回调
    console.log('audio recorder pause success');
});
audioRecorder.on('resume', () => {                                                 // 设置'resume'事件回调
    console.log('audio recorder resume success');
});
audioRecorder.on('stop', () => {                                                 // 设置'stop'事件回调
    console.log('audio recorder stop success');
});
audioRecorder.on('release', () => {                                                 // 设置'release'事件回调
    console.log('audio recorder release success');
});
audioRecorder.on('reset', () => {                                                 // 设置'reset'事件回调
    console.log('audio recorder reset success');
});
audioRecorder.prepare(audioRecorderConfig)                                       // 设置录制参数 ，并触发'prepare'事件回调
```

### on('error')

on(type: 'error', callback: ErrorCallback): void

开始订阅音频录制错误事件。

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

**参数：**

| 参数名   | 类型          | 必填 | 说明                                                         |
| -------- | ------------- | ---- | ------------------------------------------------------------ |
| type     | string        | 是   | 录制错误事件回调类型'error'。<br/>-&nbsp;'error'：音频录制过程中发生错误，触发该事件。 |
| callback | ErrorCallback | 是   | 录制错误事件回调方法。                                       |

**示例：**

```js
let audioRecorderConfig = {
    audioEncoder : media.AudioEncoder.AAC_LC,
    audioEncodeBitRate : 22050,
    audioSampleRate : 22050,
    numberOfChannels : 2,
    format : media.AudioOutputFormat.AAC_ADTS,
    uri : 'fd://xx',                                                     // 文件需先由调用者创建，并给予适当的权限
    location : { latitude : 30, longitude : 130},
}
audioRecorder.on('error', (error) => {                                  // 设置'error'事件回调
    console.info(`audio error called, error: ${error}`); 
});
audioRecorder.prepare(audioRecorderConfig);                            // prepare设置错误参数，触发'error'事件
```

## AudioRecorderConfig

表示音频的录音配置。

**系统能力：** 以下各项对应的系统能力均为 SystemCapability.Multimedia.Media.AudioRecorder。

| 名称                  | 参数类型                                | 必填 | 说明                                                         |
| --------------------- | --------------------------------------- | ---- | ------------------------------------------------------------ |
| audioEncoder<sup>(deprecated)</sup>          | [AudioEncoder](#audioencoder)           | 否   | 音频编码格式，默认设置为AAC_LC。<br/>**说明：** 从API Version 8 开始废弃，建议使用audioEncoderMime替代。                             |
| audioEncodeBitRate    | number                                  | 否   | 音频编码比特率，默认值为48000。                              |
| audioSampleRate       | number                                  | 否   | 音频采集采样率，默认值为48000。                              |
| numberOfChannels      | number                                  | 否   | 音频采集声道数，默认值为2。                                  |
| format<sup>(deprecated)</sup>                | [AudioOutputFormat](#audiooutputformat) | 否   | 音频输出封装格式，默认设置为MPEG_4。<br/>**说明：** 从API Version 8 开始废弃，建议使用fileFormat替代。                         |
| location              | [Location](#location)                   | 否   | 音频采集的地理位置。                                         |
| uri                   | string                                  | 是   | 音频输出URI：fd://xx&nbsp;(fd&nbsp;number)<br/>![](figures/zh-cn_image_url.png) <br/>文件需要由调用者创建，并赋予适当的权限。 |
| audioEncoderMime<sup>8+</sup>      | [CodecMimeType](#codecmimetype8)        | 否   | 音频编码格式。           |
| fileFormat<sup>8+</sup>      | [ContainerFormatType](#containerformattype8)        | 否   | 音频编码格式。         |


## AudioEncoder<sup>(deprecated)</sup>

> **说明：**
> 从 API Version 8 开始废弃，建议使用[CodecMimeType](#codecmimetype8)替代。

表示音频编码格式的枚举。

**系统能力：** 以下各项对应的系统能力均为 SystemCapability.Multimedia.Media.AudioRecorder。

| 名称    | 默认值 | 说明                                                         |
| ------- | ------ | ------------------------------------------------------------ |
| DEFAULT | 0      | 默认编码格式。<br/>仅做接口定义，暂不支持使用。 |
| AMR_NB  | 1      | AMR-NB(Adaptive Multi Rate-Narrow Band Speech Codec) 编码格式。<br/>仅做接口定义，暂不支持使用。 |
| AMR_WB  | 2      | AMR-WB(Adaptive Multi Rate-Wide Band Speech Codec) 编码格式。<br/>仅做接口定义，暂不支持使用。 |
| AAC_LC  | 3      | AAC-LC（Advanced&nbsp;Audio&nbsp;Coding&nbsp;Low&nbsp;Complexity）编码格式。 |
| HE_AAC  | 4      | HE_AAC（High-Efficiency Advanced&nbsp;Audio&nbsp;Coding）编码格式。<br/>仅做接口定义，暂不支持使用。 |


## AudioOutputFormat<sup>(deprecated)</sup>

> **说明：**
> 从 API Version 8 开始废弃，建议使用[ContainerFormatType](#containerformattype8)替代。

表示音频封装格式的枚举。

**系统能力：** 以下各项对应的系统能力均为 SystemCapability.Multimedia.Media.AudioRecorder。

| 名称     | 默认值 | 说明                                                         |
| -------- | ------ | ------------------------------------------------------------ |
| DEFAULT  | 0      | 默认封装格式。<br/>仅做接口定义，暂不支持使用。 |
| MPEG_4   | 2      | 封装为MPEG-4格式。                                           |
| AMR_NB   | 3      | 封装为AMR_NB格式。<br/>仅做接口定义，暂不支持使用。 |
| AMR_WB   | 4      | 封装为AMR_WB格式。<br/>仅做接口定义，暂不支持使用。 |
| AAC_ADTS | 6      | 封装为ADTS（Audio&nbsp;Data&nbsp;Transport&nbsp;Stream）格式，是AAC音频的传输流格式。 |


## ContainerFormatType<sup>8+</sup>

表示容器格式类型的枚举，缩写为CFT。

**系统能力：** 以下各项对应的系统能力均为 SystemCapability.Multimedia.Media.Core。

| 名称        | 值    | 说明                  |
| ----------- | ----- | --------------------- |
| CFT_MPEG_4  | "mp4" | 视频的容器格式，MP4。 |
| CFT_MPEG_4A | "m4a" | 音频的容器格式，M4A。 |

## Location

视频录制的地理位置。

**系统能力：** 以下各项对应的系统能力均为 SystemCapability.Multimedia.Media.Core。

| 名称      | 参数类型 | 必填 | 说明             |
| --------- | -------- | ---- | ---------------- |
| latitude  | number   | 是   | 地理位置的纬度。 |
| longitude | number   | 是   | 地理位置的经度。 |
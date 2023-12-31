# 使用SoundPool开发音频播放功能(ArkTS)

使用SoundPool（音频池）提供的接口，可以实现低时延短音播放。

当应用开发时，经常需要使用一些急促简短的音效（如相机快门音效、系统通知音效等），此时建议调用SoundPool，实现一次加载，多次低时延播放。

SoundPool当前支持播放1MB以下的音频资源，大小超过1MB的长音频将截取1MB大小数据进行播放。

本开发指导将以SoundPool进行一次低时延播放音频的过程为例，向开发者讲解如何使用SoundPool。详细的API声明请参考[SoundPool API参考](../reference/apis/js-apis-inner-multimedia-soundPool.md)。

过程包括：创建SoundPool实例，加载音频资源（包括资源的解封装与解码:解码格式参考[音频解码支持](audio-decoding.md#音频解码)），设置播放参数（循环模式/播放优先级等），播放控制（播放/停止），释放资源。

在应用开发过程中，开发者应通过监听方法检查当前播放状态并按照一定顺序调用接口，执行对应操作，否则系统可能会抛出异常或生成其他未定义的行为。具体顺序可参考下列开发步骤及对应说明。

## 开发步骤及注意事项

1. 调用createSoundPool方法创建SoundPool实例。

    ```ts
    let soundPool: media.SoundPool;
    let audioRendererInfo: audio.AudioRendererInfo = {
        usage : audio.StreamUsage.STREAM_USAGE_MUSIC,
        rendererFlags : 1
    }

    media.createSoundPool(5, audioRendererInfo).then((soundpool_: media.SoundPool) => {
      if (soundpool_ != null) {
        soundPool = soundpool_;
        console.info('create SoundPool success');
      } else {
        console.error('create SoundPool fail');
      }
    }).catch((error) => {
      console.error(`soundpool catchCallback, error message:${error.message}`);
    });
    ```

2. 调用load方法进行音频资源加载。
    可以传入uri或fd加载资源，此处使用传入uri的方式为例，更多方法请参考[API文档](../reference/apis/js-apis-inner-multimedia-soundPool.md#load)。

    ```ts
    let soundID: number;
    await fs.open('/test_01.mp3', fs.OpenMode.READ_ONLY).then((file: fs.File) => {
      console.info("file fd: " + file.fd);
      uri = 'fd://' + (file.fd).toString()
    }); // '/test_01.mp3' 作为样例，使用时需要传入文件对应路径。
    soundPool.load(uri).then((soundId: number) => {
      console.info('soundPool load uri success');
      soundID = soundId;
    }).catch((err) => {
      console.error('soundPool load failed and catch error is ' + err.message);
    });
    ```

3. 调用on('loadComplete')方法，用于监听“资源加载完成”。

    ```ts
    soundPool.on('loadComplete', (soundId_: number) => {
      console.info('loadComplete, soundId: ' + soundId_);
    });
    ```

4. 调用on('playFinished')方法，用于监听“播放完成”。
     
    ```ts
    soundPool.on('playFinished', () => {
      console.info("recive play finished message");
    });
    ```

5. 调用on('error')方法，设置错误类型监听。
     
    ```ts
    soundPool.on('error', (error) => {
      console.info('error happened,message is :' + error.message);
    });
    ```

6. 配置播放参数PlayParameters，并调用play方法播放音频。多次调用play播放同一个soundID，只会播放一次。
  
    ```ts
    let soundID: number;
    let streamID: number;
    let playParameters: media.PlayParameters = {
        loop: 0, // 循环0次
        rate: 2, // 2倍速
        leftVolume: 0.5, // range = 0.0-1.0
        rightVolume: 0.5, // range = 0.0-1.0
        priority: 0, // 最低优先级
      }
    soundPool.play(soundID, playParameters, (error, streamId: number) => {
      if (error) {
        console.info(`play sound Error: errCode is ${error.code}, errMessage is ${error.message}`)
      } else {
        streamID = streamId;
        console.info('play success soundid:' + streamId);
      }
    });
    ```

7. 调用setLoop方法设置循环次数。
     
    ```ts
    let streamID: number;
    soundPool.setLoop(streamID, 1).then(() => {
      console.info('setLoop success streamID:' + streamID);
    }).catch((err) => {
      console.error('soundpool setLoop failed and catch error is ' + err.message);
    });
    ```

8. 调用setPriority方法设置优先级。
     
    ```ts
    let streamID: number;
    soundPool.setPriority(streamID, 1);
    ```

9. 调用setVolume方法设置音量。

    ```ts
    let streamID: number;
    // 先调用play方法获取到对应资源的streamID

    soundPool.setVolume(streamID, 0.5, 0.5).then(() => {
      console.info('setVolume success');
    }).catch((err) => {
      console.error('soundpool setVolume failed and catch error is ' + err.message);
    });
    ```

10. 调用stop方法终止指定流的播放。
     
    ```ts
    let streamID: number;
    //先调用play方法给拿到对应的streamID

    soundPool.stop(streamID).then(() => {
      console.info('stop success');
    }).catch((err) => {
      console.error('soundpool load stop and catch error is ' + err.message);
    });
    ```

11. 调用unload方法卸载音频资源。

    ```ts
    let soundID: number;
    // 先调用load方法获取到对应资源的soundID

    soundPool.unload(soundID).then(() => {
      console.info('unload success');
    }).catch((err) => {
      console.error('soundpool unload failed and catch error is ' + err.message);
    });
    ```

12. 调用off('loadComplete')方法注销加载完成监听。

    ```ts
    soundPool.off('loadComplete');
    ```

13. 调用off('playFinished')方法注销播放完成监听。

    ```ts
    soundPool.off('playFinished');
    ```

14. 调用off('error')方法注销错误错误类型监听。

    ```ts
    soundPool.off('error');
    ```

15. 调用release方法释放SoundPool实例。

    ```ts
    soundPool.release().then(() => {
      console.info('release success');
    }).catch((err) => {
      console.error('soundpool release failed and catch error is ' + err.message);
    });
    ```

### 完整示例

下面展示了使用SoundPool进行低时延播放的完整示例代码。
  
```ts

import audio from '@ohos.multimedia.audio';
import media from '@ohos.multimedia.media';
import fs from '@ohos.file.fs'
struct Soundpool {
  private soundPool: media.SoundPool;
  private streamId: 0;
  private soundId: 0;
  private audioRendererInfo: {
    usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
    rendererFlags: 1
  }
  private PlayParameters: media.PlayParameters = {
    loop: 3, // 循环4次
    rate: audio.AudioRendererRate.RENDER_RATE_NORMAL, // 正常倍速
    leftVolume: 0.5, // range = 0.0-1.0
    rightVolume: 0.5, // range = 0.0-1.0
    priority: 0, // 最低优先级
  }
  private uri: string = "";
  async create(): Promise<void> {
    //创建soundPool实例
    this.soundPool = await media.createSoundPool(5, this.audioRendererInfo);
    //注册监听
    this.loadCallback();
    this.finishPlayCallback();
    this.setErrorCallback();
    // 加载音频资源
    await fs.open('/test_01.mp3', fs.OpenMode.READ_ONLY).then((file: fs.File) => {
      console.info("file fd: " + file.fd);
      this.uri = 'fd://' + (file.fd).toString()
    }); // '/test_01.mp3' 作为样例，使用时需要传入文件对应路径。
    this.soundId = await this.soundPool.load(this.uri);
  }
  async loadCallback(): Promise<void> {
    // 加载完成回调
    this.soundPool.on('loadComplete', (soundId_: number) => {
      console.info('loadComplete, soundId: ' + soundId_);
    })
  }
  //设置播放完成监听
  async finishPlayCallback(): Promise<void> {
    // 播放完成回调
    this.soundPool.on('playFinished', () => {
      console.info("recive play finished message");
      // 可进行下次播放
    })
  }
  //设置错误类型监听
  setErrorCallback(): void {
    this.soundPool.on('error', (error) => {
      console.info('error happened,message is :' + error.message);
    })
  }
  async PlaySoundPool(): Promise<void> {
    // 开始播放,这边play也可带播放播放的参数PlayParameters
    this.streamId = await this.soundPool.play(this.soundId);
    // 设置循环播放次数
    this.soundPool.setLoop(this.streamId, 2); // 播放3次
    // 设置对应流的优先级
    this.soundPool.setPriority(this.streamId, 1);
    // 设置音量
    this.soundPool.setVolume(this.streamId, 0.5, 0.5);
  }
  async release(): Promise<void> {
    // 终止指定流的播放
    this.soundPool.stop(this.streamId);
    // 卸载音频资源
    await this.soundPool.unload(this.soundId);
    //关闭监听
    this.setOffCallback();
    // 释放SoundPool
    await this.soundPool.release();
  }
  //关闭监听
  setOffCallback() {
    this.soundPool.off('loadComplete');
    this.soundPool.off('playFinished');
    this.soundPool.off('error');
  }
}
```

# @ohos.arkui.dragController (DragController)

本模块提供发起主动拖拽的能力，当应用接收到点击或长按等事件时可以主动发起拖拽的动作，并在其中携带拖拽信息。

> **说明：**
>
> 本模块首批接口从 API version 10 开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>
> 示例效果请以真机运行为准，当前 IDE 预览器不支持。
>
> 当前不支持同时配置excuteDrag和[onDragStart](../arkui-ts/ts-universal-events-drag-drop.md#事件)。


## 导入模块

```ts
import dragController from "@ohos.arkui.dragController";
```

## dragController.executeDrag

executeDrag(custom: CustomBuilder | DragItemInfo, dragInfo: DragInfo, callback: AsyncCallback&lt;{event: DragEvent, extraParams: string}&gt;): void

主动发起拖拽能力，传入拖拽发起后跟手效果所拖拽的对象以及携带拖拽信息。通过回调返回结果。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                             |
| -------- | ------------------------------------------------------------ | ---- | -------------------------------- |
| custom   | [CustomBuilder](../arkui-ts/ts-types.md#custombuilder8) \| [DragItemInfo](../arkui-ts/ts-universal-events-drag-drop.md#dragiteminfo说明) | 是   | 拖拽发起后跟手效果所拖拽的对象。 |
| dragInfo | [DragInfo](#draginfo)                                        | 是   | 拖拽信息。                       |
| callback | AsyncCallback&lt;{event: [DragEvent](../arkui-ts/ts-universal-events-drag-drop.md#dragevent说明), extraParams: string}&gt; | 是   | 拖拽结束返回结果的回调。         |

**示例：**

```ts
import dragController from "@ohos.arkui.dragController"
import UDMF from '@ohos.data.UDMF';

@Entry
@Component
struct DragControllerPage {
  @Builder DraggingBuilder() {
    Column() {
      Text("DraggingBuilder")
    }
    .width(100)
    .height(100)
    .backgroundColor(Color.Blue)
  }

  build() {
    Column() {
      Button('touch to execute drag')
        .onTouch((event?:TouchEvent) => {
          if(event){
            if (event.type == TouchType.Down) {
              let text = new UDMF.Text()
              let unifiedData = new UDMF.UnifiedData(text)

              let dragInfo: dragController.DragInfo = {
                pointerId: 0,
                data: unifiedData,
                extraParams: ''
              }
              class tmp{
                event:DragResult|undefined = undefined
                extraParams:string = ''
              }
              let eve:tmp = new tmp()
              dragController.executeDrag(this.DraggingBuilder(), dragInfo, (err, eve) => {
                if (eve.event.getResult() == DragResult.DRAG_SUCCESSFUL) {
                // ...
                } else if (eve.event.getResult() == DragResult.DRAG_FAILED) {
                // ...
                }
              })
            }
          }
        })
    }
  }
}
```

## dragController.executeDrag

executeDrag(custom: CustomBuilder | DragItemInfo, dragInfo: DragInfo): Promise&lt;{event: DragEvent, extraParams: string}&gt;

主动发起拖拽能力，传入拖拽发起后跟手效果所拖拽的对象以及携带拖拽信息。通过Promise返回结果。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                             |
| -------- | ------------------------------------------------------------ | ---- | -------------------------------- |
| custom   | [CustomBuilder](../arkui-ts/ts-types.md#custombuilder8) \| [DragItemInfo](../arkui-ts/ts-universal-events-drag-drop.md#dragiteminfo说明) | 是   | 拖拽发起后跟手效果所拖拽的对象。 |
| dragInfo | [DragInfo](#draginfo)                                        | 是   | 拖拽信息。                       |

**返回值：** 

| 类型                                                   | 说明               |
| ------------------------------------------------------ | ------------------ |
| Promise&lt;{event: [DragEvent](../arkui-ts/ts-universal-events-drag-drop.md#dragevent说明), extraParams: string}&gt; | 拖拽结束返回的结果。 |

**示例：**

```ts
import dragController from "@ohos.arkui.dragController"
import componentSnapshot from '@ohos.arkui.componentSnapshot';
import image from '@ohos.multimedia.image';
import UDMF from '@ohos.data.UDMF';

@Entry
@Component
struct DragControllerPage {
  @State pixmap: image.PixelMap|null = null

  @Builder DraggingBuilder() {
    Column() {
      Text("DraggingBuilder")
    }
    .width(100)
    .height(100)
    .backgroundColor(Color.Blue)
  }

  @Builder PixmapBuilder() {
    Column() {
      Text("PixmapBuilder")
    }
    .width(100)
    .height(100)
    .backgroundColor(Color.Blue)
  }

  build() {
    Column() {
      Button('touch to execute drag')
        .onTouch((event?:TouchEvent) => {
          if(event){
            if (event.type == TouchType.Down) {
              let text = new UDMF.Text()
              let unifiedData = new UDMF.UnifiedData(text)

              let dragInfo: dragController.DragInfo = {
                pointerId: 0,
                data: unifiedData,
                extraParams: ''
              }
              componentSnapshot.createFromBuilder(this.PixmapBuilder()).then((pix: image.PixelMap) => {
                this.pixmap = pix;
                let dragItemInfo: DragItemInfo = {
                  pixelMap: this.pixmap,
                  builder: this.DraggingBuilder(),
                  extraInfo: "DragItemInfoTest"
                }

                class tmp{
                  event:DragResult|undefined = undefined
                  extraParams:string = ''
                }
                let eve:tmp = new tmp()
                dragController.executeDrag(dragItemInfo, dragInfo)
                  .then((eve) => {
                    if (eve.event.getResult() == DragResult.DRAG_SUCCESSFUL) {
                      // ...
                    } else if (eve.event.getResult() == DragResult.DRAG_FAILED) {
                      // ...
                    }
                  })
                  .catch((err:Error) => {
                  })
              })
            }
          }
        })
    }
    .width('100%')
    .height('100%')
  }
}
```

## DragInfo

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

发起拖拽所需要的属性和拖拽时携带的信息。

| 名称        | 类型                                                   | 必填 | 说明                                     |
| ----------- | ------------------------------------------------------ | ---- | ---------------------------------------- |
| pointerId   | number                                                 | 是   | 设置启动拖拽时屏幕上触摸点的Id。         |
| data        | [unifiedDataChannel.UnifiedData](js-apis-data-unifiedDataChannel.md#unifieddata) | 否   | 设置拖拽过程中携带的数据。               |
| extraParams | string                                                 | 否   | 设置拖拽事件额外信息，具体功能暂未实现。 |


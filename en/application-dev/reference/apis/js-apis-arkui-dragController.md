# @ohos.arkui.dragController (DragController)

The **dragController** module provides APIs for initiating drag actions. When receiving a gesture event, such as a click or long-press event, an application can initiate a drag action and carry drag information therein.

> **NOTE**
>
> The initial APIs of this module are supported since API version 10. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>
> You can preview how this component looks on a real device. The preview is not yet available in the DevEco Studio Previewer.


## Modules to Import

```js
import dragController from "@ohos.arkui.dragController";
```

## dragController.executeDrag

executeDrag(custom: CustomBuilder | DragItemInfo, dragInfo: DragInfo, callback: AsyncCallback&lt;{event: DragEvent, extraParams: string}&gt;): void

Initiates a drag action, with the object to be dragged and the drag information passed in. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name  | Type                                                        | Mandatory| Description                            |
| -------- | ------------------------------------------------------------ | ---- | -------------------------------- |
| custom   | [CustomBuilder](../arkui-ts/ts-types.md#custombuilder8) \| [DragItemInfo](../arkui-ts/ts-universal-events-drag-drop.md#dragiteminfo) | Yes  | Object to be dragged.|
| dragInfo | [DragInfo](#draginfo)                                    | Yes  | Drag information.                      |
| callback | AsyncCallback&lt;{event: [DragEvent](../arkui-ts/ts-universal-events-drag-drop.md#dragevent), extraParams: string}&gt; | Yes  | Callback used to return the result.        |

**Example**

```ts
import dragController from "@ohos.arkui.dragController"
import UDMF from '@ohos.data.UDMF'

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
        .onTouch((event) => {
          if (event.type == TouchType.Down) {
            let text = new UDMF.Text()
            let unifiedData = new UDMF.UnifiedData(text)

            let dragInfo: dragController.DragInfo = {
              pointerId: 0,
              data: unifiedData,
              extraParams: ''
            }
            dragController.executeDrag(this.DraggingBuilder.bind(this), dragInfo, (err, {event, extraParams}) => {
              if (event.getResult() == DragRet.DRAG_SUCCESS) {
                // ...
              } else if (event.getResult() == DragRet.DRAG_FAILED) {
                // ...
              }
            })
          }
        })
    }
  }
}
```

## dragController.executeDrag

executeDrag(custom: CustomBuilder | DragItemInfo, dragInfo: DragInfo): Promise&lt;{event: DragEvent, extraParams: string}&gt;

Initiates a drag action, with the object to be dragged and the drag information passed in. This API uses a promise to return the result.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name  | Type                                                        | Mandatory| Description                            |
| -------- | ------------------------------------------------------------ | ---- | -------------------------------- |
| custom   | [CustomBuilder](../arkui-ts/ts-types.md#custombuilder8) \| [DragItemInfo](../arkui-ts/ts-universal-events-drag-drop.md#dragiteminfo) | Yes  | Object to be dragged.|
| dragInfo | [DragInfo](#draginfo)                                    | Yes  | Drag information.                      |

**Return value**

| Type                                                  | Description              |
| ------------------------------------------------------ | ------------------ |
| Promise&lt;{event: [DragEvent](../arkui-ts/ts-universal-events-drag-drop.md#dragevent), extraParams: string}&gt; | Promise used to return the result.|

**Example**

```ts
import dragController from "@ohos.arkui.dragController"
import UDMF from '@ohos.data.UDMF';
import componentSnapshot from '@ohos.arkui.componentSnapshot';
import image from '@ohos.multimedia.image';

@Entry
@Component
struct DragControllerPage {
  @State pixmap: image.PixelMap = null

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
        .onTouch((event) => {
          if (event.type == TouchType.Down) {
            let text = new UDMF.Text()
            let unifiedData = new UDMF.UnifiedData(text)

            let dragInfo: dragController.DragInfo = {
              pointerId: 0,
              data: unifiedData,
              extraParams: ''
            }
            componentSnapshot.createFromBuilder(this.PixmapBuilder.bind(this)).then((pix: image.PixelMap) => {
              this.pixmap = pix;
              let dragItemInfo: DragItemInfo = {
                pixelMap: this.pixmap,
                builder: this.DraggingBuilder.bind(this),
                extraInfo: "DragItemInfoTest"
              }

              dragController.executeDrag(dragItemInfo, dragInfo)
                .then(({event, extraParams}) => {
                  if (event.getResult() == DragRet.DRAG_SUCCESS) {
                    // ...
                  } else if (event.getResult() == DragRet.DRAG_FAILED) {
                    // ...
                  }
                })
                .catch((err) => {
                })
            })
          }
        })
    }
    .width('100%')
    .height('100%')
  }
}
```

## DragInfo

Defines the attributes required for initiating a drag action and information carried in the dragging process.

| Name       | Type                                                  | Mandatory| Description                                    |
| ----------- | ------------------------------------------------------ | ---- | ---------------------------------------- |
| pointerId   | number                                                 | Yes  | ID of the touch point on the screen when dragging is started.        |
| data        | [UDMF.UnifiedData](./js-apis-data-udmf.md#unifieddata) | No  | Data carried in the dragging process.              |
| extraParams | string                                                 | No  | Additional information about the drag action. Not supported currently.|

# Transition of Shared Elements

Shared element transition can be used for transition between pages, for example, transition from an image on the current page to the next page.

> **NOTE**
>
> The APIs of this module are supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.


## Attributes


| Name            | Parameters                                                        | Description                                                    |
| ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| sharedTransition | id: string,<br>{<br>duration?: number,<br>curve?: Curve \| string,<br>delay?: number,<br>motionPath?: <br>{<br>path: string,<br>form?: number,<br>to?: number,<br>rotatable?: boolean<br>},<br>zIndex?: number,<br>type?: [SharedTransitionEffectType](ts-appendix-enums.md#sharedtransitioneffecttype)<br>} | Transition of the shared element. If the same **id** value is configured for a component on the two pages, this component is considered as a shared element of the pages. If the **id** value is an empty string, no transition will be applied to the component.<br>- **id**: component ID.<br>- **duration**: Animation duration, in ms. The default duration is 1000 ms.<br>- **curve**: animation curve. The default curve is **Linear**. For details about the valid values, see [Curve](ts-animatorproperty.md).<br>- **delay**: Delay of animation playback, in ms. By default, the playback is not delayed.<br>- **motionPath**: motion path information.<br>- **path**: path.<br>- **from**: start value.<br>- **to**: end value.<br>- **rotatable**: whether to rotate.<br>- **zIndex**: z-axis.<br>- **type**: animation type.|


## Example

The example implements the custom transition of a shared image during redirection from one page to another, which is triggered by a click on the image.

```ts
// xxx.ets
@Entry
@Component
struct SharedTransitionExample {
  @State active: boolean = false

  build() {
    List() {
      ListItem() {
        Row() {
          Navigator({ target: 'pages/common/Animation/transAnimation/PageB', type: NavigationType.Push }) {
            Image($r('app.media.ic_health_heart')).width(50).height(50)
              .sharedTransition('sharedImage1', { duration: 800, curve: Curve.Linear, delay: 100 })
          }.padding({ left: 10 })
          .onClick(() => {
            this.active = true
          })

          Text('SharedTransition').width(80).height(80).textAlign(TextAlign.Center)
        }
      }
    }
  }
}
```

```ts
// PageB.ets
@Entry
@Component
struct BExample {

  build() {
    Stack() {
      Image($r('app.media.ic_health_heart')).width(150).height(150).sharedTransition('sharedImage1')
    }.width('100%').height(400)
  }
}
```

![en-us_image_0000001211898494](figures/en-us_image_0000001211898494.gif)

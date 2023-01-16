# @ohos.mediaquery

The **mediaquery** module provides different styles for different media types.

> **NOTE**
>
> The APIs of this module are supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.


## Modules to Import

```js
import mediaquery from '@ohos.mediaquery'
```


## mediaquery.matchMediaSync

matchMediaSync(condition: string): MediaQueryListener

Sets the media query condition. This API returns the corresponding media query listener.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name      | Type    | Mandatory  | Description                                      |
| --------- | ------ | ---- | ---------------------------------------- |
| condition | string | Yes   | Media query condition. For details, see [Syntax of Media Query Conditions](../../ui/ui-ts-layout-mediaquery.md#syntax-of-media-query-conditions).|

**Return value**

| Type                | Description                    |
| ------------------ | ---------------------- |
| MediaQueryListener | Media query listener, which is used to register or deregister the listening callback.|

**Example**

```js
let listener = mediaquery.matchMediaSync('(orientation: landscape)'); // Listen for landscape events.
```


## MediaQueryListener

Implements the media query listener, including the first query result when the listener is applied for.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

### Attributes

| Name   | Type   | Readable| Writable| Description                |
| ------- | ------- | ---- | ---- | -------------------- |
| matches | boolean | Yes  | No  | Whether the media query condition is met.  |
| media   | string  | Yes  | No  | Media query condition.|


### on

on(type: 'change', callback: Callback&lt;MediaQueryResult&gt;): void

Registers the media query listener. The callback is triggered when the media attributes change.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name     | Type                              | Mandatory  | Description              |
| -------- | -------------------------------- | ---- | ---------------- |
| type     | string                           | Yes   | Listener type. The value is fixed at **'change'**.|
| callback | Callback&lt;MediaQueryResult&gt; | Yes   | Callback registered with media query.      |

**Example**

  For details, see [off Example](#off).


### off

off(type: 'change', callback?: Callback&lt;MediaQueryResult&gt;): void

Deregisters the media query listener, so that no callback is triggered when the media attributes change.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name  | Type                            | Mandatory| Description                                                      |
| -------- | -------------------------------- | ---- | ---------------------------------------------------------- |
| type     | string                           | Yes  | Listener type. The value is fixed at **'change'**.                                  |
| callback | Callback&lt;MediaQueryResult&gt; | No  | Callback to be deregistered. If the default value is used, all callbacks of the handle are deregistered.|

**Example**

  ```js
    import mediaquery from '@ohos.mediaquery'
    
    let listener = mediaquery.matchMediaSync('(orientation: landscape)'); // Listen for landscape events.
    function onPortrait(mediaQueryResult) {
        if (mediaQueryResult.matches) {
            // do something here
        } else {
            // do something here
        }
    }
    listener.on('change', onPortrait) // Register the media query listener.
    listener.off('change', onPortrait) // Deregister the media query listener.
  ```

## MediaQueryResult

Provides the media query result.

**System capability**: SystemCapability.ArkUI.ArkUI.Full


### Attributes

| Name   | Type   | Readable| Writable| Description                |
| ------- | ------- | ---- | ---- | -------------------- |
| matches | boolean | Yes  | No  | Whether the media query condition is met.  |
| media   | string  | Yes  | No  | Media query condition.|


### Example

```ts
import mediaquery from '@ohos.mediaquery'


@Entry
@Component
struct MediaQueryExample {
  @State color: string = '#DB7093'
  @State text: string = 'Portrait'
  listener = mediaquery.matchMediaSync('(orientation: landscape)')

  onPortrait(mediaQueryResult) {
    if (mediaQueryResult.matches) {
      this.color = '#FFD700'
      this.text = 'Landscape'
    } else {
      this.color = '#DB7093'
      this.text = 'Portrait'
    }
  }

  aboutToAppear() {
    let portraitFunc = this.onPortrait.bind(this) // Bind the current JS instance.
    this.listener.on('change', portraitFunc)
  }

  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Text(this.text).fontSize(24).fontColor(this.color)
    }
    .width('100%').height('100%')
  }
}
```

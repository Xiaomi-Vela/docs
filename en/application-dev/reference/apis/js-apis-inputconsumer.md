# Combination Key

The input consumer module implements listening for key events.

> **NOTE**
>
> - The initial APIs of this module are supported since API version 8. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>
> - The APIs of this module are system APIs and cannot be called by third-party applications.


## Modules to Import


```
import inputConsumer from '@ohos.multimodalInput.inputConsumer';
```


## inputConsumer.on

on(type: "key", keyOptions: KeyOptions, callback: Callback&lt;KeyOptions&gt;): void

Enables listening for combination key events. When a combination key event that meets the specified conditions occurs, **KeyOptions** will be passed as an input parameter to **callback**.

This is a system API.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Type of the key input event to listen for. Only **key** is supported.|
| keyOptions | [keyOptions](#keyoptions) | Yes| Key option, which specifies the condition for combination key input.|
| callback | Callback&lt;[keyOptions](#keyoptions)&gt; | Yes| Callback used to return the result. When a key input event that meets the specified options occurs, **keyOptions** will be passed as an input parameter to **callback**.|

**Example**

```
let keyOptions = {preKeys: [], finalKey: 3, isFinalKeyDown: true, finalKeyDownDuration: 0}
let callback = function(keyOptions) {
    console.info("preKeys: " + keyOptions.preKeys, "finalKey: " + keyOptions.finalKey,
                 "isFinalKeyDown: " + keyOptions.isFinalKeyDown, "finalKeyDownDuration: " + keyOptions.finalKeyDownDuration)
}
inputConsumer.on('key', keyOptions, callback);
```


## inputConsumer.off

off(type: "key", keyOptions: KeyOptions, callback: Callback&lt;KeyOptions&gt;): void

Stops listening for combination key events.

This is a system API.

**System capability**: SystemCapability.MultimodalInput.Input.InputConsumer

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Type of the key input event to listen for. Only **key** is supported.|
| keyOptions | [keyOptions](#keyoptions) | Yes| Key options passed to the key input event when listening starts.|
| callback | Callback&lt;[keyOptions](#keyoptions)&gt; | Yes| Callback function passed to the key input event with the key option when listening starts.|

**Example**

```
let keyOptions = {preKeys: [], finalKey: 3, isFinalKeyDown: true, finalKeyDownDuration: 0}
let callback = function(keyOptions) {
    console.info("preKeys: " + keyOptions.preKeys, "finalKey: " + keyOptions.finalKey,
                 "isFinalKeyDown: " + keyOptions.isFinalKeyDown, "finalKeyDownDuration: " + keyOptions.finalKeyDownDuration)
}
inputConsumer.off('key', keyOptions, callback);
```


## KeyOptions

Defines the key options that are met when a combination key input event occurs.

This is a system API.

**System capability**: SystemCapability.MultimodalInput.Input.InputConsumer

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| preKeys | Array | Yes| Array of precedent keys. This parameter can be left empty. There is no requirement on the sequence of precedent keys.|
| finalKey | Number | Yes| Final key in the combination key. This parameter cannot be left blank.|
| isFinalKeyDown | boolean | Yes| Indicates whether the final key is pressed or released. By default, the final key is pressed.|
| finalKeyDownDuration | Number | Yes| Duration for pressing the final key. By default, there is no requirement on the duration.|

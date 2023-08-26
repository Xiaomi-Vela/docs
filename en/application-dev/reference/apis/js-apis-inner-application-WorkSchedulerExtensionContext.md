# WorkSchedulerExtensionContext

The **WorkSchedulerExtensionContext** module, inherited from [ExtensionContext](js-apis-inner-application-extensionContext.md), provides a context environment for the WorkSchedulerExtensionAbility.

This module provides APIs for accessing the resources of a WorkSchedulerExtensionAbility.

> **NOTE**
> 
> The initial APIs of this module are supported since API version 10. Newly added APIs will be marked with a superscript to indicate their earliest API version. 
> The APIs of this module can be used only in the stage model.

## Usage

The context is obtained through a WorkSchedulerExtensionAbility child class instance.

```ts
import WorkSchedulerExtensionAbility from '@ohos.WorkSchedulerExtensionAbility';

class MyWorkSchedulerExtensionAbility extends WorkSchedulerExtensionAbility {
    onWorkStart(workInfo) {
        let WorkSchedulerExtensionContext = this.context; // Obtain the WorkSchedulerExtensionContext.
    }
}
```
